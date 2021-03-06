---
layout: post
title: Ruby (I think that) You Must Know to Do Rails
---

### Method Calls
You can call a method in Ruby without parentheses, regardless of whether or not it takes parameters. This is done a lot.

{% highlight ruby %}
    obj.method_without_params()
    # could just be:
    obj.method_without_params
    
    obj.method_with_params(param1, param2)
    # could just be:
    obj.method_with_params param1, param2
{% endhighlight %}

Accepted practice seems to be to always leave out the parentheses unless the parameters you're passing are themselves method calls; in that case, you'd still leave out parentheses for the outermost call, but use them for all inner calls.


### Symbols and Hashes
A symbol (e.g., :key) is an object just like a string. It's not a name (like a variable name), but an actual object. The reason symbols are preferred over strings is that
1.  if you sprinkle string literals all throughout your code, each of those will be a separate object. When it comes to symbols, there will only be one instance of the symbol no matter how many places you use it in your code.
2.  it's easier on the eyes as an identifier, such as in a hash.

Which brings me to hashes. Hashes are used everywhere in Ruby. Unlike other languages, they're just as prevalent as arrays, if not moreso. A Hash object can be created in many ways:

{% highlight ruby %}
    # 1
    hash = Hash.new
    hash[:key] = value

    # 2
    hash = {}
    hash[:key] = value

    # 3
    hash = { :key => value }

    # 4
    hash = { key: value }
{% endhighlight %}

That last one was just introduced in Ruby 1.9. Use it at your own discretion.

When you're calling a method in Ruby that accepts a hash, you can do something fancy:

{% highlight ruby %}
    obj.method(:key => value)
    # or just:
    obj.method :key => value
{% endhighlight %}

Notice the lack of curly braces in either case.


### Code Blocks
You can actually pass *code* as an object. It's referred to as a code block.

As a simple example, let's say you wanted to iterate through an array and print out each item. In Ruby, it'd be something like this:

{% highlight ruby %}
    names.each do |name|
      puts name
    end
{% endhighlight %}

This can be shortened to:

{% highlight ruby %}
    names.each { |name| puts name }
{% endhighlight %}

Great, but what's it doing? Well, names is an array of names. Arrays in Ruby have an "each" method that accepts a code block as a parameter. The code block in this instance is everything between the "do" and "end" keywords, or curly braces in the second instance. What's between the pipes, you ask? Let's pretend our code block is actually a function, but without a name. Sometimes we want our functions to accept parameters, so we write a placeholder name to be our formal parameter. That's exactly what's between the pipes in a code block.

To trace the flow of execution, what happens when Ruby gets to this point is to call "each" with your code block as a parameter. So, in "each" it begins to iterate through the list and *yield* the values, in succession, to your code block. Essentially, "each" calls your code like a function for each value in the array. So, if there are 10 items in the array, your code block will be called 10 times by "each."


### Classes Are Objects
See [here](http://joel-griffith.com/2012/05/20/A-Fast-Informal-Explanation-of-Ruby%27s-Object-Model)


### Style
*  Class names: CamelCase
*  Variables: snake_case
*  Indentation: 2 spaces
*  Getters and setters: nowhere to be found. Use attr_accessor (get/set), attr_reader (get), or attr_writer (set) instead.

        
If you have any issues or corrections, feel free to leave them in the comments or [email](/contact) me.
