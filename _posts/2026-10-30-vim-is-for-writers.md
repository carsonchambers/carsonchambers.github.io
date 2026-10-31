---
layout: post
title: "Vim is for writers"
subtitle: "One of the interesting things about writing a blog in Vim is that you don't use many of the same techniques you do while writing software."
tags: [vim]
context: [thesaurus, spell]
date: 2026-10-30
---

I considered going back and rewriting that subtitle, but I think that there is a certain charm to having a sentence pertaining to how interesting a concept is combined with a written style that is so painfully dull. 

Continuing on with my wildly interesting thought...

Reflecting on my keystrokes, I found that the overlap is quite minimal after excluding
the basics of navigation. For example, some of my most commonly used commands while writing software are `i_<C-o>`, `gd`, `gri` and `ggVG`, but while blogging I
mostly use `z=`, `:set spell`, `~`, `:r _templates/post-header.md` or `dis` ( *Just not on subtitles, apparently!* ).

> **Note:** I have no idea if any of those are my most frequently used in their respective contexts, they just hopped to the top of my mind. Would be interesting to actually track that though.

Before starting this blog, I had actually never considered Vim as a tool for
writers, but then again I had never actually put any serious thought into the tools
writers actually use. When I had to write papers back when I was in school I would
just use my complimentary license of Microsoft Word. But always hated it. Trying
to do the simplest things with formatting was always just huge amounts of wasted 
hours. I grimace remembering editing my first resumé that was a double column format.

As with using an IDE like Jetbrains, Microsoft will tell you how your writing tools should look, function, feel, and behave. This is the antithesis of creativity and individuality which are paramount in strong writing. Also, monthly subscriptions *ick*.

> Microsoft will also lock you into the DOCX file format, [ISO/IEC 29500](https://www.iso.org/standard/71691.html). Part 1 alone is somewhere in the ballpark of **five thousand pages**, and that's not even the rest of OOXML.

Even though Vim is a **Text Editor**, and not a **Word Processor**, *a fact which you would have known if you had bothered to read the first page of the friendly manual*, it does an excellent job of providing you the tooling necessary for any text-based creative enterprise. 

What makes Vim so good for writing? Glad you asked. Writing is an art form, and an artist should not be constrained. I could end it right there, but I have pretty much just been ranting up until this point without sharing any real Vim tips so I should probably elaborate.

The following examples are just a few of the ways that Vim works for writers:

## Spellchecker
Were you trained in the Queen's English? Do those Yankees drive you nuts with their missing vowels?

Set your locale up for spell checks via `:setlocal spell spelllang=en_ca`.

> *No, I did **NOT** mean color*.

You can navigate between spelling mistakes with `]s` and `[s`. Once your cursor is overtop of a potentially misspelled word, you have a few remedies available to you. If the word is correct and you want to add it to your dictionary use `zg`, alternatively if you have a word that isn't getting picked up as misspelled that should be, you can send it to the shadow realm with `zw`. There are *undo's* for `zg` and `zw` that I have never needed of course, but if you find youself in that situation you can employ `zug` and `zuw` respectively. If however the word you navigated to is misspelled and you want to get the correct spelling, use `z=` which provides you with an indexed list of options to replace the given word with.

> **Note:** `:h z=` has that "This may take a long time.  Hit CTRL-C when you get bored." line, which is the style of writing in a user manual that made me fall in love with Vim. The entire manual is full of character and personality, which is something you just never see in docs.

## Pattern replacement 

Imagine you are writing a fantasy novel and as part of the plot you are going to reveal that
the antagonist is actually the protagonist's father. You unfortunately didn't have much foresight
and now realize that you had never bothered to obscure that fact by giving them different last names.

You are going to reveal this fact in Chapter 5, and obviously readers are going to start at Chapter 4, so 
you decide that only in your fourth chapter are you going to obscure the father's
name. Good choice, and Vim's got you covered. You can match only between your two chapter
markers and run a replace between them
```
:/^## Chapter 4/,/^## Chapter 5/s/Anakin Skywalker/Darth Vader/g 
```

## Auto-complete names
Or how about you are writing in your diary about your lovely trip to Azerbaijan but are feeling rather lazy, and you always forget the `i` after the `ba`, what are you to do? Not waste keystrokes on writing the full name, of course. Through the magic of keyword completion, in insert mode you can type `Az` followed by `<C-p>`. More likely than not, you have no other words starting with `Az` (barring a possible accidentally misspelled Azerbajan, of course), which means it will immediately complete your word for you. Neat! If you did have that rascally misspelled word kicking around, you can use `<C-p>` and `<C-n>` to navigate through the list. 

> **Hint:** think previous or next whenever you are using `n|p` commands.

## Thesaurus

Not that I was struggling to find another example or anything, but I did try
`:h thesaurus` and found out there is thesaurus completion `i_<C-x><C-t>`, so I
yoinked Project Gutenberg's resource and now I don't just *write*, I *annihilate*...
Maybe I didn't configure things correctly, but I think you get the point. I'm sure
when it works it is great. I spent a bit of time trying to set up `thesaurusfunc` but
in the end I was too tired and called it a night.

Happy writing. Endeavour to create beauty.
