---
   layout: post
   title:  "Trying neovim as a vscode user"
   date:   2026-04-05 20:34:41 +0800
   categories: others
   tags: neovim
---

> Recently I started switching to neovim, because I find that vscode is using too much memory (though found out later that it is the python language server that taking up too much memory)

First I used the easiest approach, [VSCodeVim](https://github.com/vscodevim/vim), it was simple to set up, supports system clipboard, and comes with useful plugins like smart line number. Then I discovered the awful undo bug, when the vim undo key `u` is pressed, it will arbitrarily delete several more edit actions compare to `Ctrl-Z` on vscode, and the best fix is to disable the vim undo, and use `Ctrl-Z` instead ([issue#2007](https://github.com/VSCodeVim/Vim/issues/2007))!

Somehow, it feels very weird mixing vscode shortcut and vim key, so I tried [VSCode Neovim](https://github.com/vscode-neovim/vscode-neovim) next, a bit more work to set up, actual neovim install is required, and you need to be careful about plugin conflicts, but mostly trouble-free thanks to [https://docs.astronvim.com/recipes/vscode/](https://docs.astronvim.com/recipes/vscode/).
