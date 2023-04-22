# Basic Vim

Vim seems complicated and it is. The goal is to make things move a
little easier for the user. If you can learn the tricks of the trade.
Vim becomes something special.

💡 With the `!` command you can run Cli commands inside of Vim. Using this
we can avoid writing filters. Use something like `Rust` of `Golang`
instead.

I don't like neovim🤬. It's not going to help me with hacking.

* [vim](https://lite.duckduckgo.com/lite?kd=-1&kp=-1&q=vim)
* [rust](https://lite.duckduckgo.com/lite?kd=-1&kp=-1&q=rust)
* [golang](https://lite.duckduckgo.com/lite?kd=-1&kp=-1&q=golang)


## Basic Vim Commands

These commands are the ones required to use and save the files.

* `:e [file]` - Opens a file, where `[file]` is the name of the file you
  want opened.
* `:w` - Saves the file you are working on.
* `:w [file]` - Saves the file to a file name were `[file]`
* `:wq` - Save your file and close Vim
* `:q!` - Quit without saving

## Movement Commands

When you use vim the goal is to use the keyboard efficiently. How can we
do this? Using the keys to navigate around. Without moving your hands
around to arrow keys.

* `h` - moves cursor to the left
* `l` - moves cursor to the right
* `j` - moves cursor down one line
* `k` move cursor up one line
* `H` - put cursor at the top of the screen
* `M` - put cursor in the middle of the screen
* `L` -put cursor at the bottom of the screen
* `w` - put cursor at the start of the next word
* `b` - put cursor at the start of the previous word
* `e` - put cursor at the end of a word
* `0` - place cursor at the beginning of a line
* `$` - place cursor at the end of a line
* `)` - start of the next sentence
* `(` - start of the previous sentence
* `{` - start next paragraph or block
* `}` - start previous paragraph or block
* `Ctrl + f` - one page forward
* `Ctrl + b` - one page back
* `gg` - start of file
* `G` - end of file

## Editing Commands

* `yank` - copy
* `put` - paste
* `y` - yank
* `p` - put
* `dd` - delete single line
* `yy` - copies a single line

💬 You can paste anything copied. If it is highlighted or copied via `yy`.
With movement commands you can add the number of times to complete that
task. For example, `5yy` copies 5 lines. 

* `yy` - copies a line
* `yw` - copies a word
* `y$` - copies from where cursor s to the end of a line
* `v` - highlight one character at a time using arrow buttons of the
  h,k,j,l buttons
* `V` - Highlights one line, and movement keys can allow you to
  highlight additional lines
* `p` - paste what is copied
* `d` - deletes highlighted text
* `dd` - deletes line of text
* `dw` - deletes a word
* `D` - deletes everything from where cursor is to the end of the
  line
* `d0` - deletes everything from where cursor is to the beginning
  of the line
* `dgg` - deletes everything from where cursor is to the beginning of the
  file
* `dG` - deletes everything from where cursor is to the end of the file
* `x` - deletes a single character
* `u` - undo last operation. `I do not understand this` u# allows you to undo multiple actions
* `Ctrl + r` - redo last undo
* `.` - repeats the last action

## Searching Text Commands

💬 Using Vim you can search your text, find and replace text within your
document. If you opt to replace multiple instances of the same keyword
or phrase, you can set Vim up to require or not require you to confirm
each replacement depending on how you put in the command.

* `/[keyword]` - searches for text in the document where keyword is
  whatever keyword, phrase or string of characters you're looking for.
* `?[keyword]` - searches previous text for your keyword, phrase or
  character string
* `n` - searches your text again in whatever direction you last search
  was
* `N` - searches your text again in the opposite direction
* `:%s/[pattern]/[replacement]/g` - replaces all occurrences of a
  pattern without confirming each one
* `:%s/[pattern]/[replacement]/gc` - replaces all occurrences of a
  pattern and confirms each one.

## Working With Multiple Files

💬 You can also edit more than one text file at a time. Vim gives
you the ability to either split your screen to show more than one file
at a time, or you can switch back and forth between documents. Document
=== buffers.

* `:bn` - switch to next buffer
* `:bp` - switch to previous buffer
* `:bd` - close a buffer
* `:sp [filename]` - opens new file and splits your screen horizontally
  to show more than one buffer
* `:vsp [filename]` - opens a new file and splits your screen vertically
  to show more than one buffer
* `:ls` - list all open buffers
* `Ctrl + ws` - split window horizontally
* `Ctrl + wv` - split window vertically
* `Ctrl + ww` - switch between windows
* `Ctrl + wq` - quit a window
* `Ctrl + wh` - moves cursor to the window to the left
* `Ctrl + wl` - moves cursor to the window to the right
* `Ctrl + wj` - moves cursor to the window below the current window
* `Ctrl + wk` - move cursor to the window above the one you are in

## Marking Text In Visual Mode

Visual mode allows you to select a block of text in Vim. Once the block
of text is selected. You can use visual commands to perform actions on
the selected text. Such as deleting it, copying it, etc.

* `v` - starts visual mode. You can select a range of text and run a
  command.
* `V` - starts line select visual mode.
* `Ctrl + v` - starts visual block mode. selects columns
* `Esc` - exit visual mode

💬 Once you have selected a range of text. You can now run command on that
text.

* `d` - delete marked text
* `y` - yank/copy marked text
* `>` - shift text right
* `<` shift text left

## Tab Pages

You can use tabs inside Vim. You can work on multiple files without
having to close and save.

* `:tabedit [file]` - opens new tab and will take you to edit [file]
* `gt` - move to next tab
* `gT` - move to previous tab
* `#gt` - move to a specific tab number
* `:tabs` - list all open tabs
* `:tabclose` - close single tab

## Sample Vim Workflow Example

* Open a new or existing file with `vim [filename]`
* Type `i` to switch into `insert` mode so that you can start editing
  the file
* Enter or modify the text in your file
* Once you are done. Press the escape key `Esc` to get out of insert
  mode and back to command mode
* Type `:wq` to save and exit your file

