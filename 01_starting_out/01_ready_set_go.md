# Ready? Set? – Go!

Al-right? … Let's get started?

If you’re a sort of a _“horrible”_ person (who – *didn't* read the intro-duction, to this thing; so – you’ve *skipped* it?) – you *might* want to read the *last* section (in – the intro-duction) any way, – be cause, it – ex-plains: 
- *What* – do you *need* (in order – to *follow* this, tutorial);
- And – *how* – we're “going” (to “load” functions).

The **first** thing (we're going, to do) – is – to “run” (the `ghc`’s) «inter-active mode», – and – to *call* (for – some “functions”): to – get a *very* “basic” feel (for – the “Haskell”)…

Open your “terminal” – and, – type in: the `ghci` … You – will be *greeted* (with – a *some*-thing like this): 

```text
“GHCi” (version – № „6.8.2“): http://www.haskell.org/ghc/  (“:?” – for help.)
Loading package base; … linking; … done!  

Pre-lude>  
```

Congratulations: you – 're in the “GHCI”! … The prompt (here) – is a `Prelude>`, but (because it can get longer, – when you load “stuff”, into the session) – we're going to use the `ghci>`! … If you want to have the *same* prompt – just – type in: `:set prompt "ghci> "`.

Here – 's some simple **arithmetic**:

```haskell
ghci> 2 + 15  
17  

ghci> 49 * 100  
4900  

ghci> 1892 - 1472  
420  

ghci> 5 / 2  
2.5  

ghci>  
```

This – is pretty *self-explanatory*… We can (also) use *several* operators (on one line); and, all the *usual* precedence rules – are *obeyed*… We – can use the *parentheses*: to, make the *precedence* – “explicit” (or – to change it):

```haskell
ghci> (50 * 100) - 4999  
1  

ghci> 50 * 100 - 4999  
1  

ghci> 50 * (100 - 4999)  
-244950  
```

Pretty cool, huh? … Yeah, I know: it's not; but, – bear, with me… A little pit-fall (to watch *out* for here) – is – **negating** numbers. If we want to have a *negative* number –
it's always best – to surround it, with parentheses… Doing a `5 * -3` – will make “GHCI” *yell* at you; but, doing a `5 * (-3)` – will work (just fine). 

Boolean algebra – is also pretty straight-forward. As you probably know: 
- `&&` – means a boolean _and_;
- `||` – means a boolean _or_;
- `not` – negates a `True` (or – a `False`).


```haskell
ghci> True && False  
False  

ghci> True && True  
True  

ghci> False || True  
True   

ghci> not False  
True  

ghci> not (True && True)  
False
```

Testing for equality – is done – like so:

 ```haskell
ghci> 5 == 5  
True  

ghci> 1 == 0  
False  

ghci> 5 /= 5  
False  

ghci> 5 /= 4  
True  

ghci> "hello" == "hello"  
True   
```

What about doing a `5 + "llama"` (or – a `5 == True`)? … Well, if we try the *first* snippet, – we’ll get a *big* scary “error” message!

```text
No instance – for (Num [Char]) –
arising from a use of `+' at <interactive>:1:0-9 …

Possible fix: add an instance declaration – for (Num [Char])  
In the expression: 5 + "llama"  
In the definition of `it': it = 5 + "llama"   
```

Yikes! What “GHCI” is telling us (here) – is that: `"llama"` – is not a number, and (so) it *doesn't* know: how – to add it – to a `5`… Even if it wasn't `"llama"` (but `"four"`, or `"4"`), – “Haskell” – *still* wouldn't consider it, to be a number… `+` – expects its *left-and-right* sides – to be numbers. If we tried to do a `True == 5` – “GHCI” would tell us that: «The types – don't match!» … Where-as `+` works only on things that are considered numbers, – the `==` – works on *any* two things (which *can* be compared). But, the catch – is that: they (both) – have to be the *same* type, of thing… You – can't compare **apples** and **oranges**! … We – 'll take a *closer* look (at types) a bit later… Note: you – can do a `5 + 4.0`, because `5` – is “sneaky” (and – can act like an “integer”, or – a floating-point number). `4.0` – can't act like an “integer”; so, `5` – is the one, that *has* to adapt!

You – may not have known it, but… we – 've been using *functions* now (all – a-long)… For instance: the `*` – is a function, which takes two *numbers* (and – multiplies them)… As you've seen, – we – call it by “sandwiching” it (be-tween them). This – is what we call an _in-fix_ function! … Most functions (which – *aren't* used with numbers) – are _pre-fix_
functions! … Let's take a look (at them)…

Functions – are (usually) “pre-fix”; so (from now – on), we  – won't (explicitly) state that: «A function – is of the pre-fix form!» (we – 'll just *assume* it). In *most* imperative languages, – functions – are called, by writing the function name, and then –  writing its parameters (in *parentheses*; usually – separated: by commas). In “Haskell”, – functions – are called – by writing the function *name*, a *space*, and (then) the parameters (separated: by spaces)… For a start,  we – 'll try calling one of the *most* boring functions (in “Haskell”). 

```haskell
ghci> succ 8  
9   
```

The `succ` function – takes any-thing, which has a defined successor – and – returns that (successor). As you can see, – we – ’ve just separated the function name – from the parameter: with a space… Calling a function with several parameters – is (also) simple. The functions `min` and `max`  – take *two* things, which can be put in an order (like
numbers!). `min` – returns the one, that's lesser; and `max` – returns the one, that's greater. See (for your self): 

```haskell
ghci> min 9 10  
9  

ghci> min 3.4 3.2  
3.2  

ghci> max 100 101  
101   
```

How-ever; if we wanted to get the successor, of the product of numbers `9` and `10`, – we – *couldn't* write just a `succ 9 * 10`, – because, that – would get the successor of a `9`, which would (then) be multiplied by a `10`: a `100`… We – 'd have to write a `succ (9 * 10)` – to get a `91`!

If a function takes *two* parameters, – we can (also) call it as an “in-fix” function: by – surrounding it, with “back-ticks”… For instance: the `div` function – takes *two* integers, and does an integral division (be-tween them). Doing the `div 92 10` – results in a `9`… But when we call it like that, – there – may be some *confusion*, – as – to: which (of the numbers) is *doing* the division, and which – is a divided being… So, we can call it, as an “in-fix” function: by doing a ``92 `div` 10`` – and (suddenly), it – 's much clearer!

Lots of people (who – come from imperative languages) – tend to stick to the notion, that: parentheses – should *denote* function application! … For example; in “C” – you use parentheses to call functions: like `foo()`, `bar(1)` or `baz(3, "haha")`… Like we said, – spaces – are used for function application in “Haskell”. So, those functions (in “Haskell”) – would be a `foo`, `bar 1` and a `baz 3 "haha"`. So, if you see something like `bar (bar 3)` – it doesn't mean that: `bar` – is called with a `bar` and a `3` – as parameters! … It means that: we (first) call the function `bar` (with `3` as the parameter) – to get some *number*; and then, we – call the `bar` again – *with* that number… In “C”, – that – would be some-thing, like: `bar(bar(3))`.