# INTRODUCTION

`praful@Swarajay:/$` - When a shell is used interactively, it displays a $ when it is waiting for a command from the user.
`root@Swarajay:/#` - If shell is running as root, the prompt is changed to #.

### What is a Bash Script?
>A bash script is a series of commands written in a file. These are read and executed by the bash program. The program executes line by line. By naming conventions, bash scripts end with a .sh. However, bash scripts can run perfectly fine without the sh extension.

### Scripts start with a bash bang.
- `#! /bin/bash` Scripts are also identified with a shebang. Shebang is a combination of bash `#` and bang `!` followed the the bash shell path.
- Executable scripts appear in a different colour from rest of the files and folders. Scripts have execution rights for the user executing them.
- `chmod u+x file.sh` modifies the existing rights of a file for a particular user and provide execution rights to user.

### The Basic Syntax of Bash Scripting
1. How to define variables
   - define a variable by using the syntax `variable_name=value`
   - To get the value of the variable, add `$` before the variable
   - [Arithmetic Expressions](#arithmetic-expressions) For decimal calculations, we can use `bc` command to get the output to a particular number of decimal places. `bc` (Bash Calculator) is a command line calculator that supports calculation up to a certain number of decimal points.
   - Numerical expressions can also be calculated and stored in a variable using the syntax `var=$((expression))`
   - `echo "scale=2;22/7" | bc` > `scale` defines the number of decimal places required in the output
2. How to read user input
   - When need to gather user input and perform relevant operations, we can take user input using the `read` command.
   - `read -p "Enter your age" variable_name` To prompt the user with a custom message, use the `-p` flag.
4. E

#### Arithmetic Expressions
| Operator  | Usage  |
|---|---|
| +  | addition  |
| -  | subtraction  |
| *  | multiplication  |
| /  | division  |
| **  | exponentiation  |
| %  | modulus  |
