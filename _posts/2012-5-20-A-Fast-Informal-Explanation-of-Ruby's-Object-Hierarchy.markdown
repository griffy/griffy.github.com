---
layout: post
title: A Fast Informal Explanation of Ruby's Object Hierarchy
---

Ruby is a cool language in no small part because it forces you to think in new ways about how to write code. While this is a great thing, learning a new concept for the first time is always challenging. For me, understanding code blocks in Ruby came more naturally than understanding its object hierarchy, but this was undoubtedly influenced by my previous exposure to closures from other languages; learning what a closure was for the first time was not so easy. My point is that you should not be discouraged when you can't grasp something the first time you're introduced to it. Instead, you should look for alternative ways of learning the topic that relate back to what you already know. 

I'd like to offer one of those alternative ways: a less jargony explanation of how Ruby's object hierarchy works.

It's often repeated that "any class you define in Ruby is an instance of the Class class, which is itself a subclass of the Object class." Well, that's a bit counterintuitive, isn't it? How can we define a Class to be a subclass of a.. class?

Ruby is an object-oriented language. We know this much. So, like Java, it has a fundamental class which all other classes are subclasses of: Object. Java cheats to accomplish this feat. If you're a Java programmer, you'll know that if you define a class you don't have to explicitly say it inherits from the Object class. Java goes behind your back and makes it implicit. 

Ruby is also a cheater, but in a slightly different way. Ruby code is dynamic. It's *alive*. By that, I mean that when you're defining your class as you would in Java, that *definition* is actually creating an object. When your program is run, Ruby takes your definition of that class and actually creates a global object, giving it the name of your class. That object? It's an instance of the Class class--which is, as I mentioned earlier, a subclass of Ruby's Object class.

This means that if you define the following class:

    class Person
    end
    
What you're actually doing is more along these lines:
    
    Person = Class.new(<definition>)
    
If you think of a class you create as being *alive*--being a real variable like any other you can manipulate--things fall into place. All of a sudden it makes sense why you write Person.new any time you want a new instance of the Person class. You're really calling the "new" method of the Person object (which, again, is an instance of the Class class), and it's returning an instance of the Person *class* that you defined.

It's all a bit like the Kansas City Shuffle.
        
If you have any issues or corrections, feel free to leave them in the comments or [email](/contact.html) me.
