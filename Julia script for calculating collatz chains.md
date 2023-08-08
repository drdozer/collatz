Julia is a modern scripting language. It's open-source, so you can download and install it for free on your computer, and it is incredibly powerful.
It also has excellent built-in support for mathematics, which makes it ideal for our purposes.

The collatz function itself can be defined like this:
```julia
function collatz(n)
	if n % 2 == 0
	  n÷2
    else
      3n+1
    end
end
```
This code first checks if n is even.
The expression `n % 2` divides n by 2 and returns the remainder, and even numbers will have the remainder 0.
If even, it halves it (using the ÷ operator that makes sure that we're using integer arithmetic).
Otherwise it multiplies by 3 and adds 1. Notice that in Julia, we use mathematical notation, so `3n` is $3 \times  n$, just like when writing normal equations.

We will need another function to repeatedly apply the collatz function until it reaches 1.
```julia
function conjecture(n)
	print(n)
	if n == 1
		println()
		return
	else
	  print(" -> ")
	  m = collatz(n)
	  conjecture(m)
	end
end
```
If we run `conjecture` on some whole number `n`, it will first print out the current number.
Then it will check if it has reached 1.
If it has, it prints a newline and returns.
Otherwise, it prints out an arrow, calculates the next collatz number and tests the conjecture on that.
If this `conjecture` function returns, then the conjecture holds for that value of `n`.
If it carries on running for ever, then we've found a value of `n` where the conjecture is false.
Simples.
Except not so much.
How can we tell the difference between an `n` that runs for ever, and one that just runs for a *really*, *really*, long time?
Or one that overflows the computer's ability to represent numbers?
