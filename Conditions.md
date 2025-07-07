# [Conditions in Shell Scripts](https://www.digitalocean.com/community/tutorials/if-else-in-shell-scripts#conditions-in-shell-scripts)
>One of the most important parts of conditional programming is the if-else statements. An if-else statement allows you to execute iterative conditional statements in your code.

### Syntax of the if-else condition
```bash
if [condition]
then
   statement1
else
   statement2
fi
```
- An important thing to keep in mind is that, like C programming, shell scripting is case sensitive. Hence, you need to be careful while using the keywords in your code.
- Complex decision-making in shell scripts can be achieved by using nested if statements, case statements, or logical operators.
- For numerical comparison, use the -eq, -ne, -gt, -lt, -ge, and -le operators.

### Useful examples of if-else in shell scripts
1. Check if two variables are equal
```bash
#!/bin/bash
m=1
n=2

if [ $n -eq $m ]
then
        echo "Both variables are the same"
else
        echo "Both variables are different"
fi
```
2. Compare two values to find the greater one
```bash
#!/bin/bash
a=2
b=7
if [ $a -ge $b ]
then
  echo "The variable 'a' is greater than the variable 'b'."
else
  echo "The variable 'b' is greater than the variable 'a'."
fi
```
3. Check if a number is even (help of the modulus operator). The modulus operator divides a number with a divisor and returns the remainder.
```bash
#!/bin/bash
n=10
if [ $((n%2))==0 ]
then
  echo "The number is even."
else
  echo "The number is odd."
fi
```
4. Check if a file exists
```bash
if [ -f file.txt ]; then echo "File exists"; else echo "File does not exist"; fi
```
5. Check if a variable is empty
```bash
if [ -z "$var" ]; then echo "Variable is empty"; else echo "Variable is not empty"; fi
```
6. Make the interface for a password prompt.
```bash
#!/bin/bash
echo "Enter password"
read pass
if [ $pass="password" ]
then
  echo "The password is correct."
else
  echo "The password is incorrect, try again."
fi
```
### Utilizing elif for multiple conditions
The `elif` statement allows you to check multiple conditions in a more structured and readable way.
```bash
#!/bin/bash
grade=85
if [ $grade -ge 90 ]; then
  echo "Grade: A"
elif [ $grade -ge 80 ]; then
  echo "Grade: B"
elif [ $grade -ge 70 ]; then
  echo "Grade: C"
else
  echo "Grade: F"
fi
```
### Constructing nested if-else statements for complex scenarios
Nested `if-else` statements are used to handle complex scenarios where multiple conditions need to be evaluated. They allow you to check additional conditions if the initial condition is true or false. This is particularly useful when dealing with multiple variables or conditions that need to be evaluated in a specific order.
```bash
#!/bin/bash
num=10
if [ $num -ge 5 ]; then
  if [ $num -le 15 ]; then
    echo "The number is within the range."
  else
    echo "The number is above the range."
  fi
else
  echo "The number is below the range."
fi
```
```bash
if [ $var -ge 5 ] && [ $var -le 15 ]; then
  echo "Variable is within the range."
elif [ $var -lt 5 ]; then
  echo "Variable is less than 5."
else
  echo "Variable is greater than 15."
fi
```
### Checking file existence and permissions
```bash
#!/bin/bash
file_path="/path/to/your/file.txt"
if [ -f "$file_path" ]; then
  if [ -r "$file_path" ]; then
    echo "The file exists and is readable."
  else
    echo "The file exists but is not readable."
  fi
else
  echo "The file does not exist."
fi
```
The script first checks if the file exists using the -f test. If the file exists, it then checks if the file has read permissions using the -r test.
### Automating user input validation
User input validation is crucial in shell scripting to ensure that the input provided by the user is valid and can be processed correctly.
```bash
#!/bin/bash
echo "Enter the first number:"
read num1
echo "Enter the second number:"
read num2

if [[ $num1 =~ ^[0-9]+$ ]] && [[ $num2 =~ ^[0-9]+$ ]]; then
  echo "Both numbers are valid."
  # Perform calculations here
else
  echo "One or both numbers are invalid. Please enter valid numbers."
fi
```
### Case Statement (alternative to if-else)
The case statement allows you to match a value against multiple patterns and execute different blocks of code based on the match.
```bash
case $var in
  1)
    echo "Variable is 1."
    ;;
  2)
    echo "Variable is 2."
    ;;
  *)
    echo "Variable is neither 1 nor 2."
    ;;
esac
```
