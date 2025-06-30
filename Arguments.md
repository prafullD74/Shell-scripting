# Command-line arguments

>Command-line arguments are parameters that are passed to a script while executing them in the bash shell. They are also known as positional parameters in Linux.
### How Shell Scripts Understand Command Line Arguments
- Command-line arguments help make shell scripts interactive for the users.
- They help a script identify the data it needs to operate on.
- The bash shell has special variables reserved to point to the arguments which we pass through a shell script. Bash saves these variables numerically ($1, $2, $3, … $n).
- Here, the first command-line argument in our shell script is $1, the second $2 and the third is $3. This goes on till the 9th argument. The variable $0 stores the name of the script or the command itself.
- The special character `$#` stores the total number of arguments. We also have `$@` and `$*` as wildcard characters which are used to denote all the arguments. We use `$$` to find the process ID of the current shell script, while `$?` can be used to print the exit code for our script.

### special variables are also to be noted while handling command-line arguments.
| Special Variable | Special Variable's details |
|---|---|
| `$1 ... $n` | Positional argument indicating from 1 .. n. If the argument is like 10, 11 onwards, it has to be indicated as ${10},${11 |
| `$0` | This is not taken into the argument list as this indicates the "name" of the shell program. In the above example, **$0 is "displayPositionalArgument.sh"** |
| `$@` | Values of the arguments that are passed in the program. This will be much helpful if we are not sure about the number of arguments that got passed. |
| `$#` | Total number of arguments and it is a good approach for loop concepts. |
| `$*` | In order to get all the arguments as double-quoted, we can follow this way |
| `$$` | To know about the process id of the current shell |
| `$?` and `$!` | Exit status id and Process id of the last command |


`find . -type f -name "*.sh"` helps to locate files based on certain patterns.


```bash
#! /bin/bash
pwd

# Check if at least one argument is provided
if [ -z "$1" ]; then
    echo "Usage: ./your_script_name.sh <username1> [username2]"
    exit 1
fi

user1="$1" # First argument
user2="$2" # Second argument (optional, if you want to compare against a second specific user)

echo "User entered as argument 1: $user1"
if [ -n "$2" ]; then # Check if a second argument was provided
    echo "User entered as argument 2: $user2"
fi

# Compare the first argument with "vaibhav" or "prafull"
if [[ "$user1" == "vaibhav" || "$user1" == "prafull" ]]; then
    echo "$user1 is correct"
else
    echo "$user1 is incorrect"
fi

# You could also compare the first argument against the second argument provided
# if that's what you meant by "comparing with two names as arguments".
# For example:
# if [[ "$user1" == "$user2" ]]; then
#     echo "The first argument ($user1) matches the second argument ($user2)."
# elif [ -n "$2" ]; then # Only show if second argument exists and doesn't match
#     echo "The first argument ($user1) does not match the second argument ($user2)."
# fi
```

In shell scripting, particularly within `if` conditions using `[ ]` or `[[ ]]`, `-z` and `-n` are **string test operators** used to check if a string is empty or not empty, respectively.

**1. `-z string` (Zero length)**

**2. `-n string` (Non-zero length)**

### String Operators | Shell Script
| Symbol | operator | Use | Syntax |
|---|---|---|---|
| `=` | Equal | used to check whether two strings are equal | `if [ $str1 = $str2 ]` |
| `!=` | Not Equal | used when both operands are not equal | `if [ $str1 != $str2 ]` |
| `\<` | Less than | used to check operand1 is less than operand2 | `if [ $str1 \< $str2 ]` |
| `\>` | Greater than | used to check the operand1 is greater than operand2 | `if [ $str1 \> $str2 ]` |
| `-n` | Check string length greater than 0 | used to check the string is not empty | `if [ -n $str ]` |
| `-z` | Check string length equal to 0 | used to check the string is empty | `if [ -z $str ]` |
| `=~` | Pattern Matching | Checks if a string matches a regular expression pattern | `if [[ "$string" =~ pattern ]]` |
