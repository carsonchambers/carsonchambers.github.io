---
layout: post
title: "neat-rw"
subtitle: "When I see people with file explorers open while they code, I can't help but judge them."
tags: [netrw, vim]
context: [mksession, netrw]
date: 2026-10-27
---

When I was first trying to convert my friends to the cult of Vim, I would try to show them that they could move their bloated development environment into the terminal:

```
:30Vexplore
<C-w><C-w>
:set splitbelow
10split | terminal
```

> **Hint:** In case you weren't aware because you have been living under a rock, you can use `:mksession foobar.vim` to save your global settings and window layouts. To reload use `vim -S foobar.vim`

While I could get a chuckle out of them, I could see in their eyes that they
were still longing for their coveted mouse support. On one occasion, I was met with
"How did you open up that *awful* file explorer mode". I recoiled in horror... he couldn't be referring to my beloved netrw... could he?

Netrw is entirely misunderstood. It allows you to navigate with Vim commands,
*transparently* edit remote files, even BROWSE THE WEB?! That's right, you can
use file protocols like https and scp when opening up a file in Vim. For
instance, if we wanted to check out the hottest blog on the web right now, we
could do `vim https://blog.nerdware.ca`, and voila, there we have it, lynx is dead!
In all seriousness though, being able to tinker with
remote files via a protocol like `scp://` is pretty flipping useful.
You can quickly

- get the log contents on a remote server  with
```
:r scp://carson@buzzbar//var/log/ipsum.log
```
> **Hint:** If this is a large log file, you're probably better off just shelling out to ssh

- edit a *.env*
```
vim scp://carson@delta//var/www/blog/.env
```
> **Note:** If you don't do so already, when just viewing a .env file, it never hurts to pass the `-M` flag first to ensure you don't accidentally modify the file.

- peruse directories at your leisure
```
vim scp://carson@delta//var/www/blog/
```

Not impressed yet? You're a tough cookie. Okay, imagine you want to grab a few files off a remote server.
You probably use sftp, or scp and try to tab-complete your way to the destination. But it would sure be a lot nicer if on that remote
server you could quickly check things out before pulling them, wouldn't it?

```
:Explore
mt
:e scp://carson@ipsum/foo/bar/
p
mf
mc
```

- `mt` Marks the directory as the target for the copy command
- `p`  Previews the file in a split so we can ensure it has the contents we want
- `mf` Marks the file to be copied back over
- `mc` Copies the marked file to the target directory

You're a liar if you aren't impressed yet. 

I guess it is possible that your computer is castle that does not want any outside connections,
so you fart in my general direction. I ask that you don't do that, because netrw still has utility to you
as well, Guy de Loimbard. You can rename a file with `R`, or to start editing the most recently modified file by sorting
with `s`, or execute a script with `X`, all the while navigating around like you are in any old buffer.

Even though you can never look cool if you have a file explorer open, you can at least look a little less uncool if that file explorer is netrw.
