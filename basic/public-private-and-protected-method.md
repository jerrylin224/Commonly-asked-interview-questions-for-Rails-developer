# Public, private and protected

## Public method

Public method is method we can call inside class or make instance as a receiver.

```ruby
class Test
  def say_hello
    puts "Hi"
  end
  
  def say_hello_again
    say_hello
  end
  
  def say_hello_twice
    self.say_hello
  end
end

test = Test.new

test.say_hello
#=> Hi

test.say_hello_again
#=> Hi

test.say_hello_twice
#=> Hi
```

## Private method

Private method can not be called with a receiver. That is, you can’t call the method with a self or the object as the receiver.

```ruby
class Test  
  def say_hello_again
    day_hello
  end
  
  def say_hello_twice
    self.say_hello
  end

  private

  def say_hello
    puts "Hi"
  end
end

test = Test.new

test.say_hello
#> NoMethodError: private method `say_hello' called for #<Test:0x007fae0e96c2d8>
#> from (irb):34
#> from /Users/pk60905/.rvm/rubies/ruby-2.1.2/bin/irb:11:in `<main>'

test.say_hello_again
#=> Hi

test.say_hello_twice
#=> NoMethodError: private method `say_hello' called for #<Test:0x007fae0e96c2d8>
#=> from (irb):24:in `say_hello_twice'
#=> from (irb):36
#=> from /Users/pk60905/.rvm/rubies/ruby-2.1.2/bin/irb:11:in `<main>'
```

## Protected method

Protected method act like the combination of public and private method, which means while inside the class, you can call the method with or without receiver, but outside of the class, you can’t call the method with a receiver.

```ruby
test = Test.new

test.say_hello
#=> NoMethodError: protected method `say_hello' called for #<Test:0x007fae0d8590b8>
#=> from (irb):52
#=> from /Users/pk60905/.rvm/rubies/ruby-2.1.2/bin/irb:11:in `<main>'

test.say_hello_again
#=> Hi

test.say_hello_twice
#=> Hi
```



