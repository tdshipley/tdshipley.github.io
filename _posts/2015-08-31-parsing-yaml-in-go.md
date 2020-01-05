---
title: Parsing YAML in GO
date: 2015-08-31T23:33:55+01:00
author: Thomas
layout: post
categories:
  - Go
tags:
  - go
  - yaml
---
Go supports JSON via its standard libraries. However, it does not support YAML - which is interesting when you think about it. [YAML is after all just JSON written in a specific way](http://yaml.org/spec/1.2/spec.html#id2759572).

It is useful to have a high-level understanding of how GO supports JSON before diving into YAML. The first thing you need to do is model your data as a struct:

https://gist.github.com/tdshipley/e5805738cc54d0a12ddd

Notice how there is a string with some metadata for each field. This tells Go what each field is named in your JSON. After this, you can include the encoding/JSON library you get a whole host of functions including:

  * [Marshal](http://golang.org/pkg/encoding/json/#Marshal) 
      * To read the struct into a JSON object.
  * [Unmarshal](http://golang.org/pkg/encoding/json/#Unmarshal) 
      * To read the JSON object into a struct.

# Adding YAML Support

It is a shame that YMAL is not supported by Go as part of the standard libraries but it can be easily added by a third party library called [go-yaml](https://github.com/go-yaml/yaml). Firstly it needs to be included in your project:

https://gist.github.com/tdshipley/64bebe12736a75003f0f

You, of course, need the library installed locally on your machine - enter and run this at the command line:

`go get gopkg.in/yaml.v2`

Once you have done this you are ready to get started. Nicely the library tries to be as similar to the standard lib for JSON as possible. First, update your struct:

https://gist.github.com/tdshipley/9d87c1c1b96b67a80053

Notice the only change is in the metadata. Now it specifies YAML and not JSON, but the intent is the same. What name does the field have in the YAML? To interact with it there is a marshal and unmarshal function:

https://gist.github.com/tdshipley/8e4f626551e9be06e4dc

Above is a complete example. The lib is imported and a struct called _Person_ created. Then in the main function, a _person_ variable is instantiated to the type _Person_ - a struct object.

On line 20 the _data_ variable - containing some valid YAML - is read into the _person_ variable using the Marshal function.

On line 23 this _person_ variable is converted back into JSON using the Unmarshal function and stored in the _personJSON_ variable. Both functions are members of the YAML class which is introduced by the lib.

# Supporting JSON and YAML

In my use case, there was not a need to support both JSON and YAML. But if you need to then check out the write up [The right way to handle YAML in Go](http://ghodss.com/2014/the-right-way-to-handle-yaml-in-golang/) by [Sam Ghods](http://ghodss.com/about/) which was an interesting read - it should set you on the right path.