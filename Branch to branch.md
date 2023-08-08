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
We can repeatedly extend the collatz graph out from these numbers in both directions until they reach a branch.

We should consider two branches, generated at two different choices of $a$. We're going to start at $a_1$ and try to make progress towards another branch by repeatedly applying collatz.

$$\begin{align}
collatz(6a_1+4) &= 3a_1+2 && \text{even} \\
\textit{is\_branch}(3a_1+2) &\implies \exists b: 6b+4=3a_1+2 \\
&\implies b = \frac{1}{2}a+\frac{2}{3} && \text{$b \notin \mathbb{Z}$} \\
&\implies \bot
\end{align}$$
So the number reached by applying the even rule to the branch is never itself a branch.
However, it could itself be even or odd, depending on if $a_1$ is even or odd.

Let's trace the even case first.
We can substitute in a new variable $a_2$ where $2a_2=a_1$.

$$\begin{align}
collatz(3a_1+2) &= \\
a_1 = 2a_2 & && \text{even case}\\
collatz(3(2a_2)+2) &= 3a_2+1  \\
\textit{is\_branch}(3a_2+1) &\implies \exists b : 6b+4=3a_2+1 \\
&\implies b = \frac{1}{2}a_2-\frac{1}{2} && \text{for odd $a_2$}\\
\text{case } a_2 = 2a_3+1 \\
& = \frac{1}{2}(2a_3+1)-\frac{1}{2}\\
& = a_3 \\
\end{align}$$
This is our first successful traversal between two nodes, indexed by $a_1$ and $a_3$.
Substituting all the values in, we get:
$$\begin{align}
a_2 &= 2a_3+1, \\
a_1 &= 2a_2, \\
 &= 4a_3+2 \\
n_1 &= 6a_1+4 \\
&= 6(4a_3+2)+4 \\
&= 24a_3 + 16, \\
n_2 &= 6a_3+4 \\
\end{align}
$$
This tells us that we can generate exactly the pairs of nodes within the collatz graph linked by two even cases as $\langle 24a+16, 6a+4\rangle$, and indeed, you can see that the two nodes differ by a factor of 4.
The first few of these pairs are as follows:

$$\begin{matrix}
a & n_1 & n_2 \\
0 & 16 & 4 \\
1 & 40 & 10 \\
2 & 64 & 16 \\
3 & 88 & 22 \\
\end{matrix}$$
These links go node-even-node.
They never touch an odd number.

We will pick up our analysis again, looking at the case where $a_2$ is not odd.
$$\begin{align}
collatz(3a_2+1) &= \\
a_2 = 2a_3 & && \text{even $a_2$ case}\\
collatz(6a_3+1) &= 3(6a_3+1) + 1 && \text{odd case}\\
&= 18a_3 + 3 + 1 \\
&= 18a_3+4 \\
a_4 = 3a_3 \\
&= 6a_4 + 4 && \text{node}\\

 \\
\end{align}$$

So we've derived a second kind of link, that goes node-even-odd-node.
$$\begin{align}
3a_3 &= a_4, \\
a_2 &= 2a_3, \\
a_1 &= 2a_2 \\
&= 4a_3 \\
&= \frac{4}{3}a_4 \\
n_1 &= 6a_1+4 \\
&= 24a_3+4 \\
n_2 &= 6a_4+4 \\
&= 18a_3+4 \\
\end{align}$$
This one is a bit different, in that the 'anchor' generator is $a_3$, from which both $a_4$ and $a_1$ can be calculated.

$$\begin{matrix}
a & n_1 & n_2 \\
0 & 4 & 4 \\
1 & 28 & 22 \\
2 & 52 & 40 \\
3 & 76 & 56 \\
\end{matrix}$$
