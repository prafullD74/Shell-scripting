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
