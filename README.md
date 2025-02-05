# Kite Python Plugin for Vim/Neovim

[![Report an issue](https://img.shields.io/badge/-Report%20an%20issue-critical)](https://github.com/kiteco/issue-tracker/issues)

Kite is an AI-powered programming assistant that helps you write Python code inside Vim. Kite helps you write code faster by showing you the right information at the right time. Learn more about how Kite helps you while you're using Vim at https://kite.com/integrations/vim/.

At a high level, Kite provides you with:
* 🧠 __[Line-of-Code Completions](#Line-of-Code-Completions)__ powered by machine learning models trained on the entire open source code universe
* 📝 __[Intelligent Snippets](#Intelligent-Snippets)__ that automatically provide context-relevant code snippets for your function calls
* 🔍 __[Instant documentation](#Kite-Copilot-for-Python-Documentation)__ for the symbol underneath your cursor so you save time searching for Python docs


## Requirements

* macOS 10.10+ or Windows 7+ or Linux (Ubuntu, Debian, Fedora, Arch Linux, Linux Mint, openSUSE, KDE, XFCE, Gnome 2, Gnome 3)
* Vim 8 or Neovim
* [Kite Engine](https://kite.com/)

Use another editor? Check out [Kite’s other editor integrations](https://kite.com/integrations/).


## Installation

### Installing the Kite Engine

The [Kite Engine](https://kite.com/) needs to be installed and running on your computer in order for the package to work properly. The package itself provides the frontend that interfaces with the Kite Engine, which performs all the code analysis and machine learning 100% locally on your computer (no code is sent to a cloud server).

__macOS Instructions__
1. Download the [installer](https://kite.com/download/) and open the downloaded `.dmg` file.
2. Drag the Kite icon into the `Applications` folder.
3. Run `Kite.app` to start the Kite Engine.

__Windows Instructions__
1. Download the [installer](https://kite.com/download/) and run the downloaded `.exe` file.
2. The installer should run the Kite Engine automatically after installation is complete.

__Linux Instructions__
1. Visit https://kite.com/linux/ to learn how to install Kite.
2. The installer should run the Kite Engine automatically after installation is complete.

### Installing the Kite plugin for Vim/Neovim

When running the Kite Engine for the first time, you'll be guided through a setup process which will allow you to install the Vim/Neovim plugin. You can also install or uninstall the Vim plugin at any time using the Kite Engine's [plugin manager](https://help.kite.com/article/62-managing-editor-plugins).

Alternatively, you can follow the instructions in the [DEVELOPMENT.md](https://github.com/kiteco/vim-plugin/blob/master/DEVELOPMENT.md) file to learn how to manually install the Vim/Neovim plugin.

Once installed, the plugin will be automatically updated by Kite when necessary.

### Configuring supported languages

Kite supports 12 languages and counting.  By default only Python is enabled.  You can configure the languages for which Kite is enabled:

```viml
" Python, JavaScript, Go
let g:kite_supported_languages = ['python', 'javascript', 'go']

" All the languages Kite supports
let g:kite_supported_languages = ['*']

" Turn off Kite
let g:kite_supported_languages = []
```

[Learn more about why Kite is the best autocomplete for Vim.](https://kite.com/integrations/vim/)


## Features

Kite's Vim/Neovim plugin provides a number of features to help you code better and faster.


### Line-of-Code Completions

Kite's ranked completions are integrated with Vim's insert-mode completion, specifically the user-defined completion.  Kite shows normal completions or signature-completions as appropriate for the cursor position.

By default Kite's completions will show up automatically as you type.  You can opt out via:

```viml
let g:kite_auto_complete=0
```

You can manually invoke the completions in insert mode with `<C-X><C-U>`.  See `:h i_CTRL-X_CTRL-U` for details.

You can disable Kite's completions altogether with this in your vimrc:

```viml
let g:kite_completions=0
```

Kite's completions include snippets by default.  To opt out of the snippets, add this to your vimrc:

```viml
let g:kite_snippets=0
```

Normally you insert the currently selected completion option with `<C-y>`.  If you'd like to use `<Tab>` instead / as well, add this to your vimrc:

```viml
let g:kite_tab_complete=1
```

For any kind of completion you must set 'completopt' as follows:

```viml
set completeopt+=menuone
```

For automatic completion, you also need either:

```viml
set completeopt+=noselect
```

or:

```viml
set completeopt+=noinsert
```

To see documentation in the preview window for each completion option, copy all the lines above into your vimrc and change the preview line to:

```viml
set completeopt+=preview
```

To have the preview window automatically closed once a completion has been inserted:

```viml
autocmd CompleteDone * if !pumvisible() | pclose | endif
```

We also recommend:

```viml
set belloff+=ctrlg  " if vim beeps during completion
```


### Intelligent Snippets

Some completions are actually autogenerated code snippets which can be filled in.  These will be highlighted with the Underline highlight group.

You can navigate between placeholders with `<CTRL-J>` (forward) and `<CTRL-K>` (backward), even after you have typed over the original placeholder text.

To change these keys:

```viml
let g:kite_previous_placeholder = '<C-H>'
let g:kite_next_placeholder = '<C-L>`
```


### Signatures

Kite can show how other people used the signature you are using.  By default this is off to save space.

To turn it on: `:KiteShowPopularPatterns`.

To turn it off: `:KiteHidePopularPatterns`.


### Kite Copilot for Python Documentation

As you edit your code, the [Kite Copilot](https://kite.com/copilot/) will automatically show examples and docs for the code under your cursor.

Alternatively, you can press `K` when the cursor is on a symbol to view its documentation in Kite Copilot.

If you have mapped `K` already, the plugin won't overwrite your mapping. You can set an alternative mapping, e.g. to `gK`, like this:

```viml
nmap <silent> <buffer> gK <Plug>(kite-docs)
```

By default you need to type `K` (or whatever you have mapped to `<Plug>(kite-docs)`) each time you want to see documentation for the keyword under the cursor.  To have the documentation continually update itself as you move from keyword to keyword:

```viml
let g:kite_documentation_continual=1
```


### Goto Definition

Use `<C-]>` or `:KiteGotoDefinition` to jump to a method's definition.


### Commands

- `KiteFindRelatedCodeFromFile` - search for code related to the current file in the Copilot.
- `KiteFindRelatedCodeFromLine` - search for code related to the current line in the Copilot.
- `KiteDocsAtCursor` - show documentation for the keyword under the cursor in the Copilot.
- `KiteOpenCopilot` - open the Kite Copilot and focus on it.
- `KiteGeneralSettings` - open Kite's settings in the Copilot.
- `KitePermissions` - open Kite's permission settings in the Copilot.
- `KiteTutorial` - show a tutorial for using Kite with Vim.
- `KiteEnableAutoStart` - start Kite automatically when Vim starts.
- `KiteDisableAutoStart` - do not start Kite automatically when Vim starts.
- `KiteGotoDefinition` - jump to a method's definition.



### Statusline

Add `%{kite#statusline()}` to your statusline to get an indicator of what Kite is doing.  If you don't have a status line, this one matches the default when `&ruler` is set:

```viml
set statusline=%<%f\ %h%m%r%{kite#statusline()}%=%-14.(%l,%c%V%)\ %P
set laststatus=2  " always display the status line
```


### Debugging

Use `let g:kite_log=1` to switch on logging.  Logs are written to `kite-vim.log` in Vim's current working directory.


---

#### About Kite

Kite is built by a team in San Francisco devoted to making programming easier and more enjoyable for all. Follow Kite on
[Twitter](https://twitter.com/kitehq) and get the latest news and programming tips on the
[Kite Blog](https://kite.com/blog/).
Kite has been featured in [Wired](https://www.wired.com/2016/04/kites-coding-asssitant-spots-errors-finds-better-open-source/),
[VentureBeat](https://venturebeat.com/2019/01/28/kite-raises-17-million-for-its-ai-powered-developer-environment/),
[The Next Web](https://thenextweb.com/dd/2016/04/14/kite-plugin/), and
[TechCrunch](https://techcrunch.com/2019/01/28/kite-raises-17m-for-its-ai-driven-code-completion-tool/).
