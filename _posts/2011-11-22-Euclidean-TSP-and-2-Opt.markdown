---
layout: post
title: Euclidean TSP and 2-Opt
---

Having noticed a lack of easy-to-read information on the web about 2-Opt, I decided to (attempt to) change that. 2-Opt is an optimization technique used to find an approximate answer to the Traveling Salesman Problem (TSP). Specifically, 2-Opt as it is used to solve the Euclidean TSP will be the topic of this post.

For those of you who might not be aware, the Euclidean formulation of the TSP requires that the triangle inequality be in place for the graph in question. In other words, distances (or "weights") between vertices are literal. If you have a triangular arrangement of vertices, one edge's weight must be less than or equal to the sum of the remaining two edges' weights. You will never see something like this in a Euclidean problem:
   
{% highlight text %}
        O
     1 / \ 1
      /   \
     O-----O 
        3
{% endhighlight %}

Now that we have a better idea of what we're dealing with, let's introduce 2-Opt. 

Given a random starting tour of vertices, 2-Opt says that an improvement to the tour can be made by performing a pairwise exchange of two edges. What is a pairwise exchange? It means that you take two edges, remove them, and replace them with two *different* edges that still connect the vertices which made up the original edges. Essentially, the operation looks like this:

{% highlight text %}
      -- O   O --                   -- O - O --
    O      X      O    becomes    O             O
      -- O   O --                   -- O - O --
{% endhighlight %}

>**Note**: Although the edges are usually drawn as crossing prior to the exchange to get the point across, this may not always be the case. It's helpful, however, to visualize the crossing edges as hypotenuses that you are removing and replacing with sides of triangles (as in the above illustration) to convince yourself of why pairwise exchanges offer improvement.

2-Opt says that we should therefore perform pairwise exchanges until improvement is no longer possible, and we will end up with a shorter overall tour than the one we started with.

Well, that sounds easy. But how do we know if two edges are worth exchanging? How do we pick our edges?

The simple answer to the first question is:

>We don't.

Since we don't know, the only way to find out is to try! Really, what we must do is iterate through all possible pairwise exchanges (therefore looking at every possible *combination* of two edges) and calculate their improvements, ultimately using the exchange that offers the most improvement. We do this until no more improvements can be made.

However, there is one issue you might run into when attempting to exchange edges: Some of them share vertices.

Assume we have a list of vertices (a, b, c, d) such that there is an assumed edge from a vertex V<span><sub>i</sub></span> to V<span><sub>i+1</sub></span> in the list. If we try to remove the edges ab and bc and reassemble them in a new way such that we still have a complete tour and no vertices have been left out, we'll find that we can't. Try it. Incidentally, this is why 2-Opt will fail to optimize a tour such as this:

{% highlight text %}
            (a)   (c)
    O ------ O     O ------ O
    |         |   |         |
    |          | |          |
    |           |           |
    |           O (b)       |
    |                       |
    O ------ O --- O ------ O
{% endhighlight %}

when the optimal is this:

{% highlight text %}
    O ------ O --- O ------ O
    |                       |
    |                       |
    |                       |
    |           O           |
    |          | |          |
    O ------ O     O ------ O
{% endhighlight %}

As you can see, ab and bc in the above illustration share the same vertex, b. So, nothing can be done to improve the tour by swapping those edges as it simply isn't possible.

Assuming once again we have a list (a, b, c, d), the pairs of edges we *can* consider are:
    
{% highlight text %}
    ab and cd
    bc and da
    cd and ab
    da and bc
{% endhighlight %}

You'll notice the last two pairs are redundant. Hold onto that thought.

Now that we know which edges to perform pairwise exchanges on, we can gauge their improvements by measuring the difference of the total weight of both edges in the original pair versus the total weight of both edges in the new pair.

We should have everything we need now. Putting it all together, we can write some pseudo-code:

{% highlight python %}
    # where G is the graph and W is the weights of edges
    def 2opt(G=(V,E), W):
        # where tour is a list of vertices with assumed edges
        tour = random_tour(V)
        do:
            best_improvement = 0
            best_i, best_j = 0
            # we only need to iterate through the first half of the edges,
            # since the rest would be redundant
            for i from 0 upto len(tour) / 2 + 1:
                first_edge_u = i     # u represents the first vertex in the edge
                first_edge_v = i + 1 # v represents the second vertex in the edge
                # based on the second edge's v, we should stop 3 sooner
                for j from 0 upto len(tour) - 3:
                    second_edge_u = (i + j + 2) % len(tour)
                    second_edge_v = (i + j + 3) % len(tour)
                    old_edge_dists = W[tour[first_edge_u], tour[first_edge_v]] 
                                   + W[tour[second_edge_u], tour[second_edge_v]]
                    new_edge_dists = W[tour[first_edge_u], tour[second_edge_u]] 
                                   + W[tour[first_edge_v], tour[second_edge_v]]
                    improvement = old_edge_dists - new_edge_dists
                    if improvement > best_improvement:
                        best_improvement = improvement
                        best_i = first_edge_u
                        best_j = second_edge_u
            if best_improvement > 0:
                # swap the "middle" vertices
                tour.swap((best_i + 1) % len(tour), best_j)
        while best_improvement > 0
        return tour
{% endhighlight %}

That's 2-Opt, folks. If you have any issues or corrections, feel free to leave them in the comments or [email](/contact) me.
