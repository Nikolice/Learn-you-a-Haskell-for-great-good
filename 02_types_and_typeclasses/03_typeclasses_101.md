# Type-classes’ «101»

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
[3, 4, 5]  

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