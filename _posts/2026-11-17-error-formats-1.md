---
layout: post
title: "Bug Hunter: Vol 1"
subtitle: "One less reason to leave Vim"
tags: [vim]
context: [errorformat]
date: 2026-11-17
---

Every program I work on works on the first try. The readers of this blog are intellectuals, so I would imagine you share the same experience as me. Unfortunately though, we work with other people and when we have to use their code, something will inevitably go wrong.

Thankfully, Vim has provided us with the ability to compile our code and handle errors in compiling gracefully all without ever leaving our editor.

This will most likely end up being a multi-part series because there is a lot of ground to cover, but to start with, we are going to look at `errorformat`. Error formatters allow us to set up a unique parser for each tool we use so that a compilation or test error becomes navigable via the `quickfix` list.

Enough yacking, time to look at an example. We will take one from the fuzzing tests from a [Go Tutorial](https://go.dev/doc/tutorial/fuzz):

```
$ go test
--- FAIL: FuzzReverse (0.00s)
    --- FAIL: FuzzReverse/e5e38b253e5d83d4 (0.00s)
        reverse_test.go:16: Number of runes: orig=1, rev=3, doubleRev=1
        reverse_test.go:21: Reverse produced invalid UTF-8 string "\x83\xb3\xe6"
FAIL
exit status 1
FAIL    nerdware.ca/fuzzing     0.583s
```

As you can see, I ran this from the command line like a schmuck instead of using Vim, so after that test I would need to re-open Vim and navigate to __reverse_test.go:16__ to look at the first error, *eughk!*.

We are going to rely on patterns and regular expressions to parse error messages. If you don't know what those are, then I retract that nice thing I said about you earlier. As we can see, our actual errors come back in the *simplest* of formats `<file_name>:<line_number>:<error_message>`. By pulling up our handy dandy manual as a reference, `:h errorformat`, we can ascertain the following:

| section | formatter |
| :--- | :--- |
| file_name | `%f` |
| line_number | `%l` |
| error_message | `%m` |

With which we will perform:

```
:set errorformat=%f:%l:\ %m
:set makeprg=go\ test
:make
```

Hot Tamale! You are taken right to the file and line for your error message and you can jump back and forth between errors with `[q` and `]q` respectively.

> **Compatibility:** `[q` and `]q` are Neovim defaults. On Vim you need to use `:cprev` and `:cnext`, or you can get the same mappings from [tpope's vim-unimpaired](https://github.com/tpope/vim-unimpaired), which comes with lots of other goodies too! Or, you know, just make the switch...

This is about as easy as it gets when it comes to error formats folks. The next post on the topic will concern itself with a multi-line error message and if the stars align in just the right way, I may even touch on more than the absolute basics of `quickfix` in the same post.
