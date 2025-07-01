# INTRODUCTION

- `praful@Swarajay:/$` - When a shell is used interactively, it displays a $ when it is waiting for a command from the user.
- `root@Swarajay:/#` - If shell is running as root, the prompt is changed to #.

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
3. [Numeric Comparison logical operators](#logical-operators) : Comparison is used to check if statements evaluate to `true` or `false`. 
4. Conditional Statements (Decision Making)
   - `if...then...fi` statements
   - `if...then...else...fi` statements
   - `if..elif..else..fi`
   - `if..then..else..if..then..fi..fi..` (Nested Conditionals)
   - To create meaningful comparisons, we can use AND `-a` and OR `-o` as well.
5. Looping and skipping
   - For loops allow you to execute statements a specific number of times.
   - While loops check for a condition and loop until the condition remains `true`. We need to provide a counter statement that increments the counter to control loop execution.
6. How to execute commands with back ticks
   - var=`df -h | grep tmpfs` to include the output of a complex command in your script, you can write the statement inside back ticks.
7. How to get arguments for scripts from the command line
   - It is possible to give arguments to the script on execution. `$@` represents the position of the parameters, starting from one.
8. How to Automate Scripts by Scheduling via cron Jobs
   - Cron is a job scheduling utility, can schedule jobs to execute daily, weekly, monthly or in a specific time of the day. Automation in Linux heavily relies on cron jobs.
   - [crontab guru](https://crontab.guru/)
   - `crontab -l` lists the already scheduled scripts for a particular user.

#### Arithmetic Expressions
| Operator  | Usage  |
|---|---|
| +  | addition  |
| -  | subtraction  |
| *  | multiplication  |
| /  | division  |
| **  | exponentiation  |
| %  | modulus  |

#### Logical operators
| Operation  | Syntax  | Explanation  |
|---|---|---|
| Equality  | num1 -eq num2  | is num1 equal to num2  |
| Greater than equal to  | num1 -ge num2  | is num1 greater than equal to num2  |
| Greater than  | num1 -gt num2  | is num1 greater than num2  |
| Less than equal to  | num1 -le num2  | is num1 less than equal to num2  |
| Less than  | num1 -lt num2  | is num1 less than num2  |
| Not Equal to  | num1 -ne num2  | is num1 not equal to num2  |

---
# [Arrays in Shell Scripts](https://www.digitalocean.com/community/tutorials/arrays-in-shell-scripts)
>Variables store single data elements. Arrays, on the other hand, can store a virtually unlimited number of data elements.
- **Indexed Arrays**: Store elements with an index starting from 0.
- **Associative Arrays**: Store elements in key-value pairs

### Accessing Array Elements Individually
```bash
assoc_array[element1]="Hello World"
```
```bash
echo ${assoc_array[element1]}
```
```bash
index_array=(1 2 3 4 5 6)
```
```bash
echo ${index_array[0]}
```
```bash
#!/bin/bash
# Use of the while or for loops in shell scripts to work through the array elements
# Copy the script below and save it as <filename>.sh
index_array=(1 2 3 4 5 6 7 8 9 0)

for i in ${index_array[@]}
do
        echo $i
done
```
### Built-in Operations for Arrays in Shell Scripts
1. **`[@]`** symbol to print all the elements at the same time or work with all the elements.
2. **`#`** symbol to to provide us the count of the elements stored in the array.
3. **`unset`** keyword to Delete Individual Array Elements.
```bash
echo ${assoc_array[@]}
```
```bash
echo ${#index_array[@]}
```
```bash
unset index_array[1]
```
