# Baby's first functions

In the previous section – we’ve got a basic “feel” for calling functions… Now – let's try making our own! Open up your favorite text editor, and – punch *in* this function (that – takes a number and multiplies it, by two): 

```haskell
doubleMe x = x + x  
```

Functions – are defined in a *similar* way by which they’re called. The function name – is followed by parameters, seperated by spaces… But: when *defining* functions – there's a `=`; and after that – we define: «*What* the function does?». Save this (as `baby.hs` – or some-thing). Now – navigate – to where it's saved; and – run `ghci` (from there). Once in-side «GHCI» – do: `:l baby`. Now (when our script is loaded) – we can “play” with the function which we’ve defined:

```haskell
ghci> :l baby  
[1 of 1] Compiling Main             ( baby.hs, interpreted )  
Ok, modules loaded: Main.  

ghci> doubleMe 9  
18  

ghci> doubleMe 8.3  
16.6   
```

Because `+` works on integers as well, as on floating-point numbers (any thing – which can be considered «a number» really) – our function (also) works on *any* number! … Let's make a function, which takes *two* numbers and multiplies each (by two) and then – adds them (together):

```haskell
doubleUs x y = x*2 + y*2   
```

Simple? … We – could have (also) defined it: as a `doubleUs x y = x + x + y + y`. Testing it out – produces pretty *predictable* results (re-member – to: append this function [to the `baby.hs` file], save it, and then – do a `:l baby` [at the in-side – of the “GHCI”]). 

```haskell    
ghci> doubleUs 4 9  
26  

ghci> doubleUs 2.3 34.2  
73.0  

ghci> doubleUs 28 88 + doubleMe 123  
478  
```

As expected – you can call *your own* functions – from other functions (which – you’ve made). With that (in mind), – we – could *re-define* the `doubleUs`, – like this: 

```haskell
doubleUs x y = doubleMe x + doubleMe y   
```

This – is a *very* “simple” ex-ample: of a common “pattern” – which you will *see* through-out the “Haskell”… Making basic functions (which – are *obviously* correct) and then – combining them: into *more* complex functions… This way – you (also) avoid re-petition… What – if some mathematicians figured out that: «`2` – is (actually) `3`!» – and, – you had to *change* your program? … You – could just re-define the `doubleMe`: to make it be a `x + x + x`, – and, – since `doubleUs` calls `doubleMe` – it would (automatically) work, in this “strange” new world (where `2` – is a `3`). 

Functions (in “Haskell”) – *don't* have to be in *any* particular **order**; so – it *doesn't* matter, if you define a `doubleMe` (first) and then – a `doubleUs`; or – if you do it the other way a-round…

Now, we're “going” – to make a function, which *multiplies* a number by `2` – but **only** if that number is “smaller” than (or – equal to) `100`, – because numbers bigger than `100` – are big *enough*, as it is! 

```haskell
doubleSmallNumber x = if x > 100  
                        then x  
                        else x*2   
```

Right here – we intro-duced “Haskell's” **“if”** statement. You're (probably) familiar (with “if” statements): from *other* languages… The difference be-tween “Haskell's” “if” statement and “if” statements in imperative languages – is that: the “else” part – is **mandatory** in “Haskell”. In imperative languages, – you can (just) *skip* a couple of steps (if – the condition isn't satisfied); but in “Haskell” – *every* ex-pression (and function) *must* re-turn some thing… We – could have (also) written that (“if” statement) in one line, but I find *this* way *more* read-able… An other thing (about the “if” statement, in Haskell) – is that: it is an _ex-pression_! … An ex-pression – is (basically) a piece of code, which – re-turns a *value*… `5` – is an ex-pression (be cause: it – re-turns `5`), `4 + 8` – is an ex-pression, `x + y` – is an ex-pression (be cause: it – re-turns the *sum*, – of `x` and `y`). Be cause: as the “else” is mandatory, – an “if” statement – will *al-ways* re-turn some thing; and that's – *why* it's an ex-pression… If we wanted «to add one» to every number, which was produced in our previous function, – we – could have its body (written), as that:

```haskell
doubleSmallNumber' x = (if x > 100 then x else x*2) + 1
```

If we would have the parentheses omitted, – it *would* have added one – only if `x` wasn't greater than `100`… Note that: the `'` – is at the end of the function’s name! … That (“apostrophe”) – doesn't have any special meaning (in “Haskell's” syntax): it's a valid character – to use in a function’s name… We (usually) use `'` – to either: de-note a **strict** version of a function (one, which isn't “lazy”) – or – a *slightly* modified version (of: a function, or
a variable). Be cause: as the `'` is a valid character (in functions), – we can make a function like that:

```haskell
conanO'Brien = "It's – a-me: Conan O'Brien!"   
```

There – are *two* (note worthy) things, here! The first – is that: in the function’s name – we *didn't* capitalize the Conan's name. That's (be cause): functions – *can't* begin with upper case letters… We'll see, why; a bit later. …  The second thing – is that: this (function) – *doesn't* take any parameters… When a function *doesn't* take any parameters, – we (usually) say: «It's – a _definition_ (or – a _name_)!» — be cause – we *can't* change, what names (and functions) mean – once we've defined them; so, `conanO'Brien` and the string `"It's a-me, Conan O'Brien!"` – can be used “inter-change-ably”!