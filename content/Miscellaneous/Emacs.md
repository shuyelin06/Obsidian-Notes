---
title: Emacs
tags:
- work-in-progress
---

Emacs is one of many popular UNIX text editors.

To run emacs, use commands `emacs`, which will open `emacs` in its own graphical window.  

```bash
emacs [file-name]
```
> Running emacs with no arguments will open a blank session.

Use option `-nw` to run emacs in the terminal, and use option `--reverse-video` to run emacs in dark mode.

# Basic Emacs Commands
Emacs supports a wide variety of commands, which can be highly useful!

Unlike other text editors, emac uses **modeless editing** - there is no command mode! Rather, to run a command, we need to first specify it by using a special key, either **control** ($C$) or **escape** ($M$).
> The escape key is denoted $M$, as in emacs it is known as the "meta" key.

Basic emacs commands are given below.

## Saving and Quitting Programs
To **save an emacs program**, enter `C-x C-s`.

To **quit emacs**, enter `C-x C-c`.
> When running an emacs session and updating a file, emacs will save a backup of the file to `[filename]~` (may vary depending on configuration)

## Cursor Movement
The basic cursor commands for emacs are given as follows:
- `C-f` / $\rightarrow$ : Move forward one character
- `C-b` / $\leftarrow$: Move backward one character
- `C-p` / $\uparrow$: Move up one line
- `C-n` / $\downarrow$: Move down one line

> Note that if emacs is open in its own graphical window, we can move the cursor by simply clicking where we want our cursor to go.

For convenience, we can also move to the beginning and end of text blocks in the file:
- `M-<`: Move to the beginning of the file
- `M->`: Move to the end of the file
- `C-a`: Move to the beginning of the current line
- `C-e`: move to the end of the current line

To jump to a specific line number, run `M-g-g` and enter in a line number.

## Editing Text
To add text in emacs, simply type in a (non-special) character for it to appear after the current cursor location.

To delete text, we have a variety of commands:
- `C-h` (Backspace): Delete character to the left of cursor
- `C-d`: Delete character to the right of cursor
- `C-k`: Delete character to the end of the line

To select a block of text, we can set a mark using `C-@` or `C-SPACE`, and then move the cursor as normal. This will select the region between the mark and our cursor.
We can then perform commands on this selected region of text:
- `M-w`: Copy a region
- `C-w`: Cut a region
- `C-y`: Paste from clipboard
- `M-C-\`: Auto-indent the region

> It may be useful to change the copy and paste commands to the standard `C-c`, `C-v`, `C-z`.
> To do this, add `cua-mode` to the end of the emacs configuration file `~/.emacs`.

To perform an incremental search for a token, we can use `C-s`. In incremental search mode, we have the following commands:
- `C-s`: Search for next occurrence
- `C-g`: Exit search, and return to original position
- `RETURN`: Exit search, leaving cursor at current position.

## Window Management
Emacs supports multiple windows at once, where each can contain different files to be edited.

Some basic window management commands are given below:
- `C-x 2`: Open a new window
- `C-x C-f`: Read / load a new file into the current window
- `C-x o`: Move to another window

If we want to remove all other windows, we can run command `C-x 1`.