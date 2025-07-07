# Functions
In shell scripting, functions are blocks of code that can be reused multiple times within a script or across different scripts. Functions are defined with a name, a set of parameters (optional), and a block of code that performs some operation. The code inside the function can access and modify variables within the function or outside the function, depending on their scope.

### Strategies for writing modular and reusable functions
1. **Write functions that perform a single, well-defined task**: A function should do one thing, and do it well. This makes the functions more focused and easier to understand and reuse.
2. **Avoid hardcoding values**: Use function arguments to pass in values that may vary, such as file names or directory paths. This makes the function more flexible and reusable.
3. **Return values instead of printing them**: Functions should return values, rather than printing them to the console. This allows the calling code to decide how to use the function’s output, making the function more flexible and reusable.
4. **Write well-documented functions**: Document your functions with clear and concise comments that explain what the functions do, what their arguments are, and what their return value is.
5. **Logically organize your functions**: Group related functions together in your script, and organize them in a way that makes sense for the tasks you are performing.

### Using function libraries in shell scripts
1. **Create a function library file**: Create a separate file that contains the functions you want to reuse. This file should contain only function definitions and no code that runs outside of a function.
2. **Source the function library file**: In each script that uses the function library, including the line ‘source /path/to/function_library.sh’ at the beginning of the script. This will load the functions from the library file into the script.
3. **Source the function library file**: In each script that uses the function library, including the line ‘source /path/to/function_library.sh’ at the beginning of the script. This will load the functions from the library file into the script.

- create and use a function library file

### Error handling in functions
>Error handling is an important part of writing functions in shell scripts. Good error-handling practices can help make your functions more reliable and robust and can make your code easier to debug.
1. Return a status code to indicate success or failure. When your function completes, it should return a status code.
2. Use the `set -e` option to exit on errors.
3. Use the `trap` command to handle errors gracefully.
4. Print error messages to the console.
5. Validate function arguments.
6. Use descriptive variables names

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
