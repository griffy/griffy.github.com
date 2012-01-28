---
layout: post
title: how is project formed? how ruby get wretten?
---

*Note*: If you don't understand the point of this post, you're not its intendended audience. ;)

### Part 1

Write a program, without creating any functions to break up the work for you, that presents the following Knock-Knock exchange:

    $ *knock knock*
    $ Who's there? <- user input
    $ Doctor
    $ Doctor who?  <- user input
    $ Exactly!

Try your best to get the formatting to look exactly like that. If the user does not enter the text exactly as it should be, print out a message saying, "You ruined the joke!" and quit.

When you finish the program, save it in a file named part1.rb

### Part 2

Let's spruce up the previous program a bit, shall we?

Should we really punish someone who types "Doctor Who?" instead of "Doctor who?" I think not! Figure out a way to accept responses ignoring case. Hint: Strings are objects, and objects have methods.

Now, perhaps our user got distracted and really didn't mean to type this:

    $ ...
    $ Doctor
    $ Derp
    
I think we should give users 3 chances to say the right thing! So, a poorly-communicated exchange should go something like this:

    $ *knock knock*
    $ What's it?
    $ I don't think you meant to say "When's it?". Let's try that again.
    $ *knock knock*
    $ Why's that?
    $ I don't think you meant to say "Why's that?". Let's try that again.
    $ *knock knock*
    $ When's this?
    $ I gave you 3 chances, and you still ruined the joke!

Tip: Doing the same thing over and over... I think there's a construct for that...

ProTip: How many .times do I have to tell you to look things up yourself!

When you've added that functionality, save the file as part2.rb

### Part 3 aka An Entirely Different Project

Use as many control statements (if statements, case statements, loops) and functions as you can for this one. If you think a section of code is redundant, it probably is. Make it a function. If you find yourself calling the same function over and over, try a loop. The more you do this, the more you get a feel for what makes sense and actually improves the code and its readability. If you have a function that calls one line of code, that's probably an unnecessary function. Though it might read better, and sometimes that increase in readability is worth the trade-off. Figure it out yo damn self!

The goal is to create... drum roll please... a text adventure of your choosing! Trolls welcome.

It should follow this general flow:
    A series of exchanges in which each exchange consists of something(s) said by you, the computer, and something returned by the user--a choice from a menu you just presented, most likely.
    
Like this:

    $ Welcome to Adventuria!
    $ You're in a dark corridor. You
    $ 1. Dance
    $ 2. Run away screaming
    $ 3. Turn on the light
    $ 3
    $ You turn on a light, and a troll appears!
    $ 1. Slay it!
    $ 2. Give it a hug
    $ 3. Tickle it
    $ 1
    $ You slay the peaceful troll and acquire one gold coin. I hope it was worth it.
    $ You win! The End.
    
#### Suggestions
Write one function per output-input exchange such that all state for it is contained inside. It could look something like this:

    def exchange1
        // print out text and a menu of choices
        // get input
        // decide next exchange to call
        // call it
    end

This is only one idea. You could do this many ways.

#### Extra Credit
See how I said "a series" and "exchanges" up there? A series is... omg, it's like a list (aka array)! As for "exchanges", that's a cool word. A solid noun. As you learn more about Object-Oriented Programming, you'll learn that when you have a solid noun like that to describe your problem, it's usually a good idea to make that your object, and make methods that operate on that object.

When done, save it as part3.rb and send it on upstream.
