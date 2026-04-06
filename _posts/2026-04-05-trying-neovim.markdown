---
   layout: post
   title: "Trying out Neovim as a VScode user"
   date:   2026-04-05 20:34:41 +0800
   categories: others
   tags: neovim
---

Disclaimer: This article is partially written with Neovim

> Recently I started switching to neovim, because I find that vscode is using too much memory (though found out later that it is the python language server that taking up too much memory)

## VSCode Vim mode

First I used the easiest approach, [VSCodeVim](https://github.com/vscodevim/vim), it was simple to set up, supports system clipboard, and comes with useful plugins like smart line number. Then I discovered the awful undo bug: when the vim undo key `u` is pressed, it will arbitrarily delete several more edit actions compare to `Ctrl-Z` on vscode, and the best fix is to disable the vim undo command, and use the good old `Ctrl-Z` instead ([issue#2007](https://github.com/VSCodeVim/Vim/issues/2007))!

Somehow, it feels very weird mixing vscode shortcuts and vim keys, so I tried [VSCode Neovim](https://github.com/vscode-neovim/vscode-neovim) next, a bit more work to set up, actual neovim install is required, and you need to be careful about plugin conflicts, but mostly trouble-free thanks to [https://docs.astronvim.com/recipes/vscode/](https://docs.astronvim.com/recipes/vscode/). But there are also some small glitches: [neovim output sometimes takes over the terminal panel](https://stackoverflow.com/questions/78611905/turn-off-neovim-messages-in-vscode), some artifact characters on screen, and not working well with multiple cursor (there's a [plugin](https://github.com/vscode-neovim/vscode-multi-cursor.nvim) for that, but not perfect). The final straw for me was that the neovim redo key (`Ctrl-R`) conflicts with vscode's open recent folder hotkey, both of which are very often used and I don't want to assign another key combo to either function.

## Neovim

Finally, I decided to switch my entire workflow away from vscode and try neovim for good. The first obstacle is to find a good terminal emulator for it, which doesn't have much of a choice if you work on a Windows machine like me.

#### Wezterm

Wez's Terminal is usually the first recommended option, however it's now currently on hold as the author is busy with real-life work.

#### Alacritty

Fast, low ram usage, and aesthetically pleasing. But there is a critical bug if you have more than one monitor ([issue#8634](https://github.com/alacritty/alacritty/issues/8634)).

#### Neovide

Just like Alacritty, it's fast, but also suffers from the same window resizing bug, as they both use the same rust window manager library.

#### Windows Terminal

Needs to set up a new profile to avoid messing with the system default terminal, and personally it feels more clunky and visually unappealing than other third-party terminal apps. But on the plus side, it has native multiple panes/tabs support.

Currently I use both Alacritty and Windows Terminal, depends on which one is most easy to open from current project location

After the terminal is settled, I gave it a go, opened a pandas project, the second problem appears, some dataframe is not being recognized as the correct type, error everywhere and no autocompletion. First I thought it was something wrong with the python environment, after some digging, the good news: neovim can auto detect python venv based on the terminal venv from whence you launched nvim, but it means the bug is in pyright/basedpyright LSP, which are more diffcult to tinker. Luckily, after more searching, I found this [question](https://vi.stackexchange.com/questions/38347/pyright-lsp-flagging-errors-in-class-using-pandas-method) and installed pandas-stubs:

> The stubs are tested with mypy and pyright and are currently shipped with the Visual Studio Code extension pylance.

Lol, guess I have to thank neovim for this learning opportunity, never knew that pandas require this extra package as vscode takes care of everything for you.

### My experience
Here is my thought after using neovim for serious development for a day:

The vim shortcut is really powerful for code editing/browsing, though I still need some time to master it, and the simple UI offers less distraction than vscode, good for concentrating your mind on code. Plus, the looking of it feels way cooler than vscode!

But on the down side, there are several features that I miss from vscode:

#### Debugger

Yes I know there are debuggers for neovim, but it just feels clunky and goes against the spirit of not making neovim into a vscode clone.

#### Terminal support/Multi-cursor

I know there is tmux/Zellij for window managing and neovim shortcut for editing multiple instances, but I am now too lazy to learn and adopt them.

#### Data Viewing

Yes there are alternatives to jupyter and data wrangler for neovim, but same as above, I don't have time to look into them, and these plugins seem less well maintained than their vscode counterparts. 

#### Remote

For most part it worked like a charm, just ssh into the remote server and start neovim, until you need to copy/paste to the SSH terminal from your system..

Gotta credit Neovide for the out-of-box support for system clipboard integration in remote mode. For Windows Terminal and Alacritty, you have to copy with `Ctrl-C`/`Ctrl-Shift-C` after select the text holding `Shift` key to override neovim selection mode, and can only paste text when in insert mode, which means no "+ registers for you in remote.

## Final verdict

For me, neovim is a handy tool for quick editing or writing small scripts. Stick to vscode for anything involves data processing, debugger, etc..
