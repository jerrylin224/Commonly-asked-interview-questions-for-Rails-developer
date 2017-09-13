# Difference between include and extend {#e9d9}

In Ruby, a Module is a collection of methods and constants. We use`include`to`mixin`the module with the current class. After`mixin`, the current class can use the methods and constants from the module, and any subclass of the current class can also inherit the methods and constants of the module.

```ruby
module Talkable
  def say_hi
    puts "Hi"
  end
end

class Example
  include Talkable
end

Example.new.say_hi
#=> Hi

Example.say_hi
# NoMethodError: undefined method `say_hi’ for Example:Class
# from (irb):17
# from /usr/local/bin/irb:11:in `<main>’
```

**Note: By using include, the module add`instance`method to the class.**

Unlike`include`, which adds module’s methods as instance methods ,`extend` allows you to add them as a class methods.

```ruby
module Talkable
  def say_hi
    puts "Hi"
  end
end
class Experiment
  extend Talkable
end

Experiment.say_hi
#=> Hi

Experiment.new.say_hi
# NoMethodError: undefined method `say_hi’ for #<Experiment:0x007fc6b90e5178>
# from (irb):16
# from /usr/local/bin/irb:11:in `<main>’
```

Resource:[Ruby Require VS Load VS Include VS Extend](http://ionrails.com/2009/09/19/ruby_require-vs-load-vs-include-vs-extend/)

  


