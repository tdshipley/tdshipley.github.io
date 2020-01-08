---
title: Using Go to Recover JPEGs from a Forensic Image
date: 2015-06-19T17:22:57+01:00
author: Thomas
layout: post
categories:
  - Forensics
  - Go
tags:
  - cs50
  - forensics
  - go
---
[CS50](http://cs50.net) is an introductory course offered by Harvard to students at the college and online via [EdX](https://github.com/tdshipley/CS50-Forensics-Without-C) and the Harvard Extension School. It teaches mostly through a series of problems sets which mostly focus on using C to solve them. One of the more interesting problem sets is [Problem Set 4: Forensics](http://cdn.cs50.net/2015/x/psets/4/pset4/pset4.html).

## The Problem

The original problem was solved in _C_ as part of the course and here will be solved using Go. But before looking at any code it is important to give a little context (all code is available on [GitHub](https://github.com/tdshipley/CS50-Forensics-Without-C) for those that are interested).

Key characteristics of the problem have been outlined below:

What we have:

  * a forensic image of a cameras SD card

What to attempt:

  * Recover 16 deleted images from the file numbered 001.jpg through to 016.jpg.

Points of note:
  * The card was wiped with zeros before images were taken and deleted (This makes the slack space of the image full of zeros simplifying image recovery).
  * The card stores data in contiguous 512-byte blocks. If an image is 500 bytes it will still occupy one block (with some slack space left).
  * Trailing zeros in the recovered image are acceptable.
  * It is OK to hardcode the path of the file.

### A Little Bit of Theory - Finding JPEGS

#### How can a jpeg file be identified in a forensic image?

As mentioned above images are stored in blocks of 512 bytes so no matter the actual size of the image it will always take up 512 bytes on the card. Therefore we know that an image _could_ start every 512 bytes – so instead of reading the file byte by byte we can read in 512-byte blocks and check that for the start of a file.

#### Now how is the file identified in the 512-byte block?

Fortunately, while JPEG files are complex their headers are simple. If the first 4 bytes of your 512-byte block match either sequence below then it is a JPEG:

```bash
0xff 0xd8 0xff 0xe0
```

Or:

```bash
0xff 0xd8 0xff 0xe1
```

Of course, if the card had not been zero wiped this part would become a lot harder as slack space could also match the pattern leading to false positives.

## Coding a Solution in Go

There were a few interesting differences in Go compared to other languages I had worked in. Quite a few are shown the snippet below:

```go
func isJPEG(fileBlock []byte) (result bool)  {
  result = false
  if (fileBlock[0] == 0xff && fileBlock[1] == 0xd8 && fileBlock[2] == 0xff && (fileBlock[3] == 0xe0 || fileBlock[3] == 0x0e1))   {
    result = true
  }
  return result
}
```

### Function Declarations - Type Position and Named Return Variables

Go uses functions which aren't too usual but look at the declaration:

```go
func isJPEG(fileBlock []byte) (result bool) {
```

A couple of interesting ideas from Go are displayed on this one line:

  * The parameter _fileBlock_ has the type (byte array) declared after its name rather than before.

The aim is making functions which take pointers more readable. Detailed in the blog post [Go's Declaration Syntax](http://blog.golang.org/gos-declaration-syntax). This same style is found in variable declarations too.

  * The second pair of parenthesis look strange (or at least it did to me) this is a [named return parameter](https://tour.golang.org/basics/7).

In Go, you can declare the variable that will be returned in the function declaration. This is considered the idiomatic approach to declaring return variables but is however optional.

  * There can also be many return variables from a function using this method. This is something I had seen a lot of it go code: 
    ```go
    file, err:= os.Open"card.raw"
    ```
    
    Here using an os package (think Ruby Gems or .Net Libraries) the **Open** function returns two variables the file and any errors that occurred as part of the process.
    
    _Note:_ The opening curly brace must be on the same line as the declaration. This is because of how Semicolons are added in Go. 
    
### Semicolons in Go

There is more to be learnt when inspecting the body of _isJPEG_:

```go
result = false
if (fileBlock[0] == 0xff && fileBlock[1] == 0xd8 && fileBlock[2] == 0xff && (fileBlock[3] == 0xe0 || fileBlock[3] == 0x0e1))   {
  result = true
}
return result
```

  * Go uses semicolons to mark the end of a statement. But there are no semicolons in my function above. The Go lexer inserts them for you following a rule defined in [Effective Go](https://golang.org/doc/effective_go.html#semicolons):  
    * * *
    
    > If the last token before a newline is an identifier (which includes words like `int` and `float64`), a basic literal such as a number or string constant, or one of the tokens.

This is a little difficult to parse but in simpler terms means _if you create a newline after a token that normally has a semicolon after it then it shall be added._

This is why a curly brace must be on the same line as the statement - for example, an if statement:

```go
if (fileBlock[0] == 0xff && fileBlock[1] == 0xd8 && fileBlock[2] == 0xff && (fileBlock[3] == 0xe0 || fileBlock[3] == 0x0e1))   {
  result = true
}
```

If the curly brace was moved from the end of the if statement the last token would be a closing parenthesis. This would have a semicolon after it so one would be inserted by the lexer and your code would be syntactically incorrect.

There are a few exceptions to all of this. The most notable of my brief experiment with the language is the _For_ _loop_ which works pretty much as you would expect any C style language would. Except in Go, there is only a For loop and all parts are optional. So not so much as you would expect!

### Variables in Go

Variables in Go can be both static and dynamically typed. There are multiple ways to define a variable:

#### The var keyword

```go
var i, j, k int
```

Above I have declared three int variables _i_, _j_ and _k_ as type _int_. But I needn't have specified a type I could just have easily defined them as:

```go
var i, j, k
```

At this point, the type will be inferred by the compiler at the first assignment.

#### Within Functions

Within a function I can shorten a dynamically typed variables declaration and assignment into one simple operator:

```go
y := 42
```

The := operator will assign a value to a newly created variable of which is named on the left of it in this case 42 is assigned to the newly declared variable y.

## Deferring a Function and Parentheses

There are two more unusual bits of Go I found through my exploration that deserve a brief mention.

### Deferring a Function

In Go, you can defer a function call to be executed immediately before the executing function returns. A good example is freeing resources like an open file:

```go
// Taken from https://golang.org/doc/effective_go.html#defer
func Contents(filename string) (string, error) {
  f, err := os.Open(filename)
  if err != nil {
      return "", err
  }
  
  defer f.Close()  // f.Close will run when we're finished.
  
  var result []byte
  return string(result), nil // f closed here
}
```

Here the file is opened and after error checking a function call to _f.close()_ is deferred. Just before the function returns the close function will be called.

Now you no longer need to remember to close just defer when opening a file.

### Parentheses in Go

In _if, for _and _switch_ you do not need parentheses however you can use them when you want to force an order of operations:

```go
if fileBlock[0] == 0xff && fileBlock[1] == 0xd8 && fileBlock[2] == 0xff && (fileBlock[3] == 0xe0 || fileBlock[3] == 0x0e1)   {
  result = true
}
```

Here I have updated the if statement for finding a JPEG. Now it only uses parentheses where they are needed at the end of the if statement around the or (||).

## Conclusions

Go reminds me a little of Ruby in its strive to make the code as clean as possible and removing redundant characters which I quite like. Although there are a few things which threw me like the type being on the right-hand side of a variable name. But clearly, readability is one of the main aims of Go, in fact, they even have a tool to format your code: [gofmt](https://golang.org/cmd/gofmt/).