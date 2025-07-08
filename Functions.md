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

### Basic Structure of a Function
```bash
function_name(){
    // body of the function
}
```
## This script finds and prints prime numbers within a given range
```bash
#!/bin/bash

# --- Get input from the user ---
read -p "Enter the starting number (Left-End): " start_num
read -p "Enter the ending number (Right-End): " end_num

# --- Function to check if a number is prime ---
check_if_prime() {
    local num_to_check=$1 # Store the argument in a more readable variable

    # Numbers less than 2 are not prime
    if [ "$num_to_check" -lt 2 ]; then
        return # Exit the function
    fi

    # Count divisors (excluding 1 and itself)
    divisor_count=0
    for (( i=2; i*i <= num_to_check; i++ )); do # Optimization: check up to sqrt(num)
        if (( num_to_check % i == 0 )); then
            divisor_count=$(( divisor_count + 1 ))
            break # Found a divisor, no need to check further, it's not prime
        fi
    done

    # If no divisors were found, it's prime
    if [ "$divisor_count" -eq 0 ]; then
        printf "%d " "$num_to_check" # Print the prime number
    fi
}

# --- Main part of the script ---
echo -e "\nPrime Numbers between $start_num and $end_num are:" # -e to enable \n

# Loop through the range and check each number
for (( current_num=start_num; current_num <= end_num; current_num++ )); do
    check_if_prime "$current_num"
done

echo "" # Add a final newline for clean output
```
- `read -p`: Combines the `echo -n` and `read` commands into one, making the input part more compact.
- `echo -e`: Used to easily include newline characters (\n).
- `echo -n`: Prevents echo from adding a newline character at the end, so the cursor stays on the same line as the prompt.
- `start_num`: The variable where the user's input will be stored.
- `$1` refers to the first argument passed to the function when it's called.
- `if [ "$num_to_check" -lt 2 ]; then return` : Prime numbers are defined as numbers greater than 1. So, if the number is 0, 1, or negative, it's not prime, and the function immediately exits (return) without doing further checks.
- `return`: If the number is less than 2, the function immediately exits, meaning no further checks are needed, and nothing is printed.
- `for (( i=2; i*i <= num_to_check; i++ )); do ... done`:
     - `i*i <= num_to_check`: This is the key optimization! If a number N has a divisor d greater than its square root (sqrt(N)), then it must also have a divisor N/d that is less than its square root. So, we only need to check for divisors up to the square root of the number. This significantly speeds up the primality test for larger numbers.
     - `i++`: Increments i by 1 in each iteration.
     - `break` immediately exits the for loop.
- `printf "%d " "$num_to_check"` : Prints the prime number followed by a space.
- `\n`: Prints a newline character, so the output starts on a fresh line.
- Explination
    * **`current_num = 4`:**

      * `check_if_prime 4` is called.
      * Inside `check_if_prime`: `num_to_check` is 4.
      * `if [ "4" -lt 2 ]` is FALSE.
      * `divisor_count = 0`.
      * `for (( i=2; i*i <= 4; i++ ))` (i.e., `for (( i=2; 4 <= 4; i++ ))`) - Loop starts.
          * **Iteration `i=2`**:
              * `if (( 4 % 2 == 0 ))` (i.e., `if (( 0 == 0 ))`) is TRUE.
              * `divisor_count=$(( 0 + 1 ))` so `divisor_count` becomes `1`.
              * `break` is executed. The loop terminates immediately.
      * `if [ "1" -eq 0 ]` is FALSE. Nothing is printed.
    * **`current_num = 5`:**

      * `check_if_prime 5` is called.
      * Inside `check_if_prime`: `num_to_check` is 5.
      * `if [ "5" -lt 2 ]` is FALSE.
      * `divisor_count = 0`.
      * `for (( i=2; i*i <= 5; i++ ))` (i.e., `for (( i=2; 4 <= 5; i++ ))`) - Loop runs.
          * **Iteration `i=2`**:
              * `if (( 5 % 2 == 0 ))` (i.e., `if (( 1 == 0 ))`) is FALSE.
          * Loop condition `i*i <= 5` will be `9 <= 5` next iteration, which is FALSE. Loop ends.
      * `if [ "0" -eq 0 ]` is TRUE.
      * `printf "%d " "5"` prints: ` 5  `
### Types of Functions
1. The functions that return a value to the caller.
2. The functions that terminate the shell using the 'exit' keyword.
3. The functions that alter the value of a variable or variables.
4. The functions that echo output to the standard output.

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
