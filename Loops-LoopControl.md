# Loop
>A loop is a powerful programming tool that enables you to execute a set of commands repeatedly.
1. **while loop**
2. **for loop**
3. **until loop**
4. **select loop**

### While Loop
While loop executes the given commands until the given condition remains true.
- Syntax
```bash
while command
do
   Statement(s) to be executed if command is true
done
```
- Example
```bash
#!/bin/sh

a=0

while [ $a -lt 10 ]
do
   echo $a
   ((a++))
done
```

### Unit Loop
Until loop executes until a given condition becomes true. The while loop is perfect for a situation where you need to execute a set of commands while some condition is true. Sometimes you need to execute a set of commands until a condition is true.
- Syntax 
```bash
until <condition>
do
    <command1>
    <command2>
    # ... more commands
done
```
- Example
```bash
#!/bin/bash

count=5

until [ $count -eq 0 ]
do
    echo "Count: $count"
    count=$((count - 1))
done

echo "Loop finished!"
```
### For Loop
For loop operates on lists of items. It repeats a set of commands for every item in a list.
- Syntax
```bash
#/bin/bash
for <var> in <value1 value2 ... valuen>
do
    <command 1>
    <command 2>
    <etc>
done
```
- Example
```bash
#!/bin/bash
for fruit in apple banana orange
do
  echo "I like $fruit."
done
```
### Select Loop
The select loop provides an easy way to create a numbered menu from which users can select options. It is useful when you need to ask the user to choose one or more items from a list of choices.
- Syntax
```bash
select variable_name in item1 item2 ... itemN
do
    # Commands to be executed based on the user's selection
done
```
- Example
```bash
#!/bin/bash

# --- Error Handling and Debugging Options ---
# set -e: Exit immediately if a command exits with a non-zero status.
# set -u: Treat unset variables as an error (e.g., if you try to use $undefined_var).
# set -o pipefail: The return value of a pipeline is the status of the last command
#                  to exit with a non-zero status, or zero if no command exited with a non-zero status.
set -euo pipefail

# --- Define Exit Codes ---
readonly EXIT_SUCCESS=0            # Script executed successfully, or user chose to quit gracefully.
readonly EXIT_INVALID_INPUT=1      # User provided invalid selection (e.g., non-existent option string).
readonly EXIT_CRITICAL_ERROR=2     # For more severe, unrecoverable internal errors (not typical for this script).

# --- Define Menu Options ---
# Using an array for options is good practice, especially if options have spaces.
# Added an explicit "Quit" option for clear user exit.
options=("tea" "coffee" "water" "juice" "apple" "all" "none" "Quit Script")

# --- Set the prompt for the select menu ---
# PS3 is a special variable that sets the prompt for the 'select' command.
PS3="Please select your drink (or 'q' to quit menu): "

# --- Main Selection Loop ---
# The 'select' loop continues until 'break' or 'exit' is called.
# It automatically handles invalid numeric input by printing "Invalid selection" and re-prompting.
select DRINK in "${options[@]}"
do
    case "$DRINK" in
        # Valid drink selections leading to canteen
        tea|coffee|water|all)
            echo "Action: Go to canteen for $DRINK."
            ;;
        # Valid drink selections leading to home
        juice|apple)
            echo "Action: $DRINK is available at home."
            ;;
        # User explicitly chooses 'none' (exit the selection loop gracefully)
        none)
            echo "Info: No drink selected. Exiting menu."
            break # Exits the 'select' loop
            ;;
        # User explicitly chooses 'Quit Script' (exit the script immediately)
        "Quit Script")
            echo "Info: User chose to quit the script."
            exit "${EXIT_SUCCESS}" # Exit the script with success status
            ;;
        # Handle cases where user just presses Enter (DRINK will be empty)
        "")
            echo "Warning: No selection made. Please choose an option number." >&2
            # Use 'continue' to re-display the menu without processing further in this iteration
            continue
            ;;
        # Handle any other invalid input (non-numeric, or numeric out of range for array)
        *)
            echo "ERROR: Invalid selection '$REPLY'. Please choose a valid number from the list." >&2
            # $REPLY contains the raw input if it didn't match an option (e.g., 'xyz')
            # Use 'continue' to re-display the menu.
            continue # Allows the loop to continue and re-prompt
            ;;
    esac
    echo # Add a newline for better readability between prompts
done

# --- Script Completion ---
# This part is reached if the 'select' loop is broken out of normally (e.g., by selecting 'none').
echo "Script operation completed."
exit "${EXIT_SUCCESS}" # Explicitly exit with a success status
```
- The `case` statement in shell scripting is designed to match a value against one or more patterns. The patterns are separated by the pipe symbol `|`, which acts as an `OR` operator for patterns. When you write tea|coffee|water|all), Bash interprets this as a single pattern clause.
### Nesting Loops
>All the loops support nesting concept which means you can put one loop inside another similar one or different loops. This nesting can go up to unlimited number of times based on your requirement.
