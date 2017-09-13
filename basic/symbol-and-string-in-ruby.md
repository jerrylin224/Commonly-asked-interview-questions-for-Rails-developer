# String and Symbol in Ruby

## What is string?

A string is a list of characters in a specific sequence. Strings are surrounded by either single quotes \(`'hi there'`\) or double quotes \(`"hi there"`\). A string is an instance of String class. Two strings with the same contents are two different objects.

```ruby
"apple".object_id
 => 70280408292320

"apple".object_id
 => 70280408286140

 "apple".class
=> String
```

## What is symbol

Ruby symbols are created by placing a colon \(:\) before a word. You can think of it as an immutable string. A symbol is an instance of Symbol class. For any given name of symbol there is only one Symbol object.

```
:apple.object_
=> 4454888

:apple.object_id
 => 4454888

:apple.class

=> Symbol
```

One more difference between string and symbol is, you can mutate the value of a string, but you can't mutate the value of a symbol\(Symbol class doesn't have any instance method to mutate the value\).

## Conversion between symbol and string

Ruby has methods to convert object from symbol to string and vice versa.

```ruby
"apple".to_sym
=> :apple
:apple.to_s
=> "apple"
```

## When to use symbol

As we mentioned above, for any given name of symbol there is only one Symbol object. So every time when we call the same symbol the program don't need to create a new object again. So compare with using string, it does save many resource.

One of the most common timing to use symbol in Ruby is defining a hash. For example if we have the following hash, and we need to get the value of the value frequently.

```ruby
hosts = {
  'tokyo' => 'machine1',
  'singapore'  => 'machine2',
  'beijing' => 'machine3',
  'taipei' =>  'machine4',
  'manila' =>　'machine5'
}

host["tokyo"]
#=> 'machine1'
```

If using string as key, every time we get the value from the hash, we have to create a new string object. Since in hash, the \`key\` is just a name, and we don't intend to change it's value. Instead of using string as the key, it is a good timing to use symbol.

```ruby
hosts　=　{
 :tokyo => 'machine1',
 :singapore  => 'machine2',
 :beijing => 'machine3',
 :taipei => 'machine4',
 :manila =>　'machine5'
}
```

Resource: [Introduction to Programming with Ruby](https://launchschool.com/books/ruby/read/basics#strings)

Resource: [Ruby Symbols](http://rubylearning.com/satishtalim/ruby_symbols.html)

Resource: [String and Symbol in Ruby](http://kaochenlong.com/en/2016/04/25/string-and-symbol-in-ruby/)

Resource: [Ruby及Rails當中的:symbol代表什麼意思？](http://ithelp.ithome.com.tw/articles/10161202)

