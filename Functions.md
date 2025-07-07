# Functions
In shell scripting, functions are blocks of code that can be reused multiple times within a script or across different scripts. Functions are defined with a name, a set of parameters (optional), and a block of code that performs some operation. The code inside the function can access and modify variables within the function or outside the function, depending on their scope.



### [How to create and enter a directory](https://www.digitalocean.com/community/tutorials/bashrc-file-in-linux#practical-bashrc-examples)
```bash
# Creates a directory and immediately enters it
mkcd ()
{
    mkdir -p -- "$1" && cd -P -- "$1"
}
```
- `mkdir -p -- "$1"`: Creates the directory. $1 represents the first argument you pass to the function (the directory name).
- The `-p` flag ensures it creates parent directories if needed. If `documents` and `projects` don't exist, `mkdir -p /home/user/documents/projects/new_project` creates them all at once.
- `&&`: This is a logical AND. The cd command will only run if the `mkdir` command was successful.
- `cd -P -- "$1"`: Changes into the newly created directory. `cd -L` (logical path) and `cd -P` (physical path).

### How to extract any archive (extract)?
```bash
# Universal extract function
extract ()
{
    if [ -f "$1" ] ; then
        case "$1" in
            *.tar.bz2)   tar xvjf "$1"    ;;
            *.tar.gz)    tar xvzf "$1"    ;;
            *.bz2)       bunzip2 "$1"     ;;
            *.rar)       unrar x "$1"     ;;
            *.gz)        gunzip "$1"      ;;
            *.tar)       tar xvf "$1"     ;;
            *.tbz2)      tar xvjf "$1"    ;;
            *.tgz)       tar xvzf "$1"    ;;
            *.zip)       unzip "$1"       ;;
            *.Z)         uncompress "$1"  ;;
            *)           echo "'$1' cannot be extracted via extract()" ;;
        esac
    else
        echo "'$1' is not a valid file"
    fi
}
```

### How to better shell history control?
```bash
# --- History Control ---
export HISTSIZE=10000
export HISTFILESIZE=10000

# Ignore duplicate commands in history
export HISTCONTROL=ignoredups
```
- HISTSIZE: The number of commands kept in memory during a session.
- HISTFILESIZE: The number of commands saved to the history file (~/.bash_history) when you exit.

### How to set environment variables and the $PATH
```bash
# --- Environment Variables ---
export EDITOR='nano'  # Set nano as the default text editor

# Add a custom scripts directory to your PATH
export PATH="$HOME/bin:$PATH"
```
### How to customize your Bash prompt (PS1)?
```bash
# --- Custom Prompt (PS1) ---

# Function to parse git branch
parse_git_branch() {
    git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/ (\1)/'
}

# The prompt settings
export PS1="\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[0;31m\]\$(parse_git_branch)\[\033[00m\]\$ "
```
- `\u`: Your username
- `\h`: The hostname
- `\w`: The full path to the current directory
- `\[\033[...m\]`: These are color codes.
- `\$(parse_git_branch)`: This calls our function to get the current Git branch.
