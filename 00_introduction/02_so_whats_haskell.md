# So: what's “Haskell”? 🤨

[“Haskell”](https://en.wikipedia.org/wiki/Haskell_(programming_language)) – is a (purely) **functional** programming language. 👾

## Paradigms: “imperative” 🆚 “functional”

### «A». “Imperative” paradigm

In “imperative” languages – you get things *done* by giving *a **sequence** of tasks* (№№ 0️⃣, 1️⃣, 2️⃣, 3️⃣, …) to the Computer 🤖, – and then – it executes them … While executing – it can change “state”; for instance: you set «“`a`” = “`5`”», – and then – *do* some **stuff**; and then – reset it, to something else … You have control flow structures, for doing some action several times! 

### «B». “Functional” paradigm

In purely “functional” programming – you don't tell (to the Computer 🤖) what to *do*, but rather – what **the stuff** *is*: 
- the “factorial” (of a *number*) = the product of **all** numbers: from «`1`» – to that number;
- the “sum” (of a list of *numbers*) = the **first** number + the “sum” of all *other* numbers;
- … and – so on.

You express that – in the form of **functions**! … You (also) *can't* set a variable to something, and then – reset it (to something else) later: if you say «_The “`a`” – is “`5`”_» – you can't say «_It's something else!_» later, because you *have* said _it **was** “`5`”_ … What are you? – Some kind of **liar**? 💔

## Benefits 👍

### № 1. “Referential transparency”

So, in purely *functional* languages, – a **function** – has *no* “side effects” ✨; the only thing it *can* do – is to calculate 🧮 – and – **return** something (as a “result”)… 

At first, this – seems (kind of) “limiting”, but – has some very *nice* consequences: if a function is being called ***twice*** (with the ***same*** parameters) – it's *guaranteed* – to return the *same* result! … 

That's – called __“referential transparency”__; and not only does it *allow* the Compiler 🤖 to *reason* about the Program's behavior, but – it (also) allows **you** to easily *deduce* (and even *prove*) that: _«The function – is **correct**!»_; and then – build more *complex* functions: by _“gluing”_ “simple” functions – together! 🧱

### № 2. “Laziness” 😴

“Haskell” – is “__lazy__”; that – means that (unless – specifically told, otherwise): “Haskell” – *won't* neither execute functions, *nor* calculate things – until – it's **really** forced, to **show** *you* the result! 💤

That – goes well with _“referential transparency”_; and – it allows *you* 🎓 to think (of programs) as of series of _“transformations”_ on *data*. It (also) allows “cool” things, – such, as ***infinite*** data structures. ♾

Say – you have: 
- an *immutable* **list** of *numbers*: «`xs = [1, 2, 3, 4, 5, 6, 7, 8]`»;
- and a **function**: “`doubleMe`”, – multiplying *every* element by “`2`”, and (then) returning a *new* list.

#### Example:
If we wanted to *multiply* our list by “`8`”:

##### Variant № 1: __“A”__ (imperative way)
If we do a «`doubleMe(doubleMe(doubleMe(xs)))`», – it would (probably): 
- pass (through the list) *once*,
- make a *copy*,
- and (then) return it… 

Then – it would *pass* (through the list) for **another** *two* times, and – return the *result*.

##### Variant № 2: __“B”__ (lazy way)

Calling «`doubleMe`» on a list (without forcing it, to *show* you the result) – ends up in the Program (sort of) “telling” you: **_«Yeah, yeah! … I'll do it, later»_**. But once you want to *see* the result, – then:

- the ***first*** “`doubleMe`” – tells to the **second** one: *«It _wants_ the result; now!»*; 1️⃣ 🤜 🖐 2️⃣ 3️⃣
- the ***second*** one – says that to the **third** one; 1️⃣ 2️⃣ 🤜 🖐 3️⃣
- and the ***third*** one – reluctantly gives back a *doubled* “`1`” (which is a “`2`”); 1️⃣ 2️⃣ 🖐 🤛 3️⃣
- the ***second*** one – *receives* that, and gives back a “`4`” (to the **first** one); 1️⃣ 🖐 🤛 2️⃣ 3️⃣
- the ***first*** one – sees that, and tells (to *you*): *«The **first** element – is an “`8`”…»*. 🤖 🤲 🤛 1️⃣ 2️⃣ 3️⃣

So – it does only **one** pass through the *list*, and only when you **“really”** need it! … That way, when you want something from a _“lazy” language_ – you can (just) take some *initial* data, and efficiently transform (and mend) it; so – it *resembles* what you want, at the end. 

### № 3. “Statically” typed

“Haskell” – is *statically* typed. When you compile your program – the **Compiler** 🤖 knows: 
- which “piece” (of code) – is a *number*; 🔢
- which – is a *string*; 🔣
- … and so on. 

That – means that: a lot of ***possible*** errors are caught at *compile* time 🤏: if you try to add (together) a *“number”* and a *“string”* – the **Compiler** 🤖 will “whine” at you! 👋 …

### № 4. Type inference

“Haskell” – uses a _type system_, which has **“type inference”**. That – means that: you *don't* have to ***explicitly*** label every piece of “code” with a type – because the “type system” can (intelligently ✨) figure out *a lot*, about it. 🤖

If you say: «“`a`” = `5 + 4`» – you *don't* need to tell “Haskell”, that _«“`a`” – is a **number**»_; – it *can* figure that out, by *itself* ! 🎲 👁‍🗨

Type inference (also) allows your code to be *more* “general”: 🎓 if a function (you make) takes ***two*** parameters (and – *adds* them, together), and you *don't* (explicitly) state their type – the function *will* work on **any** two parameters, which act like *numbers*. 🔢

### № 5. Shorter programs

“Haskell” – is elegant and concise 🎩 … Because it uses a lot of “high level” concepts – “Haskell” programs are (usually) **shorter**, than their *imperative* equivalents. And, shorter programs – are *easier* to maintain 🖇 (than *longer* ones); and have *less* “bugs”. 🐛

# Creators of the language

“Haskell” – was made by some _really_ smart guys, with “Ph. D.” 🎓

Work (on “Haskell”) – began in **1987** (when a committee of researchers got together, to design a *nice* language). 

In **2003** – the [__«“Haskell” report»__](https://www.haskell.org/onlinereport) was published (which defines a **_stable_** version, of the *language*). 