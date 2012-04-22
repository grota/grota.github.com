---
layout: post
title: "Tmux: a terminal multiplexer full of niceties"
date: 2012-04-22 18:22
comments: true
categories: [tmux]
---

[Tmux][1] is a terminal multiplexer that has been around for a few years; doing a simple google search you will find some [introductory][2] [articles][3].

There are quite a few plugins that create a seamless integration with `vim`: [tslime][6], [vimux][7] and [slimux][8]. People also use tmux extensively for [remote pair programming][5].

Tmux is a nicer and more modern alternative to screen. Beside being actively mantained tmux is also extremely configurable and scriptable.
<!--more-->
I discovered tmux only recently, mainly thanks to the [Changelog show][4] and the resulting buzz on the twittersphere. It was only a matter of time before a customized `.tmux.conf` entered the realms of [my dotfiles][9].

If you are a developer you work on text all day, and you might have a few script or long-running jobs executing in the shell. If that's the case, it's also very likely that you have to constantly switch between those applications.

You might not be aware of that, but constantly switching focus takes a toll on your brain, is a source of distraction, and is a major hindrance towards achieving what us developers crave, a state of mental performance called ***[the flow][10]***.
If that is case you should know that adopting a workflow based on tmux can reduce a lot of that background stress.  
The most common pattern that emerges, for example, is being able to keep opened, side by side in the same tmux window, two panes: one with the shell and the other with terminal vim.

In the next post I'll describe how tmux helped me reduce a lot of the context switch that is major annoyance of mine while working, and a few configuration settings that make working with tmux a pleasure.

[1]: http://tmux.sourceforge.net/ "tmux"
[2]: http://blog.hawkhost.com/2010/06/28/tmux-the-terminal-multiplexer/ "hawkhost article"
[3]: http://mutelight.org/articles/practical-tmux "Practical tmux"
[4]: http://thechangelog.com/tagged/tmux "The Changelog, #tmux"
[5]: http://thechangelog.com/post/20986196780/wemux-multi-user-terminal-multiplexing-for-party-pair-pr "wemux"
[6]: https://github.com/sjl/tslime.vim "Steve Losh's tslime"
[7]: http://thechangelog.com/post/20906204174/vimux-simple-extensible-vim-integration-with-tmux "vimux article"
[8]: http://esa-matti.suuronen.org/blog/2012/04/19/slimux-tmux-plugin-for-vim/ "slimux"
[9]: http://github.com/grota/rcfiles "My rc files"
[10]: http://en.wikipedia.org/wiki/Flow_(psychology) "The Flow, from wikipedia"
