---
layout: post
title: "Tmux: Clipboard Integration"
date: 2012-05-08 22:55
comments: true
categories: [tmux, dotfiles]
---

{% comment %}
It's also possible to obtain the structs of previous posts via
{{ site.posts[1].url }} and {{ page.previous.url }}
{% endcomment %}

This post is a follow-up to [my introduction to tmux]({{ page.previous.url }}).

Since it is not feasible to go through all of my [.tmux.conf](https://github.com/grota/dotfiles/blob/master/tmux/_tmux.conf) settings, I'll keep this post short and only talk about tmux's clipboard features, how I customized them, and how they relate to my workflow. Hopefully you will be able to find some value in this and be able to integrate my configuration snippets in your workflow.

<!-- more -->

Working in Linux, I am blessed by having two clipboards, a *system clipboard* (filled in by the typical `Ctrl-C` key combination) and the *selection clipboard*, (filled in by the mouse selection).
Since I usually keep fidgeting text in the browser with the mouse, the selection clipboard is more volatile for me.

Tmux, like vim, is modal: by typing the right sequence of keys you enter the so called *copy mode* which permits a section of a window or its history to be copied to a paste buffer for later insertion into another window.

The cool thing, compared to the system and selection clipboards, is that it's actually a set of buffers.
You can even list them, see the picture below.

{% img center /images/posts/tmux_paste_buffers.png %}

A common requirement that pops up in my workflow is being able to both read and write to the selection and system clipboards from tmux. For example:

- I need some text that is currently in my browser to reach `bash` and `vim` running inside tmux.
- I need to copy some text inside the terminal (like some snippet of code, or a script output) into the browser.

Both can be obtained by putting the following snippet of tmux configuration inside `.tmux.conf`

```bash A piece of my .tmux.conf https://github.com/grota/dotfiles/blob/master/tmux/_tmux.conf Sauce
# C-c: save into system clipboard (+). With preselection.
bind C-c choose-buffer "run \"tmux save-buffer -b %% - | xclip -i -sel clipboard\" \; run \" tmux display \\\"Clipboard \(+\) filled with: $(tmux save-buffer -b %1 - | dd ibs=1 obs=1 status=noxfer count=80 2> /dev/null)... \\\" \" "
# C-v: copy from + clipboard.
bind C-v run "tmux set-buffer \"$(xclip -o -sel clipboard)\"; tmux paste-buffer" \; run "tmux display \"Copied from \(+\) $(xclip -o -sel clipboard | dd ibs=1 obs=1 status=noxfer count=80 2> /dev/null)... \""

# C-d: save into selection clipboard (*). With preselection.
bind C-d choose-buffer "run \"tmux save-buffer -b %% - | xclip -i\" \; run \" tmux display \\\"Clipboard \(*\) filled with: $(tmux save-buffer -b %1 - | dd ibs=1 obs=1 status=noxfer count=80 2> /dev/null)... \\\" \" "
# C-f: copy from * clipboard.
bind C-f run "tmux set-buffer \"$(xclip -o)\"; tmux paste-buffer" \; run "tmux display \"Copied from \(*\) $(xclip -o | dd ibs=1 obs=1 status=noxfer count=80 2> /dev/null)... \""
```

this makes use of the [xclip](http://sourceforge.net/projects/xclip/) program to access the system and selection clipboards.

Now, while in tmux:

1. Everytime you press the `prefix` key followed by `C-v` you will get the content of the system clipboard inside tmux.
2. Everytime you press the `prefix` key followed by `C-c` you will be asked to choose from the list of tmux paste-buffers. The buffer selected will be put into the system clipboard.

The same *copy/paste* behaviour can be applied to the selection clipboard by using `C-f` and `C-d`.  

Now admittedly point 1 above is not strictly necessary because there are usually system-wide shortcuts to do that, (`Shift-Ctrl-v` and `Shift-Insert` are the usual defaults in Linux) but I'm a sucker for symmetry.
