## Shortcuts

 - `ctrl-c` -- cancels the current line and gives you a new shell prompt, usually kills a non-interactive running program
 - `ctrl-d` -- exits most interactive programs (your shell, the debugger, sftp, etc)
 - `ctrl-a` -- jump to the start of the line
 - `ctrl-e` -- jump to the end of the line
 - `option-left/right` -- jump forward/backward 1 word
 - `ctrl-r` --history search. 
 - `ctrl-d` -- forward delete 1 character
 - `ctrl` + mouseclick -- move the cursor
 - `ctrl-u` delete before the cursor
 - `ctrl-k` -- delete the rest of the line
 - `history` -- show all previous commands. `!n` run the nth command
 - `!fi` -- rerun the last command that start with `fi` 
 - `ctrl-l` -- clear the whole screen
 - `cmd-k` -- clear scrollback

## Terminal Commands

### basic
 - `ls -l` the long form of ls
 - `cd ~` go home
 - `cp -r source destination` copy files in source directory into destination directory
 - `rm -r dir` remove a directory
 - `rm -rf dir` force remove a directory 

### find

`find dir` + options: ex: `find . -type f -mmin -10` 

 - type
   - d directories
   - f files
 - name
 - iname case-insensitive
 - mmin 
   - -n modified less than n minutes ago
   - +n modified more than n minutes ago
 - mtime: like mmin but with days
 - size
   - +5G greater than 5GB
   - +5M greater than 5MB
   - +5k greater than 5k
 - empty: find empty files
 - perm
 - exec: run following commands on the results
   - + or \; to end the command
   - {} as placeholder
 - maxdepth: 1 if only searching for current dir

### grep: global regular expression print
 - `grep text file`: search for text in file
 - `grep -w text file` search but with whole word
 - `grep -i` case-insensitive search
 - `grep -n` print out line number
 - `grep -B 4` print out the four lines before
 - `grep -A 4` print out the four lines after
 - `grep -C 2` 2 lines before and 2 lines after
 - `grep text ./*` search for all files in the curr dir
 - `grep -r` search recursively
 - `grep -l text dir` only list which files contain text
 - `grep -lc` count how many matches in each file
 - `history | grep "git commit"` search for history commands that have git commit
 - `grep "regex"` search using POSIX regular expressions

### curl
 - `curl url -o filename` download file from the url and name it as filename

### rsync
 - `rsync srcdir/* destdir/` copy all files from src to dest.
 - `rsync -r srcdir/ destdir/` copy everthing from src to dest.
 - `rsync -v --dry-run srcdir/* destdir` see what files are gonna be copied (v: verbose)
 - `rsync -a`: archive, copy everything and info
 - `rsync --delete` sync and delete files in destination but don't exist in source
 - `rsync -zaP` zip, archive, and show Progress

### crontab: cronos table

 - `crontab -l` show all tasks
 - `crontab -e` edit table
 - timing: 
   - minute (0-59)
   - hour(0-23) 
   - day of month (1-31) 
   - month (1-12)
   - day of week(0-6) (Sunday to Saturday)
   - or could use * to match every value
 - use `,` to have multiple values
 - `*/n` every n mintes, hours, ...
 - `n-m` range
 - `#` comment
 - `crontab -r` remove all tasks
 - `crontab.guru`

### alias
 - `alias name='alias name'`
 - `alias` show all aliases

### sips
 - `sips -Z 640 *.jpg` resize all images into 640 pixels, `-Z` means keeping height-width ratio unchanged
 - `sips -Z 300 *.jpg --out newfolder/` resize and output the files to a new folder 

## .bash_profile & .bashrc
 - `.bash_profile` for a login shell, `.bashrc` for a non-login shell
 - To use the same setup for login shells and non-login shells, put this in the `.bash_profile`:

		if [ -f ~/.bashrc ]; then
		    source ~/.bashrc
		fi

 - `source .bashrc` run bashrc (could also restart the terminal)
 - special characters:
   - `\h` the hostname up to the first .
   - `\n` newline
   - `\s` the name of the shell
   - `\t` the current time in 24-hour format
   - `\u` the username of the current user
   - `\w` the current working directory
   - `\W` the basename of the current working directory 

## Terminal v.s. Bash v.s. shell

 - Terminal is a terminal emulator + a shell program running inside of it. On OS X, the default shell is Bash.

## Other

 - `&&` if the previous command succeeds, execute the next one
 - `echo $?` show the result of the last program
 - `gcc x.c`
 - `gcc -o x x.c`
 - `gcc -Wall -o x x.c` show all warnings

## Vim

Modes
 - command mode
 - insert mode
 - visual mode

Commands

 - `:`+ `q` quit
 - `:` + `wq` save and quit
 - `:` + `q` + `!` quit and not save
 - `: + w` save and not quit
 - `dd` delete a line; u undo it; `ctrl + r`: redo
 - `G` go down to last line
 - `gg` go up to first line
 - `{` up one block; `}` down one block
 - `h` left; `l` right; `j` down; `k` up
 - `number + h/l/j/k/{/}` do something # times
 - `.` redo the last command
 - `yy` copy; `p` paste below; `P` paste above
 - `V` visual mode; `d` delete
 - `o` new line below and enter insert mode; `O` new line above and enter insert mode
 - `d` + `}` delete new block
 - `w` move to the next word; `W` go to the next space; `b` go back a word; `B` go back to the last space
 - `:` + `n` go to line n
 - `0` go to start of the line; `^` or `0w` go to the start of the line (not including spaces); `$` go to the end of the line
 - `t + char` move the cursor to in front of the char; `f + char` move the cursor to the char; `;` to the next instance
 - `%` go to the corresponding block sign; `d + %` delete what's between the block signs
 - `esc` cancel the command
 - `cw` (c stands for changing) delete word and enter insert mode
 - `dw` delete word
 - `D` delete rest of the line; `C` delete rest of the line and enter insert mode
 - `c + t + char` delete to char and enter insert mode
 - `d + t + char` delete to char
 - `*` go to the next occurrence of the word
 - `zz` center the cursor
 - `i` insert mode; `a` insert mode and move cursor to the right; `A` move to the end of the line
 - `x` delete the current char
 - `~` swap the case
 - `r + char` replace the current letter with char
 - `vv` indent a line of code; under visual mode, `v` indent selected lines of code
 - `q` + `char` start recording macros; `q` stop recording; @CHAR replay the macro
 - `>` indent code
 - `<` left indent code
 - `ctrl + v` select columns of chars
 - `ctrl + v` + `I` + type something + `esc` insert something in front of all lines
 - `/text` search for text; `n` go next; `N` go back

## Emacs

 - C-x, C-c ends the session
 - C-v move forward one screen
 - M-v move backward one screen
 - C-l center the cursor
 - C-b back; C-f forward; C-p previous line; C-n next line
 - M-f forward a word; M-b back a word
 - C-a beginning of line, C-e end of line; M-a begin of sentence, M-e end of sentence
 - M-< beginning of file; M-> end of file
 - C-u n command: do the command n times
 - C-g stop a command
 - C-x 1 delete all other screens
 - C-d delete next char
 - M-del kill the word before; M-d kill next word
 - C-k kill to end of line
 - M-k kill to end of sentence
 - C-space + move cursor + C-w kills text in between
 - C-y paste
 - M-y previous paste history
 - C-/ or C-_ or C-x u undo; C-g C-/ redo
 - C-x C-f open the file
 - C-x C-s save the file; C-x s save all files that need to be saved
 - C-x C-b see a list of opened files
 - C-x b buffername open the buffer
 - C-z exit emacs temporarily; fg to return to the session
 - M-x recover-this-file recover a file
 - M-x text-mode/fundamental-mode/auto-fill-mode switch to mode
 - C-h m see documentation on the current mode
 - Can only have one major mode, but multiple minor mode
 - C-x f n set the margin to be n characters
 - M-q refill the paragraph (with Auto Fill mode on)
 - C-s search, do it again to go to next one; enter exit to search; C-r reverse search
 - C-x 2 split the window into 2; C-M-v scroll the bottom window; C-x o move the cursor to the other window
 - C-x 4 C-f open another file in another window and move the cursor there
 - C-x 5 2 open a new frame; C-x 5 0 remove the selected frame













