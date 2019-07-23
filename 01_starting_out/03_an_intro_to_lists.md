# An intro – to lists

Much like shopping lists 🛍 (in the *real* world 🗺), – “lists” (in “Haskell”) are very use-ful! … It's – the *most* used data structure, and – it can be used in a *multitude* of different ways: to model (and solve) a *whole* bunch of problems… Lists – are awesome. In this section  – we'll look at the basics, of: 
- lists;
- strings (which – *are* lists);
- and – list comprehensions. 

In “Haskell”, lists – are a **homo-genous** data structure. It – stores *several* elements, of the *same* type! … That – means that: we – can have a *list*: of integers 🔢 (or – of *characters* 🔤); but: we – can't have a list, which has a *few* integers – and (then) – a few *characters*… And (now), – a list! 

> **Note**: We – can use the `let` key-word (to define a name) – right in “GHCI”… Doing a `let a = 1` (inside “GHCI”) – is an equivalent of: writing (a `a = 1`) in a script, and (then) loading it. 

```haskell
ghci> let lostNumbers = [4,8,15,16,23,42]  

ghci> lostNumbers  
[4,8,15,16,23,42]  
```

As you can see, – lists – are de-noted by “square” brackets (**“`[`” & “`]`”**); and, the “values” (in lists) – are separated: by *commas*! … If we would (ever) tried parsing, – of a list, similar to a `[1,2,'a',3,'b','c',4]`, – the “Haskell” – would complain: the *characters* 🔤 (in single quotes) – *are’t* numbers 🔢! ⚠ … 

Speaking of *characters*; – strings – are *lists* (of characters 🔤): a `Hello!` – is the syntactic “sugar” of a `['H','e','l','l','o','!']`… And (be cause) the strings are *lists*, – we – can use the “list’s” functions (on them); – which – is *really* handy ✨! … So, a common task (of – putting 2 lists, together) – can be done: by a `++` operator:

```haskell
ghci> [1,2,3,4] ++ [9,10,11,12]  
[1,2,3,4,9,10,11,12]

ghci> "Hello" ++ " " ++ "World"
"Hello World"  

ghci> ['w','o'] ++ ['o','t']  
"woot"
```

Watch out – when (repeatedly) using a `++` operator (on *long* strings):
- When you put together *two* lists (even – if you append a *single-ton* list – to a list; for instance: `[1,2,3] ++ [4]`), – internally – “Haskell” – *has* to do a long walk: through the *whole* list, on the “left” side (of – the `++`)… That's – *not* a problem – when dealing with lists, which “aren't” too “big”.
- But: putting some *thing* at the *end* (of a list; – which – 's a *fifty* “million” entries, long 🌌) – is … going to take *a while*. 
- How ever; putting some thing at the *beginning* (of a list) (with – using the `:` operator; – also – called the “cons” operator) – is – “instantaneous” ✨…

```haskell
ghci> 'A':" SMALL CAT"  
"A SMALL CAT"  

ghci> 5:[1,2,3,4,5]  
[5,1,2,3,4,5]
```

Notice, how `:` takes a number 🔢 (and, a list: of numbers) (or: a character 🔤 – and – a *list*, of characters) – where-as the `++` takes *two* lists? … Even if you're adding (an element) to the *end* of a list (with a `++`), – you – *have* to surround it (with – the “square” brackets): so – it “becomes” a list. 

`[1,2,3]` – is (actually) just a syntactic sugar ✨ (of the `1:2:3:[]`). And `[]` – is an empty list… If we prepend a `3` (to it), – it becomes a `[3]`. If we (then) prepend a `2` (for it), – it becomes a `[2,3]`; – and, – so – on!

> **Note**: a “`[]`”, a “`[[]]`”, (and) a “`[[],[],[]]`” – are (all) *different* things: 
> - The “first” one – is an empty list;
> - the “second” one – is a list, – containing *one* empty list;
> - … and, the “third” one – is a list, containing *three* empty lists.

If you want to get an element *out* of a list, by “index”, – use the `!!` (the indices –
start at a `0`):

```haskell
ghci> "Steve Buscemi" !! 6  
'B'  

ghci> [9.4,33.2,96.2,11.2,23.25] !! 1  
33.2  
```

But; if you try to get the *sixth* element (from a list, which (only) has *four* elements), –
you'll – get an “error”; so – be care-ful. ⚠

Lists – can (al-so) “contain” lists. They – can (al-so) contain lists; – which – can contain lists, –
which (al-so) can be containing lists: 

```haskell
ghci> let b = [[1,2,3,4],[5,3,3,3],[1,2,2,3,4],[1,2,3]]  

ghci> b  
[[1,2,3,4],[5,3,3,3],[1,2,2,3,4],[1,2,3]]  

ghci> b ++ [[1,1,1,1]]  
[[1,2,3,4],[5,3,3,3],[1,2,2,3,4],[1,2,3],[1,1,1,1]]  

ghci> [6,6,6]:b  
[[6,6,6],[1,2,3,4],[5,3,3,3],[1,2,2,3,4],[1,2,3]]  

ghci> b !! 2  
[1,2,2,3,4]   
```

The lists *with/in* a list – can be of *different* lengths; but… they – can't be of “different” types! Just like you can't have a list, which has *some* characters 🔤 and *some* numbers 🔢, – you – can't have a list, which has: some lists – of *characters*, and some lists – of *numbers*. 🔤🔢 ⚠

Lists – can be compared, if the stuff (which – they contain 📦) *can* be compared. When using the `<`, the `<=`, the `>` (and) the `>=` (to – “compare” lists), – they – are compared in a **lexico-graphical** order: first – the “heads” are compared; … if they are “equal”, – then – the *second* elements – are compared; – et cetera.

```haskell
ghci> [3,2,1] > [2,1,0]  
True  

ghci> [3,2,1] > [2,10,100]  
True  

ghci> [3,4,2] > [3,4]  
True  

ghci> [3,4,2] > [2,4]  
True  

ghci> [3,4,2] == [3,4,2]  
True  
```

What (else) – can you do (with lists)? … Here – are some *basic* functions (which – operate, on
lists):

**`head`** – takes a list and returns its head. The head of a list – is (basically) its first element.

```haskell
ghci> head [5,4,3,2,1]  
5   
```

**`tail`** – takes a list – and returns its tail. In other words; – it chops off a list's head.

```haskell
ghci> tail [5,4,3,2,1]  
[4,3,2,1]   
```

**`last`** – takes a list – and returns its last element.

```haskell
ghci> last [5,4,3,2,1]  
1   
```

**`init`** – takes a list – and returns every thing, except the *last* element.

```haskell
ghci> init [5,4,3,2,1]  
[5,4,3,2]   
```

If we think of a list as of a monster – here's what's what:

![](http://s3.amazonaws.com/lyah/listmonster.png)

But; *what* happens – if we try to get the *head*, of… an *empty* list? 😕

``` haskell
ghci> head []  
*** Exception: Prelude.head: empty list  
```

Oh, my! … It all blows up; in our face! 🔥 … If there's no “monster”, – it – doesn't have a head… When using the `head`, the `tail`, the `last` and the `init`, – be careful: not to use *them* on empty lists! … This (“error” ⚠) – cannot be caught at «compile time»; so, it's always a good practice 👼 – to take “pre-cautions” (against – *accidentally* telling “Haskell” – to give you some elements, from an *empty* list)…

**`length`** – takes a list; – and – returns its length (obviously):

```haskell
ghci> length [5,4,3,2,1]  
5  
```

**`null`** – checks, if a list is empty. If it *is*, – it – returns `True`; other-wise, – it – returns a `False`… Use this function – *instead* of a `xs == []` (if – you have a list, called `xs`).

``` haskell
ghci> null [1,2,3]  
False  

ghci> null []  
True  
```

**`reverse`** – re-verses a list:

``` haskell
ghci> reverse [5,4,3,2,1]  
[1,2,3,4,5]  
```

**`take`** – takes – a number, and a list… It – extracts *that* many elements (from – the
beginning, of the list); – watch:

``` haskell
ghci> take 3 [5,4,3,2,1]  
[5,4,3]  

ghci> take 1 [3,9,3]  
[3]  

ghci> take 5 [1,2]  
[1,2]  

ghci> take 0 [6,6,6]  
[]  
```

See? – how (if – we try to take *more* elements, than there *are*; in the list) it just
*re-turns* the list? … If we “try” to take `0` elements, – we – ’ll get an *empty* list. ⚠

**`drop`** – works in a similar way; only: it drops the number of elements – from the *beginning* (of a list).

``` haskell
ghci> drop 3 [8,4,2,1,5,6]  
[1,5,6]  

ghci> drop 0 [1,2,3,4]  
[1,2,3,4]  

ghci> drop 100 [1,2,3,4]  
[]   
```

**`maximum`** – takes a list of stuff, which can be “put” in-to some kind of an order, and – returns the “biggest” element.

**`minimum`** – returns the smallest.

``` haskell
ghci> minimum [8,4,2,1,5,6]  
1  
ghci> maximum [1,9,2,3,4]  
9   
```

**`sum`** – takes a list (of numbers) and returns their sum.

**`product`** – takes a list (of numbers) and returns their product.

``` haskell
ghci> sum [5,2,1,6,3,2,5,7]  
31  

ghci> product [6,2,1,2]  
24  

ghci> product [1,2,5,6,7,9,2,0]  
0   
```

**`elem`** – takes a thing (and – a list, of things) – and tells us – if that (thing) is an element, of the list… It's (usually) called as an “in-fix” function; – because it's easier (to read) that way.

``` haskell
ghci> 4 `elem` [3,4,5,6]  
True  

ghci> 10 `elem` [3,4,5,6]  
False  
```

Those – were (a few) basic functions, which operate on lists… We'll take a look – at (more) list functions [later](/06_modules/02_data_list.html)