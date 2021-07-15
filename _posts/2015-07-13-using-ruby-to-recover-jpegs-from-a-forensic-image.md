---
title: Using Ruby to Recover JPEGs from a Forensic Image
date: 2015-07-13T22:22:28+01:00
author: Thomas
layout: single
categories:
  - Forensics
  - Ruby
tags:
  - cs50
  - forensics
  - ruby
---
* * *

_This is the second post in a series investigating different programming languages applied to a forensics recovery problem. More detail about the problem can be found in [Using Go to Recover JPEGs from a Forensic Image](http://mrshipley.com/?p=23). The code is available on [GitHub](https://github.com/tdshipley/CS50-Forensics-Without-C)._

* * *

Continuing from the last post the next language I looked at was Ruby. As a brief recap, the problem was to recover 16 JPEG files from a forensic image which had been zero wiped before they were taken.

## About Ruby

Ruby is a language that was popularised by the web framework [Ruby on Rails](http://rubyonrails.org). It can be best surmised by the quote on the [official website](https://www.ruby-lang.org/en/):

> _Ruby is a dynamic, open source programming language with a focus on simplicity and productivity. It has an elegant syntax that is natural to read and easy to write._

Ruby is very focused on readable syntax in an effort to hide complexity unless it is needed.

## Coding a Solution in Ruby

Ruby has a few concepts which can make it quite different from other languages.

### Everything is an Object

When Ruby developers tell you everything is an object they really mean it. Everything is an object of a corresponding class even the Ruby equivalent to _NULL_, _nil _which is an object of the [NilClass](http://ruby-doc.org/core-2.2.2/NilClass.html). Consider the line below:

```ruby
x = 4 + 1
```

This is syntactically correct Ruby code which as expected stores the number five in the variable _x_. But this is just syntactic sugar for calling the addition method on the four object. It could also be written as:

```ruby
x = 4+(1)
```

While strange looking this is syntactically correct. The reason the syntactic sugar works is because of another Ruby feature.

### Poetry Mode

The Ruby idiom _Poetry Mode_ is an idiomatic pattern often found in Ruby code it refers to two things:

  * The omission of characters which are not needed by the parser to understand the intent of your code.

```ruby
out_file.close unless out_file.nil?
```

The code above omits parenthesis in order to be more readable it could of also been written like this:

```ruby
out_file.close() unless out_file.nil?()
```

  * Using hashes as the single parameter to a method which in turn take multiple parameters.

This style is quite often used in Ruby code to accept multiple optional parameters in a clean way. It is similar to the concept of Named Arguments in other languages like _C# _for example:

```ruby
def method(regular_variable, hash_variable={})
    # Internal workings of the method which expects
    # one variable and some optional named ones 
end

method "12", a: "14"
method "13", b: "15"
method "13", b: "15", a: "14"
method "13", b: "15", a: "14"
method "13", { b: "15", a: "14" }
```

A hash in Ruby is an associative array. Above there is a method which takes a normal variable and a hash. Because this is a hash it can be passed multiple key/value pairs but none of them is required (at least by the method signature). The last usage example shows the full syntax of declaring a hash but because of the first point, this is not needed.

Poetry mode, however, can confuse the parser so if in doubt about the order of operations or that your code will not be understood add some parentheses which will add clarity for the reader and the parser.

### Readable Method Names

Method names can contain special characters which are why in the addition example from earlier is named the _+()_ method. But it also leads to some idiomatic conventions such as using a question mark (?) for methods that return a boolean value:

```ruby
until file.eof?
```

Above is the beginning of an until block (like a while block) which will continue looping until the e_of?_ the method returns true.

For methods which perform dangerous actions like throwing an error or editing a variable in place then an exclamation mark or otherwise known as a bang (!) is commonly added:

```ruby
x = hEllO
x.downcase # returns "hello" x == hEllO
x.downcase!   #=> x == "hello"
```

Above the first method call is to the _downcase _method which will return a copy of the string while the variable _x _remains unchanged - _downcase! _however, will edit the string in place changing the content of the variable.

### String Interpolation

Strings which are enclosed in double quotes can have values interpolated into them while ones enclosed in single quotes cannot. This leads to an idiomatic convention of only using double quotes when you need to interpolate a value:

```ruby
puts "#{getFilename(filenumber)}.jpeg"
```

Using the #{} syntax the string can have Ruby code embedded into it - the value resulting from it is added into the string. In the case above as part of my solution, I create a file name using the value returned from the method _getFilename._

### Semicolons

Throughout my code you will notice by now there are no semicolons like _Go_ the programmer does not need to insert semicolons however unlike Go this is because they are not used at all!

### File Encoding

When I solved this problem in Ruby I found file encodings to be an issue when comparing the bytes read in from the image file to hexadecimal values - unlike Go. We can see this in the _isJPEG?_ method:

```ruby
# @param [Object] block A 512 byte block to check if it contains a jpeg header in first 4 bytes
def isJPEG?(block)
  # Encodings are diff between reading an image file and strings so block[0] == 0xFF wont work
  # http://stackoverflow.com/questions/16815308/ruby-comparing-hex-value-to-string
  jpeg_header_part = ['FFD8FF'].pack('H*')
  return block[0,3] == jpeg_header_part && (block[3] == 0xe0.chr || block[3] == 0x0e1.chr)
end
```

Reading the bytes from my file return a 512 byte ASCII encoded string. But my code was encoded in UTF-8 so the comparisons would not work. There is a couple of solutions to this explained well by [Stefan](http://stackoverflow.com/questions/16815308/ruby-comparing-hex-value-to-string) at StackOverflow. Above I decided on two options:

  * Encoding the first 3 expected byte values into a hexadecimal string using the _[Pack](http://ruby-doc.org/core-2.0.0/Array.html) _method which returns a binary sequence for an array of values - in my case an array of one value.
  * Using the _[chr](http://ruby-doc.org/core-2.0.0/Integer.html#method-i-chr) _method which returns a string encoded by the receivers encoding.

## Conclusions

Having used Ruby a little before when experimenting with Ruby on Rails I wasn't completely new to the language. Coding a solution in Ruby was enjoyable thanks to its expressiveness and I felt it was a little more readable than the Go solution although this could be down to my previous experience. However, in one area this was not true. The encoding of the bytes read out of the card file compared to the string values in the code was less readable than the Go solution.