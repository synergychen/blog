---
layout: post
title: 4 Steps to Configure Sublime Text 3 + Vim
date: 2016-04-06 22:03:23
categories: tools
---

> Slim, fast and open.

Here is my routes of using editor tools:
`sublime text` -> `vim` -> `RubyMine` -> `Atom` -> `Sublime Text 3`

It's loop, back to Sublime Text, which is my favorite up to now.

### Step 1: install package control

Open `View > Show Console` and run
{% highlight bash %}
import urllib.request,os,hashlib; h = '2915d1851351e5ee549c20394736b442' + '8bc59f460fa1548d1514676163dafc88'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
{% endhighlight %}

### Step 2: install packages

Using `command + shift + p` and type `Package Control: Install Package` to install one package at a time or `Package Control: Advanced Install Package` to install multiple at once.

For `Advanced Install Package`, use `,` to split package names as follows:

{% highlight bash %}
All Autocomplete,Emmet,GitGutter,Git,AdvancedNewFile
{% endhighlight %}

### Step 3: custom user settings

`command + shift + p` and type `Preferences: Settings - User` to custom user settings, if you want to refer more setting options, use same way to open `Preferences: Settings - Default`.

Following are my personal preferences

{% highlight bash %}
{
  "font_size": 11,
  "ignored_packages":
  [
  ],
  "vintage_start_in_command_mode": true,
  "auto_complete": true,
  "auto_complete_commit_on_tab": true,
  "copy_with_empty_selection": true,
  "ensure_newline_at_eof_on_save": true,
  "index_files": true,
  "rulers":
  [
  79
  ],
  "tab_size": 2,
  "translate_tabs_to_spaces": true,
  "trim_trailing_white_space_on_save": true
}
{% endhighlight %}

Notice `Vim` mode is turned off by default. In above settings, `ignored_packages` is empty to enable `Vim` mode.

### Step 4: custom key bindings

`command + shift + p` and type `Preferences: Key Bindings - User` to start editing.

{% highlight bash %}
[
  { "keys": ["ctrl+l"], "command": "next_view" },
  { "keys": ["ctrl+h"], "command": "prev_view" }
]
{% endhighlight %}

For more preference options, refer to `Preferences: Key Bindings - Default`.

You are ready to go.
