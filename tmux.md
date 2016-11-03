#### tmux 
`tmux list-keys`  
`tmux list commands`  

##### shortcuts (after the `CTRL + b` prefix )
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



##### commands 
`tmux ls` show sessions  
`tmux new -s session-name` new session  
`tmux a -t session-name` attach to a session  
`tmux switch -t session_name` switch to that session
`tmux detach`  detach from the session you are in  
`tmux kill-session -t session-name` end session entirely  
`killall tmux` end all sessions  

