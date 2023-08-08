In [[The collatz function of even and odd numbers]] we show that every number is on the collatz graph.
We also showed that the collatz graph passes through all integers.
However, this doesn't prove the collatz conjecture.
It's possible that there's some subset of the natural numbers that never join up with the graph that passes through 1.
Perhaps we can make progress by better understanding the topology of the graph.

The graph itself has two kinds of nodes.
All nodes have a single out-going link.
However, the even numbers reached from odd numbers have two incoming links.
They are the branching nodes.
Is it possible to collapse away all the other numbers, leaving only the branching nodes behind, without loosing any generality?
To prove this, we need to show that all numbers are branches themselves, or are between two branches.

The branches themselves are the numbers $6a+4$.
So that leaves us all the other numbers $6a+b$ where b is is one of ${0,1,2,3,5}$ that are not branch points.
We can repeatedly apply the collatz function to each of these, and see if they do hit a branch.
The odd cases hit a branch 

