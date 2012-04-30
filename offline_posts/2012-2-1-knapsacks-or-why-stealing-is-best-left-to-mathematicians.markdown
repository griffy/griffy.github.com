---
layout: post
title: Knapsacks; or Why Stealing is Best Left to Mathematicians
---

The Knapsack Problem is one of the first examples of <s>cheating The Man</s> dynamic programming a fledgling computer scientist will be presented with in academia. Robert Sedgewick, in *C++ Algorithms*, states the problem as such:
>A thief robbing a safe finds it filled with N types of items of varying size and value, but has only a small knapsack of capacity M to use to carry the goods. The *knapsack problem* is to find the combination of items which the thief should choose for his knapsack in order to maximize the total value of all the items he takes.

Fantastic. I can't tell you how many M-sized backpacks I've gone through just this year carrying N books.

With bottom-up for knapsack, the goal is to solve the problem for every capacity *up to* M, assuming you have N items.

So, since you will always be considering N items (and not necessarily a bag of size M), it makes sense to have a for loop counting up to N, such that you can try out each item with each possible capacity. Because of this, it also makes sense to have another for loop inside the previous that counts up to M (since you're considering each possible capacity/bag for each item).

Inside this loop, you'll first want to check that the item you're considering is actually smaller than or equal in size to the capacity of the bag you're considering. If it is, carry on.

Now that size is no longer a matter, the only thing left to do is find out if the current "cost" (maybe better read as value) of a bag of this capacity is less than the value of a bag of size capacity-size_of_current_item + value_of_current_item. If it is, we've found the new optimal packing for this capacity. so, replace both the value of this capacity with the new one, AND (since we want to keep track of the items that make up any given optimal packing arrangement) set the optimal item for this size capacity to be the item.

