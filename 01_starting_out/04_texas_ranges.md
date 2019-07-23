# Texas’ ranges

What – if we wanted a list: of *all* numbers, between `1` and `20`? … Sure; we – could (just) type them (all) out, – but (obviously) that's *not* a *solution* for gentle-men, who – demand *excellence* (from – their programming languages)… Instead, we'll – use **ranges**! … 

Ranges – are a way of making lists, – which – are – to be *arithmetic* sequences: of numerable “elements”… Numbers – *can* be numerated: “One”, “Two”, “Three”, “Four”, – et – cetera… Characters – can (also) be enumerated: the Alpha-Bet – is an enumeration, – of characters, from `A` – to `Z`. 

Names – can't be enumerated: what – comes after “John”? … I – don't know. 😕

To make a list (containing – *all* the “natural” numbers, from `1` – to `20`), – you (just) write: `[1..20]`… That – is the equivalent – of writing a `[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20]` ✨; and, there's – no difference (between – writing one, or the other), – ex-cept that: writing out a *long* enumeration (as a *sequence*) “manually” ✍ – is *not* a good practice! ⚠

```haskell
ghci> [1 .. 20]

[1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20]  
```

```haskell
ghci> ['a'..'z']  

"abcdefghijklmnopqrstuvwxyz"
```

```haskell
ghci> ['K'..'Z']  

"KLMNOPQRSTUVWXYZ"   
```

“Ranges” – are “cool” ⛄, – because you can (also) specify a *step*… 

What – if we want all *even* numbers (between – `1` and `20`)?

```haskell
ghci> [2, 4 .. 20]  

[2, 4, 6, 8, 10, 12, 14, 16, 18, 20]  
```

Or – every *third* number (between – `1` and `20`)?

```haskell
ghci> [3, 6 .. 20]  

[3, 6, 9, 12, 15, 18]   
```

It's (simply) a matter – of separating the *first* two elements (with – a “comma”), and (then) – specifying: what – the upper limit is… 

While pretty “smart”, – ranges (with steps) *aren't* as smart 🎓, as some people may expect them (to be): you – *can't* do a `[1, 2, 4, 8, 16 .. 100]` (to get *all* the “powers” – of `2`): 
- Firstly, because – you can (only) specify *one* step. 
- And, secondly because, – some sequences (which – *aren't* “arithmetic”) – are “ambiguous”, if they are being set by only a *few* of their “first terms”. 

To make a list (with *all* the numbers: from `20` – to `1`) – you can't just do a `[20 .. 1]`; – you have to do a `[20, 19 .. 1]`…

Watch out – when using *floating point* numbers (in ranges) ⚠ … Because they are *not* completely “precise” (by definition), – their use (in ranges) – can yield some pretty “funky” results:

```haskell
ghci> [0.1, 0.3 .. 1]  

[0.1, 0.3, 0.5, 0.7, 0.8999999999999999, 1.0999999999999999]  
```

My advice – is not to use them (in – list ranges). 👼

You – can (also) use ranges – to make *infinite* lists: by (just) not specifying an “upper” limit… Later – we'll go into *more* detail (on infinite lists). 

For now, – let's examine: how – you would get the *first* `24` multiples, of a `13`? … 

Sure; you – could do a `[13, 26 .. 24*13]`. 

But there's – a “better” way: `take 24 [13, 26..]`. Because “Haskell” is lazy – it *won't* try to evaluate the infinite list “immediately”, because it would *never* finish… It'll wait (to see): *«What – do you want to get **out** (of that, infinite list)?»* … And, here – it sees: «You (just) – want the … first `24` elements?»; – and – it (gladly) obliges…

A handful of functions (which – produce *infinite* lists):

**`cycle`** – takes a list – and cycles it (into – an infinite list). If you just try to display the result, – it will go on *for ever*; – so, you have to “slice” it off, some-where.

```haskell
ghci> take 10 (cycle [1,2,3])  

[1,2,3,1,2,3,1,2,3,1]  
```
```haskell
ghci> take 12 (cycle "LOL ")  

"LOL LOL LOL "   
```

**`repeat`** – takes an element – and produces an infinite list (of just that element). It's like cycling a list – with only one element.

```haskell
ghci> take 10 (repeat 5)  

[5,5,5,5,5,5,5,5,5,5]  
```

Although, it's simpler – to just use the **`replicate`** function (if you want some number of the same element, in a list): `replicate 3 10` – returns `[10, 10, 10]`.