# Practical .bashrc examples
1. Aliases are custom shortcuts for longer commands. The syntax is `alias name='command'`.

```bash
# Human-readable ls with all files and sizes
alias ll='ls -lha'
```
```bash
# A more visual and helpful grep
alias grep='grep --color=auto'
```
```bash
# Shortcut to clear the terminal
alias c='clear'
```
```bash
# Constantly updating and upgrading your system? (For Debian/Ubuntu)
alias update='sudo apt update && sudo apt upgrade -y'
```
```bash
# Get your public IP address
alias myip='curl ifconfig.me; echo'
```

