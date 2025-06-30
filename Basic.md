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
   - Arithmetic Expressions
   - Numerical expressions can also be calculated and stored in a variable using the syntax `var=$((expression))`
3. How to read user input
