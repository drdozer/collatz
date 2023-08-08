In the [[All numbers are either odd or even|even/odd]] chapter, we derive various proof for even and odd numbers, as well as for the collatz function as it relates to even and odd numbers.
Here we provide some julia functions that codify these.
```julia
# even/odd predicates
is_even(n) = n ÷ 2 == 0
is_odd(n) = n ÷ 2 == 1

# even/odd generators
gen_even(n) = n*2
gen_odd(n) = n*2+1

# collitz link generators
gen_odd_link(n) = gen_odd(n), gen_even(3n+2)
gen_even_link(n) = gen_even(n), n
```