+++
date = "2025-07-29T22:19:41"
draft = false
title = "efficient terminal tools"
+++

In this post, I hope to give the best, most useful, and most practical terminal-based tools that I regularly use. These are the tools I wish someone had forced me to try years ago, so I hope to convince you to try them here.

> This post was originally written for a presentation I gave to coworkers. I plan to update it over time with any new discoveries I make.

<!-- mdformat-toc start --slug=github --no-anchors --maxlevel=6 --minlevel=1 -->

- [prerequisite: you need a good tty](#prerequisite-you-need-a-good-tty)
- [cht.sh](#chtsh)
- [gh-copilot](#gh-copilot)
- [ripgrep and fd](#ripgrep-and-fd)
- [gh](#gh)
- [atuin](#atuin)
- [lazygit and lazydocker](#lazygit-and-lazydocker)
- [vim](#vim)
- [nushell](#nushell)
- [Honorable Mentions](#honorable-mentions)

<!-- mdformat-toc end -->

---

As I progressed in my education and experience as a software engineer, I received a lot of guidance as to how to improve how my software was structured. However, I was never really instructed on the _process_ of creating that software. I moved between Eclipse, JetBrains, and VS Code without ever really learning how to navigate a codebase quickly, script programs together, or work with `git` beyond the dreaded:

```bash
git add . && git commit -m "changes" && git push
```

<figcaption>still a classic, but there is so much more</figcaption>

Later, I saw online what certain engineers and [bash wizards](https://www.youtube.com/watch?v=L967hYylZuc) were capable of. Certain things feel intractable—like mastering every `awk` and `bash` nuance. However, as I used the tools, I got more comfortable and began to move faster.

Additionally, there’s been an influx of usability improvements. As developer interest grows in languages like Rust and Zig, the chance to redesign from scratch has led to a new wave of excellent, easy-to-use tools.

---

## prerequisite: you need a good tty

> I will cry if you run these in Command Prompt.

Terminal applications can only do so much if the surrounding terminal interface is poor.

**For Linux and Mac**, I highly recommend either [kitty](https://sw.kovidgoyal.net/kitty/) or [ghostty](https://ghostty.org/). Both have excellent performance and support all the fancy terminal features. Namely, they work with the [kitty terminal graphics protocol](https://sw.kovidgoyal.net/kitty/graphics-protocol/) that lets you display images in the terminal!

**For Windows**, [alacritty](https://alacritty.org/index.html) is the best native option I have found. Not _quite_ as feature-rich in my experience, but the only tty of this class that is windows-native (that I have found).

**Also important:** Install a [Nerd Font](https://www.nerdfonts.com/)! Many programs depend on these for icons.

---

## cht.sh

When the maze of arguments and options are starting to slow you down, **[cht.sh](https://cht.sh/) is your best friend**. At any terminal with internet access, you can use it to search for command-line tools and their usage.

Lets say you are trying to do a simple tar operation.

[![hugo](images/tar.webp#large "Obligatory xkcd.")](https://xkcd.com/1168/)

First, you can use it directly from your browser _or through curl_: `curl cht.sh/tar`

Or, you can install their [command line client](https://github.com/chubin/cheat.sh#command-line-client-chtsh). I prefer this, as you don't need to use URL syntax to search. I'll run `cht.sh tar`:

{{< include-html "content/posts/efficient_terminal_tools/html/cht_sh.html" >}}

---

## gh-copilot

For the more complicated tasks, or for when you're not even sure which _command_ you need, I will often reach for the **[gh-copilot](https://github.com/github/gh-copilot) extension for `gh`**.

{{< asciicast src="/casts/gh-copilot.demo" >}}

I have this aliased to `??` in my terminal so I can quickly search for commands. I find this to be a lot more ergonomic than switching to something like [Warp Terminal](https://www.warp.dev/) when I need to search how to use a single command. [^warp]

---

## ripgrep and fd

When I speak of older tools getting a modern redesign, these are probably the prime examples.

**[fd](https://github.com/sharkdp/fd) and [ripgrep](https://github.com/BurntSushi/ripgrep)** are fantastic alternatives to `find` and `grep`, and are multithreaded by default. [^multithread] They have become my default for scripting operations to find certain regex patterns and file names quickly.

{{< asciicast src="/casts/rg_fd.demo" >}}

---

## gh

This section is basically here to say: **stop trying to script GitHub with `curl`!**

**[gh](https://github.com/cli/cli)** provides a helpful wrapper over many GitHub APIs and `git` operations. This integration allows for commands like `gh repo clone drew-council/nixconf`, which clones based on the GitHub repo name using your preference setting for SSH/HTTP. It also lets you make queries like `gh repo list --visibility=public`:

```
NAME                     DESCRIPTION              INFO              UPDATED
drew-council/nixconf     Nix Configuration Files  public            about 1 hour ago
drew-council/drew-cou...                           public            about 2 hours ago
drew-council/nixpkgs     Nix Packages collect...  public, fork      about 19 hours ago
drew-council/typeracer-FPGA                           public, archived  about 4 days ago
drew-council/hugo        The world’s fastest ...  public, fork      about 4 days ago
drew-council/zed         configuration for ze...  public            about 5 days ago
...
```

`gh` can output as `json`, which can be used in scripting quite easily.

---

## atuin

One of the most aggravating thing about working in the terminal can be when you know you have run a command before but it can't be found in your history. Maybe it was in another session, maybe your history ran out of space, or maybe it was run on a completely different machine.

**[atuin](https://github.com/ellie/atuin)** is a terminal history manager that aims to always capture the history of the commands you run. This means syncing across sessions, windows, different terminals, and even different devices if you choose.

It stores all of your command history in a local SQLite database and replaces your `CTRL+R` search with a fuzzyfind of that history database in a nice TUI.

{{< asciicast src="/casts/atuin.demo" speed=1.5 >}}

---

## lazygit and lazydocker

`lazygit` and `lazydocker` are wonderful TUIs for `git` and `docker` respectively by [@jesseduffield](https://github.com/jesseduffield/).

{{< asciicast src="/casts/lazytui.demo" speed=2 >}}

<figcaption>When you learn just a few keyboard shortcuts, you can really move quickly in these tools.</figcaption>

In both, the keybinds are nicely displayed for you at the bottom, but you can even _use your mouse_.

Both have almost entirely replaced most of the `docker` and `git` calls I would type out before. `lazygit` especially has completely changed how I work with git, as it allows for quickly selecting files to add, exclude, and discard from your working `git` changes to your commit.

---

## vim

I don't mean to beat a dead horse, but I truly don't understand why vi-style keybindings are not the industry standard.

I'm not adamant that you use full-fledged `vim` itself. VS Code has [VSCodeVim](https://github.com/VSCodeVim/Vim), which works great most of the time. I use [zed](https://zed.dev/) for my development, which has an extremely robust vim mode. Even `emacs` has "evil" mode.

Regardless, I _highly_ recommend taking a week, or even a weekend, to just give the keybinds a try in your favorite editor. Once you summit the initial learning curve, you will really see the benefits. I was a doubter myself at first, but after trying it, I haven't looked back.

---

## nushell

[Nushell](https://www.nushell.sh/) is my absolute favorite of these tools.

It is probably wrong to even call it a _tool_, as `nu` is a fully-fledged _shell_ which can be in lieu of `bash`/`zsh`/`fish`. [^posix] The key feature that sets `nu` apart from these is **Pipelines**.

Pipelines are a lot like traditional piping of stdin to stdout, but in `nu` they can store _structured data_. These look a lot like `json` and are printed as nicely formatted tables. You can then leverage the `nu` language functional operators to do some fairly powerful things:

{{< asciicast src="/casts/nushell.demo" >}}

Here's a `nu` script to get the Git-LFS files in a repo and sort by the ones using the most space.

```nu
#!/usr/bin/env nu

let lfs_file_data = (
  git lfs ls-files --size |
    detect columns -n |
    reject column1 |
    rename hash file size |
    update size {|row| $row.size | str substring 1..-2 | into filesize} |
    sort-by size
)

print $lfs_file_data

let total_size = ($lfs_file_data | get size | math sum)
print $"Total size: ($total_size)"
```

Here's what the script output looks like:

{{< include-html "content/posts/efficient_terminal_tools/html/lfs_sizes.html" >}}

The nice things here:

- `git lfs` commands don't have the ability to output `json`, but you can just pipe them into `detect columns` and it will figure the data structure out for you!
- There is a first-class `filesize` datatype, which we convert a string to and sort by. I don't even want to know the crazy scripting it would take to properly compare mega**bits** with kilo**bytes** without this.
- The biggest selling point for me: _I didn't have to look up anything._ No googling. No reading manpages. `nu` has a very high skill floor, and it can become very powerful if you take the time to read through the [excellent Nushell Book](https://www.nushell.sh/book/).

## Honorable Mentions

These tools are more niche, but come in handy for specific tasks.

I have never had a good experience going to shady file type conversion websites. They are always slow, covered in ads, and usually don't work.

For converting, cropping, editing, and re-encoding videos, use [**ffmpeg**](https://ffmpeg.org/). For images, use [**imagemagick**](https://imagemagick.org/).

> This isn't a terminal tool, but for PDF arranging, try [**pdfarranger**](https://github.com/pdfarranger/pdfarranger).

If you are working with docker images, [**dive**](https://github.com/wagoodman/dive) is a great tool for inspecting and analyzing docker images. It has often highlighted issues I could not find with any other image analysis tool.

`bat` is just `cat` with syntax highlighting. I use it all the time, especially because it behaves exactly like `cat` if it detects it is being piped into another command.

\[^warp\]: Warp Terminal is pretty cool, but it lacks a lot of the rendering features I have come to expect from my TTY and can have some compatibility issues with some TUI applications.

\[^multithread\]: A capable user of [GNU Parallel](https://www.gnu.org/software/parallel/) can make `grep` and `find` operations parallelized, which is useful in scripting. However, for most use cases, having these optimizations compiled in is very beneficial.

\[^posix\]:
Similar to `fish`, `nu` is _extremely_ not POSIX compliant, so copy-pasting or running scripts with `nu` as the interpreter are bound to fail often.

```
Never set a non-POSIX shell as your system's default shell. I set `nu` as the default program that launches when I start my TTY.
```
