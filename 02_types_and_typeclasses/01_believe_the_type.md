# Believe the «Type»?

Previously mentioned: “Haskell” – has a static type system… Expression’s type – is known to the compiler… Wrong types («Divide a Boolean, by a number?») – won't compile! … That's – good, – to catch errors, not be “crashed”… Every *thing* (in “Haskell”) – has a *type*; so, the compiler – can *“reason”* (about programs), before compiling.

Un-like “Java” (and – “Pascal”), – “Haskell” – has the «type inference»! … If we (would) give a number, – tell not its type: it is inferred… So, – we – *don't* have to (explicitly) write *out* the types (of functions, expressions) – to get things *done*! … 

We – have covered some *basics* (of “Haskell”), with only a very “superficial” glance (at types)… How-ever; under-standing the type system – is a *very* important part (of – learning a “Haskell”)…

A type – is a (kind of) “label”, – which – *every* expression has. It – tells us: in which *category* (of things) – that (expression) fits:
- The expression `True` – is a Boolean;
-`"Hello!"` – is a string;
- Et – cetera.

Now – we'll use the **“GHCI”**: to examine, – the *types* – of *some* expressions… We'll do that – by using the `:t` command, – which (followed – by *any* valid expression) tells us its type… 

Let's give it a *whirl*? … :cyclone:

```haskell
ghci> :t 'a'  

'a' :: Char  
```

```haskell
ghci> :t True  

True :: Bool  
```

```haskell
ghci> :t "HELLO!"  

"HELLO!" :: [Char]  
```

```haskell
ghci> :t (True, 'a')  

(True, 'a') :: (Bool, Char)  
```

```haskell
ghci> :t 4 == 5  

4 == 5 :: Bool
```

Here – we see *that*: doing a `:t` (on an *expression*) – prints out the *expression* (followed – by: a `::`, and its type)… The `::` – is read, as: `«Has – the type, of a “…”»`. “Explicit” types – are (always) denoted: with, – the first “letter” – in “capital” case. 

`'a'` (as it *would* seem) – has a type: of a `Char`; it's – not hard, to conclude that: it – stands for a “Character”. 

`True` – is of a `Bool` type… That – makes sense? :smirk: 

But what's – *this*? … Examining the type of a `"HELLO!"` – *yields* (out): a `[Char]`. The square brackets – denote a list… So, – we read that, as: «It’s – being a list: of characters!» … 

Un-like lists – each tuple length has its *own* type… So, the expression `(True, 'a')` – has a type of `(Bool, Char)`, – where-as an expression such as `('a','b','c')` – would have the *type* of a `(Char, Char, Char)`… 

`4 == 5` – will (always) return a `False`; – so, – its type – is of a `Bool`. 

## Functions!

Functions – *also* have types! … When writing our *own* functions, – we – can choose to give (them) an *explicit* type declaration… This – is (generally) considered to be a *good* practice, – except – when writing *very* short functions… From here on – we'll give (to all the functions, which we make) the *type* declarations! Re-member the list comprehension (we made previously) which filters the string, so only the “caps” re-main? … Here's – how it looks like, *with* a type declaration:

```haskell
removeNonUppercase :: [Char] -> [Char]  

removeNonUppercase st = [ c | c <- st, c `elem` ['A'..'Z'] ]
```

`removeNonUppercase` – has a type of `[Char] -> [Char]`, – meaning that: it – maps, from a `string` – to a `string`… That's – because it takes *one* `string` (as a “parameter”), – and – returns another, – as a result… The `[Char]` type – is synonymous with a `String`; so, it's clearer – if we write the `removeNonUppercase :: String -> String`… We – didn't have to give this function a type declaration – because the compiler *can* infer (by itself) that: «It's – a function: from a string – to a string!» – but – we did (anyway). But *how* do we write out the type – of a function, which takes *several* parameters? … Here's – a simple function, which takes *three* integers – and adds them (together): 

```haskell
addThree :: Int -> Int -> Int -> Int  

addThree x y z = x + y + z  
```

The parameters – are separated with a `->`; and, there's – no special distinction: between the parameters – and – the return type… The return type – is the *last* item (in the declaration), and, the parameters – are the *first* *three*… Later on – we'll see, why they're all just separated with a `->` – instead – of having some *more* explicit distinction (between – the return types, and, the parameters), – like: `Int, Int, Int -> Int` – or – something. 

If you want to give your function a type declaration (but – are unsure, – as to *what* it should be?), – you can (always) just write the function *without* it; and (then) – check it: with a `:t`. Functions – are expressions too; so, the `:t` – works on them (without a problem).

Here's – an overview: of some common types.

`Int` –  stands for an “integer”; it's used for “whole” numbers: `7` – can be an `Int` (but: `7.2` – can not). `Int` – is bounded, which means that: it has – a *minimum*, and, a *maximum* (of possible value)… Usually (on 32-bit machines), the maximum possible `Int` – is a `2147483647`; and, the *minimum* – is a `-2147483648`. 

`Integer` – stands for, er … also “integer”. The main difference – is that: it's “not” bounded; so, it can be used to represent really-really big numbers! … I mean: like **_really_** big… `Int` (how-ever) – is “more” efficient. 

```haskell
factorial :: Integer -> Integer  

factorial n = product [1..n]  
```

```haskell
ghci> factorial 50  

30414093201713378043612608166064768844377641568960512000000000000  
```

`Float` – is for a “real” floating point, with single precision.

```haskell
circumference :: Float -> Float  

circumference r = 2 * pi * r  
```

```haskell
ghci> circumference 4.0  

25.132742  
```

`Double` – is a “real” floating point, with *double* the precision!

```haskell
circumference' :: Double -> Double  

circumference' r = 2 * pi * r  
```

```haskell
ghci> circumference' 4.0  
25.132741228718345  
```

`Bool` – is a boolean type. It can have only two values: `True` – or – `False`. 

`Char` – represents a character. Denoted – by single quotes. A list (of characters) – is a string. 

`Tuples` – are types, but they are “dependent” on their length (as well – as the types of their components); so, there – is (theoretically) an “infinite” number (of tuple types), which – is too many (to cover, in this tutorial)… 

> Note that: the empty tuple `()` – is also a type, – which – can *only* have a single value: `()`.