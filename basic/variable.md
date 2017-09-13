# Variable

## What is variable

Variable are used to store information to be referenced and manipulated in a computer program. In Ruby, There are five types of variable, which includes `constant`, `global variable`, `class variable`, `instance variable` and `local variable`.

### Constant

Constant is one kind of variable we want it value remained the same and should be immutable. How name a constant with uppercase and camel case.

Basically we will use a freeze method to freeze the value we assign to the constant. If you try to modify the value, you will get a RuntimeError.

```ruby
MY_CONSTANT = "foo".freeze
MY_CONSTANT << "bar" # => RuntimeError: can't modify frozen string
```

Constant can’t be declared in method definitions, and are available through the application’s scopes.

### Local variable

In Ruby, the scope is defined by a block. For local variable, the inner scope variable can access the variable in outer scope, but not vice versa.

```ruby
b = 7             # variable is initialized in the outer scope
c = 9

3.times do |n|    # method invocation with a block
  a = 3           # is a accessible here, in an inner scope?
  b = 11
end

puts a
# NameError: undefined local variable or method `a' for main:Object
#     from (irb):171
#     from /Users/pk60905/.rvm/rubies/ruby-2.1.2/bin/irb:11:in `<main>'
puts b
#=> 11

puts c
#=> 9
```

From the above example we can see

1. We can reference the `a` variable from the outer scope
2. We mutate the `b` variable inside the block, which means the variable in inner scope can reference variable in outer scope.
3. While in the same scope we can reference variable directly, so that's why we can print `c` in the console.

**Note: A method can reference a local variable in outer scope, unless you pass the local variable through parameter.**

```ruby
local_variable = 10

def new_method
  puts local_variable
end

new_method
# NameError: undefined local variable or method `variable' for main:Object
#    from (irb):1:in `new_method'
#    from (irb):2
#    from /Users/pk60905/.rvm/rubies/ruby-2.1.2/bin/irb:11:in `<main>'
```

We can do the following instead.

```ruby
local_variable = 10

def new_method(num)
  puts num
end

new_method(local_variable)
#=> 10
```

### I**nstance variable**

Instance variables are variables that start with`@` and are scoped at the object level. They are used to track individual object state, and do not cross over between objects.

```ruby
class Student
  def initialize(name)
    @name = name
  end

  def say_hello
    puts "Hi, my name is #{@name}"
  end
end

student1 = Student.new("Jon Snow")
student2 = Student.new("Tyrion Lannister")

student1.say_hello
#=> "Hi, my name is Jon Snow"
student2.say_hello
#=> "Hi, my name is Tyrion Lannister"
```

### Class variable

#### Class Variable Scope

Class variables start with`@@`and are scoped at the class level. They exhibit two main behaviors:

* all objects share 1 copy of the class variable. \(This also implies objects can access class variables by way of instance methods.\)
* class methods can access class variables, regardless of where it's initialized.

```ruby
class Student
  @@total_student_number = 0

  def initialize(name)
    @name = name
    @@total_student_number += 1
  end

  def total_student_number
    puts "#{@@total_student_number}"
  end

  def self.total_student_number
    puts "#{@@total_student_number}"
  end
end

student1 = Student.new("Jon Snow")
student2 = Student.new("Tyrion Lannister")

student1.total_student_number
#=> 2

student2.total_student_number
#=> 2

Student.total_student_number
#=> 2
```

### Global variable

Global variables are declared by starting the variable name with the dollar sign \(`$`\). These variables are available throughout your entire app, overriding all scope boundaries. Rubyists tend to stay away from global variables as there can be unexpected complications when using them.

Example of a global variable declaration:

```
$var = 'I am also available throughout your app.'
```

Resource:[ Introduction to Programming with Ruby](https://launchschool.com/books/ruby/read/variables#whatisavariable)

Resource: [Object Oriented Programming with Ruby](https://launchschool.com/books/oo_ruby/read/classes_and_objects_part1#instancevariables)









