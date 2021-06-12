# 01 - Introduction to Blockchain

## Cryptographic Hash Functions

- take any string as input
- output a fixed size output (ex. 256 bits)
- efficiently computable

### Property 1: Collision Free

We cannot find x,y such that x != y and H(x) = H(y)
Note that collisions are possible, considering that our output is fixed size.
Hash is also good for a message digest, quick comparison between 2 documents.

### Property 2: Hiding

Given H(x), infeasible to find x
But if there are only a few values for x, it's very easy to reverse engineer.
Instead, we introduce another value r, that has high-min-entropy.
`high-min-entropy` means that distribution is very spread out.
We concatenate x with r and compute H(r | x), now it's hard to find x.

Application: commitments => commit to a value and reveal it later
To commit: (com, key) := commit(msg) => publish com
To match/reveal, publish key, msg: match:= verify(com, key, msg)
Security properties:

hiding: given com, infeasible to find msg
binding: infeasible to find another msg that will give the same verify result
Using Hash Functions:
commit(msg) := H(key | msg), key
verify(com, key, msg) := H(key | msg) == com

### Property 3: Puzzle-friendly

If k is chosen with high-min-entropy, it is infeasible to find x such that H(k | x) = y
This is to support #2, if we introduce k, it's hard to find x.
x is the solution.
Puzzle-friendly property implies that no solving strategy is much better than trying random values of x.

## SHA-256

Add padding to end of message to make it divisible into 512 bit blocks.
