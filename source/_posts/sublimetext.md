---
title: 必要的装备（1）SublimeText
date: 2016-05-19
tags: 工具
---

文章目录
===
<!-- toc -->
--------

[Sublimetext](http://sublimetext.com) 真是个招人喜欢的编辑器…… （我以前用 TextMate，现在彻底转到 Sublimetext 上了。）

{% img middle /images/ubuLOF1.gif "The text editor you'll fall in love with." %}

下载
===

[Sublimetext](http://sublimetext.com) 可以永远免费使用，但也接受购买，价格是 $70（也支持团购）—— 其实是非常值的，想想它能提高的效率罢，时间比什么都高贵。

配置
===

这种灵活的高级编辑器，往往需要自己不断手动配置，增加各种功能，逐步熟练掌握。

基本配置文件
---

依次点击 Sublimetext 菜单，```Sublime Text > Preferences > Settings - User```，而后在编辑器里拷贝粘贴以下配置代码保存即可。（暂时看不懂没关系，早晚会一眼看清楚……）

{% codeblock "Sublime Text > Preferences > Settings - User" lang:javascript %}
{
  "color_scheme": "Packages/Color Scheme - Default/Solarized (Dark).tmTheme",
  "bold_folder_labels": true,
  "font_face": "Menlo",
  "font_options": "subpixel_antialias",
  "font_size": 16,
  "highlight_line": true,
  "highlight_modified_tabs": true,
  "ignored_packages":
  [
      vintage
  ],
  "line_padding_bottom": 1,
  "line_padding_top": 1,
  "rulers":
  [
      80
  ],
  "scroll_past_end": true,
  "tab_size": 4,
  "tab_completion": false,
  "translate_tabs_to_spaces": true,
  "trim_trailing_white_space_on_save": true,
  "word_wrap": true
  "path": "/usr/bin:/bin:/usr/sbin:/sbin"
}
{% endcodeblock %}

从 Terminal 里唤出 Sublimetext
---

一般在命令行下大家喜欢用缩写，比如```subl```，我觉得没啥必要，反正输入```sub```之后用```⇥```自动补全也一样，所以我还是直接用```sublime```:

{% codeblock "ln -s sublime" lang:shell %}
ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/sublime
{% endcodeblock %}

在 Finder 上添加个按钮，“Open with sublimetext”
---

用 Automator 创建一个 Application（不是 Workflow 或者 Service），添加一个 AppleScript:

{% img /images/open-with-sublime-applescript.png %}

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

而后把这个 Application 保存到 ```~/Applications``` 目录中，在按住 Command 键的同时，将这个程序拖到 Finder 工具栏上……

安装 Package Control
---

使用快捷键 ``` ⌃ + ` ``` 呼出控制台，在输入框中输入：

{% codeblock "安装 Package Control:" lang:python packagecontrol https://packagecontrol.io/installation %}
import urllib.request,os,hashlib; h = '2915d1851351e5ee549c20394736b442' + '8bc59f460fa1548d1514676163dafc88'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
{% endcodeblock %}

安装常用插件
---

⇧ + ⌘ + P，呼出 Package Control, 输入 Packge install，按回车键，而后选择相应的 Package 安装……

> * SidebarEnhancement
> * AllAutoComplete
> * Alignment
> * SublimeGit
> * GitGutter
> * Origami
> * MarkdownEditing
> * Ctags
> * Table Editor
> * Emmet
> * Terminal
> * ColorPicker
> * FileDiffs

关掉 Vintage
---

Sublimetext 兼容那个神一样的编辑器 Vi/Vim，所以也有 Visual/Comman/Insert 模式，可对于那些不使用或者不会使用 Vi/Vim 的人来说，这个模式很耽误事儿，想要关掉它，还挺费劲：

{% codeblock "使用“Shift+Command+P”打开 Package Control" lang:shell %}
    Shift+Command+P > Package Control: Disable Packages > Vintage
{% endcodeblock %}

插件
===

安装 Package Control
---

使用快捷键 ⌃ + ` 呼出控制台，在输入框中输入：

{% codeblock "安装 Package Control:" lang:python packagecontrol https://packagecontrol.io/installation %}
import urllib.request,os,hashlib; h = '2915d1851351e5ee549c20394736b442' + '8bc59f460fa1548d1514676163dafc88'; pf = 'Package Control.sublime-package'; ipp = sublime.installed_packages_path(); urllib.request.install_opener( urllib.request.build_opener( urllib.request.ProxyHandler()) ); by = urllib.request.urlopen( 'http://packagecontrol.io/' + pf.replace(' ', '%20')).read(); dh = hashlib.sha256(by).hexdigest(); print('Error validating download (got %s instead of %s), please try manual install' % (dh, h)) if dh != h else open(os.path.join( ipp, pf), 'wb' ).write(by)
{% endcodeblock %}

关掉 Vintage
---
Sublimetext 兼容那个神一样的编辑器 Vi/Vim，所以也有 Visual/Comman/Insert 模式，可对于那些不使用或者不会使用 Vi/Vim 的人来说，这个模式很耽误事儿，想要彻底关掉它，还挺费劲；最好是通过 Package Control 去做：

{% codeblock 用“⇧+⌘+P”打开 Package Control lang:shell %}
  Disable Packages > Vintage
{% endcodeblock %}

常用插件
---

> * SidebarEnhancement
> * AllAutoComplete
> * Alignment
> * SublimeGit
> * GitGutter
> * Origami
> * MarkdownEditing
> * Ctags
> * Table Editor
> * Emmet
> * Terminal
> * ColorPicker
> * FileDiffs


其它
===

Sublimetext 的图标
---

这两个都不错，反正比原生的强太多了：

> - https://dribbble.com/shots/2273297-Sublime-Text-Icon
> - https://dribbble.com/shots/337996-Sublime-Text-2-Icon

多台机器使用同一个配置
---

到```~/Application Support```目录里，把```Packages```和```Installed Packages```这两个目录拷贝到 iCloud 目录里，而后用```ln -s```命令创建硬链：

{% codeblock "使用 iCloud 同步配置文件" lang:shell %}
mkdir ~/Library/Mobile\ Documents/com~apple~CloudDocs/Sublime\ Text\ 3
mv ~/Application\ Support/Sublime\ Text\ 3/Packages ~/Library/Mobile\ Documents/com~apple~CloudDocs/Sublime\ Text\ 3
mv ~/Application\ Support/Sublime\ Text\ 3/Installed\ Packages ~/Library/Mobile\ Documents/com~apple~CloudDocs/Sublime\ Text\ 3
cd ~/Application\ Support/Sublime\ Text\ 3
ln -s ~/Library/Mobile\ Documents/com~apple~CloudDocs/Sublime\ Text\ 3/Packages
ln -s ~/Library/Mobile\ Documents/com~apple~CloudDocs/Sublime\ Text\ 3/Installed\ Packages
{% endcodeblock %}


