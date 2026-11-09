---
layout: post
title: "Cursor go up, cursor go down"
tags: [vim]
context: [up-down-motions]
date: 2026-11-04
---

You can tell where someone is at in their Vim journey by asking them to move the cursor down a line while they are in insert mode:
- **The Novice:** `↓`
- **The Apprentice:** `<Esc>ji`
- **The Expert:** `<C-o>j`
- **The Master:** `↓`

I'm only somewhat joking. I do find there are times where I subconsciously slip a down arrow in and go about my day as if I didn't just break the first rule of Vim club.

Dogmatic belief in the superiority of `hjkl` is common, but unfounded. It is
probably necessary to dissuade newcomers from continuing on their filthy habits,
but when you live and breathe ergonomics, you will stumble into many finger
layouts in which the optimal solution is `↓`.

> **Fun fact:** I guessed the digraph for ↓ on my first try,
> unfortunately however, I did not correctly guess up arrow. Déjà vu.
> [__Simple minds find simple joys__]({% post_url 2026-10-15-i-like-digraphs %}).

To instill the importance of `hjkl` while still permitting arrow keys when they are valid, someone — not me of course, I'm busy and got things to do! Someone like *you* is who I had in mind — should create a plugin for gamifying Vim that starts off with arrow and `<Esc>` keys disabled, and let's you unlock them with points you get by using new keyboard shortcuts.

Now, what I actually wanted to look at today was the different ways in which you can move your cursor up or down a line:

- `k` / `j`
- `<C-p>` / `<C-n>`: same as `k` / `j`
- `↑` / `↓`: same as `k` / `j`
- `<C-j>`: same as `j`
  > **Note:** There is no `<C-k>` counterpart. It does nothing in normal mode, and in insert mode it starts a digraph. Wonky, right?
- `-` / `+`: Brings you to the first non-whitespace character of the previous / next line.
- `<C-m>` / `<CR>`: same as `+`
  > **Note:** Again, no counterpart here...
- `gk` / `gj`: Display line navigation up / down
- `g↑` / `g↓`: same as `gk` / `gj`

What is neat is that you can use each of those within insert mode when you
first enter one-shot mode with `i_<C-o>`, *and* you can give them a count
too, wow!

So, for example, if while in insert mode you want to jump to the first non-whitespace
character three lines down you can use `<C-o>3<C-m>`, and voila. Without the
`<C-o>`, `<C-m>` in insert mode is just `<CR>`, so it breaks the line at your
cursor.

I left `O` and `o` out of that list intentionally because they are neat and
warrant their own little blurb. `O` and `o` create a new line above or below
your current line and move your cursor to it. If you give them a count, then
whatever you enter while in insert mode will be repeated on that many lines in
total once you leave insert mode. I personally never use the count functionality, but while writing code
I commonly use `i_<C-o>O` when I want to add a comment above my current line.

With my infinite knowledge of line motions, I have still never created a mapping I am happy with for quickly writing a new function signature. I have settled on snippets but I keep imagining doing something like `inoremap <leader>{} {<CR>}<Esc>O` so that I can write `function foobar() {}` which would convert to
```javascript
function foobar() {
    // cursor indented correctly to here
}
```

The problem is that I don't like insert mode remaps with my leader key because it is set to space, so things get super clunky. If I had a comment section you could show me a better way to do this...

> **Update (2026-11-08):** After some reflection on this, I have decided to opt for `inoremap {<CR> {<CR>}<C-o>O` because in insert mode, if I ever drop a curly brace then enter, my expectation is going to be the indentation, and there will be no hangup on it either because I have no { maps. Looks like I don't need your input after all.
