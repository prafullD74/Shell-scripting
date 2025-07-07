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
An important thing to keep in mind is that, like C programming, shell scripting is case sensitive. Hence, you need to be careful while using the keywords in your code.

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
