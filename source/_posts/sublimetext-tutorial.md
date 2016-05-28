---
title: Sublimetext Tutorial
date: 2016-05-25
tag: sublimetext texteditor puretext
---

# Prerequisites

> * using a mac;
> * familiar with google search;
> * having bought a VPN (for those who's in China)

# Goal

Write like a professional programmer.

# Steps

## Download Sublimetext

> http://sublimetext.com

### Try...

Remember the rule of thumb:

> Always Google first... now and then...

It's a super trick to google these keyword combination:

> * sublimetext reasons
> * sublimetext tricks tips
> * sublimetext tutorial
> * sublimetext shortcuts
> * sublimetext cheatsheet

Put these keywords into your head (tutorial, cheatsheet, etc.), they're extremely useful whenever you're learning a new set of skills online.

Set a timer, for example, 1 hour, more or less, and then surf the web on your search results. When the timer beeps, come back to follwoing steps.

When you're back, you've learned a lot, really a lot, and you're not the same person as you are 1 hour before.

## Basic Setups

### User Settings File

```Preference``` > ```Settings - User```

In the opened file copy & paste the following code, it's doesn't matter you understand it or not for now:

{% codeblock %}
{
  "bold_folder_labels": true,
  "color_scheme": "Packages/Color Scheme - Default/Monokai.tmTheme",
  "font_face": "Monaco",
  "font_options": "subpixel_antialias",
  "font_size": 16,
  "highlight_line": true,
  "highlight_modified_tabs": true,
  "ignored_packages":
  [
    "Vintage"
  ],
  "line_padding_bottom": 1,
  "line_padding_top": 1,
  "rulers":
  [
    100
  ],
  "scroll_past_end": true,
  "tab_completion": true,
  "tab_size": 2,
  "translate_tabs_to_spaces": true,
  "trim_trailing_white_space_on_save": true,
  "word_wrap": true
}
{% endcodeblock %}

The whole interface now looks just quite different than a moment before.

### Try...

Open a new file with <kbd>⌘</kbd> + <kbd>n</kbd>, copy the text below into the sublimetext:

> Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.

Now, try to click keyboard in sequence:

> <kbd>c</kbd>
> <kbd>l</kbd>
> <kbd>m</kbd>
> <kbd>⇥</kbd>

... after you click the TAB key (<kbd>⇥</kbd>), ```clm``` mysteriously becomes ```cillum```. This is the magic power of the TAB key in the sublimetext. The TAB key (<kbd>⇥</kbd>) tiggers auto-completion, tries to find words contains the letters before the cursor, if such a word exists, then copletes it, like a magic.

Try another:

> <kbd>c</kbd>
> <kbd>n</kbd>
> <kbd>⌃</kbd> + <kbd>space</kbd>


(<kbd>⌃</kbd> means the ```control``` key.)

... you may well see two options:

> consequat
> consectetur

You can use <kbd>↑</kbd> and <kbd>↓</kbd> to select...

Now you know that the TAB key (<kbd>⇥</kbd>) can do unlimited tricks in sublimetext.

## Advanced Setups

### Install Package Control

Go the the website: https://packagecontrol.io and follow the instruction.

### Try...

Google again!

> sublimetext popular packages

Read, and try them out.

For example, you might well find out some better color themes. I personally love [Spacegray theme](https://github.com/kkga/spacegray/) so much.

### Packges you can't live without

> - SidebarEnhancement
> - All Autocomplete
> - ColorPicker
> - AlignTab

A lot more you'll install in the future, so just don't try too much right now. Time to go forward.

## Like a programmer...

### Learn HTML

In fact, you can learn HTML within 5 minutes.

> What is HTML? Writing HTML is to add some tags to a pure text so that it can be properlly displayed in the browsers.

That's it.

{% codeblock lang:html %}
What is <strong>HTML</strong>? Writing HTML is
<em>to add some tags to a pure text so that it
can be properlly displayed in the browsers</em>.
{% endcodeblock %}

... the browser interpretes this "tagged text", and display them in a proper format.

> What is **HTML**? Writing HTML is _to add some tags to a pure text so that it can be properlly displayed in the browsers_.

You see the text in *bold* and the _italic_ format? ? Over. Your learning phase is over. Now that you know the essence of writing HTML, the only thing needed is to try out the all tags. Google again, merely search the word 'html', and then you'll encounter the famous site: [W3Schools](http://www.w3schools.com/html/)

Give yourself one whole afternoon, or night, fill those tags into your brain.

## Integrating Terminal, Finder, Sublime Text, and the Browsers...

### Use a more advanced Command Line Tool: iTerm

Same as before, you can search on Google:

> * iTerm reasons
> * iTerm tricks tips
> * iTerm tutorial
> * iTerm shortcuts

Then you'll surely prefer iTerm over Terminal.

Open iTerm, use the keybinding <kbd>⌘</kbd> + <kbd>,</kbd> to call out the ```preference panel```, in the Keys tab, check "Show/hid iTerm2 with a system-wide hotkey", set Hotkey as <kbd>⌘</kbd> + <kbd>.</kbd>.

### Write and view HTML simultaneously

There're several options:

> - [LiveReload](http://livereload.com/)
> - [LiveStyle](http://livestyle.io/)
> - [Fire](http://fireapp.kkbox.com/)

However the most convenient way is to use a sublimetext package:

### Open here (files/folder) with Sublimetext in Finder

In Spotlight, call out the program Automator, create an Application (rather than Workflow or Service),

{% img /images/open-with-sublime-applescript.png %}

add a AppleScript to the created Application:

{% codeblock "Automator Application AppleScript" lang:AppleScript%}
on run {input, parameters}

  set finderSelection to ""
  set theTarget to ""
  set appPath to path to application "Sublime Text"
  set defaultTarget to (path to home folder as alias)
  -- comment line above and uncomment line below to open desktop instead of user home when there's no selection or open folder in the Finder:
  -- set defaultTarget to (path to desktop folder as alias)

  if (input as string) is "" then
    tell application "Finder"
      set finderSelection to (get selection)
      if length of finderSelection is greater than 0 then
        set theTarget to finderSelection
      else
        try
          set theTarget to (folder of the front window as alias)
        on error
          set theTarget to defaultTarget
        end try
      end if

      tell application "Finder"
        open theTarget using appPath
      end tell

    end tell
  else
    try
      set targets to {}
      set oldDelimiters to text item delimiters
      set text item delimiters to tab
      set qArray to every text item of q
      set text item delimiters to oldDelimiters
      repeat with atarget in qArray

      if atarget starts with "~" then
        set userHome to POSIX path of (path to home folder)
        if userHome ends with "/" then
          set userHome to characters 1 thru -2 of userHome as string
        end if

        try
          set atarget to userHome & characters 2 thru -1 of atarget as string
        on error
          set atarget to userHome
        end try
      end if

        set targetAlias to ((POSIX file atarget) as alias)
        set targets to targets & targetAlias
      end repeat

      set theTarget to targets

      tell application "Finder"
        open theTarget using appPath
      end tell

      on error
        return (input as string) & " is not a valid file or folder path."
      end try
  end if

  return input
end run
{% endcodeblock %}

### Open here (folder) with iTerm/Terminal in Finder

In Spotlight, call out the program Automator, create an Application (rather than Workflow or Service), add a AppleScript to the created Application:

{% codeblock "Open here in iTerm" lang:AppleScript %}
on run {input, parameters}
  tell application "Finder"
    set dir_path to quoted form of (POSIX path of (folder of the front window as alias))
  end tell
  CD_to(dir_path)
end run

on CD_to(theDir)
  tell application "iTerm"
    activate

    try
      set sesh to current session of current terminal
    on error
      set term to (make new terminal)
      tell term
        launch session "Default"
        set sesh to current session
      end tell
    end try

    tell sesh
      write text "cd " & theDir & ";clear;"
    end tell
  end tell
end CD_to
{% endcodeblock %}

Save the Application anywhere with any name, then drap the Application to Finder's toolbar while holding the <kbd>⌘</kbd> key.

### Open here (folder) with Finder from iTerm/Terminal

{% codeblock %}
$ open .
{% endcodeblock %}

### Open here (folder) with Sublimetext in iTerm/Terminal

{% codeblock %}
ln -s "/Applications/Sublime\ Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/subl
{% endcodeblock %}

Then you can open the current folder with Sublimetext like this:

{% codeblock %}
$ subl .
{% endcodeblock %}

### Open files/folder with iTerm/Terminal/Finder in Sublimetext

In Package Control, install the Package, Sidebar Enhencement. (You might have already installed this package...)

### Refresh Browsers in Sublimetext

> Browser Refresh

Check it out on [its github page](https://github.com/gcollazo/BrowserRefresh-Sublime).

## Final Tips

### Move cursor forward over braces, quotes

in ```Preference > Keybindings - User```:

{% codeblock  %}
[
  { "keys": ["enter"], "command": "move", "args": {"by": "characters", "forward": true}, "context":
  [
      { "key": "following_text", "operator": "regex_contains", "operand": "^[),;:'}\"\\]]", "match_all": true },
      { "key": "auto_complete_visible", "operator": "equal", "operand": false }
  ]
  },
]
{% endcodeblock %}

If you don't want to move cursor, instead you want to break the line, use <kbd>⇧</kbd> + <kbd>⏎</kbd>.

### AlignTab

This is a little bit hard for beginners, but you'd better try hard to understand. Go figure it out.

### Keybindings, Macros, Snippets

As you go forward, you'll need more tricks to meet your need, you'll set your own kebindings, macros, and snippets... But what are they? Don't mind right now, just remember these words, and you are going to naturally Google them now and then.

My own Snippets is being saved on Github:

> https://github.com/xiaolai/sublime-snippets

And in the README.md file, my own User/Keybinding is also included.