# Bash Scripting Notes

## Scripting vs Programming Languages

The primary distinction between **scripting** and **programming languages** lies in their execution process. 
- **Scripting languages**: Executed directly without compilation. 
- **Programming languages**: Require compilation before execution.

**Analogy**:
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

# Function to check if the required file exists
check_file() {
    local file=$1
    if [[ ! -f "$file" ]]; then
        printf "Error: File %s not found!\n" "$file" >&2
        return 1
    fi
}

# Function to read ingredients (input) from a file
get_ingredients() {
    local ingredients_file="ingredients.txt"
    if ! check_file "$ingredients_file"; then
        return 1
    fi
    printf "Reading ingredients from %s...\n" "$ingredients_file"
    cat "$ingredients_file"
}

# Function to simulate cooking with loops
cook_dish() {
    local cooking_time=$1
    for (( i = 1; i <= cooking_time; i++ )); do
        printf "Cooking... minute %d of %d\n" "$i" "$cooking_time"
        sleep 1
    done
    printf "Dish is ready!\n"
}

# Main function controlling the script flow
main() {
    printf "Starting the cooking process...\n"
    
    # Get the ingredients
    local ingredients
    ingredients=$(get_ingredients) || exit 1
    
    # Cook for 5 minutes
    cook_dish 5
}

# Execute the main function
main
