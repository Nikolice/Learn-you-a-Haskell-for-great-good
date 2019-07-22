# So: what's “Haskell”?

[“Haskell”](https://en.wikipedia.org/wiki/Haskell_%28programming_language%29) – is a purely _functional_ programming language…

In *imperative* languages, – you – get things *done* – by giving (to the computer) a *sequence* (of “tasks”); and (then), – it – *executes* them… While executing them, – it – *can* change “state”.

For instance: you – set a variable (`a`) – to a `5`; and (then), – do – some *stuff*; and (then) – set it – to some-thing else… You – have some *control flow structures* (for – doing some action, several times)… 

But; in purely *functional* programming, – you – *don't* tell (to the computer) «What – to *do*» (as such), but (rather) – you tell it: «What – the “stuff” *is*»: 
- The *“factorial”* (of a number) – is: the *product* – of *all* the numbers: from `1` – to that number;
- The *“sum”* (of a *list*, of numbers) – is: the *first* number, – plus – the sum – of all the *other* numbers;
- … and, – so – on. 

You – express “that” – in the form of *functions*! … You (also) – *can't* set a *variable* (to some-thing), – and (then) *re-set* it (to – some-thing else), later… If you say that: «The “`a`” – is `5`!» – you *can't* say «It's – some-thing else…» later; – because, – you – have said: «It – was `5`!» … What – are you: some kind – of liar? :-(

So, in purely *functional* languages, – a function – has **no** side-effects… The only thing (a function can do) – is to calculate some-thing, and – return it (as a *result*)… At first, this – seems (kind of) “limiting”; but, it (actually) has some *very* nice con-sequences: if a function is called twice (with – the same parameters), – it's guaranteed – to re-turn the *same* result. That's – called “referential transparency”; and not only does it allow (the compiler) to reason about the program's behavior, but – it (also) allows *you* – to *easily* deduce (and, even – prove), that a function – is correct; and then – build more *complex* functions (by – gluing simple functions together). 

“Haskell” – is **lazy**. That means, that (un-less *specifically* told other-wise) “Haskell” – *won't* execute functions (and – calculate things), until it's **really** forced (to show you a “result”)… That – goes well – with “referential transparency”; and, it allows you – to think of programs – as of a series of **trans-formations (on data)**… It (also) allows “cool” things: such, as – *infinite* data structures. Say – you have an *immutable* list (of numbers: `xs = [1, 2, 3, 4, 5, 6, 7, 8]`), and – a function (`doubleMe`: which – multiplies *every* element, by “2”; and, – then – returns a *new* list)… If we wanted to *multiply* our list by “8” (in – an *imperative* language), and did a `doubleMe(doubleMe(doubleMe(xs)))`, – it would (probably) *pass* through the list *once*, and – make a *copy*, and (then) re-turn it… Then – it would *pass* (through the list) for *another* two times; and – re-turn the *result*… In a “lazy” language, – calling `doubleMe` on a list (without – forcing it – to show you the result) – ends up – in the program (sort of) “telling” you: «Yeah, yeah… I'll do it; later!». But once you want to *see* the result, – then, the *first* `doubleMe` – tells (to the *second* one): «It – wants the result: now!». The second one – says that to the *third* one; and – the third one (reluctantly) – gives back a doubled `1` (which – is a `2`). The second one – receives that, and – gives back a `4` (to – the first one)… The first one – sees that, – and tells (to you): «The *first* element – is an `8`…». So, it (only) does *one* pass (through the list); and, only – when you **really** need it! … That way, when you want some-thing (from a *lazy* language) – you can (just) take some *initial* data, and (efficiently) transform (and mend) it; so, – it resembles, what you want, – at the end. 

“Haskell” – is **statically**  typed. When you compile your program, – the compiler – knows: 
- Which “piece” (of code) – is a number;
- Which – is a string;
- … and, – so – on. 

That means, that a lot of (possible) errors – are caught – at *compile* time! … If you try, to add (together) a “number” and a “string”, – the compiler – will **whine** at you! … “Haskell” – uses a type system, which has a **type inference**. That means, that you *don't* have to *explicitly* label every piece (of code) with a type, – because the “type system” can (intelligently) figure out *a lot* about it… If you say: «`a = 5 + 4`» – you *don't* have to tell “Haskell” that: «a – is a number», – it can figure that out (by itself). Type inference (also) allows your code to be *more* general! … If a function (you make) takes two parameters (and – adds them, together), and you *don't* (explicitly) state their type, – the function *will* work on *any* two parameters (which – act like numbers). 

“Haskell” – is **elegant** and **concise**… Because it uses a lot of “high level” concepts, – “Haskell” programs – are (usually) shorter, than their (imperative) equivalents. And, shorter programs – are *easier* – to maintain (than – longer ones), and – have *less* “bugs”. 

“Haskell” – was made by some **_really_** smart guys (with – “Ph. D.”s). Work (on “Haskell”) – began in 1987: when a committee (of researchers) got together, to design a *nice* language… In 2003 – the «“Haskell” report» – was published (which – defines a **stable** version, of the *language*). 