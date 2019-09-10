---
layout: post
title:      "TDD Basics: How to write an RSpec test"
date:       2019-09-10 12:53:19 +0000
permalink:  tdd_basics_how_to_write_an_rspec_test
---


![](https://thepracticaldev.s3.amazonaws.com/i/hxl9mja9w2jc67r4lese.png)


Testing can be intimidating, especially for beginners, but it really doesn't have to be that way. With a little practice, writing tests is actually fun. So let's learn RSpec from the ground up and give this testing thing a try. We'll start from scratch and learn how to write a test while solving a basic Codewars challenge using Test Driven Development (TDD). _Keep in mind as we do this that the file structure I'm using is overkill for the task of solving a simple code challenge._ It is, however, the way you would do it for a larger project, so I'm teaching it this way on purpose so you understand how to properly install, set up, and use RSpec.

**Installation**

From your project directory, run `gem install rspec`.

![gem install rspec](https://thepracticaldev.s3.amazonaws.com/i/wloyemubgrb0ch3qhsvg.png)

Now run `rspec --init`

![rspec --init](https://thepracticaldev.s3.amazonaws.com/i/w5n0eao7079kn3kbeawn.png)

**Setup**

You will see that this command created a `.rspec` file in your project directory, and a `spec` folder with a `spec_helper.rb` file inside it. These files are for configuration and you don't need to worry about them right now, except to say that we will need to require our `spec_helper.rb` file in the file we write our tests in. More on that in a moment.

The Codewars challenge we'll be working with today is called [Descending Order](https://www.codewars.com/kata/5467e4d82edf8bbf40000155). Here's the brief:
>Your task is to make a function that can take any non-negative integer as a argument and return it with its digits in descending order. Essentially, rearrange the digits to create the highest possible number.

>Examples:
>Input: 21445 Output: 54421

>Input: 145263 Output: 654321

>Input: 1254859723 Output: 9875543221

Lets start by creating a `descending_order.rb` file where we'll code our solution.

![descending_order.rb](https://thepracticaldev.s3.amazonaws.com/i/leu5tfvb6u65xqbh1f2w.png)

Now in your `spec` directory, create a `descending_order_spec.rb` file. This is where we'll write our tests.

![descending_order_spec.rb](https://thepracticaldev.s3.amazonaws.com/i/r0btz7suj9v7jw551141.png)

Whenever you create a file to write tests in, it must be located in the `spec` folder, and it must follow this convention: `[filename]_spec.rb`. When you run RSpec, it will look in your `spec` folder for any `_spec.rb` files, and it'll run those. If your filenames don't follow that convention, RSpec won't be able to find them.

At the top of `spec/descending_order_spec.rb` require your `spec_helper` file and your `descending_order.rb` file.

```ruby
require_relative './spec_helper.rb'
require_relative '../descending_order.rb'
```
**Writing the test**

Test Driven Development involves writing a test that fails, and then writing code to make it pass, followed by refactoring. Because failing test output is colored red in your terminal, and passing test output is colored green, the TDD process is frequently described as Red-Green-Refactor.

First, we start with a `describe` block that specifies what we're testing. In this case we'll be testing a method that we'll call `descending_order` when we write it.

```ruby
describe 'descending_order' do

end
```
Next we write an `it` block with a description of what our method will do when it works. At this point we know what our method needs to do, but we don't know exactly how we're going to make that happen.

```ruby
describe 'descending_order' do
  it 'takes any integer and returns its digits in descending order' do


  end
end
```
Now we call our as yet unwritten method, passing in an example argument that RSpec will use to test the code in our `descending_order` method. Set that to a variable for convenience and organization. This will make it easier to test other values later.

```ruby
describe 'descending_order' do
  it 'takes in any integer and returns its digits in descending order' do
    ordered_1 = descending_order(1587956342)


  end
end
```
And lastly we write our expectation. Let's think about this part for a second. This is what we know at this point:

1. We need to write a method called `descending_order` that takes an integer value and sorts the digits from highest to lowest.
2. Our test is going to call `descending_order`, passing in `1587956342` as an argument.
3. Our method will need to then return `9876554321`.
4. So, since our method call is set to the variable `ordered_1`, if our code works, we expect `ordered_1` to equal `9876554321`.

The beauty of RSpec is that it gives us several methods that we can use to set expectations for working code. In this example, we're utilizing the methods `expect`, `to`, and `equal`. I'll talk about others, and give you resources on them in subsequent posts.

```ruby
describe 'descending_order' do
  it 'takes in any integer and returns its digits in descending order' do
    ordered_1 = descending_order(1587956342)

    expect(ordered_1).to eq(9876554321)
  end
end
```
And we just wrote our first test!

**Running the test suite**

Run the test by typing `rspec` into your terminal. Alternately, and this is useful if you have a very large test suite, you can run specific test files like so: `rspec spec/descending_order_spec.rb`.

**Pro-tip:** As you start working with larger test suites, it can become overwhelming to run your tests and see dozens of failing examples. Appending `--fail-fast` or simply `--f-f` will show you one failing test at a time. Like so: `rspec --f-f`.

Running your tests should give you output similar to this:

![failing test output](https://thepracticaldev.s3.amazonaws.com/i/6rfvqjj019j0paeu8oba.png)

Here we have our first error. Lets break it down line by line.

`1) descending_order takes in any integer and returns its digits in descending order`

This first line is our `it` block from our test. It's telling us what the method is supposed to be doing but isn't.

`Failure/Error: ordered_1 = descending_order(1587956342)`

The next line tells us where in our test the failure occurred, in this case it failed when we assigned the `descending_order` method to the `ordered_1` variable.

`NoMethodError:
          undefined method 'descending_order' for ...`

This line here is the actual error that occurred. Here RSpec is telling us that it can't find a `descending_order` method in the file we're testing, which makes sense because we haven't written one yet.

**Pro-tip:** Get in the habit now of reading the entire error message, not just the specific exception. The entire error contains valuable information that will help you debug your code. I can't stress this enough. _Read the whole error message_.

Also, this line here, right underneath the `NoMethodError`

```ruby
# ./spec/descending_order_spec.rb:6:in `block (2 levels) in <top (required)>'
```
might not look too useful at first, but this is powerful information because it tells you the exact line that failed in your test suite. In this case, the failure occurred on line 6 in the file `descending_order_spec.rb` in the `spec` directory, as shown here in the first half of that line:

`# ./spec/descending_order_spec.rb:6`

If you find yourself in a situation where you're working on an unfamiliar application with a full test suite, it's always a good idea to go into the specs and read the tests. They will give you valuable information about how the code works/is supposed to work, and you will understand the tests better when they are run.

For example, in our test we have the line `expect(ordered_1).to eq(9876554321)`. This line is much easier to understand when you read the whole test and see that `ordered_1` contains the argument `1587956342`. So now we understand right away that when passed `1587956342` the method is supposed to return `9876554321`. That's not obvious from the test output itself.

This is probably a good time to mention that it's extremely important that your tests be clean, organized, and understandable to anyone who will read them after you. One of the purposes of testing is to guard your code against regression. When your code needs to be debugged in the future, either by you or someone else, the test suite should be able to be read and understood right away.

So now we need to define a `descending_order` method. Let's do that. Open `descending_order.rb` and write the following:

```ruby
def descending_order(num)

end
```
And run the test again.

![new error](https://thepracticaldev.s3.amazonaws.com/i/h9fh83r5sbfxvjunnzot.png)

We have a new error now, which is great news! That means we're making progress. At this point in our test, RSpec called the `descending_order` method, and passed it `1587956342`. It expected the method to then return `9876554321`, but instead it returned `nil`. This is because we've only defined the method, we haven't yet given it any sorting ability.

We know that Ruby has a handy `#sort` method, so lets try that.

```ruby
def descending_order(num)
  num.sort
end
```
![another error](https://thepracticaldev.s3.amazonaws.com/i/ncu1pkqojfigz2fovd41.png)

Another error! It's counter-intuitive because encountering one error after another can be frustrating, but always remember that new errors mean you're making progress toward a solution (most of the time, anyway).

The test output is telling us we tried to call `#sort` on an integer, and that's not allowed. `1587956342` is a single integer value, and `#sort` can't sort individual digits like that. How can we get access to the individual digits? Well, we need to split our integer, perhaps into an array. We can do that a number of ways, but the simplest way is to use the `#digits` method.

```ruby
def descending_order(num)
  num.digits.sort
end
```
Running our test again gives us this output:

![returns a sorted array](https://thepracticaldev.s3.amazonaws.com/i/ovfwn0caf9h6zp2fxdv5.png)

We're getting closer! In this case, RSpec expected `9876554321`, but got `[1, 2, 3, 4, 5, 5, 6, 7, 8, 9]`, a sorted array! The problem (one of them) is that it's sorted in ascending order, and we need it sorted in descending order.

We can do that like so, using one of my favorite operators, `<=>`, the [spaceship](https://stackoverflow.com/questions/827649/what-is-the-ruby-spaceship-operator):

```ruby
def descending_order(num)
  num.digits.sort{ |a, b| b <=> a }
end
```
![array sorted in descending order](https://thepracticaldev.s3.amazonaws.com/i/k6vf0vkmzfjioyx1vwoh.png)

Excellent! Our array is sorted in the right order, but now we need it to be an integer again. Let's join it.

```ruby
def descending_order(num)
  num.digits.sort{ |a, b| b <=> a }.join
end
```
![string](https://thepracticaldev.s3.amazonaws.com/i/psyooixrq9wpr1oydjik.png)

We're so close now! Let's convert that string to an integer and we should be passing.

```ruby
def descending_order(num)
  num.digits.sort{ |a, b| b <=> a }.join.to_i
end
```
![passing test](https://thepracticaldev.s3.amazonaws.com/i/mnkqqzkty41gr1logh83.png)

It works! We successfully used TDD to solve this code challenge. We're not quite done yet, though.

**Refactoring the test and the code**

It's important to make sure that your tests are simple, but also thorough. Let's add a couple more variables, just to make sure everything still works. Since we're solving a Codewars challenge, we'll use the ones they use.

```ruby
describe 'descending_order' do
  it 'takes in any integer and returns its digits in descending order' do
    ordered_1 = descending_order(1587956342)
    ordered_2 = descending_order(21445)
    ordered_3 = descending_order(145263)
    ordered_4 = descending_order(1254859723)

    expect(ordered_1).to eq(9876554321)
    expect(ordered_2).to eq(54421)
    expect(ordered_3).to eq(654321)
    expect(ordered_4).to eq(9875543221)
  end
end
```
The tests should still be passing when you run `rspec` now.

It's also important to account for edge cases. What does our method do if it's passed a single digit integer, for example? We can guess, but let's find out for sure. Because we're testing a different functionality of this method, we'll write a new test for it.

We'll start with our `it` block:

```ruby
it 'returns the original integer if it only has one digit' do

end
```
Pass in arguments and set to variables:

```ruby
it 'returns the original integer if it only has one digit' do
  int_0 = descending_order(0)
  int_1 = descending_order(1)

end
```
And set our expectations:

```ruby
it 'returns the original integer if it only has one digit' do
  int_0 = descending_order(0)
  int_1 = descending_order(1)

  expect(int_0).to eq(0)
  expect(int_1).to eq(1)
end
```
So now our full test suite for this challenge looks like this:

```ruby
require_relative './spec_helper.rb'
require_relative '../descending_order.rb'

describe 'descending_order' do
  it 'takes in any integer and returns its digits in descending order' do
    ordered_1 = descending_order(1587956342)
    ordered_2 = descending_order(21445)
    ordered_3 = descending_order(145263)
    ordered_4 = descending_order(1254859723)

    expect(ordered_1).to eq(9876554321)
    expect(ordered_2).to eq(54421)
    expect(ordered_3).to eq(654321)
    expect(ordered_4).to eq(9875543221)
  end

  it 'returns the original integer if it only has one digit' do
    int_0 = descending_order(0)
    int_1 = descending_order(1)

    expect(int_0).to eq(0)
    expect(int_1).to eq(1)
  end
end
```
Running `rspec` shows us that both of our tests are still passing. Congratulations! You just used TDD and RSpec to solve a Codewars challenge. At this point, if we had more than a three-line method, we would refactor the code, in keeping with best practices and the Red-Green-Refactor methodology. This is not necessary now, but it's an important last step that you don't want to forget. Keep these basic principles in mind as we move ahead and, with practice, Test Driven Development will become second nature.
