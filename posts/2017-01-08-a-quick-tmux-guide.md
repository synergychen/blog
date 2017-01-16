---
layout: post
title: A Quick Tmux Guide
date: 2017-01-08 21:07:00
categories: Tools
---

> If you could use one to fit all, why using two?

### What is Tmux

The basic logic of tmux is very simple: do everything in one window.

### Install

Life would be easiler with brew:

```
brew install tmux
```

### Start

Start tmux is as say as type `tmux` in terminal.

### Customize

Open `~/.tmux.conf` to add customized settings. Create the file if it does not exist.

Here is a list of settings to start with, where `C` is `Ctrl` and `M` is `Alt`.

```
# reload tmux config
bind r source-file ~/.tmux.conf

# set zsh as your default Tmux shell
set-option -g default-shell /bin/zsh

# remap prefix to Control + a
set -g prefix C-a

# bind 'C-a C-a' to type 'C-a'
bind C-a send-prefix
unbind C-b

# start windows and panes from 1
set -g base-index 1
setw -g pane-base-index 1

# no delay for escape key press
set -sg escape-time 0

# switch windows
bind -n C-Left  previous-window
bind -n C-Right next-window
bind -n S-Left  previous-window
bind -n S-Right next-window

# split panes using | and -
bind | split-window -h
bind - split-window -v

# vim style pane selection
bind h select-pane -L
bind j select-pane -D
bind k select-pane -U
bind l select-pane -R
```
