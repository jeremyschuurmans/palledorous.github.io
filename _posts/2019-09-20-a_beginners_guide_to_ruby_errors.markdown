---
layout: post
title:      "A Beginners Guide to Ruby Errors"
date:       2019-09-20 22:14:25 +0000
permalink:  a_beginners_guide_to_ruby_errors
---


One of the hardest things about programming, especially for the total beginner, is errors. You’ll see error messages way more often than you’ll see your code actually working, so learning to read and understand them is an essential skill that you have to develop. I struggled to understand error messages for the first several months of my programming journey. But when someone finally taught me how to read them, it completely changed my world. Debugging was so much easier (and more fun), and I started to become less frustrated. So I’m writing this for you, dear code newbie, because I wish someone had written something like this for me when I started. We’re going to talk about what errors are, the five most common errors you’ll encounter, what the errors mean, and how to resolve them. I won't be able to tell you how to deal with every situation in which you might see these errors, but I'll try and give you a basic framework to work with.

### What are errors?

Ruby will throw, or raise, an error when something in your program is not working properly. Error messages are your interpreter telling you that something needs to be fixed. If you don't know what I mean by "interpreter", don't worry so much about it now. It's beyond the scope of this post, but just understand that it has to do with how your code is read and executed in your computer. (If you're dying to know more, Google around, but finish reading this first).

Write this down on a Post-it and stick it next to your computer: _errors are not setbacks, they’re opportunities_. When your program throws an error, it doesn’t mean that you’re a bad programmer. I think that many of us in the beginning stages feel that if we were better at programming we could build an application and see minimal errors. Thinking this way will only lead to misery, so the first thing you need to realize is that errors are normal. Your program won’t be transmitted from your brain to your text editor in flawless form with awe-inspiring functionality. It will start broken, and require you to fix it. This is the fun part about programming, believe it or not. This is where you get to solve problems and gain the satisfaction that comes from that. And that’s what errors are there for. Errors are your friend, not your foe. Listen to them. They want to help you. Frustration is normal, but always remember that running into errors does not mean you’re a bad programmer. Instead, read on, and learn how to use them to your advantage.

### How do I read an error message?

Error messages give you three key pieces of information, the “where”, the “why”, and the “what”.

A typical error message looks like this:

```ruby
lib/my_file.rb:32::undefined local variable or method `some_variable' for main:Object (NameError)
```

`lib/my_file.rb:32` tells you that the error occurred in the `lib` directory, in the file `my_file.rb`, on `line 32` of that file. That's the "where".

```ruby undefined local variable or method `some_variable'``` tells you what went wrong. In this case, that Ruby found a local variable or method it didn't recognize, and it needs to be defined. That's the "why".

`(NameError)` tells you the type of exception Ruby raised. In this case, a `NameError`. You got it, that's the "what".

The most important piece of advice I can give you is to _always read the whole error_. When you're debugging, you're a detective and you need all the clues you can find. First, find out where the error occurred, and go to that line. Read that line of code, and all the lines immediately preceding and following it. Are there any other methods that call the one where the error occurred? Read those too. Once you do that, you can read the rest of the error message, and find out why the error was thrown, and what error it is. Suddenly you are no longer blindly trying to debug your code, but you have some perspective. You have information that you can use to figure out exactly what went wrong.

Let's start with this one, and talk about a few other common errors you'll encounter.

### NameError

**What the what?**

Generally, this error is raised when you call a variable or method that Ruby doesn’t recognize.

**How do I fix it?**

The first question to ask yourself is, did you define the method or variable in question? I can't tell you how many times I've tried to call a variable that I forgot to define. Check your spelling. Sometimes the problem is as simple as a spelling error in the variable or method you’re trying to call. Or did you assign something to a variable called "user_input", but mistakenly call it "input" in your method? Have you actually built the method you’re trying to call? If that all checks out, then you need to think about scope (if you have no idea what I mean by scope, [click here](http://ruby-for-beginners.rubymonstas.org/writing_methods/scopes.html)). Did you assign a local variable in one method and try to call it in another?


### SyntaxError
```ruby
32: syntax error, unexpected end-of-input, expecting keyword_end
```

**What the what?**

By far the most common error I encounter every day is the syntax error. You’ll see this bad boy pop up when there is something amiss with the structure of your code. For instance, if you forget an `end` somewhere.

**How do I fix it?**

Do what the error says. Fixing this one is as simple as adding an `end` where it says it needs one. Except when it’s not. Sometimes the error message will say you need a closing `end` but the source of your trouble is actually several lines above. Start at the top of your code and follow it down, making sure that everything is syntactically correct. Did you iterate over something (`do`) and forget to close it with an `end`? Are all your `if`, `elsif`, and `else` statements being used properly? One thing that will help you immensely is to learn to indent your code properly as you write it. Keep your code as organized and clean as you can. It will make it much easier to catch your syntax mistakes along the way.

### NoMethodError

**What the what?**

Closely related to the NameError is the NoMethodError. This means that you are trying to call a method on an object that doesn’t know how to do what you’re asking it to do. If you try and do math with a number that’s a string and not an integer, for instance, or if you created a variable with a nil value, and then forgot to assign another value to it.

Imagine a scenario in which you want to manipulate a range of numbers. You're not sure how to begin, so you start with something like this:

```ruby
def split_numbers
  1..10.split
end
```

If you try running this code to see what it returns, you would see:

```ruby
errors.rb:2:in `split_numbers': undefined method `split' for 10:Integer (NoMethodError)
 ```

**How do I fix it?**

Google around and make sure you’re using the right method for your object. In the example above, calling .split won't work because you can't call it on an integer, even if you're dealing with a range of integers. It's a method that operates on strings. Take a close look at your code, as well. It might not be so much that you're using the wrong method, but maybe you're using it in the wrong way.

### ArgumentError

**What the what?**

Say we have the following method:

```ruby
def upcase_this_string(string)
  puts string.upcase
end
```


If we call `upcase_this_string("I love Ruby")`, it will output "I LOVE RUBY". But if we call `upcase_this_string("I love Ruby", "a lot")`, we'll see this:
```ruby
1:in `upcase_this_string': wrong number of arguments (given 2, expected 1) (ArgumentError)
```

What this is telling you is that you gave two arguments in your method call, but your method was written to only take one argument.

**How do I fix it?**

There are a few scenarios that will cause Ruby to throw an ArgumentError, so make sure the number of arguments are correct, and that the datatype you are trying to use is valid.


### TypeError

**What the what?**

This particular error had me confused for a long time, and I'm sure I'm not alone, so let's dig in. Let's say you're doing some super simple arithmetic:
```ruby
def add_one_plus_one
  puts 1+1
end
```

Calling `add_one_plus_one` and running this file will output `2` to your terminal. but what if instead of `puts 1+1`, you had for some reason written `puts "one"+1`? You would see:
```ruby
errors.rb:2:in `+': no implicit conversion of Integer into String (TypeError)
```

**How do I fix it?**

Basically, all Ruby is telling you here is that when you tried to call `+1`, it expected the value behind the + sign to be an integer as well. Instead, you tried to call `+1` on a string. Ruby encountered an object that wasn't the type of object it expected it to be. So make sure that for whatever operation you are trying to perform, you are using the proper type of object. For this example, it would have to be either `1+1` which would output `2`, or `"one"+"one"`, which would result in `"oneone"`.

### FUN-FACT

You've probably heard that Ruby is a pure object-oriented language, and that everything in Ruby is an object. Would it blow your mind if I pointed out that this holds true for your errors as well? Errors are objects, instances of the Exception class. If you don't find this cool yet, just wait. Object-orientation is awesome. Suspend disbelief until you get there, and you'll see what I mean.

### Resources

For more information on the Exception class, and Ruby errors, see [the Ruby docs](https://ruby-doc.org/core-2.2.0/Exception.html)


If I've done my job, error messages now seem more understandable, less intimidating, and you now have some idea how to resolve them.

Happy coding!
