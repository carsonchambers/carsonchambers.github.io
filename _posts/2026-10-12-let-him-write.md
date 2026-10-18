---
layout: post
title: "Let him write!"
date: 2026-10-12
tags: [vim]
context: ["++p", "c_%", "filename-modifiers", "::S", ":w_c", ":terminal"]
---

I am sure you have found yourself in this dreaded position before. You open
`nvim foo/bar/ipsum.zig`, write some code, and:

<pre><code>:w
<span class="vim-error">E212: Can't open file for writing: no such file or directory</span></code></pre>

Maybe you try one of these three options:

1. `:qa!` and call it quits for the day.
2. `<C-z>` → `mkdir -p foo/bar/` → `fg` → `:w`
3. `:!mkdir -p %:h` → `:w`

Each of those *may* solve the problem, but there is a better way: Neovim comes
with a flag to save you from any nastiness, `:w ++p`. It creates the missing
parent directories for you before writing.

> **Note:** On option 3: `%:h` is not shell-escaped. That can lead to some not
> so fun unintended consequences, specifically when doing something like
> `:!rm %`. Add the `:S` modifier to escape it safely: `:!mkdir -p %:h:S`.

It actually became evident to me while writing the Note above that many people
probably don't know the magic of the `%` shortcut. On the command line, `%`
expands to the current file name, and it allows for modifiers to do things
like:

- `%:h` the directory part (drops the file name)
- `%:~` the path relative to your home directory (`~/...`)
- `%:e` the extension of the file name
- `%:S` the file name escaped for use in a shell command

I'll probably write a dedicated post on this at some point, because it is a
great utility to have under your belt.

*Okay, but Carson, the real headache for me is when I try to edit a file that I
actually don't have permission for!*

Ah, yes, the ol' <code><span class="vim-error">E45</span></code>, then
<code><span class="vim-error">E212</span></code>.

In Vim you can do the following:
```vim
" Vim
:w !sudo tee %:S >/dev/null
```

> And remember kids, `:w !sudo` ≠ `:w! sudo`


Whereas Neovim's `:!` runs in a noninteractive shell connected over a pipe into a terminal, so `sudo` has nowhere to ask for your password. Instead, write to a temporary file and copy it back from a terminal buffer instead:

```vim
" Neovim
:w /tmp/foobar
:terminal sudo cp /tmp/foobar %:S
```

Also, if you have passwordless sudo on, I think you could maybe just do a sudo write without anything special. I am too lazy to verify that myself though, call it an exercise for the reader.

