# Shell-scripting
Shell scripts are widely used to automate repetitive tasks, such as backups, log file processing, system administration routines, and more. Shell scripts can be used to manage and configure operating system settings, start or stop services, and perform file management tasks.

1. **Terminal**: The terminal serves as the interface, appearing as a window on the screen where commands are typed and output is viewed.
2. **Shell**: The shell is a program that interprets and executes commands typed into the terminal. It translates human-readable commands into instructions the operating system's kernel can understand and execute.
3. **Bash**: Bash (Bourne Again Shell) is a specific type of shell frequently used in Unix-like operating systems, such as Linux and macOS.

### [What is a .bashrc file?](https://www.digitalocean.com/community/tutorials/bashrc-file-in-linux)
- The .bashrc file is a shell script that the Bash shell runs whenever it is started interactively. In simple terms, every time you open a new terminal window, Bash reads and executes the commands within this file.
- **Interactive login shell**: (e.g., connecting via SSH) Bash looks for `/etc/profile` first, then searches for `~/.bash_profile`, `~/.bash_login`, and `~/.profile` in that order. It only reads and executes the first one it finds.
- **nteractive non-login shell**: (e.g., opening a new terminal window on your desktop) Bash reads and executes `~/.bashrc`. This is the most common scenario for desktop users.
- Crucially, most distributions’ `~/.bash_profile` or `~/.profile` files contain a small script that explicitly checks for and runs `~/.bashrc`. This ensures that your `.bashrc` settings are loaded even in a login shell, unifying your environment.

| File Name | Scope | When It’s Executed | Common Use Cases |
|---|---|---|---|
| `/etc/bash.bashrc` | System-wide | For every user’s interactive, non-login shell | Set default aliases and functions for all users on the system. |
| `~/.bashrc` | User-specific | For a user’s interactive, non-login shells | The main file for personal aliases, functions, and prompt customizations. |
| `~/.bash_profile` | User-specific | For a user’s login shell | Set environment variables and run commands that only need to happen once per session. |
| `~/.profile` | User-specific | Fallback for `~/.bash_profile` | A more generic version that can be used by other shells, not just Bash. |

For your day-to-day terminal customizations like aliases and prompt settings, `~/.bashrc` is the correct file to edit. To view the file, use `ls -a` in your home directory `/home/user` to see all the hidden files.
```bash
praful@Swarajay:~$ ls -altr
total 84
drwxr-xr-x  3 root   root    4096 Dec 23  2024 ..
-rw-r--r--  1 praful praful   807 Dec 23  2024 .profile
-rw-r--r--  1 praful praful  3771 Dec 23  2024 .bashrc
-rw-r--r--  1 praful praful   220 Dec 23  2024 .bash_logout
```

### How to safely edit .bashrc?
Before you make any changes, you must create a backup.
```bash
cp ~/.bashrc ~/.bashrc.bak
```
Once edits are saved, you must reload the configuration using the `source` command for changes to take effect.
```bash
source ~/.bashrc
```
