---
layout: lecture
title: "編輯器 (Vim) （尚未翻譯）"
date: 2019-01-15
ready: true
video:
  aspect: 56.25
  id: a6Q8Na575qc
---

<!-- Writing English words and writing code are very different activities. When
programming, you spend more time switching files, reading, navigating, and
editing code compared to writing a long stream. It makes sense that there are
different types of programs for writing English words versus code (e.g.
Microsoft Word versus Visual Studio Code). -->
寫作和寫程式實際上差異很大。
當我們寫程式的時候，會常常切換檔案、閱讀、尋找與改正程式碼，而寫作時往往會連續鍵入文字。
所以對於寫作和寫程式常常由不同種類的程式來處理（比如 Microsoft Word 和 Visual Studio Code）。

<!-- As programmers, we spend most of our time editing code, so it's worth investing
time mastering an editor that fits your needs. Here's how you learn a new
editor: -->
作為程式設計師，我們會與編輯器共同度過許久，因此使用些時間熟練使用適合自己需求的編輯器是值得的。

<!-- - Start with a tutorial (i.e. this lecture, plus resources that we point out)
- Stick with using the editor for all your text editing needs (even if it slows
you down initially)
- Look things up as you go: if it seems like there should be a better way to do
something, there probably is -->
- 閱讀指導 （例如此課程與我們列出的資源）
- 堅持使用它來完成所有文字輸入（即使在開始時速度很慢）
- 隨時查閱：如果看起來可能有更好地辦法做某件事，通常確實會有

<!-- If you follow the above method, fully committing to using the new program for
all text editing purposes, the timeline for learning a sophisticated text
editor looks like this. In an hour or two, you'll learn basic editor functions
such as opening and editing files, save/quit, and navigating buffers. Once
you're 20 hours in, you should be as fast as you were with your old editor.
After that, the benefits start: you will have enough knowledge and muscle
memory that using the new editor saves you time. Modern text editors are fancy
and powerful tools, so the learning never stops: you'll get even faster as you
learn more. -->
若我們可以遵循上述方法，並使用新編輯器完成所有文書處理工作，學習一個複雜的文字編輯器的時間線大概如此：
在一兩小時之內，學習到基本操作，例如開啟或編輯檔案、儲存與退出、瀏覽暫存區域。
學習二十小時之後，我們可以達到與使用舊編輯器同樣的速度。
在此之後，優勢盡顯：我們已經有了足夠的知識與肌肉記憶，使得我們可以使用新編輯器節省時間。
現代文字編輯器都是奇妙且強大的工具，學習不止，學得越多，效率越高。

<!-- # Which editor to learn? -->
# 應該選擇什麼編輯器？

<!-- Programmers have [strong opinions](https://en.wikipedia.org/wiki/Editor_war)
about their text editors. -->
程式設計師往往對自己的文字編輯器有[很強的執著](https://en.wikipedia.org/wiki/Editor_war)

現今最受歡迎的編輯器是什麼？ 這裡有一份[Stack Overflow 的調查](https://insights.stackoverflow.com/survey/2019/#development-environments-and-tools)
(這個調查可能有偏見，因為Stack Overflow的使用者不能代表所有程式設計師)。
[Visual Studio Code](https://code.visualstudio.com/) 是最受歡迎的編輯器。
[Vim](https://www.vim.org/)則是最受歡迎的命令列編輯器。

## Vim

<!-- All the instructors of this class use Vim as their editor. Vim has a rich
history; it originated from the Vi editor (1976), and it's still being
developed today. Vim has some really neat ideas behind it, and for this reason,
lots of tools support a Vim emulation mode (for example, 1.4 million people
have installed [Vim emulation for VS code](https://github.com/VSCodeVim/Vim)).
Vim is probably worth learning even if you finally end up switching to some
other text editor. -->
此課程的所有講師都使用 Vim 作為編輯器。
Vim 歷史悠久，起源於 Vi 編輯器 (1976)，並且直至今日還在成長。
Vim 有非常簡潔的行事理論，因此，許多工具支援類 Vim 的編輯模式（例如，140萬人安裝了[Vim emulation for VS code](https://github.com/VSCodeVim/Vim)）。
即使你決定使用其他編輯器，Vim依然是值得學習的。

<!-- It's not possible to teach all of Vim's functionality in 50 minutes, so we're
going to focus on explaining the philosophy of Vim, teaching you the basics,
showing you some of the more advanced functionality, and giving you the
resources to master the tool. -->
在 50 分鐘之內教授完Vim的功能是不可能的，所以我們只會專注與介紹Vim的處世哲學，教授一點基礎知識，展示一些高階功能，並為你提供掌握Vim的學習資源。

<!-- # Philosophy of Vim -->
# Vim之哲學

<!-- When programming, you spend most of your time reading/editing, not writing. For
this reason, Vim is a _modal_ editor: it has different modes for inserting text
vs manipulating text. Vim is programmable (with Vimscript and also other
languages like Python), and Vim's interface itself is a programming language:
keystrokes (with mnemonic names) are commands, and these commands are
composable. Vim avoids the use of the mouse, because it's too slow; Vim even
avoids using the arrow keys because it requires too much movement. -->
寫程式時，我們的大部分時間都使用在閱讀/編輯而非寫本身。
因此，Vim是 _模式化_ 編輯器：它具有鍵入文字和處理文字的不同模式。
Vim是可程式化的（利用 Vimscript 以及 Python 等其他語言），並且 Vim 介面自身就是程式語言：
鍵擊（使用助記符）是指令，並且這些指令可以相互組合。
Vim 避免使用滑鼠，因為滑鼠是低效率的；Vim甚至避免使用方向鍵，因為需要太多次移動。

<!-- The end result is an editor that can match the speed at which you think. -->
最終的結果是，使用 Vim 編輯跟得上我們思考的速度。

<!-- # Modal editing -->
# 編輯模態

<!-- Vim's design is based on the idea that a lot of programmer time is spent
reading, navigating, and making small edits, as opposed to writing long streams
of text. For this reason, Vim has multiple operating modes. -->
Vim 設計基於使用者花費大量時間進行閱讀，瀏覽與小修改，
而不是編寫長文字。因此，Vim 擁有多種模式：

<!-- - **Normal**: for moving around a file and making edits
- **Insert**: for inserting text
- **Replace**: for replacing text
- **Visual** (plain, line, or block): for selecting blocks of text
- **Command-line**: for running a command -->
- **標準(Normal)**: 在檔案中移動並更正文字
- **插入(Insert)**: 插入文字
- **替換(Replace)**: 替換文字
- **視覺化(Visual)** (以字元，列， 或文字塊): 選中文字
- **命令列(Command-line)**: 執行指令

<!-- Keystrokes have different meanings in different operating modes. For example,
the letter `x` in Insert mode will just insert a literal character 'x', but in
Normal mode, it will delete the character under the cursor, and in Visual mode,
it will delete the selection. -->
在不同的模式下鍵擊的作用也不同。例如，`x` 在插入模式下會鍵入 'x'，但在標準模式下
會刪除當前游標下的字元，若在可視模式下會刪除選中的文字。

<!-- In its default configuration, Vim shows the current mode in the bottom left.
The initial/default mode is Normal mode. You'll generally spend most of your
time between Normal mode and Insert mode. -->
在預設配置下，Vim會在底部左端顯示當前的模式。
Vim 的預設模式是標準模式。 通常我們會將大部分時間用在標準與插入模式上。

<!-- You change modes by pressing `<ESC>` (the escape key) to switch from any mode
back to Normal mode. From Normal mode, enter Insert mode with `i`, Replace mode
with `R`, Visual mode with `v`, Visual Line mode with `V`, Visual Block mode
with `<C-v>` (Ctrl-V, sometimes also written `^V`), and Command-line mode with
`:`. -->
我們可以按下 `<ESC>` 來從任意模式轉換為標準模式。
在標準模式中，使用 `i` 進入插入模式，使用 `R` 進入替換模式，使用 `v` 進入可視模式，
使用 `V` 進入可視(列)模式，使用 `<C-v>` (Ctrl-V, 有時寫成 `^V`) 來進入可視(塊)模式，
使用 `:` 進入命令列模式。

<!-- You use the `<ESC>` key a lot when using Vim: consider remapping Caps Lock to
Escape ([macOS
instructions](https://vim.fandom.com/wiki/Map_caps_lock_to_escape_in_macOS)). -->
在使用Vim時會市場用到 `<ESC>`: 清考慮將 Caps Lock 重對映至 Escape ([macOS
指引](https://vim.fandom.com/wiki/Map_caps_lock_to_escape_in_macOS)).

<!-- # Basics -->
# 基本

<!-- ## Inserting text -->
## 插入文字

<!-- From Normal mode, press `i` to enter Insert mode. Now, Vim behaves like any
other text editor, until you press `<ESC>` to return to Normal mode. This,
along with the basics explained above, are all you need to start editing files
using Vim (though not particularly efficiently, if you're spending all your
time editing from Insert mode). -->
在標準模式下，按下 `i` 來進入插入模式。
現在 Vim 和許多其他編輯器一樣，直到我們按下 `<ESC>` 來回到標準模式。
只需知道這一點與之前介紹的內容，就足以使用 VIm 來編輯檔案了(雖然只使用插入模式效率不高)。

<!-- ## Buffers, tabs, and windows -->
## 緩存, 標籤頁，視窗

<!-- Vim maintains a set of open files, called "buffers". A Vim session has a number
of tabs, each of which has a number of windows (split panes). Each window shows
a single buffer. Unlike other programs you are familiar with, like web
browsers, there is not a 1-to-1 correspondence between buffers and windows;
windows are merely views. A given buffer may be open in _multiple_ windows,
even within the same tab. This can be quite handy, for example, to view two
different parts of a file at the same time. -->
Vim 會維護一系列打開的檔案，其叫做 "緩存"。
一個 Vim 會話包含許多標籤頁，每個標籤頁持有許多視窗(分割窗格)。
每個視窗顯示一個緩存。
與網頁瀏覽器等其他我們熟悉的程式不一樣的是，緩存與視窗不是一一對應的關係；
視窗是單純的瀏覽介面。一個緩存可以被 _多個_ 視窗所開啟，也可以在同一個標籤頁內開啟。
這個功能很好用，例如在檢視同一個檔案的不同部分的時候。

<!-- By default, Vim opens with a single tab, which contains a single window. -->
預設情況下，Vim 會開啟一個標籤頁，這個標籤頁包含一個視窗。

<!-- ## Command-line -->
## 命令列

<!-- Command mode can be entered by typing `:` in Normal mode. Your cursor will jump
to the command line at the bottom of the screen upon pressing `:`. This mode
has many functionalities, including opening, saving, and closing files, and
[quitting Vim](https://twitter.com/iamdevloper/status/435555976687923200). -->
在標準模式下鍵入 `:` 來進入命令列模式。
此時游標會立即跳至熒幕下方的命令列。
這個模式包含許多功能，如開啟，儲存，關閉檔案，以及[退出 Vim](https://twitter.com/iamdevloper/status/435555976687923200).

<!-- - `:q` quit (close window)
- `:w` save ("write")
- `:wq` save and quit
- `:e {name of file}` open file for editing
- `:ls` show open buffers
- `:help {topic}` open help
    - `:help :w` opens help for the `:w` command
    - `:help w` opens help for the `w` movement -->
- `:q` 退出 (關閉視窗)
- `:w` 儲存 ("寫入")
- `:wq` 儲存後退出
- `:e {檔案名}` 開啟檔案
- `:ls` 顯示現有的緩存
- `:help {topic}` 顯示幫助
    - `:help :w` 顯示關於 `:w` 指令的幫助
    - `:help w` 顯示關於 `w` 移動方式的幫助

<!-- # Vim's interface is a programming language -->
# Vim 的介面是一種程式語言

<!-- The most important idea in Vim is that Vim's interface itself is a programming
language. Keystrokes (with mnemonic names) are commands, and these commands
_compose_. This enables efficient movement and edits, especially once the
commands become muscle memory. -->
Vim 最重要的想法就是 Vim 自身的介面就是一種程式語言。
鍵擊是指令， 這些指令可以 _結合_。
這使得移動與編輯更加高效，尤其是在這些指令成為肌肉記憶的情況下。

<!-- ## Movement -->
## 移動

<!-- You should spend most of your time in Normal mode, using movement commands to
navigate the buffer. Movements in Vim are also called "nouns", because they
refer to chunks of text. -->
通常情況下我們應該在標準模式下使用移動指令來導航緩存。
在 Vim 中移動被稱為 "名詞"，因為這些移動指令參考了文字塊。

<!-- - Basic movement: `hjkl` (left, down, up, right)
- Words: `w` (next word), `b` (beginning of word), `e` (end of word)
- Lines: `0` (beginning of line), `^` (first non-blank character), `$` (end of line)
- Screen: `H` (top of screen), `M` (middle of screen), `L` (bottom of screen)
- Scroll: `Ctrl-u` (up), `Ctrl-d` (down)
- File: `gg` (beginning of file), `G` (end of file)
- Line numbers: `:{number}<CR>` or `{number}G` (line {number})
- Misc: `%` (corresponding item)
- Find: `f{character}`, `t{character}`, `F{character}`, `T{character}`
    - find/to forward/backward {character} on the current line
    - `,` / `;` for navigating matches
- Search: `/{regex}`, `n` / `N` for navigating matches -->
- 基礎移動: `hjkl` (左，下，上，右)
- 詞: `w` (下一詞), `b` (詞首), `e` (詞尾)
- 列: `0` (列首), `^` (第一個非空字元), `$` (列尾)
- 熒幕: `H` (熒幕首列), `M` (中間), `L` (熒幕末尾)
- 滾動: `Ctrl-u` (向上), `Ctrl-d` (向下)
- 檔案: `gg` (檔案頭), `G` (檔案尾)
- 列數: `:{列數}<CR>` or `{列數}G` (列 {列數})
- 雜項: `%` (尋找配對)
- 查找: `f{character}`, `t{character}`, `F{character}`, `T{character}`
    - 在此列中 查到/到 向前/向後查找 {character}
    - `,` / `;` 來導向結果
- 搜尋: `/{regex}`, `n` / `N` 用於匹配導航

<!-- ## Selection -->
## 選擇

視覺化模式:

<!-- - Visual
- Visual Line
- Visual Block -->
- 視覺化
- 視覺化(列)
- 視覺化(塊)

<!-- Can use movement keys to make selection. -->
可以使用移動鍵來選擇

<!-- ## Edits -->
## 編輯

<!-- Everything that you used to do with the mouse, you now do with the keyboard
using editing commands that compose with movement commands. Here's where Vim's
interface starts to look like a programming language. Vim's editing commands
are also called "verbs", because verbs act on nouns. -->
所有我們曾用滑鼠做的事情，現在都可以使用鍵盤上的編輯與移動指令來完成。
從此時起 Vim 的介面開始有些像程式語言了。
Vim 的編輯命令也被稱為 "動詞"， 因為動詞可以操作名詞。

<!-- - `i` enter Insert mode
    - but for manipulating/deleting text, want to use something more than
    backspace
- `o` / `O` insert line below / above
- `d{motion}` delete {motion}
    - e.g. `dw` is delete word, `d$` is delete to end of line, `d0` is delete
    to beginning of line
- `c{motion}` change {motion}
    - e.g. `cw` is change word
    - like `d{motion}` followed by `i`
- `x` delete character (equal do `dl`)
- `s` substitute character (equal to `xi`)
- Visual mode + manipulation
    - select text, `d` to delete it or `c` to change it
- `u` to undo, `<C-r>` to redo
- `y` to copy / "yank" (some other commands like `d` also copy)
- `p` to paste
- Lots more to learn: e.g. `~` flips the case of a character -->
- `i` 進入插入模式
    - 但是對於操作/刪除文字，想使用除了 backspace 的方法完成
- `o` / `O` 在此列前/後插入新列
- `d{motion}` 刪除 {motion}
    - 例如 `dw` 刪除詞, `d$` 刪除至列尾, `d0` 刪除至列首
- `c{motion}` 變更 {motion}
    - 例如 `cw` 更改詞
    - 如同 `d{motion}` 後執行 `i`
- `x` 刪除字元 (與 `dl` 效果相同)
- `s` 替換字元 (與 `xi` 效果相同)
- 視覺化模式搭配操作
    - 選中文字, 使用 `d` 刪除或使用 `c` 更改
- `u` 復原, `<C-r>` 重做
- `y` 複製 / "yank" (有些其他指令如 `d` 也會複製)
- `p` 貼上
- 還有許多其他值得學習的: 例如 `~` 改變字元的大小寫

## Counts

You can combine nouns and verbs with a count, which will perform a given action
a number of times.

- `3w` move 3 words forward
- `5j` move 5 lines down
- `7dw` delete 7 words

## Modifiers

You can use modifiers to change the meaning of a noun. Some modifiers are `i`,
which means "inner" or "inside", and `a`, which means "around".

- `ci(` change the contents inside the current pair of parentheses
- `ci[` change the contents inside the current pair of square brackets
- `da'` delete a single-quoted string, including the surrounding single quotes

# Demo

Here is a broken [fizz buzz](https://en.wikipedia.org/wiki/Fizz_buzz)
implementation:

```python
def fizz_buzz(limit):
    for i in range(limit):
        if i % 3 == 0:
            print('fizz')
        if i % 5 == 0:
            print('fizz')
        if i % 3 and i % 5:
            print(i)

def main():
    fizz_buzz(10)
```

We will fix the following issues:

- Main is never called
- Starts at 0 instead of 1
- Prints "fizz" and "buzz" on separate lines for multiples of 15
- Prints "fizz" for multiples of 5
- Uses a hard-coded argument of 10 instead of taking a command-line argument

{% comment %}
- main is never called
  - `G` end of file
  - `o` open new line below
  - type in "if __name__ ..." thing
- starts at 0 instead of 1
  - search for `/range`
  - `ww` to move forward 2 words
  - `i` to insert text, "1, "
  - `ea` to insert after limit, "+1"
- newline for "fizzbuzz"
  - `jj$i` to insert text at end of line
  - add ", end=''"
  - `jj.` to repeat for second print
  - `jjo` to open line below if
  - add "else: print()"
- fizz fizz
  - `ci'` to change fizz
- command-line argument
  - `ggO` to open above
  - "import sys"
  - `/10`
  - `ci(` to "int(sys.argv[1])"
{% endcomment %}

See the lecture video for the demonstration. Compare how the above changes are
made using Vim to how you might make the same edits using another program.
Notice how very few keystrokes are required in Vim, allowing you to edit at the
speed you think.

# Customizing Vim

Vim is customized through a plain-text configuration file in `~/.vimrc`
(containing Vimscript commands). There are probably lots of basic settings that
you want to turn on.

We are providing a well-documented basic config that you can use as a starting
point. We recommend using this because it fixes some of Vim's quirky default
behavior. **Download our config [here](/2020/files/vimrc) and save it to
`~/.vimrc`.**

Vim is heavily customizable, and it's worth spending time exploring
customization options. You can look at people's dotfiles on GitHub for
inspiration, for example, your instructors' Vim configs
([Anish](https://github.com/anishathalye/dotfiles/blob/master/vimrc),
[Jon](https://github.com/jonhoo/configs/blob/master/editor/.config/nvim/init.vim) (uses [neovim](https://neovim.io/)),
[Jose](https://github.com/JJGO/dotfiles/blob/master/vim/.vimrc)). There are
lots of good blog posts on this topic too. Try not to copy-and-paste people's
full configuration, but read it, understand it, and take what you need.

# Extending Vim

There are tons of plugins for extending Vim. Contrary to outdated advice that
you might find on the internet, you do _not_ need to use a plugin manager for
Vim (since Vim 8.0). Instead, you can use the built-in package management
system. Simply create the directory `~/.vim/pack/vendor/start/`, and put
plugins in there (e.g. via `git clone`).

Here are some of our favorite plugins:

- [ctrlp.vim](https://github.com/ctrlpvim/ctrlp.vim): fuzzy file finder
- [ack.vim](https://github.com/mileszs/ack.vim): code search
- [nerdtree](https://github.com/scrooloose/nerdtree): file explorer
- [vim-easymotion](https://github.com/easymotion/vim-easymotion): magic motions

We're trying to avoid giving an overwhelmingly long list of plugins here. You
can check out the instructors' dotfiles
([Anish](https://github.com/anishathalye/dotfiles),
[Jon](https://github.com/jonhoo/configs),
[Jose](https://github.com/JJGO/dotfiles)) to see what other plugins we use.
Check out [Vim Awesome](https://vimawesome.com/) for more awesome Vim plugins.
There are also tons of blog posts on this topic: just search for "best Vim
plugins".

# Vim-mode in other programs

Many tools support Vim emulation. The quality varies from good to great;
depending on the tool, it may not support the fancier Vim features, but most
cover the basics pretty well.

## Shell

If you're a Bash user, use `set -o vi`. If you use Zsh, `bindkey -v`. For Fish,
`fish_vi_key_bindings`. Additionally, no matter what shell you use, you can
`export EDITOR=vim`. This is the environment variable used to decide which
editor is launched when a program wants to start an editor. For example, `git`
will use this editor for commit messages.

## Readline

Many programs use the [GNU
Readline](https://tiswww.case.edu/php/chet/readline/rltop.html) library for
their command-line interface. Readline supports (basic) Vim emulation too,
which can be enabled by adding the following line to the `~/.inputrc` file:

```
set editing-mode vi
```

With this setting, for example, the Python REPL will support Vim bindings.

## Others

There are even vim keybinding extensions for web
[browsers](http://vim.wikia.com/wiki/Vim_key_bindings_for_web_browsers) - some
popular ones are
[Vimium](https://chrome.google.com/webstore/detail/vimium/dbepggeogbaibhgnhhndojpepiihcmeb?hl=en)
for Google Chrome and [Tridactyl](https://github.com/tridactyl/tridactyl) for
Firefox. You can even get Vim bindings in [Jupyter
notebooks](https://github.com/lambdalisue/jupyter-vim-binding).

# Advanced Vim

Here are a few examples to show you the power of the editor. We can't teach you
all of these kinds of things, but you'll learn them as you go. A good
heuristic: whenever you're using your editor and you think "there must be a
better way of doing this", there probably is: look it up online.

## Search and replace

`:s` (substitute) command ([documentation](http://vim.wikia.com/wiki/Search_and_replace)).

- `%s/foo/bar/g`
    - replace foo with bar globally in file
- `%s/\[.*\](\(.*\))/\1/g`
    - replace named Markdown links with plain URLs

## Multiple windows

- `:sp` / `:vsp` to split windows
- Can have multiple views of the same buffer.

## Macros

- `q{character}` to start recording a macro in register `{character}`
- `q` to stop recording
- `@{character}` replays the macro
- Macro execution stops on error
- `{number}@{character}` executes a macro {number} times
- Macros can be recursive
    - first clear the macro with `q{character}q`
    - record the macro, with `@{character}` to invoke the macro recursively
    (will be a no-op until recording is complete)
- Example: convert xml to json ([file](/2020/files/example-data.xml))
    - Array of objects with keys "name" / "email"
    - Use a Python program?
    - Use sed / regexes
        - `g/people/d`
        - `%s/<person>/{/g`
        - `%s/<name>\(.*\)<\/name>/"name": "\1",/g`
        - ...
    - Vim commands / macros
        - `Gdd`, `ggdd` delete first and last lines
        - Macro to format a single element (register `e`)
            - Go to line with `<name>`
            - `qe^r"f>s": "<ESC>f<C"<ESC>q`
        - Macro to format a person
            - Go to line with `<person>`
            - `qpS{<ESC>j@eA,<ESC>j@ejS},<ESC>q`
        - Macro to format a person and go to the next person
            - Go to line with `<person>`
            - `qq@pjq`
        - Execute macro until end of file
            - `999@q`
        - Manually remove last `,` and add `[` and `]` delimiters

# Resources

- `vimtutor` is a tutorial that comes installed with Vim - if Vim is installed, you should be able to run `vimtutor` from your shell
- [Vim Adventures](https://vim-adventures.com/) is a game to learn Vim
- [Vim Tips Wiki](http://vim.wikia.com/wiki/Vim_Tips_Wiki)
- [Vim Advent Calendar](https://vimways.org/2019/) has various Vim tips
- [Vim Golf](http://www.vimgolf.com/) is [code golf](https://en.wikipedia.org/wiki/Code_golf), but where the programming language is Vim's UI
- [Vi/Vim Stack Exchange](https://vi.stackexchange.com/)
- [Vim Screencasts](http://vimcasts.org/)
- [Practical Vim](https://pragprog.com/book/dnvim2/practical-vim-second-edition) (book)

# Exercises

1. Complete `vimtutor`. Note: it looks best in a
   [80x24](https://en.wikipedia.org/wiki/VT100) (80 columns by 24 lines)
   terminal window.
1. Download our [basic vimrc](/2020/files/vimrc) and save it to `~/.vimrc`. Read
   through the well-commented file (using Vim!), and observe how Vim looks and
   behaves slightly differently with the new config.
1. Install and configure a plugin:
   [ctrlp.vim](https://github.com/ctrlpvim/ctrlp.vim).
   1. Create the plugins directory with `mkdir -p ~/.vim/pack/vendor/start`
   1. Download the plugin: `cd ~/.vim/pack/vendor/start; git clone
      https://github.com/ctrlpvim/ctrlp.vim`
   1. Read the
      [documentation](https://github.com/ctrlpvim/ctrlp.vim/blob/master/readme.md)
      for the plugin. Try using CtrlP to locate a file by navigating to a
      project directory, opening Vim, and using the Vim command-line to start
      `:CtrlP`.
    1. Customize CtrlP by adding
       [configuration](https://github.com/ctrlpvim/ctrlp.vim/blob/master/readme.md#basic-options)
       to your `~/.vimrc` to open CtrlP by pressing Ctrl-P.
1. To practice using Vim, re-do the [Demo](#demo) from lecture on your own
   machine.
1. Use Vim for _all_ your text editing for the next month. Whenever something
   seems inefficient, or when you think "there must be a better way", try
   Googling it, there probably is. If you get stuck, come to office hours or
   send us an email.
1. Configure your other tools to use Vim bindings (see instructions above).
1. Further customize your `~/.vimrc` and install more plugins.
1. (Advanced) Convert XML to JSON ([example file](/2020/files/example-data.xml))
   using Vim macros. Try to do this on your own, but you can look at the
   [macros](#macros) section above if you get stuck.
