# «Types» and «Type-Classes»

## Believe the «Type»?

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

## Type variables

What (do you think) is the type – of the `head` function? … Because `head` takes a *list* (of – *any* type), and returns the *first* element, – so – *what* could it be? … Let's check:

```haskell
ghci> :t head  

head :: [a] -> a  
```

Hm-m-m! … What – is this `a`? … Is it a *type*? … Remember that? – we (previously) stated: types – are written in capital case, so it can't (exactly) be a type. Because it's *not* (in capital case) – it's (actually) a type variable… That – means that: `a` – can be of *any* type! … This – is much like “generics” (in other languages), – only (in “Haskell”) it's much more powerful: because – it allows us – to *easily* write *very* “general” functions (if – they *don't* use any “specific” behavior, of the types in them). Functions (which – have type *variables*) – are called “polymorphic” functions! The type declaration of `head` – states that: it – takes a list (of – any type), and, returns one element – of *that* type. 

Although type variables – can have names longer (than – one character), – we (usually) give them names: of `a`, `b`, `c`, `d` …

Remember `fst`? – It returns the *first* component (of a “pair”). Let's – examine, its type:

```haskell
ghci> :t fst  

fst :: (a, b) -> a  
```

We – see that: `fst` – takes a tuple (which – contains two types), and – returns an element, which is *of* the same type, as the (pair's) *first* component. That's – why we can use `fst` – on a pair, which contains *any* two types. Note that: just because `a` (and `b`) are different (type variables), – they – *don't* have to be different “types”: it (just) states that: the *first* (component's) type, and, the *return* (value's type) – are – the same. 

## Type-classes’ «101»

A “type-class” – is a sort of interface, which *defines* some behavior. If a type is a part (of a type-class), – that – means that: it – supports (and – implements) the *behavior*, – which, – the type-class – de-scribes. A lot (of people, coming from “O.O.P.”/object-oriented programming) – get confused: by type-classes; – because, – they – think: “they – are (like) classes (in – object-oriented languages)”. Well; … they – 're not! … You – can think (of them), – kind of, – as “Java” interfaces; – only, – better. 

What's – the type signature, of the `==` function?

```haskell
ghci> :t (==)  

(==) :: (Eq a) => a -> a -> Bool  
```

> Note: the equality operator (`==`) – is a *function*. So are – `+`, `*`, `-`, `/`, and (pretty much) *all* operators… If a function is comprised *only* of special characters – it's (considered) an “infix” function (by default). If we want to: *examine* its type, *pass* it (to another function), or *call* it (as a prefix function), – we – have to surround it: in parentheses.

Interesting? … We – see a new thing here: the `=>` symbol. Everything before the `=>` symbol – is called a “class constraint”… We can read (the previous type declaration) – like this: the equality function – takes **any** two values (which – are of the **same** type) – and – returns a `Bool`… The type of those two values – **must** be a member of the `Eq` class (this – was the class’ constraint).

The `Eq` (type-class) – provides an interface: for testing for *equality*… Any type (where – it makes sense: to test – for equality: between two values, of that type) – should be a *member* – of the `Eq` class! … All (standard) “Haskell” types (except – for `IO`: the type – for dealing with *in-put* and *out-put*) and functions – are – a part of the `Eq` type-class.

The `elem` (function) – has a type of `(Eq a) => a -> [a] -> Bool` – because it uses a `==` over a list: to check – “Whether some value (we're looking for) is in it?”.

## Some basic type-classes:

`Eq` – is used for types, which support “equality testing”… The functions its members implement, – are: `==` and a `/=`. So, if there's an `Eq` class constraint (for a type variable in a function) – it uses a `==` (or `/=`) – some-where inside its definition. All the types we mentioned previously (except for functions) – are parts of `Eq`, so they *can* be tested for equality.

```haskell
ghci> 5 == 5  
True  

ghci> 5 /= 5  
False  

ghci> 'a' == 'a'  
True  

ghci> "Ho Ho" == "Ho Ho"  
True  

ghci> 3.432 == 3.432  
True  
```

`Ord` – is for types, which have an ordering.

```haskell
ghci> :t (>)  
(>) :: (Ord a) => a -> a -> Bool  
```

All the types we covered so far (except for functions) – are part of `Ord`. The `Ord` covers *all* the standard comparing functions (such as: `>`, `<`, `>=` and `<=`). The compare function – takes *two* `Ord` members (of the same type) – and – returns an ordering… Ordering – is a type, which can be: `GT`, `LT` or `EQ`, – meaning: “Greater than”, “Lesser than” and “Equal” (respectively). 

To be a member of `Ord`, – a type must (first) have membership: in the “prestigious” (and “exclusive”) `Eq` club.

```haskell
ghci> "Abrakadabra" < "Zebra"  
True  

ghci> "Abrakadabra" `compare` "Zebra"  
LT  

ghci> 5 >= 2  
True  

ghci> 5 `compare` 3  
GT  
```

Members of `Show` – can be presented as strings. All types covered so far (except for functions) – are a part of `Show`. The most used function (which – deals, with the `Show` type-class) – is `show`. It – takes a value (whose type – is a member of `Show`), and, presents it (to us) – as a “string”.

```haskell
ghci> show 3  
"3"  

ghci> show 5.334  
"5.334"  

ghci> show True  
"True"  
```

`Read` – is sort of the opposite type-class of `Show`. The read function – takes a string – and – returns a type, which is a member of `Read`.

```haskell
ghci> read "True" || False  
True  

ghci> read "8.2" + 3.8  
12.0  

ghci> read "5" - 2  
3  

ghci> read "[1,2,3,4]" ++ [3]  
[1,2,3,4,3]
```

So far – so good? … Again: all types covered (so far) – are in this type-class. But; what happens – if we try to do (just) `read "4"`?

```haskell
ghci> read "4"  
<interactive>:1:0:  
    Ambiguous type variable `a' in the constraint:  
      `Read a' arising from a use of `read' at <interactive>:1:0-7  
    Probable fix: add a type signature that fixes these type variable(s)  
```

What *GHCI* is telling us (here) – is that: it – doesn't know, what we want (in return)… Notice that: in the previous uses of `read` – we did something (with the result) afterwards! … That way, *GHCI* could infer: what kind (of result) we wanted out (of our `read`). If we used it as a Boolean, – it knew: it – had to return a `Bool`. But now, – it knows: we – want some type, which is a part of the `Read` class; it – just doesn't know: “Which one?”… Let's take a look – at the type signature of `read`:

```haskell
ghci> :t read  
read :: (Read a) => String -> a  
```

See? … It returns a type, which’s a part of `Read`; but if we *don't* try to use it (in some way later) – it has *no* way of knowing: “Which type?” … That's for – we should use “explicit” type annotations. Type annotations – are a way of (explicitly) saying, what the type (of an expression) should be. We do that – by adding a `::` (at the end of expression), and then – specifying a type. Observe: 

```haskell
ghci> read "5" :: Int  
5  

ghci> read "5" :: Float  
5.0  

ghci> (read "5" :: Float) * 4  
20.0  

ghci> read "[1,2,3,4]" :: [Int]  
[1,2,3,4]  

ghci> read "(3, 'a')" :: (Int, Char)  
(3, 'a')  
```

Most expressions – allow compiler to infer a type. But sometimes – it is `Int` or `Float` (as in: `read "5"`). To define, – “Haskell” would evaluate. So (for statically typed), types should be preset: for compilation, GHCI evaluation; it asks: “Is that the type?”

`Enum` members (`()`, `Bool`, `Char`, `Ordering`, `Int`, `Integer`, `Float`, `Double`) – can be: enumerated, sequenced (`succ`-essor; `pred`-ecessor), ranged.

```haskell
ghci> ['a'..'e']  
"abcde"  

ghci> [LT .. GT]  
[LT, EQ, GT]  

ghci> [3 .. 5]  
[3,4,5]  

ghci> succ 'B'  
'C'  
```

Bounded members – have an *upper* and a *lower* bound:

```haskell
ghci> minBound :: Int  
-2147483648  

ghci> maxBound :: Char  
'\1114111'  

ghci> maxBound :: Bool  
True  

ghci> minBound :: Bool  
False  
```

`minBound` & `maxBound` – are interesting: they – have a type of the `(Bounded a) => a` (in a sense: they – are “poly-morphic” constants).

All tuples – are (also) a part of `Bounded` (if, – the components – are also in it).

```haskell
ghci> maxBound :: (Bool, Int, Char)  

(True, 2147483647, '\1114111')  
```

`Num` – is a numeric type/class. Members – can “act” like numbers… Let’s examine the type, of a number:

```haskell
ghci> :t 20  

20 :: (Num t) => t  
```

It – appears that: whole numbers – are (also) polymorphic constants… They – can act like *any* type, which's a member of the `Num` typeclass.

```haskell
ghci> 20 :: Int  
20  

ghci> 20 :: Integer  
20  

ghci> 20 :: Float  
20.0  

ghci> 20 :: Double  
20.0  
```

Those – are `Num` type-class types. `*` type accepts all numbers:

```haskell
ghci> :t (*)  

(*) :: (Num a) => a -> a -> a  
```

It takes 2 numbers (same type) and returns 1 number (that type). That's why `(5 :: Int) * (6 :: Integer)` has “type error”, but `5 * (6 :: Integer)` is `Integer` (`5`: both `Integer` & `Int`). 

To join `Num` – a type must already be “friends” with `Show` & `Eq`.

`Integral` – is (also) numeric. `Num` – includes all *numbers* (“real” & “integral”), but the `Integral` – is *only* integral (“whole”): with `Int` & `Integer`.

`Floating` – for “floating point”: `Float` and `Double`.

A very useful function (for – dealing with numbers) – is a `fromIntegral`… It – has a type declaration, of: `fromIntegral :: (Num b, Integral a) => a -> b`. From its type signature – we see: it – takes an *integral* number, and, turns it – into a *more* general number! … That's – *useful* – to let “integral” & “floating point” work together… For instance: the `length` – has a type declaration of `length :: [a] -> Int` – instead of having *more* general type (`(Num b) => length :: [a] -> b`)… I think, that's – for historical reasons (or something); although (in my opinion) not nice… Anyway, if we try to get a *length* (of a list), and then – add it: to a `3.2`; – we'll get an error, because we tried to add (together) an `Int` and a “floating point” number! … So, to get around this – we’d do a `fromIntegral (length [1,2,3,4]) + 3.2` – and… it all – works out.

> Notice that: `fromIntegral` – has *several* class constraints (in – its type signature)… That's – completely valid; and (as you can see), the class constraints – are separated by commas (inside the parentheses).