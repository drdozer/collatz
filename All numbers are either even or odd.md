It is obvious that all numbers are either even or odd.
But maths isn't about what is obvious.
Instead, it is about what we can prove.
Let's first define what an even number is:
$$even(m) \iff \exists n: m = 2n$$
Let's unpack that notation a bit, as we will be using similar notation throughout.
The expression $even(m)$ says that we apply the predicate[^1] $even$ to the value $m$.
In this case, we expect the $even$ function to be true when $m$ is even, and false otherwise.
The $\iff$ arrow is a way to write down $\textit{iff}$, which isn't a misspelling of $\textit{if}$, but rather, it means "if and only if".
The right part says that there exists some value for $n$ such that $m=2n$.
This is called *existential quantification*, and you can think of it as summoning a value for $n$ into existence, as long as it satisfies some constraint.
We've separated the summoning from the constraint using '$:$' although we could have used brackets, as in $\exists n (m = 2n)$.
I personally like to avoid brackets where possible.
So putting it all together, we say that a number $m$ is even if it can be written as $2n$, or in every-day language, if it is a multiple of two.
Because we used $\iff$ to link the two halves of the equation together, it means we can always replace either side with the other, anywhere they appear.

This definition for even numbers lets us define two functions, one to test if a function is even, the other to generate an even number given any starting number.
$$\begin{align}
\mathit{is\_even}(n) &: n \mod 2 = 0 \\
\mathit{gen\_even}(n) &: 2n
\end{align}$$

# Proof using a predicate definition of odd numbers

Odd numbers are the ones that are not even.
So we can write this as follows:
$$\begin{align}
odd(m) &\iff \neg even(m) \\
&\iff \nexists n:m = 2n
\end{align}$$

We've introduced some more notation, so let's go through that as well.
The $\neg$ symbol means "not", and applies to whatever comes after it.
So $\neg\mathit{true} = \mathit{false}$, for example.
We're saying that if a number is not even, then it is odd.
Now, by substituting in the definition of even, we get the second line.
The $\nexists$ symbol is like the $\exists$ symbol, but instead of meaning "exists", it means "does not exist".
We can read this as "there is no number $n$ where $m = 2n$.

The eagle-eyed among you will be saying, "hang on, 3 is odd and $3 = 1.5 \times 2$ so that definition is broken!", to which I say, award yourself a cup of tea and a biscuit, because you are right.
But you are also wrong.
When we use existentials to summon possible values, we don't summon any old value.
We aren't summoning apples and triangles and the Milky Way galaxy.
The values always come from some implicitly or explicitly defined collection of values.

In this case, both $m$ and $n$ are integers, which is the maths name for whole numbers ${\dots, -2, -1, 0, 1, 2, \dots}$ extending for ever in each direction.
The symbol for whole numbers is $\mathbb{Z}$.
We have already met $\mathbb{N}$ which is the natural numbers, ${1, 2, \dots}$ but this is another case where mathematicians are often a bit sloppy with their notation.
Sometimes when you see $\mathbb{N}$, it includes zero, and other times it does not, depending on the mathematician.
It is supposed to be obvious from context, but if you aren't sufficiently initiated, it may not be obvious to *you*.
To disambiguate, you may see $\mathbb{N}^+$ used for the whole numbers starting at 1, and  $\mathbb{N}_0$  for the whole numbers starting at 0.

Lastly, as well as saying that some value must (or must not exist), we can say that something is true for all values.
The way we write this is with the $\forall$ symbol, called the *universal quantifier*.

We're now armed with enough notation to clarify our even/odd equations, by saying where $m$ and $n$ come from.

$$\begin{align}
\forall m \in \mathbb{Z}: even(m) &\iff \exists n \in \mathbb{Z}: m = 2n \\
\forall m \in \mathbb{Z}: odd(m) &\iff \neg even(m) \\
&\iff \nexists n \in \mathbb{Z}:m = 2n
\end{align}$$
That's certainly a lot more precise, but it is also a lot harder to read.
There is always a trade-off between how explicitly we write things down, and how easy it is to read them.
Because of this, there tend to be conventions where particular variable names are introduced as always referring to things of a particular type, to avoid writing in their type at every use.

Given our definitions, we can see right away that every integer is either even or odd.
But let's prove it just for kicks.
The technique we will use is *proof by contradiction*.
We're going to need a couple more symbols to help us along.
The $\wedge$ symbol is logical *and*.
The $\top$ and $\bot$ symbols are true and false respectively.

Let us say there was a number $a$ that is not even and not odd, and let's plug this in to our definitions.
$$\begin{align}
\neg even(a) \wedge \neg odd(a) && \text{(proposition)}\\
\neg even(a) = odd(a) && \text{(definition of odd)} \\
odd(a) \wedge \neg odd(a) && \text{(substitute )} \\
\bot && \text{(contradiction)}
\end{align}$$
# A constructive definition of odd numbers

In the previous proof, we showed that if we define odd numbers as all numbers that are not even, we can show that there's a contradiction if a number is both odd and even.
This is a perfectly serviceable way to go.
However, if we compare the definition for even and odd numbers in that proof, you see something quite starkly different between them.
The definition for even numbers suggests a way to generate even numbers.
The definition for odd numbers lets us test if a number is odd, but it does not let us make examples of odd numbers.

The definition of even numbers is *generative* or  *constructive*, as it allows us to construct all of the even numbers.
It would be nice to have a *constructive* definition of odd numbers as well, so that we can make all of those.
Then it would be nice to prove from this constructive definition that all numbers are either even or odd.

Odd numbers can not be written as $2n$.
The number 0 can be written as $2 \times 0$, so is even.
1 can not be written as $2 \times n$ for any integer value $n$.
So 1 is the smallest odd number.
2 is, obviously, $2 \times 1$, so is even.
But $2=1+1$.
So it appears that when we add 1 to an even number, we get an odd number and when we add 1 to an odd number, we get an even number.
Let's prove this.

$$\begin{align}
even(n) \wedge even(n+1) \implies && \text{(proposition)}\\
n = 2a, && \text{(definition of even for $n$ )} \\
(n+1) = 2b, && \text{(definition of even for $n+1$)} \\
2a + 1 = 2b, && \text{(substitute $2a$ for $n$)} \\
a + \frac{1}{2} = b, && \text{(divide by 2)} \\
a \in \mathbb{Z} \implies b \notin \mathbb{Z} \implies \bot, && \text{(contradicts $b \in \mathbb{Z}$)} \\
b \in \mathbb{Z} \implies a \notin \mathbb{Z} \implies \bot. && \text{(contradicts $a \in \mathbb{Z}$)}


\end{align}$$
We have proven another contradiction.
Remember that both $a$ and $b$ must be integers.
But if $a$ is an integer then $b = a+\frac{1}{2}$ is definitely not an integer, and if $b$ is an integer then $a = b - \frac{1}{2}$ is also not an integer.
So, we've proven by contradiction that for any even $n$, that $n+1$ is not even.
Let us use this to define odd numbers.
$$even(n) \iff odd(n+1)$$
This gives us a constructive definition of odd:
$$\textit{odd}(n) \iff \exists m \in \mathbb{Z}: n = 2m + 1$$
Armed with this, we can define the corresponding test and generator functions:
$$\begin{align}
\mathit{test\_odd}(n) &: n \mod 2 = 1 \\
\mathit{gen\_odd}(n) &: 2n+1
\end{align}$$

What can we say about $n+1$ for odd values of $n$?
Again, we can use proof by contradiction.
$$\begin{align}
odd(n) \wedge odd(n+1) \implies && \text{(proposition)} \\
n = 2a+1, && \text{(definition of odd for $n$)} \\
n+1 = 2b + 1, && \text{(defnition of odd for $n+1$)}\\
(2a+1)+1 = 2b+1, && \text{(substitute $2a$ for $n$)} \\ 
2a+1 = 2b, && \text{(cancel 1)} \\
a + \frac{1}{2} = b, &&\text{(divide by 2)}\\
a \in \mathbb{Z} \implies b \notin \mathbb{Z} \implies \bot, && \text{(contradicts $b \in \mathbb{Z}$)} \\
b \in \mathbb{Z} \implies a \notin \mathbb{Z} \implies \bot. && \text{(contradicts $a \in \mathbb{Z}$)}

\end{align}$$
This looks pretty similar to the previous proof, and shows that one more than an odd number is not itself odd.
Lastly, let's show that it is actually even, just to make sure.
$$\begin{align}
odd(n) \implies n &= 2a+1 && \text{(definition of odd)}\\
m &= n + 1 && \text{(let's name $n+1$)}\\
&= 2a+1+1 && \text{(substitute the value of a)}\\
&= 2a+2 && \text{(arithmetic)}\\
&= 2(a+1) && \text{(common factors)}\\
b &= a+1 && \text{(name $a+1$)}\\
m = 2b &\implies even(m) && \text{(definition of even)}
\end{align}$$
# Sums of even and odd numbers
Next, we will show that adding two even numbers gives you an even number, adding two odd numbers gives you an odd number and adding two odd numbers gives you an even number.
We will prove it by substituting in the definitions, shuffling a bit, and showing that the existential quantified variable introduced does have a value.
$$\begin{align}
even(m) \wedge even(n) \implies even(m + n) && \text{(goal)} \\
even(m) \implies \exists a: 2a = m, && \text{(definition)}\\
even(n) \implies \exists b: 2b = n, && \text{(definition)}\\
even(m + n) \implies \exists c: 2c = m+n, && \text{(definition)}\\
2c = 2a + 2b, && \text{(substitution for $m$, $n$)}\\
c = a+b && \text{(integer $c$ exists)}
\end{align}$$
The next case is adding two odd numbers:
$$\begin{align}
odd(m) \wedge odd(n) \implies even(m + n) && \text{(goal)} \\
odd(m) \implies \exists a: 2a+1 = m, && \text{(definition)}\\
odd(n) \implies \exists b: 2b+1 = n, && \text{(definition)}\\
even(m + n) \implies \exists c: 2c = m+n, && \text{(definition)}\\
2c = 2a + 1 + 2b + 1, && \text{(substitution for $m$, $n$)}\\
c = a+b+1 && \text{(integer $c$ exists)}
\end{align}$$
And lastly, adding an even and an odd number. The sum operation isn't affected by the ordering, so we'll only prove it for one case:
$$\begin{align}
even(m) \wedge odd(n) \implies odd(m + n) && \text{(goal)} \\
even(m) \implies \exists a: 2a = m, && \text{(definition)}\\
odd(n) \implies \exists b: 2b+1 = n, && \text{(definition)}\\
odd(m + n) \implies \exists c: 2c+1 = m+n, && \text{(definition)}\\
2c + 1= 2a + 2b + 1, && \text{(substitution for $m$, $n$)}\\
c = a+b && \text{(integer $c$ exists)}
\end{align}$$
# Products of even and odd numbers
In a similar way, we can prove things about the products of even and odd number.
Firstly, the product of an even integer with any other integer is even.
$$\begin{align}
even(m) \implies even(m \times n) && \text{(goal)} \\
even(m) \implies \exists a: 2a = m, && \text{(definition)} \\
even(m*n) \implies \exists b: 2b = m \times n, && \text{(definition)} \\
2b = 2a\times n, && \text{(substitution of $m$)} \\
b = a \times \frac{n}{2} && \text{(integer $b$ exists)}
\end{align}$$
Secondly, the product of two odd integers is an odd integer.
$$\begin{align}
odd(m) \wedge odd(n) \implies odd(m \times n) && \text{(goal)} \\
odd(m) \implies \exists a: 2a+1 = m && \text{(definition)} \\
odd(n) \implies \exists b: 2b+1 = n && \text{(definition)} \\
odd(m \times n) \implies \exists c: 2c+1 = m \times n && \text{(definition)} \\
2c + 1 = (2a+1)(2b+1) && \text{(substitute $m$, $n$)} \\
2c + 1 = 2a \times 2b + 2a + 2b + 1 && \text{(expand)}\\
2c + 1 = 2(2ab + a + b) + 1 && \text{(factorise)}\\ 
c = 2ab + a + b && \text{(integer $c$ exists)}
\end{align}$$
# The collatz function of any odd number is even
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
\forall n: collatz(2n+1) = 6n + 4 \\
\textit{gen\_odd\_collatz}(n): \langle \textit{gen\_odd}(n), \textit{gen\_even}(3n+2) \rangle
\end{align}$$
The pairs $\langle 2n+1, 6n+4 \rangle$ are all of the pairs of numbers linked by green arrows in the [[The Collatz Conjecture|introduction]].
Notice that while every odd number is a source of an odd-to-even jump in the collatz function, only some even numbers are destinations.

Lastly, let's think about collatz for the even case.
$$\begin{align}
even(n) & \implies \exists a: 2a = n, \\
collatz(n : n \text{ is even}) &= n/2, \\
&= a
\end{align}$$
So that was a long-winded way of deriving the obvious constructor for all destinations from an even source.
$$\begin{align}
\forall n: collatz(2n) = n \\
\textit{gen\_even\_collatz}(n): \langle \textit{gen\_even}(n), n \rangle
\end{align}$$
Again, we can see that $\langle 2n, n \rangle$ are all pairs of numbers linked by grey arrows in the [[The Collatz Conjecture|introduction]].
This is quite neat.
We can, if we wished, count through all possible values of $n$, starting at 0 and going up, and by applying these two rules, we will generate all possible steps in all possible collatz sequences.

This is the power of proofs.
They don't just tell us that something is true in particular, but they tell us that some rule is true always.
Knowing it's true always lets us use this to build other things, like these collatz arrow generators, and know that we haven't missed anything out.

[^1]: A *predicate* is a function that evaluates to a truth value. They are sometimes called indicator functions. They are also sometimes thought of as unary *relations*, where relations are usually used to relate multiple things together.