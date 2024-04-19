## salary negotiation ZK app

### Problem

This is a salary negotiation ZK app.

Alice is willing to work for at least `m` salary. When Bob makes an offer, Alice sometimes wants to answer the offer is at least `m`, without revealing the number `m` itself.

### Protocol

1. Alice chooses `m`
2. Alice picks a random number `s`
3. Alice shares `h(m || s)` to Bob where `h` is some hash function
4. Bob makes an offer `o`
5. Alice chooses to accept, ignore the offer, or prove `o` is smaller than `m`
6. go back to 4.

Note: Alice has an option to ignore the offer because otherwise Bob can start from zero and increase the offer one-by-one.

### This codebase

This codebase implements a tool for using in step 5. Alice can prove the offer is smaller than the minimum salary. Bob can verify Alice's claim.

This can be achieved with a ZK circuit with:

Inputs
* public `c` : commitment published already
* public `o` : offer from Bob
* private `m` : minimum salary Alice is willing to work for
* private `s` : salt, random number Alice picked


and assertions
* `o < m`
* `h(m || s) = c`


### Limitation & Sad news

> The current implementation of the Nexus VM does not yet support public and auxiliary/private inputs

https://docs.nexus.xyz/Specs/nexus-vm

So, at the moment everything is embedded as literals in the program.

This will be fixed as soon as private inputs become availble in nexus-vm.

### Try it

Follow the README of https://github.com/nexus-xyz/nexus-zkvm to install the dependencies.

I haven't finished proving yet, but perhaps you can
```
cargo nexus prove
cargo nexus verify
```
