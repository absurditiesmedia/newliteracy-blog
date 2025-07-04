---
publishDate: "01 July 2025"
title: CLI pager commands - more, less, and most 
description: pager commands allow navigation through large text files or data streams.
excerpt: These **PAGER** commands allow you to navigate through file and data stream content with a variety of useful commands.
tags: ["cli", "linux"]

---

These **PAGER** commands allow you to navigate through file and data stream content with a variety of useful commands. If you need to manually visually navigate through a lot of text or data, you'll find yourself using one of these commands. 
They can be used to open files like so:
```
less ./filename.txt
```

or they can handle piped data like this:

```
history 1 | most 
```

or this

```
tail -f /some/log/file | grep "searchtext"  | more
```


## More 
More is the original pager program. It is very basic. And unfortunately it doesn't really have any advantages over the other pager programs other than it is most likely to be available on the simplest *nix systems. So, you should at least be aware that it exists, and like the the others, you can access its help screen by pressing `h`

### HISTORY
(from the manpage `man more`) The more command appeared in 3.0BSD (Released 1979). This man page documents more version 5.19 (Berkeley 6/29/1988), which is currently in use in the Linux community. Documentation was produced using several other versions of the man page, and extensive inspection of the source code.

In other words, this is *ancient* software. The most recent version of **more** was relased in 1988. 37 years ago 2025. 

```
Most commands optionally preceded by integer argument k.  Defaults in brackets.
Star (*) indicates argument becomes new default.
-------------------------------------------------------------------------------
<space>                 Display next k lines of text [current screen size]
z                       Display next k lines of text [current screen size]*
<return>                Display next k lines of text [1]*
d or ctrl-D             Scroll k lines [current scroll size, initially 11]*
q or Q or <interrupt>   Exit from more
s                       Skip forward k lines of text [1]
f                       Skip forward k screenfuls of text [1]
b or ctrl-B             Skip backwards k screenfuls of text [1]
'                       Go to place where previous search started
=                       Display current line number
/<regular expression>   Search for kth occurrence of regular expression [1]
n                       Search for kth occurrence of last r.e [1]
!<cmd> or :!<cmd>       Execute <cmd> in a subshell
v                       Start up '/usr/bin/vim' at current line
ctrl-L                  Redraw screen
:n                      Go to kth next file [1]
:p                      Go to kth previous file [1]
:f                      Display current file name and line number
.                       Repeat previous command
-------------------------------------------------------------------------------
```


## Less 

Less is probably the most sophisticated of the pagers. It provides the following unique functionality:

1. Searching across multiple files. 
2. Piping content within a specified range to external shell commands. 
3. Filtering lines by search pattern. 
4. Subpattern matching. 
5. Finding matching brackets/parentheses. 
6. Saving input to a file


```
                   SUMMARY OF LESS COMMANDS

      Commands marked with * may be preceded by a number, N.
      Notes in parentheses indicate the behavior if N is given.
      A key preceded by a caret indicates the Ctrl key; thus ^K is ctrl-K.

  h  H                 Display this help.
  q  :q  Q  :Q  ZZ     Exit.
 ---------------------------------------------------------------------------

                           MOVING

  e  ^E  j  ^N  CR  *  Forward  one line   (or N lines).
  y  ^Y  k  ^K  ^P  *  Backward one line   (or N lines).
  f  ^F  ^V  SPACE  *  Forward  one window (or N lines).
  b  ^B  ESC-v      *  Backward one window (or N lines).
  z                 *  Forward  one window (and set window to N).
  w                 *  Backward one window (and set window to N).
  ESC-SPACE         *  Forward  one window, but don't stop at end-of-file.
  d  ^D             *  Forward  one half-window (and set half-window to N).
  u  ^U             *  Backward one half-window (and set half-window to N).
  ESC-)  RightArrow *  Right one half screen width (or N positions).
  ESC-(  LeftArrow  *  Left  one half screen width (or N positions).
  ESC-}  ^RightArrow   Right to last column displayed.
  ESC-{  ^LeftArrow    Left  to first column.
  F                    Forward forever; like "tail -f".
  ESC-F                Like F but stop when search pattern is found.
  r  ^R  ^L            Repaint screen.
  R                    Repaint screen, discarding buffered input.
        ---------------------------------------------------
        Default "window" is the screen height.
        Default "half-window" is half of the screen height.
 ---------------------------------------------------------------------------

                          SEARCHING

  /pattern          *  Search forward for (N-th) matching line.
  ?pattern          *  Search backward for (N-th) matching line.
  n                 *  Repeat previous search (for N-th occurrence).
  N                 *  Repeat previous search in reverse direction.
  ESC-n             *  Repeat previous search, spanning files.
  ^O^N  ^On         *  Search forward for (N-th) OSC8 hyperlink.
  ^O^P  ^Op         *  Search backward for (N-th) OSC8 hyperlink.
  ^O^L  ^Ol            Jump to the currently selected OSC8 hyperlink.
  ESC-u                Undo (toggle) search highlighting.
  ESC-U                Clear search highlighting.
  &pattern          *  Display only matching lines.
        ---------------------------------------------------
        A search pattern may begin with one or more of:
        ^N or !  Search for NON-matching lines.
        ^E or *  Search multiple files (pass thru END OF FILE).
        ^F or @  Start search at FIRST file (for /) or last file (for ?).
        ^K       Highlight matches, but don't move (KEEP position).
        ^R       Don't use REGULAR EXPRESSIONS.
        ^S n     Search for match in n-th parenthesized subpattern.
        ^W       WRAP search if no match found.
        ^L       Enter next character literally into pattern.
 ---------------------------------------------------------------------------

                           JUMPING

  g  <  ESC-<       *  Go to first line in file (or line N).
  G  >  ESC->       *  Go to last line in file (or line N).
  p  %              *  Go to beginning of file (or N percent into file).
  t                 *  Go to the (N-th) next tag.
  T                 *  Go to the (N-th) previous tag.
  {  (  [           *  Find close bracket } ) ].
  }  )  ]           *  Find open bracket { ( [.
  ESC-^F <c1> <c2>  *  Find close bracket <c2>.
  ESC-^B <c1> <c2>  *  Find open bracket <c1>.
        ---------------------------------------------------
        Each "find close bracket" command goes forward to the close bracket 
          matching the (N-th) open bracket in the top line.
        Each "find open bracket" command goes backward to the open bracket 
          matching the (N-th) close bracket in the bottom line.

  m<letter>            Mark the current top line with <letter>.
  M<letter>            Mark the current bottom line with <letter>.
  '<letter>            Go to a previously marked position.
  ''                   Go to the previous position.
  ^X^X                 Same as '.        
  ESC-m<letter>        Clear a mark.
  ---------------------------------------------------
        A mark is any upper-case or lower-case letter.
        Certain marks are predefined:
             ^  means  beginning of the file
             $  means  end of the file
 ---------------------------------------------------------------------------

                        CHANGING FILES

  :e [file]            Examine a new file.
  ^X^V                 Same as :e.
  :n                *  Examine the (N-th) next file from the command line.
  :p                *  Examine the (N-th) previous file from the command line.
  :x                *  Examine the first (or N-th) file from the command line.
  ^O^O                 Open the currently selected OSC8 hyperlink.
  :d                   Delete the current file from the command line list.
  =  ^G  :f            Print current file name.
 ---------------------------------------------------------------------------

                    MISCELLANEOUS COMMANDS

  -<flag>              Toggle a command line option [see OPTIONS below].
  --<name>             Toggle a command line option, by name.
  _<flag>              Display the setting of a command line option.
  __<name>             Display the setting of an option, by name.
  +cmd                 Execute the less cmd each time a new file is examined.

  !command             Execute the shell command with $SHELL.
  #command             Execute the shell command, expanded like a prompt.
  |Xcommand            Pipe file between current pos & mark X to shell command.
  s file               Save input to a file.
  v                    Edit the current file with $VISUAL or $EDITOR.
  V                    Print version number of "less".
 ---------------------------------------------------------------------------

                           OPTIONS

        Most options may be changed either on the command line,
        or from within less by using the - or -- command.

        Options may be given in one of two forms: either a single
        character preceded by a -, or a name preceded by --.

  -?  ........  --help
                  Display help (from command line).
  -a  ........  --search-skip-screen
                  Search skips current screen.
  -A  ........  --SEARCH-SKIP-SCREEN
                  Search starts just after target line.
  -b [N]  ....  --buffers=[N]
                  Number of buffers.
  -B  ........  --auto-buffers
                  Don't automatically allocate buffers for pipes.
  -c  -C  ....  --clear-screen --CLEAR-SCREEN
                  Repaint by clearing rather than scrolling.
  -d  ........  --dumb
                  Dumb terminal.
  -D xcolor  .  --color=xcolor
                  Set screen colors.
  -e  -E  ....  --quit-at-eof  --QUIT-AT-EOF
                  Quit at end of file.
  -f  ........  --force
                  Force open non-regular files.
  -F  ........  --quit-if-one-screen
                  Quit if entire file fits on first screen.
  -g  ........  --hilite-search
                  Highlight only last match for searches.
  -G  ........  --HILITE-SEARCH
                  Don't highlight any matches for searches.
  --old-bot
                  Revert to the old bottom of screen behavior.
  -h [N]  ....  --max-back-scroll=[N]
                  Backward scroll limit.
  -i  ........  --ignore-case
                  Ignore case in searches that do not contain uppercase.
  -I  ........  --IGNORE-CASE
                  Ignore case in all searches.
  -j [N]  ....  --jump-target=[N]

                  Screen position of target lines.
  -J  ........  --status-column
                  Display a status column at left edge of screen.
  -k file  ...  --lesskey-file=file
                  Use a compiled lesskey file.
  -K  ........  --quit-on-intr
                  Exit less in response to ctrl-C.
  -L  ........  --no-lessopen
                  Ignore the LESSOPEN environment variable.
  -m  -M  ....  --long-prompt  --LONG-PROMPT
                  Set prompt style.
  -n .........  --line-numbers
                  Suppress line numbers in prompts and messages.
  -N .........  --LINE-NUMBERS
                  Display line number at start of each line.
  -o [file] ..  --log-file=[file]
                  Copy to log file (standard input only).
  -O [file] ..  --LOG-FILE=[file]
                  Copy to log file (unconditionally overwrite).
  -p pattern .  --pattern=[pattern]
                  Start at pattern (from command line).
  -P [prompt]   --prompt=[prompt]
                  Define new prompt.
  -q  -Q  ....  --quiet  --QUIET  --silent --SILENT
                  Quiet the terminal bell.
  -r  -R  ....  --raw-control-chars  --RAW-CONTROL-CHARS
                  Output "raw" control characters.
  -s  ........  --squeeze-blank-lines
                  Squeeze multiple blank lines.
  -S  ........  --chop-long-lines
                  Chop (truncate) long lines rather than wrapping.
  -t tag  ....  --tag=[tag]
                  Find a tag.
  -T [tagsfile] --tag-file=[tagsfile]
                  Use an alternate tags file.
  -u  -U  ....  --underline-special  --UNDERLINE-SPECIAL
                  Change handling of backspaces, tabs and carriage returns.
  -V  ........  --version
                  Display the version number of "less".
  -w  ........  --hilite-unread
                  Highlight first new line after any forward movement.
  -x [N[,...]]  --tabs=[N[,...]]
                  Set tab stops.
  -X  ........  --no-init
                  Don't use termcap init/deinit strings.
  -y [N]  ....  --max-forw-scroll=[N]
                  Forward scroll limit.
  -z [N]  ....  --window=[N]
                  Set size of window.
  -" [c[c]]  .  --quotes=[c[c]]
                  Set shell quote characters.
  -~  ........  --tilde
                  Don't display tildes after end of file.
  -# [N]  ....  --shift=[N]
                  Set horizontal scroll amount (0 = one half screen width).

                --exit-follow-on-close
                  Exit F command on a pipe when writer closes pipe.
                --file-size
                  Automatically determine the size of the input file.
                --follow-name
                  The F command changes files if the input file is renamed.
                --header=[L[,C[,N]]]
                  Use L lines (starting at line N) and C columns as headers.
                --incsearch
                  Search file as each pattern character is typed in.
                --intr=[C]
                  Use C instead of ^X to interrupt a read.
                --lesskey-context=text
                  Use lesskey source file contents.
                --lesskey-src=file
                  Use a lesskey source file.
                --line-num-width=[N]
                  Set the width of the -N line number field to N characters.
                --match-shift=[N]
                  Show at least N characters to the left of a search match.
                --modelines=[N]
                  Read N lines from the input file and look for vim modelines.
                --mouse
                  Enable mouse input.
                 --no-keypad
                  Don't send termcap keypad init/deinit strings.
                --no-histdups
                  Remove duplicates from command history.
                --no-number-headers
                  Don't give line numbers to header lines.
                --no-search-header-lines
                  Searches do not include header lines.
                --no-search-header-columns
                  Searches do not include header columns.
                --no-search-headers
                  Searches do not include header lines or columns.
                --no-vbell
                  Disable the terminal's visual bell.
                --redraw-on-quit
                  Redraw final screen when quitting.
                --rscroll=[C]
                  Set the character used to mark truncated lines.
                --save-marks
                  Retain marks across invocations of less.
                --search-options=[EFKNRW-]
                  Set default options for every search.
                --show-preproc-errors
                  Display a message if preprocessor exits with an error status.
                --proc-backspace
                  Process backspaces for bold/underline.
                --PROC-BACKSPACE
                  Treat backspaces as control characters.
                --proc-return
                  Delete carriage returns before newline.
                --PROC-RETURN
                  Treat carriage returns as control characters.
                --proc-tab
                  Expand tabs to spaces.
                --PROC-TAB
                  Treat tabs as control characters.
                --status-col-width=[N]
                  Set the width of the -J status column to N characters.
                --status-line
                --use-backslash
                  Subsequent options use backslash as escape char.
                --use-color
                  Enables colored text.
                --wheel-lines=[N]
                  Each click of the mouse wheel moves N lines.
                --wordwrap
                  Wrap lines at spaces.


 ---------------------------------------------------------------------------

                 Highlight or color the entire line containing a mark.
                                       LINE EDITING

        These keys can be used to edit text being entered 
        on the "command line" at the bottom of the screen.

 RightArrow ..................... ESC-l ... Move cursor right one character.
 LeftArrow ...................... ESC-h ... Move cursor left one character.
 ctrl-RightArrow  ESC-RightArrow  ESC-w ... Move cursor right one word.
 ctrl-LeftArrow   ESC-LeftArrow   ESC-b ... Move cursor left one word.
 HOME ........................... ESC-0 ... Move cursor to start of line.
 END ............................ ESC-$ ... Move cursor to end of line.
 BACKSPACE ................................ Delete char to left of cursor.
 DELETE ......................... ESC-x ... Delete char under cursor.
 ctrl-BACKSPACE   ESC-BACKSPACE ........... Delete word to left of cursor.
 ctrl-DELETE .... ESC-DELETE .... ESC-X ... Delete word under cursor.
 ctrl-U ......... ESC (MS-DOS only) ....... Delete entire line.
 UpArrow ........................ ESC-k ... Retrieve previous command line.
 DownArrow ...................... ESC-j ... Retrieve next command line.
 TAB ...................................... Complete filename & cycle.
 SHIFT-TAB ...................... ESC-TAB   Complete filename & reverse cycle.
 ctrl-L ................................... Complete filename, list all.
```
  
  
## Most
Most is simpler than **less** but it has some interesting functions that make it unique and useful is certain situations. 

Unique features of **most**:
1. Window splitting 
2. Binary (hex) view. 

Most will search by regular expression, and can read compressed data in `gz` and `bzip2` formats. 

```
  Quitting:

  Q                      Quit MOST.
  :N,:n                  Quit this file and view next.
                            (Use UP/DOWN arrow keys to select next file.)

Movement:

  SPACE, D              *Scroll down one Screen.
  U, BACKSPACE          *Scroll Up one screen.
  RETURN, DOWN          *Move Down one line.
  UP                    *Move Up one line.
  T                      Goto Top of File.
  B                      Goto Bottom of file.
  > , TAB                Scroll Window right
  <                      Scroll Window left
  RIGHT                  Scroll Window left by 1 column
  LEFT                   Scroll Window right by 1 column
  J, G                   Goto line.
  %                      Goto percent.

Window Commands:

  Ctrl-X 2, Ctrl-W 2     Split window.
  Ctrl-X 1, Ctrl-W 1     Make only one window.
  O, Ctrl-X O            Move to other window.
  Ctrl-X 0               Delete Window.

Searching:

  S, f, /               *Search forward
  ?                     *Search Backward
  N                     *Find next in current search direction.

Miscellaneous:

  W                      Toggle width between 80 and 132 char mode.
  Ctrl-X Ctrl-F          Read a file from disk
  R, Ctrl-R              Redraw Screen.
  F                      Simulate tail -f mode
  :o                     Toggle options:  b-binary, w-wrap, t-tab
  E                      Edit file.  Uses MOST_EDITOR and EDITOR
```

## Moar

[Moar project page on Github](https://github.com/walles/moar)

Moar is very similar to more and most in that it has a limited set of commands. You may still want to add **moar** to your system because it features one thing that **more**, **less**, and **most** do not. Syntax highlighting. 

The key sequence to access the help screen is apparently undocumented, at least `h` alone doesn't work on my system. If pressing `h` doesn't bring up the help screen, try pressing the sequence `h`->`v`->`ESC`. It was by pure luck that I managed to discover this.  

Similar to less, moar is capable of:
1. Reading from compressed data in the following formats `.gz`, `.bz2`, `.xz`, `.zst`, and `.zstd`
2. Setting multiple marks by using a letter to differentiate them
3. Search by regular expression 
4. Open the viewed file in the editor set to EDITOR environment variable

Unique functionality provided by **moar**:
1. Syntax Highlighting
2. Mouse Support 


```
Welcome to Moar, the nice pager!

Miscellaneous
-------------
* Press 'q' or 'ESC' to quit
* Press 'w' to toggle wrapping of long lines
* Press '=' to toggle showing the status bar at the bottom
* Press 'v' to edit the file in your favorite editor

Moving around
-------------
* Arrow keys
* Alt key plus left / right arrow steps one column at a time
* Left / right can be used to hide / show line numbers
* Home and End for start / end of the document
* 'g' for going to a specific line number
* 'm' sets a mark, you will be asked for a letter to label it with
* ' (single quote) jumps to the mark
* CTRL-p moves to the previous line
* CTRL-n moves to the next line
* PageUp / 'b' and PageDown / 'f'
* SPACE moves down a page
* < / 'gg' to go to the start of the document
* > / 'G' to go to the end of the document
* Half page 'u'p / 'd'own, or CTRL-u / CTRL-d
* RETURN moves down one line

Filtering
-------* Search is case sensitive if it contains any UPPER CASE CHARACTERS
* Search is interpreted as a regexp if it is a valid one

Reporting bugs
--------------
File issues at https://github.com/walles/moar/issues, or post
questions to johan.walles@gmail.com.

Installing Moar as your default pager
-------------------------------------
Put the following line in your ~/.bashrc, ~/.bash_profile or ~/.zshrc:
  export PAGER=moar

Source Code
-----------
Available at https://github.com/walles/moar/.
--
Type '&' to start filtering, then type your filter expression.

While filtering, arrow keys, PageUp, PageDown, Home and End work as usual.

Press 'ESC' or RETURN to exit filtering mode.

Searching
---------
* Type / to start searching, then type what you want to find
* Type ? to search backwards, then type what you want to find
* Type RETURN to stop searching, or ESC to skip back to where the search started
* Find next by typing 'n' (for "next")
* Find previous by typing SHIFT-N or 'p' (for "previous")
```
