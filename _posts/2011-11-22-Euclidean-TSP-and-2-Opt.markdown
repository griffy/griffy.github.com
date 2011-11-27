---
layout: post
title: Euclidean TSP and 2-Opt
---

Having noticed a lack of easy-to-read information on the web about 2-Opt, I decided to (attempt to) change that. 2-Opt is an optimization technique used to find an approximate answer to the Traveling Salesman Problem (TSP). Specifically, 2-Opt as it is used to solve the Euclidean TSP will be the topic of this post.

For those of you who might not be aware, the Euclidean formulation of the TSP requires that the triangle inequality be in place for the graph in question. In other words, distances (or "weights") between vertices are literal. If you have a triangular arrangement of vertices, one edge's weight must be less than or equal to the sum of the remaining two edges' weights. You will never see something like this in a Euclidean problem:
   
        O
     1 / \ 1
      /   \
     O-----O 
        3
        
Now that we have a better idea of what we're dealing with, let's introduce 2-Opt. 

Given a random starting tour of vertices, 2-Opt says that an improvement to the tour can be made by performing a pairwise exchange of two edges. What is a pairwise exchange? It means that you take two edges, remove them, and replace them with two *different* edges that still connect the vertices which made up the original edges. Essentially, the operation looks like this:

      -- O   O --                   -- O - O --
    O      X      O    becomes    O             O
      -- O   O --                   -- O - O --

>**Note**: Although the edges are usually drawn as crossing prior to the exchange to get the point across, this may not always be the case. It's helpful, however, to visualize the crossing edges as hypotenuses that you are removing and replacing with sides of triangles (as in the above illustration) to convince yourself of why pairwise exchanges offer improvement.

2-Opt says that we should therefore perform pairwise exchanges until improvement is no longer possible, and we will end up with a shorter overall tour than the one we started with.

Well, that sounds easy. But how do we know if two edges are worth exchanging? How do we pick our edges?

The simple answer to the first question is:

>We don't.

Since we don't know, the only way to find out is to try! Really, what we must do is iterate through all possible pairwise exchanges (therefore looking at every possible *combination* of two edges) and calculate their improvements, ultimately using the exchange that offers the most improvement. We do this until no more improvements can be made.

However, there is one issue you might run into when attempting to exchange edges: Some of them share vertices.

Assume we have a list of vertices (a, b, c, d) such that there is an assumed edge from a vertex V<span><sub>i</sub></span> to V<span><sub>i+1</sub></span> in the list. If we try to remove the edges ab and bc and reassemble them in a new way such that we still have a complete tour and no vertices have been left out, we'll find that we can't. Try it. Incidentally, this is why 2-Opt will fail to optimize a tour such as this:

            (a)   (c)
    O ------ O     O ------ O
    |         |   |         |
    |          | |          |
    |           |           |
    |           O (b)       |
    |                       |
    O ------ O --- O ------ O

when the optimal is this:

    O ------ O --- O ------ O
    |                       |
    |                       |
    |                       |
    |           O           |
    |          | |          |
    O ------ O     O ------ O

As you can see, ab and bc in the above illustration share the same vertex, b. So, nothing can be done to improve the tour by swapping those edges as it simply isn't possible.

Assuming once again we have a list (a, b, c, d), the pairs of edges we *can* consider are:
    
    ab and cd
    bc and da
    cd and ab
    da and bc
    
You'll notice the last two pairs are redundant. Hold onto that thought.

Now that we know which edges to perform pairwise exchanges on, we can gauge their improvements by measuring the difference of the total weight of both edges in the original pair versus the total weight of both edges in the new pair.

We should have everything we need now. Putting it all together, we can write some pseudo-code:

    // where G is the graph and W is the weights of edges
    def 2opt(G=(V,E), W)
        // where tour is a list of vertices with assumed edges
        tour = random_tour(V)
        do
            best_improvement = 0
            best_i, best_j
            // the -3 means we avoid the above redundant calculations
            for i from 0 to |V|-3
                for j from i+2 to |V|
                    old_edge_dists = W[tour[i], tour[i+1 or 0]] + W[tour[j], tour[j+1 or 0]]
                    new_edge_dists = W[tour[i], tour[j]] + W[tour[i+1 or 0], tour[j+1 or 0]]
                    improvement = old_edge_dists - new_edge_dists
                    if improvement > best_improvement
                        best_improvement = improvement
                        best_i = i
                        best_j = j
            tour.swap(best_i+1 or 0, best_j)
        while best_improvement > 0
        return tour
        
That's 2-Opt, folks. If you have any issues or corrections, feel free to leave them in the comments or [email](/contact.html) me.
