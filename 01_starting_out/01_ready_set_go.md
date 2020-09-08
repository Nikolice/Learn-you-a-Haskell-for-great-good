# Ready? Set? – Go! 🏁

## Alright? … Let's get started?

§ № <a id="1">«1»</a>. If you’re sort of a _“horrible”_ person (who *didn't* read the introduction, to this thing; so, you’ve *skipped* it?) – you might *want* to read the **last** section of introduction anyway, because it explains: 
- *what* do you *need* (in order to follow this tutorial); 🛒
- *how* we're going to “load” functions. 🤏

§ № <a id="2">«2»</a>. The **first** thing we're going to do – is – to “run” the `ghc`’s «interactive mode», and – to *call* for some **functions** (to get a *very* “basic” feel, for the “Haskell”). 

## The preparation procedure 

§ № <a id="3">«3»</a>. Open your “terminal” – and type in: «`ghci`» ⌨ … You will be *greeted* with something like this: 

```text
“GHCi”: version № „6.8.2“ (http://www.haskell.org/ghc). 

Enter “:?” for help.

Loading package base; … linking; … done!  

Prelude> _
```
Congratulations: *you're in the “GHCi” !* … The prompt (here) – is a „`Prelude`“; but (because it can *get* longer, when you load “stuff” into the *session*) we're “going” to use a „`ghci`“ ! … If you want to have *same* prompt – type in: 

```text
:set prompt "ghci> "
```

§ № <a id="4">«4»</a>. Here's – some simple arithmetics: 🎓

```haskell
ghci>       2 + 15   →   17 
           49 * 100  → 4900  
         1892 − 1472 →  420  
            5 / 2    →    2.5  
```

This – is *pretty* self-explanatory … We – can (also) use *several* operators, on *one* line; and all the *“usual”* precedence rules – are obeyed … We – can use the *parentheses*: to make the *precedence* *__explicit__* (or – to *change* it): 🔢

```haskell
ghci>  ( 50  *   100 ) − 4999  →        1  
         50  *   100   − 4999  →        1  
         50  * ( 100   − 4999) →  −244950  
```

Pretty “cool”, huh? … Yeah, I know: it's – not; but – bear with me. 

§ № <a id="5">«5»</a>. A little “pitfall” (to watch *out*, for here) – is – **negating** numbers! … If we’d (ever) want to have a *negative* number – it's (always) best to “surround” it with *parentheses*: 
- doing a «`5 * -3`» – will make the “GHCi” *yell* at you;
- but, doing a «`5 * (-3)`» – will work, just fine. 

§ № <a id="6">«6»</a>. Boolean’s algebra – is (also) pretty “straight forward”. As you (probably) know: 
- «`&&`» – means **“and”**;
- «`||`» – means **“or”**;
- «`not`» – negates a «`True`» (or a «`False`»).


```haskell
ghci>      True && False → False
           True && True  → True

          False || True  → True 

               not False → True 

      not (True && True) → False
```

§ № <a id="7">«7»</a>. Testing for “equality” – is done like so:

```haskell
ghci>    5    ==    5     →  True
         1    ==    0     →  False

         5    /=    4     →  True
         5    /=    5     →  False

      "hello" == "hello"  →  True
```

§ № <a id="8">«8»</a>. What about doing a «`5 + "llama"`» (or – a «`5 == True`»)? … Well; if we try the *first* “snippet” – we’ll get a *big* “scary” error message:

```text
No instance – for «Num [Char]», – arising from a use of a `+', at <interactive>:1:0-9 …

Possible fix: 
add an “instance declaration” (for the «Num [Char]») in the expression «5 + "llama"» in the definition of `it': «it = 5 + "llama"».
```

Yikes! … What __“GHCI”__ is telling us (here) – is that: the `"llama"` – is *not* a number, – and (so) it *doesn't* know: how – to add it (to a «`5`») … Even if it *wasn't* `"llama"` (but `"four"`, or `"4"`), – “Haskell” – *still* wouldn't consider it to be a “number”.

«`+`» – expects its *left-&-right* sides to be “numbers”. If we tried to do a «`True == 5`» – __“GHCI”__ would tell us: __«The _types_ – _don't_ match!»__.

§ № <a id="9">«9»</a>. Whereas «`+`» works *only* on things, which are considered __“numbers”__ – the «`==`» works on *__any__* two things, which can be **compared** … But, the “catch” – is that: they (both) – have to be the *__same__* type, of thing; – you *__can't__* compare *apples* and *oranges*! … We'll take a *closer* look (at types), a bit later… 

> **Note:** you *can* do a «`5` + `4.0`», because «`5`» is _“sneaky”_ (and – can act  like an “integer”, or, a “floating point” number)… «`4.0`» – *can't* act like an “integer”; so, «`5`» – is the one, which *__has__* to adapt!

§ № <a id="10">«10»</a>. You may *not* have known it, but … we've been using *__functions__* now (all along)! … 

> For instance: the «`*`» – is a function, which takes **two** numbers (and *multiplies* them)… As you've *seen* – we call it *out* by “sandwiching” it, between them. This – is what we call an __“infix”__ function! … Most functions, which *aren't* used with *numbers*, – are __“prefix”__ functions! … Let's take a look (at them)…

§ № <a id="11">«11»</a>. Functions – are (usually) **“prefix”**; so (from “now” – on), we won't (explicitly) state that: «A function – is of the **_prefix_** form!» (we'll just *assume* it). In *most* imperative languages, – functions – are called by writing the function *name*, and then – writing its *parameters* (in *parentheses*; usually – separated, by commas). In “Haskell” – functions – are called, by writing: 
- the function’s *__name__*, 
- a *__space__*, 
- and (then) – the *__parameters__* (separated, by spaces)… 

§ № <a id="12">«12»</a>. For a start – we'll try *calling* one of the **most** boring functions (in “Haskell”):

```haskell
ghci> succ 8 → 9   
```

The “`succ`” function: takes *any* thing, which has a *__defined__* successor (and – returns that successor)… As you can *see* – we've **separated** the function’s _name_, from the _parameter_ (with a **space**).

§ № <a id="13">«13»</a>. Calling a function with *__several__* parameters – is (also) simple. The functions «`min`» and «`max`» – take *__two__* things (which – can be put in an **order**, like **numbers**). «`min`» – returns the one, which's lesser; and «`max`» – returns the one, which's greater. See – for yourself: 

```haskell
ghci>   min    9     10     →    9
        min    3.4    3.2   →    3.2 
        max  100    101     →  101
```

§ № <a id="14">«14»</a>. However; if we wanted to get the *successor* of the **product** (of numbers «`9`» & «`10`») – we *couldn't* write just a «`succ 9 * 10`», – because – that would *get* the successor of «`9`», which would (then) be multiplied by «`10`», resulting in a «`100`» … We'd have to write: «`succ (9 * 10)`» – to get the «`91`»!

§ № <a id="15">«15»</a>. If a function takes *two* parameters – we can (also) call it like an “infix” function: by *surrounding* it with “back-ticks” … 

For instance – the «`div`» function: takes *two* integers, and does an *integral* division (between them) … Doing a «`div 92 10`» – results in «`9`»; but (when we call it like *that*) – there *may* be some **confusion**, – as: 

- which (of the numbers) – is doing the *division*?
- and, – which – is a *divided* being? 

… So – we can call it, as an “infix” function: by doing a «``92 `div` 10``» – and (suddenly) – it's much more *clear*.

§ № <a id="16">«16»</a>. Lots of people (who came from *imperative* languages) tend to stick to the notion, that: parentheses – should denote function’s *application* … For an example, in __“C”__ – you use parentheses, to *call* functions like: 
- «`foo()`», 
- «`bar(1)`»,
- or «`baz(3, "haha")`»… 

As we said, – **spaces** – are used for function *application* (in “Haskell”) … So, those functions (in “Haskell”) – would be: 
- «`foo`», 
- «`bar 1`», 
- and – «`baz 3 "haha"`»… 

So, if you see *something* like «`bar (bar 3)`» – it *doesn't* mean that: _«The `bar` – is called with a [__“`bar`”__] and a [__“`3`”__], as the parameters!»_; – it means that: we (first) call for the *inner* function «`bar`» (with a [«`3`»], as a parameter) to get some *number*, and then – we call the «`bar`» again: *with* that number… In __“C”__, – *that* – would be something like: «`bar(bar(3))`».