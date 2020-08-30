# So: what's “Haskell”? 🤨

[“Haskell”](https://en.wikipedia.org/wiki/Haskell_(programming_language)) – is a purely *functional* programming language. 👾

In *imperative* languages – you get things *done* by giving (to the Computer 🤖) a *sequence* of tasks (0️⃣, 1️⃣, 2️⃣, 3️⃣, …), and then – it executes them … While executing them – it can change “state”; for instance: you set a variable `a` to `5`, and then – do some “stuff”, and then – *reset* it (to something else). You have control flow structures (for doing some action, *several* times). 

But, in purely *functional* programming – you *don't* tell (to the Computer 🤖) *what to __do__*, but (rather) *what the stuff __is__*: 
- The “_factorial_” (of a number) – **is** the product of *all* the numbers: from `1` – to that number;
- The “_sum_” (of a list of numbers) – **is** the *first* number, plus – the sum of all *other* numbers;
- … and – so – on.

You express **_that_** – in the form of **functions**. You (also) can't *set* a variable to *something* – and (then) *reset* it (to something else) later. If you say: «The `a` – is `5`» – you can't say «It's something *else*!» later, because you *have* said: «It – was `5`» … What are you – some kind of **_liar_**? 💔

… So, in purely *functional* languages – a *function* has *no* side-effects! ✨ … The *only* thing it can do – is – to calculate (and return) something (as a _result_) 🧮 … At first, – this – seems “limiting”, – but – has some *very* nice consequences: if a function is called *twice* (with **the _same_** parameters) – it's *guaranteed* – to return the **same** _result_! … That's – called **_“referential transparency”_**; and – not only does it allow the **Compiler** 🤖 to reason about the Program's _behavior_, – but – it (also) allows **you** to easily *deduce* (and – even *prove*) that: «The **function** is _correct_!»; – and (then) – build more *complex* functions: by “gluing” simple functions, together. 🧱

“Haskell” – is **_“lazy”_** 😴; that – means that (un-less *specifically* told other-wise): “Haskell” *won't* execute functions (and – calculate things) until it's *really* forced to show you the “result” 💤 … That – goes well with **_“referential transparency”_**; and – it allows *you* 🎓 to think of **programs** as of series of _transformations_ on *data* … It (also) allows “cool” things, – such as *infinite* data structures … Say, you have an *immutable* list (of numbers: `xs = [1, 2, 3, 4, 5, 6, 7, 8]`), and – a function (`doubleMe`, which multiplies *every* element by “2”, and then returns a *new* list):
- If we wanted to multiply our list by “8” (in an *imperative* language), and did a `doubleMe(doubleMe(doubleMe(xs)))` – it would (probably) pass (through the list) *once*, and – make a *copy*, and (then) – re-turn it; … then – it would *pass* (through the list) for *another* two times, and – re-turn the *result*. 
- In a “lazy” language, – calling `doubleMe` on a list (without forcing it, to show you the result) – ends up in the program (sort of) “telling” you: **_«Yeah, yeah! … I'll do it, later!»_**. But once you want to *see* the result – then, the *first* `doubleMe` tells (to the *second* one): **_«It wants the result; now!»_**. The second one – says that to the *third* one; and the third one (reluctantly) – gives back a doubled `1` (which – is a `2`). The second one – receives that, and gives back a `4` (to the first one)… The first one – sees that, and tells (to you): **_«The *first* element – is an `8`…»_**. So, it (only) does *one* pass (through the list); and – only when you **really** need it! … That way, when you want some-thing (from a *lazy* language) – you can (just) take some *initial* data, and (efficiently) transform (and mend) it; so – it resembles, what you want, at the end. 

“Haskell” – is **statically** typed. When you compile your Program, – the Compiler 🤖 knows: 
- Which “piece” (of code) is a number;
- Which – is a string;
- … and – so – on. 

That means, that: a lot of (possible) errors – are caught at *compile* time! … If you try to add (together) a “number” and a “string” – the compiler 🤖 will **whine** at you! … “Haskell” uses a type system, which has a **type inference**. That means, that: you *don't* have to *explicitly* label every piece (of code) with a type – because the “type system” can (intelligently) figure out *a lot* about it… If you say: «`a = 5 + 4`» – you *don't* have to tell “Haskell” that: **_«`a` – is a number»_**, – it can figure that out (by itself). Type inference (also) allows your code to be *more* general! … If a function (you make) takes two parameters (and – adds them, together), and you *don't* (explicitly) state their type – the function *will* work on *any* two parameters (which – act like numbers). 

“Haskell” – is **elegant** and **concise** … Because it uses a lot of “high level” concepts, – “Haskell” programs are (usually) shorter, than their *imperative* equivalents. And, shorter programs – are *easier* to maintain (than *longer* ones), and – have *less* “bugs”. 🐛

“Haskell” – was made by some **_really_** smart guys (with “Ph. D.”s 🎓). Work (on “Haskell”) – began in 1987: when a committee (of researchers) got together to design a *nice* language… In 2003 – the «“Haskell” report» was published (which – defines a **stable** version, of the *language*). 