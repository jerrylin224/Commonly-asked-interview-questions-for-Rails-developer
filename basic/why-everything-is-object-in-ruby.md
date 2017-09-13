# Everything is object in Ruby {#a513}

I often heard “Everything is object in Ruby”, but sometimes I felt confused about the concept. I know`block`is not an object. But how about`class`and`module`, are they objects?

Before discussing are`class`and`module`are objects or not, we should declare what exactly object is.

## Object

> **All objects are instances of a class.**

This is how we create an object. But what exactly object is? You can think of object as something contains state and behavior.

> **object = state + behavior**

This is still kind of vague explanation. Let’s create a class and an object.

```ruby
class Student
  def initialize(name, gender)
    @name = name
    @gender = gender
  end

  def name
    @name
  end

  def age
    @age
  end
  
  def say_hello
    "#{@name} say 'Hello'"
  end
end

student1 = Student.new("John Snow", "male")
student2 = Student.new("Daenerys Targaryen", "female")

student1.name #=> "Jon Snow"
student2.age  #=> "female"
student2.say_hello #=> "Daenerys Targaryen say 'Hello'"
```

We use the class`Student`to instantiate 2 objects. Both of the object have`state,`which are their name and gender, and`behavior`\(to say hello\).

The`@name` and `@gender` are what we call `instance variable`, but we won’t talk too much what it is here. But basically it is an variable to store information for each object.

## Class {#e41d}

We saw we can create an object from a`class`, but what is class and how it creates object?

#### How class create a object {#8eb0}

The simple answer is call the `new` class method and pass necessary arguments.

```ruby
new_student = Student.new("your name", "your gender")
```

You can think of`class`as a template. It pre-defines what state and behavior of the object it creates should have. So every object created from the same class will have the same structure\(have same state and same behavior\). So the 2 objects `student1` and `student2`both have `name, age` and can `say_hello`.

One thing needs to note here is, the “information\(or data\)” store in the state may be different, but the behavior will be the same.

## Are Class and Module objects?

The fastest way to check they are objects or not is use the `class` method. Open you irb to call the `class` method with anything you think is object as receiver.

```ruby
"string".class
 => String
 
1.class
=> Fixnum

Class.class
=> Class

Module.class
=> Class
```

So, the string is object of`String`class, integer is object of`Fixnum`class, and`Class`and`Module`are objects of`Class`class.

### Superclass/subclass {#18e6}

Another interesting concept you need to know is the `method lookup path` . You can invoke the `ancestors` method with any class as it’s receiver to check what classes it inherit from.

```ruby
String.ancestors
=> [String, Comparable, Object, Kernel, BasicObject]

Class.ancestors
=> [Class, Module, Object, Kernel, BasicObject]

Module.ancestors
=> [Module, Object, Kernel, BasicObject]

Fixnum.ancestors
=> [Fixnum, Integer, Numeric, Comparable, Object, Kernel, BasicObject]

BasicOject.class
=> class
```

So the result show what classes a class inherit from and what modules the class\(or its ancestors\) mixed in with. The upmost superclass for all class is BasicObject class, including the `Class` class and `Module `class. But you may notice that the `BasicObject` class is also the object of `Class` class. You can check the diagram from the [Skilldrick](http://skilldrick.co.uk/) site, which outlines all the classes and superclasses links.

![](/Diagram from Skilldrick/import.png)



So, whenever you are not sure something is object or not, you just use the `class` method to verify it. Then you should start believing that “almost” everything is object in Ruby.

Resource: [Understanding the Ruby object model](http://skilldrick.co.uk/2011/08/understanding-the-ruby-object-model/)

