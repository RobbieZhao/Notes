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

## Terminal v.s. Bash v.s. shell

 - Terminal is a terminal emulator + a shell program running inside of it. On OS X, the default shell is Bash.

## Other

 - `&&` if the previous command succeeds, execute the next one
 - `echo $?` show the result of the last program
 - `gcc x.c`
 - `gcc -o x x.c`
 - `gcc -Wall -o x x.c` show all warnings

## Vim

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
 - `.` do it again
 - `yy` copy; `p` paste below; `P` paste above
 - `V` visual mode; `d` delete
 - `o` new line below and enter insert mode; `O` new line above and enter insert mode
 - `d` + `}` delete new block
 - `w` move to the next word; `W` go to the next space; `b` go back a word; `B` go back to the last space
 - `:` + `n` go to line n
 - `0` go to start of the line; `^` or `0w` go to the start of the line (not including spaces); `$` go to the end of the line
 - `t + char` move the cursor to in front of the char; `f + char` move the cursor to the char
 - `%` go to the corresponding block sign; `d + %` delete what's between the block signs
 - `esc` cancel the command