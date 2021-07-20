---
title: Calculating a Percentage in Ruby Elegantly
date: 2015-09-08T09:00:29+01:00

layout: single
categories:
  - Ruby
tags:
  - ruby
---
In a recent project it would have been handy to write some ruby code which looked like:

```ruby
10.percentage_of 100 # => 10
```

When searching through the ruby libraries there wasn't any indication it existed. Wanting to avoid a class method - a quick google turned up this StackOverflow post - [Calculate percentage in ruby](http://stackoverflow.com/questions/3668345/calculate-percentage-in-ruby){.question-hyperlink}.

It presents a nice solution to the problem (one I should have thought of!). Create a class called Numeric and add the method to it:

```ruby
# Taken from http://stackoverflow.com/questions/3668345/calculate-percentage-in-ruby
class Numeric
  def percent_of(n)
    self.to_f / n.to_f * 100.0
  end
end

1.percent_of 10    # => 10.0  (%)
```

Now a number object has a method called _percent_of _which takes itself and another number as an argument to calculate the percentage.

# How Does It Work?

There are two tricks going on here.

## The self Keyword

On line 4 the first number in the percent of equation is not passed to the method. Instead, the method refers to the value of its own object. In the example above this is a Numeric object with the value 10. So the value 10 is used.

## Extending a Class

More interestingly the Numeric class is part of the standard ruby library. So how come it can be extended? Ruby has a great feature - to add to an existing class just create it within your codebase and add to it. In contrast, other languages might need to use _this_ keyword (or similar) on an object passed to the method (see: [C# Extension Methods](https://msdn.microsoft.com/en-gb/library/bb383977.aspx)).

Here this is used to create an elegant result. Within the codebase just add a _numeric.rb_ file with a _Numeric_ class in it. Then the percent_of method can be defined. Ruby will treat it as part of the original class. Pretty neat.

You can find another example of this at the blog [Ruby Fleebie](http://www.rubyfleebie.com/how-to-add-methods-to-existing-classes/).