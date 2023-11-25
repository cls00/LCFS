# Extending LCF codes

LCF code or LCF notation [[1](https://en.wikipedia.org/wiki/LCF_notation),[2](https://mathworld.wolfram.com/LCFNotation.html)] were created to describe large graphs while consuming little ink and paper and allowed the easy replication of graphs by hand.
The code works as follow:
- Use a sequence of integers written in brakets and an integer that describes the number of repeatitio. i.e. [5,-2]4
- The integers are interpreted modulo N where N is the number of vertices
- Arrange the vertices in a circle and form an hamiltonian cycles
- Start from an arbitrary vertex 
- Iterate over the sequence of integers and for each number connect the current node to the node that you obtain by moving, clockwise for positive numbers and anticlockwise for negative integer, along the cycle. After connecting the two nodes move clockwise by one node.
- Repeat as many times as specified.
- The sequence does not accept 0, 1 and N-1 values
- The sequence can only form Hamiltonian cycles
The code creates a beautiful process and many interesting graphs.

As soon as I saw it I thought it didn't feel right that 0 and 1 were not accepted. If we start producing random sequences we will definitely encounter those cases and in computer science sometimes those are all the numbers we have!
The other thought was: can we make it produce non-hamiltonian graphs? How about all the graphs?

First extension: The first idea is to use the Hamiltonian cycle constructed at the start only as scaffolding and removing it in the final graph. In my python implementation this hamiltonian is never really created and is 'there' only by virtue of the module operator wrapping things into a loop. In order to allow the code to construct a Hamiltonian cycle in case this was the desired product the number 1 is now accepted. So the sequence [1]10 in a 10 nodes graph will produce a classic Hamiltonian cycle. The “same” effect is achieved, just in reverse, by allowing N-1.

While the previous version of the code produces graphs that are always one connected component this code allows sequences that could produce disjoint graphs.
Can this produce any graphs? how easy is it to control the subsets/connected components? It is still not easy for me.

This led to the second extension which allows 0 as an input. The 0 is now associated with a 'skip' function in which no edges are added during this iteration.
When I wired the new code to a random sequences generator it produced all sorts of graphs. Some very ugly ones. Some bio-like and chemistry-like ones. Some others are just nice.

Coincidentally this was the first graph I produced and I was very pleased with it.
![image](Nugget121/First.png)

I do not know the sequence for this graph, so I learned straight away to print the actual sequence with each produced graph.
Admittedly many of the graphs that followed were not as pretty, you can see some of them in the [associated folder](https://github.com/stacs-cp/nuggets/tree/master/FinishedNuggets/Nugget121).

[In this colab](https://colab.research.google.com/drive/1yAuRioEPWvIgCE4tHrwgP7lDlyLGzR-O?usp=sharing) you can try out your own sequences or generate more random ones.

### Questions
How do we isolate families of sequences that produce graphs with desired properties? what kind of symmetries exists? different sequences may produce the same graph,  and for any given graph there is a smallest possible LCF code, how do we search it efficiently?

