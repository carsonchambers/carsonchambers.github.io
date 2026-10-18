---
layout: post
title: "Vim probably has that"
tags: [vim, rant]
context: ["lsp", "packages", "registers", "motion.txt", "quickfix"]
date: 2026-10-13
---

> **Note:** I use Neovim as my daily driver. I don't use native Vim that often, but I hear LSP support is better in Neovim than Vim.

As of the time of writing, I have had a 0% success rate in making any converts
to the church of Vim. The heretics are usually split between "I already know
this IDE" and "Vim doesn't have the functionality of my IDE". To the former, we
call that Stockholm Syndrome. To the latter, we call that ignorance.

Today we will discuss why Vim can do most of what your *fancy-dancy* editor does, and more. I will cover the most common objections, namely: Database integration, Version control integration, Language Server Protocol support (not that most people actually know to call it that), a plugin ecosystem, and remote development support. What you will find, is that all of these are from plugins, but that is sorta the point. Get what you want, nothing more, nothing less.

## Databases
[Tim Pope](https://github.com/tpope) has an incredible plugin called [vim-dadbod](https://github.com/tpope/vim-dadbod). This plugin gives you access to databases with customizable configurations for all of the big names. Once you have this up and running you can execute sql chunks from files, entire files, or adhoc queries and get autocomplete results as you write.

## Version control integration (git, of course)
Well, [tpope](https://github.com/tpope) saves the day again with [vim-fugitive](https://github.com/tpope/vim-fugitive). You can simply issue your cli git
commands in Command-line mode, have an intuitive UI, and customize it to your liking. When
combined (optionally) with [diffview](https://github.com/sindrets/diffview.nvim)
for reviewing diffs of a specific file or commit, and [gitsigns](https://github.com/lewis6991/gitsigns.nvim) for gutter markup and jumping to
hunks, you really get all of the gitting you could possibly need.


## Language Server Protocol
Some people have a tough time getting started with LSP's, but that's only
because of a skill issue. It's really simple, and there are a thousand videos
on the topic if you prefer that to just reading the docs `:h lsp`. Below is an
example of all that can be needed sometimes for a configuration (Which is almost 100% copy paste from the README):
```lua

local vim = vim

-- Install `ziglang/zig.vim` using the built-in plugin manager (Neovim 0.12.0+)
-- A tool like `vim-plug` or `lazy.nvim` can also be used instead.
vim.pack.add({
  'https://codeberg.org/ziglang/zig.vim',
})

-- don't show parse errors in a separate window
vim.g.zig_fmt_parse_errors = 0
-- disable format-on-save from `ziglang/zig.vim`
vim.g.zig_fmt_autosave = 0
-- enable  format-on-save from vim.lsp + ZLS
--
-- Formatting with ZLS matches `zig fmt`.
vim.api.nvim_create_autocmd('BufWritePre', {
  pattern = { "*.zig", "*.zon" },
  callback = function(ev)
    vim.lsp.buf.format()
  end
})

vim.lsp.config['zls'] = {
  -- Set to 'zls' if `zls` is in your PATH
  cmd = { '/home/carson/.config/nvim/lua/lang/zls/zig-out/bin/zls' },
  filetypes = { 'zig' },
  root_markers = { 'build.zig' },
  -- There are two ways to set config options:
  --   - edit your `zls.json` that applies to any editor that uses ZLS
  --   - set in-editor config options with the `settings` field below.
  --
  -- Further information on how to configure ZLS:
  -- https://zigtools.org/zls/configure/
  settings = {
    zls = {
      -- Whether to enable build-on-save diagnostics
      --
      -- Further information about build-on save:
      -- https://zigtools.org/zls/guides/build-on-save/
      -- enable_build_on_save = true,

      -- omit the following line if `zig` is in your PATH
      zig_exe_path = '/usr/bin/zig'
    }
  },
}
vim.lsp.enable('zls')
```

With those lines I get first class editor support when working with Vim.

## Plugin ecosystem
As you might have picked up on from reading the above sections, there is infact
a plugin ecosystem for Vim. There are a ton of different plugins, plugin
managers, and ways to integrate them all. I personally use `vim.pack` which is
native, but I believe most people use
[Mason](https://github.com/mason-org/mason.nvim). Part of Bram's vision with
Vim was a tight consistent core that could be extended by individuals as they
saw fit. I find this part alone to be such a compelling argument for using Vim.
It is the idea that Vim is a Personalized Development Environment (I know the
phrase is attributed to [tj_devries](https://github.com/tjdevries) but I coulda
sworn I heard it in someone's conference talk before that... anywho...). I can
keep my editor lightweight, and bring in things as I want or need them, for
instance I absolutely love the
[nvim-surround](https://github.com/kylechui/nvim-surround) plugin so I can do
things like changing a surrounding parenthesis to a bracket or changing a
surrounding function. But if you didn't like having that kind of power at your
fingertips (coward!), you are not forced to include it in your editor.

## Remote development
This is a bit embarassing, but I actually did not have this set up until quite
recently. I work on a few codebases that have remote development dev
environments, and I had been leaving my JetBrains IDE in a hidden tab in order
to keep my remote development code flow working. Eventually, I admitted the
error of my ways, and just added in two simple additions to my .nvim.lua file
(namely a PostBufWrite rsync, and a function RsyncProj that I can use to sync
over all of the files after something like a git branch switch). It took a
little bit of trial and error to get my excludes working as intended, but I
think I had it all working in only a few hours.

## Some bonuses you don't get from other editors
- Macros
- Registers
- Vim-motions
- Modes
- Developing an unhealthy superiority complex
- Quickfix List
- Can work on any remote server with your same daily setup (either running Vim on the server or via netrw-transparent)
