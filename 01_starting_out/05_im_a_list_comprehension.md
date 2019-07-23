# I'm – a *list* comprehension!

If you've ever taken a course in mathematics, you've probably run into set comprehensions. They're normally used for building more *specific* sets out of *general* sets. A basic comprehension for a set that contains the first ten even natural numbers is `S = {2*x | x is a natural <= 10}`. The part before the pipe – is called the output function, `x` is the variable, `N` is the input set, and `x <= 10` – is the predicate. That means that: the set contains the *doubles* of all natural numbers which satisfy the predicate. 

If we wanted to write that in “Haskell” – we could do something like: `take 10 [2, 4 ..]`. But what if we *didn't* want doubles of the first `10` natural numbers, but some kind of *more* complex function applied on them? … We could use a list comprehension for that. List comprehensions – are very *similar* to set comprehensions. We'll stick to getting the first `10` even numbers for now. The list comprehension we could use – is `[x*2 | x <- [1 .. 10]]`. The `x` is drawn from `[1 .. 10]`, and for every element in `[1 .. 10]` (which we have bound to `x`) we get that element doubled. Here's that comprehension in action:

```haskell
ghci> [x*2 | x <- [1..10]]  

[2, 4, 6, 8, 10, 12, 14, 16, 18, 20]  
```

As you can see, we get the desired results. Now – let's add a condition (or a predicate) to that comprehension. Predicates go after the binding parts – and are separated (from them) by a comma. Let's say: we want only the elements, which (doubled) are greater than (or equal) to `12`. 

```haskell
ghci> [x*2 | x <- [1 .. 10], x*2 >= 12]  

[12, 14, 16, 18, 20]  
```

Cool; it works. How about if we wanted all numbers (from `50` to `100`) whose remainder (when divided with the number `7`) is `3`? … Easy:

```haskell
ghci> [ x | x <- [50 .. 100], x `mod` 7 == 3]  

[52, 59, 66, 73, 80, 87, 94]   
```

Success! … 

> Note that: weeding out lists (by predicates) – is also called **filtering**. We took a list of numbers – and we filtered them (by the predicate). Now – for another example. 

Let's say: we want a comprehension which replaces *each* odd number (greater than `10`) with a "BANG!", and each odd number (which's less than `10`) with a "BOOM!"… If a number isn't odd – we throw it out of our list. For convenience, we'll put that comprehension inside a function – so we can *easily* reuse it.

```haskell
boomBangs xs = [ if x < 10 then "BOOM!" else "BANG!" | x <- xs, odd x]   
```

The last part of the comprehension – is the predicate. The function `odd` – returns `True` on an odd number – and `False` on an even one. The element is included in the list – only if *all* the predicates evaluate to `True`. 

```haskell
ghci> boomBangs [7 .. 13]  

["BOOM!", "BOOM!", "BANG!", "BANG!"]   
```

We – can include *several* predicates! … If we wanted *all* numbers from `10` to `20` (which – are not: `13`, `15`, or `19`), – we'd – do:

```haskell
ghci> [ x | x <- [10 .. 20], x /= 13, x /= 15, x /= 19]  

[10, 11, 12, 14, 16, 17, 18, 20]  
```

Not only can we have *multiple* predicates in list comprehensions (an element must satisfy *all* the predicates – to be included in the resulting list); – we can (also) draw from several *lists*… When drawing from several *lists* – comprehensions produce *all* combinations of the given lists; and then, – join them – by the output function we supply… A list, – produced by a comprehension, which draws from two lists of length `4`, – will have a length of `16` (provided, we don't *filter* them). If we have *two* lists (`[2, 5, 10]` and `[8, 10, 11]`) and we want to get the *products* (of – *all* the possible combinations, – between numbers, in those *lists*) – here's – what we'd *do*:

```haskell
ghci> [ x*y | x <- [2, 5, 10], y <- [8, 10, 11]]  

[16, 20, 22, 40, 50, 55, 80, 100, 110]   
```

As expected, the length (of the *new* list) – is `9`… What – if we wanted all (possible) products, which – are more, than `50`?

```haskell
ghci> [ x*y | x <- [2, 5, 10], y <- [8, 10, 11], x*y > 50]  

[55, 80, 100, 110]   
```

How – about a list comprehension, which combines [a list of *adjectives*] and [a list of *nouns*]? … for epic “hilarity”:

```haskell
ghci> let nouns = ["hobo", "frog", "pope"]  

ghci> let adjectives = ["lazy", "grouchy", "scheming"]  

ghci> [adjective ++ " " ++ noun | adjective <- adjectives,  noun <- nouns]  

["lazy hobo", "lazy frog", "lazy pope", 
"grouchy hobo", "grouchy frog", "grouchy pope", 
"scheming hobo", "scheming frog", "scheming pope"]   
```

I know! … Let's write our *own* version – of length! … We'll – call it a `length'`:

```haskell
length' xs = sum [1 | _ <- xs]   
```

`_` – means that: we – *don't* care what we'll *draw* (from the list) anyway, so (instead of writing a *variable* name, – which we'll never use) we just write: `_` … This (function) – replaces *every* element (of a list): with a `1`; – and (then) – sums that, up… This – means that: the resulting *sum* – will be the *length* of our list.

Just a friendly reminder: because strings are lists – we *can* use list comprehensions (to process and *produce* strings). Here's – a function – which takes a *string* and removes everything (except – upper-case letters) from it:

```haskell
removeNonUppercase st = [ c | c <- st, c `elem` ['A' .. 'Z']]   
```

Testing it out: 

```haskell
ghci> removeNonUppercase "Hahaha! Ahahaha!"  

"HA"  
```

```haskell
ghci> removeNonUppercase "IdontLIKEFROGS"  

"ILIKEFROGS"   
```

The predicate here – does all the work. It says that: the character – will be included in the new list – only if it's an element of the list `['A' .. 'Z']`. Nested list comprehensions – are also possible, if you're operating on lists which contain lists. 

A list – contains several lists of numbers. Let's remove *all* odd numbers without flattening the list:

```haskell
ghci> let xxs = [[1, 3, 5, 2, 3, 1, 2, 4, 5], [1, 2, 3, 4, 5, 6, 7, 8, 9], [1, 2, 4, 2, 1, 6, 3, 1, 3, 2, 3, 6]] 

ghci> [ [ x | x <- xs, even x ] | xs <- xxs]  

[[2, 2, 4], [2, 4, 6, 8], [2, 4, 2, 6, 2, 6]]  
```

You can write list comprehensions across *several* lines. So if you're not in `GHCI`, it's better to split longer list comprehensions across multiple lines; especially – if they're nested.