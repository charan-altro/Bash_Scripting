# Bash Scripting Notes

## Scripting vs Programming Languages

The primary distinction between **scripting** and **programming languages** lies in their execution process. 
- **Scripting languages**: Executed directly without compilation. 
- **Programming languages**: Require compilation before execution.

**Computer Language**:
- **Programming Language**: Think of it as a recipe for a dish. You gather your ingredients (code), follow the recipe (compile the code), and then serve the dish (run the program). If you want to change something, you have to go back to the recipe, make changes, and cook the dish again (recompile and execute).
  
- **Scripting Language**: This is like freestyle cooking. You add ingredients on the go, adjusting and tasting in real time (running the code immediately). If you want to modify the recipe, you don’t need to start over—you simply tweak as you go.

**In short**, scripting languages are executed immediately, while programming languages require compilation before execution.

### Examples of Programming Languages:
1. **C**: A popular, general-purpose language known for its simplicity and flexibility.
2. **C++**: An extension of C, used in game development, system drivers, and applications requiring performance.
3. **Java**: Versatile and widely used for enterprise-scale applications.
4. **C#**: Developed by Microsoft, primarily for Windows applications and game development with Unity.
5. **Swift**: Developed by Apple, used for iOS, macOS, and tvOS apps.
6. **Go (Golang)**: Known for its simplicity, efficiency, and concurrency handling.

These languages require compilation, making them suitable for building large-scale applications, video games, etc.

### Examples of Scripting Languages:
1. **Bash**: Primarily used in Linux for automating tasks in the command line.
2. **Node.js**: Allows developers to build server-side applications with JavaScript.
3. **Ruby**: Known for its simplicity and flexibility, commonly used in web development.
4. **Python**: Easy-to-learn and widely used for automation, scripting, and web development.
5. **JavaScript**: Key language for web development (both client and server-side scripting).
6. **PHP**: Used in web development, especially for server-side tasks.

Scripting languages are **interpreted** and allow for real-time execution without needing a compilation step.

---

## Scripting Language Structure

The structure of a scripting language can be broken down into several essential components, much like preparing a meal:

1. **Input & Output**: These are like the ingredients and the final dish. You start with raw data (input) and transform it into something useful (output).
   - Example: Reading a file and printing the content.

2. **Arguments, Variables & Arrays**: 
   - **Arguments**: Instructions given to tools, like setting the oven to 350°F.
   - **Variables**: Storage containers for data, much like bowls that hold different ingredients.
   - **Arrays**: Collections of similar data, like muffin tins holding multiple cupcakes.

3. **Conditional Execution**: 
   - Following different steps based on conditions.
   - Example: If the oven is preheated, start baking; otherwise, wait.

4. **Arithmetic**: 
   - Simple mathematical operations, like measuring ingredients.
   - Example: Adding flour or dividing the recipe in half.

5. **Loops**: 
   - Repeating tasks, like stirring a sauce until it thickens or whisking eggs until peaks form.
   - Example: A `for` loop to iterate over files in a directory.

6. **Comparison Operators**: 
   - Used to check conditions, like whether the cake is golden brown or if the temperature has reached 165°F.
   - Example: `if [ "$x" -gt "$y" ]; then`

7. **Functions**: 
   - Reusable procedures, like chopping onions or frying vegetables. Once defined, they can be reused across different parts of the script.
   - Example: A function that logs errors or processes data in a specific way.

---

### Example Bash Script:

```bash
#!/bin/bash

# Shebang: This line tells the system to use bash to interpret the script.

# Global Variables
LOGFILE="script.log"
EXIT_SUCCESS=0
EXIT_FAILURE=1

# Positional Parameters: $0 is the script name, $1 and $2 are the first and second arguments passed to the script.
SCRIPT_NAME="$0"
FIRST_ARG="$1"
SECOND_ARG="$2"

# Example of setting and using variables
NAME="John"
AGE=25
printf "Name: %s, Age: %d\n" "$NAME" "$AGE"

# IFS (Internal Field Separator) usage example: 
# Temporarily change IFS to split colon-separated values
input="apple:banana:cherry"
IFS=":"
for fruit in $input; do
    printf "Fruit: %s\n" "$fruit"
done
IFS=" "  # Reset IFS to default

# Reading input (stdin) from the user
printf "Enter a number: "
read -r user_input
printf "You entered: %s\n" "$user_input"

# Output redirection: stdout and stderr
printf "This is standard output.\n"
printf "This is an error message.\n" >&2

# Arithmetic operations
num1=10
num2=20
sum=$(( num1 + num2 ))
printf "Sum of %d and %d is %d\n" "$num1" "$num2" "$sum"

# Conditional execution using if-elif-else and AND/OR logic
if [[ $sum -eq 30 ]]; then
    printf "The sum is exactly 30.\n"
elif [[ $sum -gt 30 ]]; then
    printf "The sum is greater than 30.\n"
else
    printf "The sum is less than 30.\n"
fi

# AND (&&) / OR (||) logic example
if [[ $num1 -gt 5 && $num2 -lt 25 ]]; then
    printf "num1 is greater than 5 AND num2 is less than 25.\n"
fi

if [[ $num1 -lt 5 || $num2 -gt 15 ]]; then
    printf "Either num1 is less than 5 OR num2 is greater than 15.\n"
fi

# Example of a while loop
counter=1
while [[ $counter -le 5 ]]; do
    printf "Counter is at %d\n" "$counter"
    ((counter++))  # Increment counter
done

# For loop example
for i in {1..3}; do
    printf "Iteration %d of for loop.\n" "$i"
done

# Case statement example (similar to switch-case in other languages)
case "$FIRST_ARG" in
    start)
        printf "Starting the process...\n"
        ;;
    stop)
        printf "Stopping the process...\n"
        ;;
    restart)
        printf "Restarting the process...\n"
        ;;
    *)
        printf "Unknown command. Use start, stop, or restart.\n"
        ;;
esac

# Function to check exit status of commands
check_exit_status() {
    if [[ $? -eq 0 ]]; then
        printf "Command executed successfully.\n"
    else
        printf "Command failed with status code $?.\n" >&2
    fi
}

# Example using the exit status of a command
mkdir -p /tmp/testdir
check_exit_status  # Check if directory creation was successful

# Demonstrating positional parameters
printf "Script name: %s\n" "$SCRIPT_NAME"
printf "First argument: %s\n" "$FIRST_ARG"
printf "Second argument: %s\n" "$SECOND_ARG"

# Demonstrating arrays in bash
my_array=("apple" "banana" "cherry")
printf "First item in the array: %s\n" "${my_array[0]}"
printf "All items in the array: %s\n" "${my_array[@]}"

# Reading multiple values using an array
printf "Enter three space-separated fruits: "
read -r -a fruits
printf "You entered: %s, %s, and %s\n" "${fruits[0]}" "${fruits[1]}" "${fruits[2]}"

# Return codes in functions
return_example() {
    local num=$1
    if [[ $num -gt 10 ]]; then
        return 0  # Success if num > 10
    else
        return 1  # Failure if num <= 10
    fi
}

# Check return code of the function
return_example 15
if [[ $? -eq 0 ]]; then
    printf "Function returned success.\n"
else
    printf "Function returned failure.\n"
fi

# Logging messages to a file
log_message() {
    local message=$1
    printf "%s\n" "$message" >> "$LOGFILE"
}

log_message "This is a log entry."

# Script exit with success or failure
exit $EXIT_SUCCESS

# EOF: Marks the end of the script
