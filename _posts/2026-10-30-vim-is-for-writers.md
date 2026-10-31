---
layout: post
title: "Vim is for writers"
subtitle: "One of the interesting things about writing a blog in Vim is that you don't use many of the same techniques you do while writing software."
tags: [vim]
context: [thesaurus, spell]
date: 2026-10-30
---

I considered going back and rewriting that subtitle, but I think that there is a certain charm to having a sentence pertaining to how interesting a concept is combined with a written style that is so painfully dull. 

Continuing on with my wildly interesting thought... Reflecting on my keystrokes, I found that the overlap is quite minimal after excluding
the basics of navigation. For example, some of my most commonly used commands while writing software are `i_<C-o>`, `gf`, `gri` and `ggVG`, but while blogging I
mostly use `z=`, `:set spell`, `~`, `:r _templates/post-header.md` or `dis` ( *Just not on subtitles, apparently!* ).

> **Note:** I have no idea if any of those are my most frequently used in their respective contexts, they just hopped to the top of my mind. Would be interesting to actually track that though.

I have spent just enough time attempting to write content in Microsoft Word to know I hate it. The formatting is never what I want, I always get stuck in lists, and I can't for the life of me seem to only indent one section. What frustrates me most is that I know I *should* be able to do those things in it, and there *are* ways to do them, but somehow I can just never get it right. As with all corporate software, Microsoft will tell you how your editor should look, function, feel, cost, and behave. I really do believe that setting your environment up just the way you like it is essential to a productive workflow; from your physical surroundings, to the tactile response of your keys, to the colour of your font and the editor in which you type.

> Microsoft will also lock you into the DOCX file format, [ISO/IEC 29500](https://www.iso.org/standard/71691.html). Part 1 alone is somewhere in the ballpark of **five thousand pages**, and that's not even the rest of OOXML.

Even though Vim is a **Text Editor**, not a **Word Processor**, *a fact which you would have known if you had bothered to read the first page of the friendly manual*, it is still the superior tool for writing novels, blogs, journals, and diaries. I would wager that you could conduct a scientific study using sentiment analysis on the contents of a diary and prove that individuals use more positive language after adopting Vim.

> **Hint:** When making an argument with reference to research, always refer to any studies as *scientific*.

What makes Vim so good for writing? Glad you asked. Writing is an art form, and art should not be constrained. I could end it right there, but I only have 23 lines written so far so I should probably elaborate.

## Spellchecker
Were you trained in the Queen's English? Do those Yankees drive you nuts with their missing vowels? Set your locale up for spell checks via `:setlocal spell spelllang=en_ca`. *No, I did **NOT** mean color*.

You can jump around spelling mistakes with `]s` and `[s`, and use the following shortcuts to quickly interact with'm. If it is a word that you want to add to your dictionary use `zg`, alternatively send a word to the shadow realm with `zw`. I have never needed `zu[wg]` of course, but if you do make a mistake and add the wrong word to a list, you will probably appreciate that little undo. The niftiest little shortcut to use with spell though is `z=` which provides you with an indexed list of options to replace your word with.

> **Note:** `:h z=` has that "This may take a long time.  Hit CTRL-C when you get bored." line, which is the style of writing in a user manual that made me fall in love with Vim. The entire manual is full of character and personality, which is something you just never see in docs.

## Pattern replacement
Imagine you are writing a fantasy novel and in a later chapter you are going to reveal that the antagonist is actually the protagonist's father. You didn't have much foresight and realized that you had never bothered to hide that fact by giving them different last names. You decide that only in your fourth chapter are you going to obscure the father's name. Vim's got you covered, you can match only between your two chapter markers and run a replace between them
```
:/^## Chapter 4/,/^## Chapter 5/s/Anakin Skywalker/Darth Vader/g
```

## Auto-complete names
You are writing in your diary about your lovely trip to Azerbaijan but are feeling rather lazy (and always forget the `i` after the `ba`), what are you to do? Not waste keystrokes on writing the full name, of course. Through the magic of keyword completion, in insert mode you can type `Az` followed by `<C-p>`. More likely than not, you have no other words starting with `Az` (barring a possible accidentally misspelled Azerbajan, of course), which means it will immediately complete your word for you. Neat! If you did have that rascally misspelled word kicking around, you can use `<C-p>` and `<C-n>` to navigate through the list. *Hint: think previous or next whenever you are using `n|p` commands*.

## Thesaurus

Not that I was struggling to find another example or anything, but I did try
`:h thesaurus` and found out there is thesaurus completion (`i_<C-x><C-t>`), so I
yoinked Project Gutenberg's resource and now I don't just *write*, I *annihilate*...

I went into the list I downloaded and deleted all of the entries that were multi-words so that matches
like 'write off' and 'write in' would not get included in the thesaurus
suggestions, but apparently I missed something and am too tired to figure out
how to set up `thesaurusfunc` correctly. 

So on that note, happy writing, endeavour to create beauty.
