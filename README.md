# Programming as Conversation Part 3: Introduction to Abstraction With Methods

## Learning Goals

- Demonstrate abstraction with methods
- Produce the shell of a method definition
- Define "implementation"
- Define "invoke" method, "call" method
- Define DRY
- Define a method
- Call a method

## Introduction

_Methods_ are used to bundle one or more activities into a single unit. In
daily life we do this all the time: "get ready for work" means: "take a shower,
walk the dog, eat breakfast." But each of _those_ activities are made up of
other sub-activities, and sub-sub activities.  "Take a shower" involves steps
like "wash hair" which itself has steps like "wet head under shower", "apply
shampoo", etc. At some point we reach "atomic" activities.

Nearly all programming languages have the idea of "bundling up work" under a
programmer-created name. While different languages might call them
"subroutines," "methods," or "functions," they all mean the same thing:
grouping work under a name that _we_ think is appropriate.

In this lesson we'll introduce methods, distinguish them from data types, and
cover how to create and execute them in your Ruby program.

## Demonstrate Abstraction With Methods

Methods define a new thing that your program can do. While variables in Ruby
store data, methods store a new routine or behavior your program can use.
Variables are like "nouns", things; methods are like "verbs," actions.

For example, imagine needing to say "Hello World!" five times. It could look
like this:

```ruby
puts "Hello World!"
puts "Hello World!"
puts "Hello World!"
puts "Hello World!"
puts "Hello World!"
```

This meets the requirement alright.  Now imagine that later in your program you
want to say "Hello World!" five times _again_. We would have to write "Hello
World!" five more times.

```ruby
puts "Hello World!"
puts "Hello World!"
puts "Hello World!"
puts "Hello World!"
puts "Hello World!"

# Other work here....

puts "Hello World!"
puts "Hello World!"
puts "Hello World!"
puts "Hello World!"
puts "Hello World!"
```

But we're repeating the same `String` over and over. It'd be easy to make a
typo and miss the error coding like this. Let's put that message in a variable
called `message`.

```ruby
message = "Hello World!"
puts message
puts message
puts message
puts message
puts message

# Other work here....

puts message
puts message
puts message
puts message
puts message
```

Here we made use of a variable to store the message, and didn't change anything
else.  You should be able to see here that by doing this our code is easier to
change. From "Hello World!" we could easily go to "Hola Mundo!" by making _one_
change versus making _10_ changes.

But all those `puts` appearing multiple times...there's something...that
bothers our programmer brains about this. It's seeing _so much repetition_.

![We sense something wrong about this](https://gph.is/2AinZom)

Could we reduce the repetition somehow?

If we created a _method_ to contain this "saying `message` five times action" we
could get rid of some of that repetition. Let's get to it! First, let's look at
the "template" of a method:

## Produce the Shell of a Method Definition

```ruby
def name_of_method(parameter1, parameter2, ... parameter_n)
# Code goes here
end
```

A method is defined by using the Ruby language word (or "keyword") `def`
followed by a name of our choosing.  The first line of `def name_of_method` is
called the method _signature_, it defines the basic properties of the method
including the name of the method, `name_of_method`. A method's name should
begin with a lowercase letter.  If you need multiple words, Rubyists use a `_`
to separate them. Separating words by underscore (`_`) is called _snake-case_
(because the shape looks like the words were `swallowed_up_by_a_snake`).

We'll ignore the parameters for the time being (but they'll come momentarily!).
Lastly we have to provide the keyword `end`.

Between the `def` and the `end` we write our _implementation_ or _method body_.

## Define "Implementation"

The implementation is the "more atomic" evaluations and statements that do the
work implied by the method's name. Just like `make_dinner` includes all sorts
of work around cooking, frying, and dicing, `say_hello_world_five_times`
involves something around outputting five times.

> **TIP**: A good practice is to define the method and then immediately close
> it with `end` _before_ writing the _implementation_. Many expressions in Ruby use
> `do...end` and it can be confusing to keep them all straight. By creating the
> `def (name)`...`end` "bookends," and _then_ filling out the implementation,
> we help prevent possible confusion.
>
> ```ruby
> def greeting # type this first
>   # # Third: start typing your implementation
> end # type this second
> ```

Here's the _implementation_ of `say_hello_world_five_times`.

```ruby
def say_hello_world_five_times
  message = "Hello World!"
  puts message
  puts message
  puts message
  puts message
  puts message
end
```

And, once integrated, our full code that said "Hello World" ten times could be
made much simpler:


```ruby
def say_hello_world_five_times
  message = "Hello World!"
  puts message
  puts message
  puts message
  puts message
  puts message
end

say_hello_world_five_times
# other work
say_hello_world_five_times
```

When you test this code, you'll see that the output is the same.
What's happening in this latest code is you're _teaching_ Ruby the word
`say_hello_world_five_times`. You tell Ruby to _do_ that work when you _invoke_
or _call_ the method.

## Define "Invoke" Method, "Call" Method

When we type the word `say_hello_world_five_times` in our program, it will
"invoke" or "call" the method, running the code within the method. You can
imagine that Ruby sees this new, invented word and then finds that word's
`def`inition and then hops up to it &mdash; breaking the **default sequence**.
It then "steps into" the method's implementation and follows the statements /
expressions until it reaches `end`. Then it hops back to where the method was
invoked and resumes the **default sequence**.

Follow the execution sequence in this following even-cleaner _implementation_
of `say_greeting_five_times`:

```ruby
def say_hello_world_five_times
   5.times do
    puts "Hello World!"
  end
end

say_hello_world_five_times
# other work
say_hello_world_five_times
```

That's certainly much more readable and understandable than our initial
_un-abstract_ code from the start of this lesson.

Programmers would say "We _abstracted_ the 'action,' or 'procedure,' of
`puts`-ing 'Hello World!' five times into a method." Later, we'll see ways of
making this code _even more_ abstract.

> **THINK AHEAD**: What if you wanted to change the message? What if you wanted
> to change the number of times you repeat? A version of
> `say_hello_world_five_times` which says, instead, any chosen `String` any
> number of times would be _even more_ "abstract."

## Define DRY

Programmers like abstraction. Programmers dislike repeating themselves. They
talk so much about non-repetition that there's an initialism for not repeating
oneself: DRY.

DRY stand for "Don't Repeat Yourself," a basic principle of software
development aimed at reducing repetition of information. Less code is good: It
saves time and effort, is easier to maintain, and reduces the chances of bugs.

> **RESEARCH FACT**: Numerous doctoral research projects have looked at the
> relationship between lines of code and bugs. It turns out the only
> significant predictor of fewer bugs is..._fewer lines of code_!

***Creating methods is a common and powerful tool of abstraction.***

When we see unsophisticated repetition, we want to reach for a form of
_abstraction_.


## Define a Method

Let's code a method for ourselves, step by step. Create a new file called `greeting.rb`. You can
use: `touch greeting.rb` from your terminal to do so. Open up `greeting.rb` in
your editor and paste the following code into it:

```ruby
def greeting
  puts "Hello World"
end
```

If you save your file and try to run it with `ruby greeting.rb`, you'll see:

```bash
$ ruby greeting.rb
$
```

You'll notice that when you run your program, there is no output and nothing
happens. We successfully _defined_ the method, but never _executed_ or _called_
it anywhere in the code. It's like we screwed in a new lightbulb, but never
flipped the switch to "on." Ruby reads your definition of `greeting` and then
says..."I'm done. Exit." Let's give it something to do before exiting: _call_
`greeting`.

## Call a Method

Update the code in `greeting.rb` to read:

```ruby
def greeting
  puts "Hello World"
end

greeting
```

Now we've called the method at the bottom our file. Save this file and run it
with `ruby greeting.rb`. You'll see:

```bash
$ ruby greeting.rb
Hello World
$
```

Now your program _actually executed_ the code in the method! Let's update the
code in `greeting.rb` again to the following:

```ruby
def greeting
  puts "Hello World"
end

greeting
greeting
greeting
greeting
greeting
```

Now we've written `greeting` five times at the bottom of the code. Save your
file and run it with `ruby greeting.rb`. You'll see:

```bash
$ ruby greeting.rb
Hello World
Hello World
Hello World
Hello World
Hello World
$
```

The word `greeting` will execute the body of the defined method for each
time it was called.

As a final step we could write a method to do the work of "say greeting five times:"

```ruby
def greeting
  puts "Hello World"
end

def say_greeting_five_times
  5.times do
    greeting
  end
end

say_greeting_five_times
```

You should start to see that bigger programs could be built of methods calling
sub-methods and those sub-methods calling sub-sub-methods. It was this style of
building procedures from others that was used inside the space shuttle or all
the servers in Amazon's AWS service. It can support staggeringly huge problems'
solutions!

## Conclusion

Methods are a big part of programming in Ruby and pretty much _every_ language.
We use them to save and perform repeatable actions. Knowing how to define and
call methods is crucial to building programs, as well as your development as a
programmer. You'll have to use them often, in big or small programs.

## Resources

* [Ruby Programming/Syntax/Method Calls](https://en.wikibooks.org/wiki/Ruby_Programming/Syntax/Method_Calls)
* [Ruby - Methods](https://www.tutorialspoint.com/ruby/ruby_methods.htm)
* [Ruby Methods](https://www.w3resource.com/ruby/ruby-methods.php)
