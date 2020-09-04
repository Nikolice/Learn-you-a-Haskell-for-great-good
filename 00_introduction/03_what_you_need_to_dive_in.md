# What do you need, to “dive” in? 🤿

1. Text editor; 📝
2. “Haskell” compiler. 🤖

## № 1. Text editor 📝

You (probably) already *have* your *__favorite__* text editor installed – so we *won't* waste time, on that! ⚡ ⏳

## № 2. “G.H.C.” 🤖 (“Glasgow Haskell compiler”)

For the purposes of this _tutorial_ – we'll be using the __“G.H.C.”__ (the most *widely* used “Haskell” compiler). The _best_ way to get started – is to download the [*“Haskell” __Platform__*](https://www.haskell.org/platform/) (which – is (basically) “Haskell” «with batteries included»). 🔋🔋🔋

### “Interactive” mode 🏓

__“G.H.C.”__ – can take a “Haskell” _script_ (they (usually) have an “__.hs__”-extension) – and _compile_ it 📜; but it (also) has an __interactive__ mode – which allows you to _“interactively interact”_ with scripts, interactively … 📝

You can *call* functions (from _scripts_, which you _load_) – and – the _results_ are displayed _immediately_! ⚡ … For __learning__ 🎓 – it's a lot _easier_ (and faster), than recompiling _every_ time, when you make a *change* (and then – “running” the program, from the prompt). 

#### Invoking the mode ✨

The _“interactive mode”_ – can be invoked by typing in «`ghci`», at your prompt. ⌨ 

#### Loading files 📂

If you *have defined* some functions (in a “file” called (say) «`myfunctions.hs`» 🗄):
- You load up those **_functions_** – by typing in: «`:l myfunctions`» … Then – you can *“play”* with them (provided – the «`myfunctions.hs`» is in the *same* folder 📂, from which the «`ghci`» was invoked).
- If you _change_ the __“.hs” script__ – just run «`:l myfunctions`» again (or – do a «`:r`», – which is _equivalent_, because it _reloads_ the current script 🔁).

### Usual workflow 💡

The usual workflow (for me, when playing around in stuff) – is:

- defining some _**functions**_ (in a __“.hs”__-file), 📝
- *loading* them up, 📦
- and – “messing around”, with them; … 👾🖥⌨🖱
- and (then) – changing the __“.hs”__-file, 📝
- loading it up (again), 📦
- … and, – so – on. 🔁

**This** – is (also) what we'll be doing, here.