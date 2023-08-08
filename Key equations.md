Evens and odds
$$\begin{align}
even(n) &\iff \exists a: n = 2a \\
even(n) &\iff odd(n+1) \\
\textit{odd}(n) &\iff \exists a : n = 2a + 1 \\
\mathit{odd(n)} &\iff \mathit{even}(n+1) \\
even(m) &\implies \forall n: even(m \times n) \\
odd(m) \wedge odd(n) &\implies odd(m \times n) \\
\\
\mathit{gen\_even}(a) &: 2a \\
\mathit{gen\_odd}(n) &: 2n+1 \\

\end{align}$$
Collatz
$$\begin{align}
\mathit{collatz}(n) &= \begin{cases}
n/2, & \text{if } n \text{ is even} \\
3n+1, & \text{if } n \text{ is odd}
\end{cases} \\
\\
collatz(2a) &= a && \text{even}\\
collatz(2a+1) &= 6a + 4 && \text{odd} \\
collatz(collatz(2a+1)) &= 3a+2 && \text{even $\circ$ odd} \\
\\
\textit{gen\_even\_collatz}(a) &: \langle \textit{gen\_even}(a), a \rangle \\
\textit{gen\_odd\_collatz}(a) &: \langle \textit{gen\_odd}(a), \textit{gen\_even}(3a+2) \rangle
\end{align}$$
