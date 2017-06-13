# quickstart / quick reference  

## help
`tmux list-keys`  
`tmux list commands`  

## shortcuts (after the `CTRL + b` prefix )  

Shortcut|result
--------|------
 |`tmux "windows"`
`d` | detach
`c` | new window
`0-9` | window 0 to 9 based on index
`,` | rename a window
 | `tmux "panes"`
`"` | two vertical panes
`%` | horizontal panes
`{` or `}` | swap panes

# panes  
`^b` `x` kill current pane  

# sessions
`tmux ls` show sessions  
`tmux new -s session-name` new session  
`tmux a -t session-name` attach to a session  
`tmux switch -t session_name` switch to that session -- or `CTRL+b, s, <n>` for a menu of sessions.
`tmux detach`  detach from the session you are in  

`tmux rename-session -t old_name new_name`  
OR  
`tmux rename-session new_name` if you are in a session and wish to rename that session.  
OR
`Ctrl + B, $` and type new name
OR
`Ctrl + B, :` and use either of the first two invocations.

`tmux kill-session -t session-name` end session entirely  
`killall tmux` end all sessions  

## view, search stdout and copy and paste  
`[` enter copy mode to view, find and copy what is of interest  
`]` paste most recent buffer of text  

`:setw -g mode-keys vi` to set bindings to vim  
`/` to search forward  
`?` to search backward  

# sources
`man tmux`  
https://robots.thoughtbot.com/a-tmux-crash-course
http://www.dayid.org/comp/tm.html
