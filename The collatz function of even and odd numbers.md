In [[All numbers are either odd or even]] we used proofs to derive some things about odd and even numbers, and to make generators that can construct all of them.
Here, we apply this to the collatz function, and use it to derive some useful stuff.
# The collatz function of any odd number is always even
The next thing we will do in this section on odd and even numbers is show that collatz(n) is even when n is odd.
Then we've done all we need to do now with oddness and evenness.
As we've got a bit more comfortable with constructing and writing proofs, we're going to be a it more terse, combining some steps.
$$\begin{align}
odd(n) \implies even(collatz(n)) && \text{(goal)} \\
odd(n) \implies \exists a: 2a+1=n, && \text{(definition)}, \\
collatz(n \text{ if } n \text{ is odd}) = 3n+1, && \text{(definition)}\\
even(3n+1) \implies \exists b : 2b = 3n+1, && \text{(definition)}\\
2b = 3(2a+1)+1 && \text{(substitute $n$)}\\
b = 3a + \frac{3}{2} + \frac{1}{2} && \text{(simplify)} \\
b = 3a+2 && \text{(integer b exists)}
\end{align}$$
Not only does this give us a proof that the collatz function always generates an even number from an odd one, but it gives us a way to construct all of the (even) integers reached by applying collatz to odd numbers, together with the odd number that they came from.
$$\begin{align}
\forall a: collatz(2a+1) = 6a + 4 \\
\textit{gen\_collatz\_odd}(a): \langle \textit{gen\_odd}(a), \textit{gen\_even}(3a+2) \rangle
\end{align}$$
The pairs $\langle 2n+1, 6n+4 \rangle$ are all of the pairs of numbers linked by green arrows in the [[The Collatz Conjecture|introduction]].
Notice that while every odd number is a source of an odd-to-even jump in the collatz function, only some even numbers are destinations.

As we always reach an even number, we know we can immediately apply collatze again to derive:
$$collatz(collatz(2a+1)) = 3a+2$$
# The collatz function of even numbers could be even or odd
Lastly, let's think about collatz for the even case.
$$\begin{align}
even(n) & \implies \exists a: 2a = n, \\
collatz(n : n \text{ is even}) &= n/2, \\
&= a
\end{align}$$
So that was a long-winded way of deriving the obvious constructor for all destinations from an even source.
$$\begin{align}
\forall n: collatz(2a) = a \\
\textit{gen\_collatz\_even}(a): \langle \textit{gen\_even}(a), a \rangle
\end{align}$$
Again, we can see that $\langle 2a, a \rangle$ are all pairs of numbers linked by grey arrows in the [[The Collatz Conjecture|introduction]].
This is quite neat.
We can, if we wished, count through all possible values of $n$, starting at 0 and going up, and by applying these two rules, we will generate all possible steps in all possible collatz sequences.

This is the power of proofs.
They don't just tell us that something is true in particular, but they tell us that some rule is true always.
Knowing it's true always lets us use this to build other things, like these collatz arrow generators, and know that we haven't missed anything out.

# Every number is part of a collatz graph
Is it possible that there is some number that no collatz sequence passes through?
If so, then this would be a number that can't reach 1.
We can show that no such "missing" number exists quite easily.

1. the collatz function is defined for all numbers, so all numbers have following numbers in a chain, and
2. given any number $a$, the even case for the collatz function reaches $a$ from $2a$.
Given this, we know that the graph of all pairs of integers linked by the collatz function passes through all integers.