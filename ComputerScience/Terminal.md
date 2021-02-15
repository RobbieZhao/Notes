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
 - 

 
 
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
 - `r + char` replace the current letter with t
 - `vv` indent a line of code; under visual mode, `v` indent selected lines of code
 - `q` + `char` start recording macros; `q` stop recording; @CHAR replay the macro
 - `>` indent code
 - `<` left indent code
 - `ctrl + v` select columns of chars
 - `ctrl + v` + `I` + type something + `esc` insert something in front of all lines
 - `/text` search for text; `n` go next; `N` go back
 - 