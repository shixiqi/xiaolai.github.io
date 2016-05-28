---
title: 必要的装备（2）iTerm
date: 2016-05-21
tags: 工具
---

iTerm 比 OS X 里自带的 Terminal 不知道要强大多少倍…… 看两张图片就知道了。更多的功能介绍，可直接移步 [iTer 官方网站](https://www.iterm2.com/features.html)了解。

{% img /images/iterm-autocomplete.png %}

{% img /images/iterm-pastehistory.png %}

## 在 Finder 上添加一个按钮，“Open here in iTerm”


用 Automator 创建一个 Application（不是 Workflow 或者 Service；与[创建 Sublimetext 的 Finder 工具栏应用一样](http://xiaolai.li/#在-finder-上添加个按钮open-with-sublimetext)），添加一个 AppleScript:

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

而后把这个 Application 保存到 ```~/Applications``` 目录中，在按住 Command 键的同时，将这个程序拖到 Finder 工具栏上……