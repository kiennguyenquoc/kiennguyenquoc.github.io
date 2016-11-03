---
layout: post
title: Một số khái niệm cơ bản trong Ruby on rails.
tags: background
excerpt: "Bài viết này đề cặp tới một số kiến thức nền tảng mà một người mới học lập trình Rails nên nắm vững."
categories: [Ruby on Rails]
comments: true
image:
  feature: background.jpg
---

## I. Ruby variables and the rules of ruby scoping.
1. Ruby Global Variables.
* Global variables begin with `$`. Uninitialized global variables have the value `nil`.
* Assignment to global variables alters global status. It is not recommended to use global variables. They make programs cryptic`(bí ẩn)`.
* A class variable is a variable that is shared amongst all instances of a class. This means that only one variable value exists for all objects instantiated from this class. This means that if one object instance changes the value of the variable, that new value will essentially change for all other object instances.
* Another way of thinking of thinking of class variables is as global variables within the context of a single class.
2. Ruby Instance Variables.
* Instance variables begin with `@`. Uninitialized instance variables have the value `nil `.
* Instance variables are similar to Class variables except that their values are local to specific instances of an object. 
3. Ruby Class Variables.
* Class variables begin with `@@` and must be initialized before they can be used in method definitions.
* Referencing an uninitialized class variable produces an error. Class variables are shared among descendants of the class or module in which the class variables are defined.
4. Ruby Local Variables.
*  Local variables begin with a lowercase letter or `_`. The scope of a local variable ranges from `class`, `module`, `def`, or `do` to the corresponding `end` or from a `block` of opening brace to its close brace `{}`.
*  When an uninitialized `local variable` is referenced, it is interpreted`(thông dịch, biên dịch)` as a call to a method that has no arguments.
*  Assignment to uninitialized local variables also serves as variable declaration. The variables start to exist until the end of the current scope is reached. The lifetime of local variables is determined when Ruby parses`(phân tích cú pháp)` the program.
  
5. Ruby Constants Variables.
* Constants begin with an uppercase letter and may be all letters. Constants defined within a class or module can be accessed from within that class or module, and those defined outside a class or module can be accessed globally.
* Constants may not be defined within methods. Referencing an uninitialized constant produces an error. Making an assignment to a constant that is already initialized produces a warning.
* Constants defined outside of a class have global scope. Note that a constant variable means that which object is bound to the constant won't change, not that the object itself won't change internal state.

6. Ruby Pseudo-Variables.
* They are special variables that have the appearance of local variables but behave like constants. You can not assign any value to these variables.
  - `self`: The receiver object of the current method.
  - `true`: Value representing true.
  - `false`: Value representing false.
  - `nil`: Value representing undefined.
  - `__FILE__`: The name of the current source file.
  - `__LINE__`: The current line number in the source file.
  
### Ruby Variable Scope: A Quick Reference
* `Class variable` (@@a_variable): Available from the class definition and any sub-classes. Not available from anywhere outside.
* `Instance variable` (@a_variable): Available only within a specific object, across all methods in a class instance. Not available directly from class definitions.
* `Global variable` ($a_variable): Available everywhere within your Ruby script, regardless of where they are declared
* `Local variable` (a_variable): It depends on the scope. You’ll be working with these most and thus encounter the most problems, because their scope depends on various things.

### How to access instance variables from one class while inside another class.

- To create accessors for instance variables the simple way, use `attr_accessor`.
- As you might understand, use `attr_reader` and `attr_accessor` accordingly. Only use `attr_accessor` when you need a `getter` AND a` setter` and use `attr_reader` when you only need a `getter`

```
class TestDevice   
  attr_accessor :loghash

  def initialize  
    @loghash = { }  
    ....  
  end  
end
```

You can also manually define an accessor.

```
class TestDevice
  def loghash
    @loghash
  end
  def loghash=(val)
    @loghash = val
  end
end
```

- This is effectively what `attr_accessor` does behind the scenes.
- You can use `instance_variable_get`

## II. Class and Instance Methods.
* Class methods are methods that are called on a class and instance methods are methods that are called on an instance of a class. Here is a quick example and then we’ll go into a bit more detail.

```
class Foo
  def self.bar
    puts 'class method'
  end
  
  def baz
    puts 'instance method'
  end
end

Foo.bar # => "class method"
Foo.baz # => NoMethodError: undefined method ‘baz’ for Foo:Class

Foo.new.baz # => instance method
Foo.new.bar # => NoMethodError: undefined method ‘bar’ for #<Foo:0x1e820>
```

## III. Explain some about operators in Ruby.
- A common misconception is that `a ||= b` is equivalent to `a = a || b`, but it behaves like `a || a = b`.
- In `a = a || b`, `a` is set to something by the statement on every run, whereas with `a || a = b`, `a` is only set if `a` is logically `false` (i.e. if it's `nil` or `false`) because `||` is 'short circuiting'. That is, if the left hand side of the `||` comparison is `true`, there's no need to check the right hand side.

## IV. Reference
- http://www.railstips.org/blog/archives/2009/05/11/class-and-instance-methods-in-ruby/
- http://www.rubyinside.com/what-rubys-double-pipe-or-equals-really-does-5488.html