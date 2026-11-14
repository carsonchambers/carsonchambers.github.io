---
layout: post
title: "JetBrains hates these 10 Simple Tricks"
tags: [vim]
context: [i_CTRL-X, vim.keymap]
date: 2026-10-14
---

Having trouble getting noticed by the ladies? Tired of settling for pay-per-token AI girlfriends? That used to be me too, but with these 10 simple tips, I learned how to make myself irresistible:

1. Remap your capslock key. Now now, don't go telling me "Carson, I already did
   that, Capslock → ^[ did not get me any girlies" because I wasn't going to
tell you to remap it to escape! Remap that sucka to Left Ctrl. Why would you
want this? E-R-G-O-N-O-M-I-C-S. When you make your sensai proud and finally get
past that Vim white-belt, you will begin to realize that sliding your pinky
down to do all of these necessary actions like `<C-x>`, `<C-o>`, or `<C-k>`
when you are in insert mode is wasting time and muscular stamina for your that
little itty bitty finger.
2. So, what about escape then? You still use an escape key? No wonder you haven't
   been noticed by the hunnies yet. How about you grow up and start using
`<C-[>` like a real man. Pair this with tip #1 for spectacular results.
3. Set your Man pager to Vim with `export MANPAGER="nvim +Man!"`. No, like seriously, do that now. No more sobbing because you can never figured out what the heck to do with `curl(4)`, just `<Shift-k>` yourself around town like the baller you are.
4. Use these keyboard shortcuts for adding clipboard support because they are
   scientifically proven to be superior:
```neovim
" Neovim
vim.keymap.set("x", "<leader>y", '"+y', { desc = "Yank selection to system clipboard" })
vim.keymap.set("x", "<leader>Y", '"+d', { desc = "Cut selection to system clipboard" })
vim.keymap.set({ "n", "x" }, "<leader>p", '"+p', { desc = "Paste from system clipboard" })
```
> **Note:** Some people have issues getting clipboard working. But as the kids say on Stack Overflow, Read the Friendly Manual `:h provider-clipboard`.

5. Whatever you do, stay away from Neovim starter packs. These reek of someone
   who is *trying* to be cool. The first rule of being cool is to not look like
you're trying to be cool. When I first made the switch away from JetBrains, I
started with Lazyvim, and still to this day, if you get too close to me you will get a
whiff of that rancid poser stench.
6. Rely on LLM's for every detail of your life and can't determine how many __r__'s to put in strawberry? Just hit a word with `<C-x> <C-s>` in insert mode (after having run `:set spell`), or `z=` in normal mode to use the built-in spell-checker. 
7. Forgot to capitalize your name? Are you still navigating back to the first letter of the word with `b` and then using `r` to replace with the upper case character? Why not use `~` instead! Feel like capitalizing the whole word? Then `guiw` is your friend!
8. Okay so you finished vim-tutor and know about `w` to go to the next word, but how about `W` to use the next whitespace as your word boundary!? You can pair that with other commands like `diW` to make entries from lists go POOF! And just because I am feeling generous, I will let you know it works with `b` and `B` as well. Not even charging you an extra tip for that.
9. Read crontabs? Then hold onto your hat because this two-fer tip will rock
   your sox. `vim -M /etc/crontab` opens up your buffer in unmodifiable mode,
which means you will have to try really hard to screw things up this time. Once
you are in crontab, want to know the contents of `/etc/cron.hourly`? Navigate
to it in normal mode and use `gf` to go to the file
> **Note:** `gf` command does not give you a gf.
10. And, for big tip number ten, *touch grass*.
