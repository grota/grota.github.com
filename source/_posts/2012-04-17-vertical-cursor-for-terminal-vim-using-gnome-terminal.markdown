---
layout: post
title: "Vertical cursor for terminal vim using gnome-terminal"
date: 2012-04-17 18:31
comments: true
categories: [vim, dotfiles, linux]
---

A few people know I am a vim aficionado, and I figured I could share a little bit of my vim knowledge on this blog.
While browsing the [r/vim subreddit](http://reddit.com/r/vim) a while ago I found a little piece of vim configuration that lets you have a vertical bar for the cursor in terminal vim, using gnome-terminal as a terminal emulator.
<!-- more -->
Without further ado, here's the snippet, which you can put in your `.vimrc`, for example.

```vim
if has("autocmd") && has('GUI_GTK')
  au InsertEnter * silent execute "!gconftool-2 --type string --set /apps/gnome-terminal/profiles/Default/cursor_shape ibeam"
  au InsertLeave * silent execute "!gconftool-2 --type string --set /apps/gnome-terminal/profiles/Default/cursor_shape block"
  au VimLeave * silent execute "!gconftool-2 --type string --set /apps/gnome-terminal/profiles/Default/cursor_shape block"
endif
```

Those of you using `gvim` might already have this, since the feature is builtin and might only need to be enabled.

If you use gnome-terminal in Linux, on the other hand, this is not natively supported, and it might be on your *nice-to-have* list, especially if you use tmux.

