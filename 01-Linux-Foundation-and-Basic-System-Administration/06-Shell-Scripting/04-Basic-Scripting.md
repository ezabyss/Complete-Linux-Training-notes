# Basic Shell Script Examples

Shell scripts allow us to automate common tasks such as:

- Printing text to the screen
- Displaying system information
- Creating files and directories
- Processing text
- Running multiple commands automatically

---

# 1. Creating a Directory for Scripts

Create a directory to store scripts.

`mkdir my_scripts`

Verify:

`ls`

Navigate into the directory:

`cd my_scripts`

# 2. Creating Your First Script

Create a new script using vi.

`vi output_screen`

Press `i` to enter insert mode.

Add the following code:

```
#!/bin/bash

echo "Hello World"
```

Save and exit:

Esc
`:wq`

# 3. Verify Script Content

Check the script contents:

`cat output_screen`

Output:
```
#!/bin/bash
echo "Hello World"
```

# 4. Make Script Executable

By default scripts are just files.

Add execute permission:

`chmod +x output_screen`

Verify:

`ls -ltr`

Executable files usually appear in green color.

# 5. Run the Script

Run the script from the current directory:

`./output_screen`

Output:

`Hello World`


# 6. Running Script Using Absolute Path

Scripts can also run using the full path.

Example:

`/home/user/my_scripts/output_screen`

Output:

`Hello World`

# 7. Script Example: Running Multiple Commands

Create another script:

`vi run_commands`

Insert:

```
#!/bin/bash

# This script performs small tasks
# Written by ezabyss
# Date: 2026 March 06

whoami
echo
pwd
hostname
ls -ltr
```

Save and exit.

Make it executable:

`chmod +x run_commands`

Run it:

`./run_commands`

Example Output:
```
ezabyss

/home/ezabyss/my_scripts
linux-server
total 8
-rwxr-xr-x 1 ezabyss ezabyss 20 output_screen
-rwxr-xr-x 1 ezbyss ezabyss 75 run_commands
```

# Explanation of commands:

| Command	| Purpose |
|---------|---------|
| whoami | Shows current username |
| echo | Creates a blank line |
| pwd	| Shows current directory |
| hostname | Shows system hostname | 
| ls | -ltr	Lists files in directory |

## 8. Script Example: Using Variables

Variables store values that scripts can reuse.

Create another script:

`vi variable_command`

Insert:
```
#!/bin/bash

# Script demonstrating variables

A=ezabyss
B=Abhishek
C="Linux class"

echo "My first name is $A"
echo "My surname is $B"
echo "My class is $C"
```

Save and exit.

Make executable:

`chmod +x variable_command`

Run the script:

`./variable_command`

Output:
```
My first name is ezabyss
My surname is Abhishek
My class is Linux class
```

## 9. Troubleshooting Scripts

If a script fails:

Check:
- Syntax errors
- Missing permissions
- Incorrect variables
- Error line number

Example error:
```
line 6: command not found
```
This indicates the problem is in line 6 of the script.

## 10. Common Commands Used in Scripts

Shell scripts often automate these commands:

| Command |	Purpose |
|--------|--------|
| echo |	Display output |
| pwd |	Show directory |
| whoami |	Current user |
| hostname |	System name |
| ls | List files |
| mkdir | Create directories |

---

Scripts can also automate text processing commands:
```
cut
grep
sort
uniq
```

---
## ✅ Key Takeaways
- Shell scripting allows you to:
- Automate repetitive tasks
- Run multiple commands together
- Simplify system management
- Create reusable scripts

Even simple scripts like Hello World are the first step toward learning programming.

---

**✍️ Notes By Abhishek (Ez Abyss)**
