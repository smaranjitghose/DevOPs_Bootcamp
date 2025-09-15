# Module 3: Scripting Fundamentals - From Commands to Automation

## Bhanu's Journey: From File Explorer to Scripting Sorcerer

After mastering the art of file navigation, folder structures, and permissions in Module 2, Bhanu felt confident navigating the digital kingdom. But soon, Bhanu noticed something frustrating - having to type the same commands over and over again. Every morning, Bhanu would:

1. Create backup folders with `mkdir backup_$(date +%Y%m%d)`
2. Copy important files with `cp reports/*.txt backup_$(date +%Y%m%d)/`
3. Check disk space with `df -h`
4. Look for errors in logs with `grep -i error /var/log/system.log`

<img style="background: black" src="./image/Module3/Bhanu Journey From File Explorer to Scripting Sorcerer.png" alt="Bhanu Journey From File Explorer to Scripting Sorcerer" />

"It's tedious doing this manually every day," Bhanu thought while sipping coffee at the Digital Café. "There must be a better way!"

That's when Bhanu met maheedhar, a seasoned Shell Scripting Sorcerer who noticed Bhanu's frustration.

"Ah, I see you're performing the same ritual daily," maheedhar said with a knowing smile. "Why not create a magic spell - a script - that does all this for you automatically?"

"A script?" Bhanu asked curiously. "Like a text file with commands?"

"Precisely!" maheedhar replied. "But with special powers. Let me show you how to transform from a file explorer into a scripting sorcerer..."

---

## 3.1 Writing Your First Shell Script

<img style="background: black" src="./image/Module3/Writing Your First Shell Script.png" alt="Writing Your First Shell Script" width="250px"/>

---

## Concept Introduction

A **shell script** is nothing more than a text file that contains a series of commands you could type manually in the terminal. The difference? Instead of repeating yourself, you save them into a file and run it as a program.

To write scripts, you’ll use **text editors** — special tools to create and edit plain text.

---

## Technical Deep Dive

### Text Editors vs Script Files

* **Text Editors** → Programs used to write and edit text files.

  * Examples: `nano`, `vim`, `gedit`
* **Regular Text File** → Stores plain text, like `notes.txt` with “Meeting at 3pm.”
* **Shell Script File** → A text file with commands that can be executed, like `backup.sh`.

---

### Creating Your First Script

* With **Nano** (easy to use):

  ```bash
  nano daily_backup.sh
  ```
* With **Vim** (powerful, advanced):

  ```bash
  vim daily_backup.sh
  ```
* With **Gedit** (GUI editor, if available):

  ```bash
  gedit daily_backup.sh
  ```

Inside the editor, you can now start writing your first script!

---

### Script Structure: The Skeleton of a Spell

Every script has three essential parts:

1. **Shebang (`#!/bin/bash`)** – Tells the system which interpreter to use.

   ```bash
   #!/bin/bash
   ```

   Must be the very first line.
2. **Comments (`#`)** – Notes for humans, ignored by the computer.

   ```bash
   # This script creates daily backups
   ```
3. **Commands** – The actual magic!

   ```bash
   mkdir backup_$(date +%Y%m%d)
   ```

   This command creates a folder with today’s date in its name.

---

## Bhanu’s First Spell (Example Script)

Bhanu types the following into his file `daily_backup.sh`:

```bash
#!/bin/bash
# My first backup script
mkdir backup_$(date +%Y%m%d)
cp reports/*.txt backup_$(date +%Y%m%d)/
df -h
```

He saves the file and smiles. He just bottled his daily ritual into a single script!

---

## Practice Exercise

1. Create a new script called `hello.sh`.
2. Inside it, add:

   * A shebang line (`#!/bin/bash`)
   * A comment (`# This script prints a message`)
   * A command:

     ```bash
     echo "Hello, World!"
     ```
3. Save it. In the next chapter, we’ll learn how to **execute** it.

---

## 3.2 Executing Scripts

<img style="background: black" src="./image/Module3/Executing Scripts - visual selection.png" alt="Executing Scripts - visual selection" />

Perfect 👌 let’s now transform your **Executing Scripts** notes into the same **book-style format** we agreed on.

---

Bhanu stared at his new script, `daily_backup.sh`. It looked perfect — a neat little spell written on his digital scroll.

But when he tried to run it:

```bash
./daily_backup.sh
```

The terminal replied coldly:

```
Permission denied
```

Bhanu groaned. *“I wrote the script… why won’t it obey me?”*

Maheedhar chuckled knowingly.
“Ah, young apprentice, not all scrolls are enchanted to work right away. A script must be granted **execution rights** before it can spring into action.”

---

## Concept Introduction

Linux is like a kingdom with strict gatekeepers. Every file has **permissions** that decide:

* Who can **read** it,
* Who can **write** (edit) it,
* Who can **execute** it (run it like a program).

A shell script, by default, is just a text file. To make it runnable, you must **add execute permission**.

---

## Technical Deep Dive

### Understanding Script Permissions

* Check permissions with:

  ```bash
  ls -l daily_backup.sh
  ```

  Example output:

  ```
  -rw-r--r-- 1 bhanu users 120 Sep 15 10:00 daily_backup.sh
  ```

  * `r` = read, `w` = write, `x` = execute.
  * Notice there’s no `x` yet — meaning Bhanu can’t execute it.
* After granting permission:

  ```bash
  chmod +x daily_backup.sh
  ls -l daily_backup.sh
  ```

  ```
  -rwxr-xr-x 1 bhanu users 120 Sep 15 10:00 daily_backup.sh
  ```

  Now the file is executable.

---

### Making Scripts Executable

* Add execute permission for **everyone**:

  ```bash
  chmod +x daily_backup.sh
  ```
* Add execute permission for **owner only**:

  ```bash
  chmod u+x daily_backup.sh
  ```
* Verify with `ls -l`:

  ```
  -rwxr--r-- 1 bhanu users 120 Sep 15 10:00 daily_backup.sh
  ```

---

### Methods to Execute Scripts

1. **Run directly (requires execute permission):**

   ```bash
   ./daily_backup.sh
   ```
2. **Run with Bash interpreter (no execute permission needed):**

   ```bash
   bash daily_backup.sh
   ```
3. **Run in current shell context (affects environment variables):**

   ```bash
   source daily_backup.sh
   ```

---

### Execution Flow (Step by Step)

1. Create the script file with a text editor.
2. Add the shebang line:

   ```bash
   #!/bin/bash
   ```
3. Write your commands.
4. Save the file.
5. Add execute permission:

   ```bash
   chmod +x script.sh
   ```
6. Execute with:

   ```bash
   ./script.sh
   ```

---

## Bhanu’s First Execution

Bhanu fixes his script:

```bash
chmod +x daily_backup.sh
./daily_backup.sh
```

The terminal responds by creating a backup folder, copying reports, and showing disk usage. Bhanu grins. *“Finally! My spell works!”*

---

## Practice Exercise

1. Write a script `greet.sh` that prints:

   ```
   Hello, this is my first executable script!
   ```
2. Try running it without `chmod +x`. Observe the error.
3. Use `chmod +x greet.sh` and run it again with `./greet.sh`.
4. Bonus: Try running it with `bash greet.sh` and `source greet.sh`. Compare the behavior.

---

## 3.3 Variables and Data Types

<img style="background: black" src="./image/Module3/Shell Scripting Variables and Data Types - visual selection.png" alt="Variables and Data Types - visual selection" style="margin: auto; width: 500px; height: auto;"/>


##  Story Hook

Bhanu had successfully executed his first script. But soon, he realized a problem: every time he needed to change the backup folder name or number of files, he had to **edit the script directly**.

“This feels inefficient,” he thought. “There must be a way to store values and reuse them without rewriting everything.”

That’s when Maheedhar explained:
“In scripting, we use **variables** — containers that hold values like text, numbers, or lists. Instead of hardcoding values, you assign them to variables and use them throughout your script.”

---

##  Concept Introduction

A **variable** is like a named container. Instead of typing values repeatedly, you assign them once and reuse them. This makes scripts:

* Easier to read,
* Easier to maintain,
* More flexible.

---

##  Technical Deep Dive

### Understanding Variables in Scripts

* **Definition**: Variables store data (strings, numbers, or arrays).

* **Example**:

  ```bash
  backup_dir="backup_$(date +%Y%m%d)"
  echo $backup_dir
  ```

  Output:

  ```
  backup_20250915
  ```

* **Naming rules**:

  * ✅ `backupDir`, `backup_dir`
  * ❌ `backup dir` (spaces not allowed)

---

### String Variables

* Assign a string:

  ```bash
  backup_dir="backup_$(date +%Y%m%d)"
  ```
* Access value:

  ```bash
  echo $backup_dir
  ```
* Update variable:

  ```bash
  backup_dir="backup_archive"
  ```
* Recommended: use braces to avoid ambiguity:

  ```bash
  echo "${backup_dir}/reports"
  ```

---

### Integer Operations

Shell variables normally store text, but arithmetic is supported using special syntax:

* Arithmetic evaluation:

  ```bash
  ((backup_count=5+3))
  echo $backup_count   # Output: 8
  ```

* Inline calculation:

  ```bash
  echo $((10-4))   # Output: 6
  ```

* Using `let`:

  ```bash
  let "file_count=5*4"
  echo $file_count   # Output: 20
  ```

* Legacy method (`expr`):

  ```bash
  expr 5 + 3   # Output: 8
  ```

---

### Array Handling

Bash also supports arrays for handling multiple values.

* Declare array:

  ```bash
  file_types=("txt" "doc" "pdf")
  ```

* Access elements:

  ```bash
  echo ${file_types[0]}   # Output: txt
  ```

* Access all elements:

  ```bash
  echo ${file_types[@]}   # Output: txt doc pdf
  ```

* Get length:

  ```bash
  echo ${#file_types[@]}   # Output: 3
  ```

* Modify element:

  ```bash
  file_types[2]="xlsx"
  echo ${file_types[@]}   # Output: txt doc xlsx
  ```

---

##  Example Script – Backup with Variables

```bash
#!/bin/bash
# Backup script using variables

backup_dir="backup_$(date +%Y%m%d)"
file_types=("txt" "doc" "pdf")

mkdir $backup_dir
cp reports/*.${file_types[0]} $backup_dir/
cp reports/*.${file_types[1]} $backup_dir/
cp reports/*.${file_types[2]} $backup_dir/

echo "Backup completed in $backup_dir"
```

This script dynamically names the backup folder and copies multiple file types using variables and arrays.

---

##  Practice Exercises

1. Create a variable `name` with your name and print:

   ```
   Hello, <name>! Welcome to scripting.
   ```

2. Assign two numbers to variables and calculate their sum.

3. Create an array of 3 colors and print:

   * The first color,
   * The total number of colors,
   * All colors at once.


---

## 3.4 Reading User Input


Bhanu’s scripts were working well, but they still felt rigid. Each time he wanted to change the backup directory or number of days, he had to edit the script itself.

“This doesn’t feel very flexible,” Bhanu thought. *“What if I want to reuse the same script for different directories?”*

Maheedhar explained:
“Scripts can interact with the user. Instead of hardcoding values, you can **ask for input** while the script runs. That way, the script becomes dynamic.”

---

##  Concept Introduction

The **`read` command** allows a script to capture input from the user.

* It pauses execution,
* Waits for the user to type something,
* Stores that value in a variable for later use.

This makes scripts customizable and interactive.

---

## Technical Deep Dive

### Basic `read` Command

* **Read into variable**:

  ```bash
  read username
  echo "Welcome, $username"
  ```

  The script pauses until the user types something.

* **Custom prompt (`-p`)**:

  ```bash
  read -p "Enter backup directory: " backup_dir
  echo "Backing up files to $backup_dir"
  ```

* **Silent input (`-s`)** – useful for passwords:

  ```bash
  read -s -p "Password: " pass
  echo
  echo "Password captured but hidden"
  ```

* **Read into array (`-a`)**:

  ```bash
  read -a file_names
  echo "First file: ${file_names[0]}"
  echo "All files: ${file_names[@]}"
  ```

---

### Input Validation

Scripts should not assume users always provide correct input. Validation ensures safety.

* **Check if input is empty**:

  ```bash
  if [ -z "$backup_dir" ]; then
      echo "Directory cannot be empty"
  fi
  ```

* **Check if input is numeric**:

  ```bash
  if [[ $days =~ ^[0-9]+$ ]]; then
      echo "Valid number"
  else
      echo "Numbers only"
  fi
  ```

* **Check against allowed values with `case`**:

  ```bash
  read -p "Continue? (y/n): " confirm
  case $confirm in
      [yY]*) echo "Proceeding..." ;;
      [nN]*) echo "Stopping..." ;;
      *) echo "Invalid choice" ;;
  esac
  ```

---

## Example Script – Interactive Backup

```bash
#!/bin/bash
# Interactive backup script

read -p "Enter backup directory name: " backup_dir
if [ -z "$backup_dir" ]; then
    echo "Error: Directory name cannot be empty"
    exit 1
fi

mkdir "$backup_dir"
cp reports/*.txt "$backup_dir/"

echo "Backup completed in $backup_dir"
```

This script asks the user where to store backups and validates that the directory name is not empty.

---

## Practice Exercises

1. Write a script that asks for your name and greets you.
2. Write a script that asks for a number and prints whether it is **even or odd**.
3. Extend your backup script to confirm with the user (`y/n`) before copying files.

---

## 3.5 Basic Operators

<img style="background: black" src="./image/Module3/Basic Operators - visual selection.png" style="margin: auto; width: 500px; height: auto;"/>

### Arithmetic Operators

| Operator | Description        | Example & Explanation            |
| -------- | ------------------ | -------------------------------- |
| `+`    | Addition           | `echo $((5+3))` → Outputs: 8  |
| `-`    | Subtraction        | `echo $((10-4))` → Outputs: 6 |
| `*`    | Multiplication     | `echo $((5*4))` → Outputs: 20 |
| `/`    | Division           | `echo $((10/2))` → Outputs: 5 |
| `%`    | Modulo (remainder) | `echo $((10%3))` → Outputs: 1 |
| `**`   | Exponentiation     | `echo $((2**3))` → Outputs: 8 |

### Relational Operators

| Operator | Description                        | Example & Explanation                                                                |
| -------- | ---------------------------------- | ------------------------------------------------------------------------------------ |
| `-eq`  | Equal to (numbers)                 | `if [ $file_count -eq 5 ]` → True if file_count equals 5                          |
| `-ne`  | Not equal to (numbers)             | `if [ $file_count -ne 5 ]` → True if file_count not equal to 5                    |
| `-gt`  | Greater than (numbers)             | `if [ $file_count -gt 5 ]` → True if file_count greater than 5                    |
| `-lt`  | Less than (numbers)                | `if [ $file_count -lt 5 ]` → True if file_count less than 5                       |
| `-ge`  | Greater than or equal to (numbers) | `if [ $file_count -ge 5 ]` → True if file_count greater than or equal to 5        |
| `-le`  | Less than or equal to (numbers)    | `if [ $file_count -le 5 ]` → True if file_count less than or equal to 5           |
| `==`   | Equal to (strings)                 | `if [ "$filename" == "report.txt" ]` → True if filename equals "report.txt"       |
| `!=`   | Not equal to (strings)             | `if [ "$filename" != "report.txt" ]` → True if filename not equal to "report.txt" |

### Logical Operators

| Operator | Description | Example & Explanation                                                          |
| -------- | ----------- | ------------------------------------------------------------------------------ |
| `&&`   | Logical AND | `if [ -f "$file" ] && [ -r "$file" ]` → True if file exists and is readable |
| `\|\|`   | Logical OR  | `if [ "$ext" == "txt" ] \|\| [ "$ext" == "csv" ]` → True if ext is txt or csv |
| `!`    | Logical NOT | `if [ ! -d "$backup_dir" ]` → True if backup_dir doesn't exist              |

---

## 3.6 Control Flow

<img style="background: black" src="./image/Module3/Control Flow.png" alt="String Manipulation" style="margin: auto; width: 500px; height: auto;"/>

Bhanu’s scripts could now take input, but they still followed a straight line of execution.

“What if I want the script to do something only when a file exists?” Bhanu asked.
Maheedhar smiled:
“That’s where **control flow** comes in. Scripts become truly powerful when they can **decide** and **repeat** actions—just like we make decisions every day and repeat tasks until they’re done.”

---

## Concept Introduction

Control flow in shell scripting is about:

1. **Making decisions** → Using `if`, `if-else`, and `case`.
2. **Repeating actions** → Using loops (`for`, `while`, `until`).

Together, they give scripts **logic and intelligence**.

---

##  Technical Deep Dive

###  Conditional Statements

* **Simple if statement**

  ```bash
  if [ -f "report.txt" ]; then
      echo "File exists"
  fi
  ```

* **If-else**

  ```bash
  if [ -f "report.txt" ]; then
      echo "File exists"
  else
      echo "File not found"
  fi
  ```

* **If-elif-else (multiple conditions)**

  ```bash
  if [ $count -gt 10 ]; then
      echo "Many"
  elif [ $count -gt 5 ]; then
      echo "Some"
  else
      echo "Few"
  fi
  ```

* **Case statement (multi-branch)**

  ```bash
  case $file_type in
      txt) echo "Text file" ;;
      csv) echo "Data file" ;;
      *)   echo "Unknown" ;;
  esac
  ```

---

### 🔹 Looping Constructs

* **For loop (list-based)**

  ```bash
  for file in *.txt; do
      echo "Processing $file"
  done
  ```

* **C-style for loop**

  ```bash
  for ((i=1; i<=3; i++)); do
      echo "Backup $i"
  done
  ```

* **While loop (condition true)**

  ```bash
  count=1
  while [ $count -le 3 ]; do
      echo "Processing $count"
      ((count++))
  done
  ```

* **Until loop (runs until condition true)**

  ```bash
  count=1
  until [ $count -gt 3 ]; do
      echo "Processing $count"
      ((count++))
  done
  ```

* **Break (exit loop immediately)**

  ```bash
  for i in {1..10}; do
      if [ $i -eq 5 ]; then
          break
      fi
      echo $i
  done
  # Prints 1–4
  ```

* **Continue (skip to next iteration)**

  ```bash
  for i in {1..5}; do
      if [ $i -eq 3 ]; then
          continue
      fi
      echo $i
  done
  # Prints 1, 2, 4, 5
  ```

---

## Example Script – File Checker

```bash
#!/bin/bash
# Script to check and process files

for file in *.log; do
    if [ -s "$file" ]; then
        echo "Processing non-empty file: $file"
    else
        echo "Skipping empty file: $file"
    fi
done
```

This script loops through `.log` files and processes only the ones that are not empty.

---

## Practice Exercises

1. Write a script that checks if a user-given number is **positive, negative, or zero**.
2. Write a script that prints numbers from **1 to 10**, but skips **5**.
3. Create a script that uses `case` to act like a simple **menu**:

   * Option 1: Show date
   * Option 2: Show current directory
   * Option 3: Exit


---

## 3.7 Functions in Shell Scripting

<img style="background: black" src="./image/Module3/Functions in Shell Scripting - visual selection.png" style="margin: auto; width: 500px; height: auto;"/>

---

Bhanu was writing longer scripts now. But each time he needed to back up files, he had to **copy-paste the same lines** again and again.

“Why can’t I just write this once and use it everywhere?” he asked.

Maheedhar replied:
“That’s exactly what **functions** are for. They let you **reuse code** without repeating yourself.”

---

## Concept Introduction

Functions in shell scripting are **blocks of reusable code**. They:

* Improve readability.
* Reduce duplication.
* Make scripts modular and easier to maintain.

Think of them as **mini-scripts inside your script**.

---

## Technical Deep Dive

### 🔹 Function Definition

Two common ways to define a function:

```bash
# Method 1
name() {
    commands
}

# Example
create_backup() {
    mkdir -p "$1"
    cp *.txt "$1/"
}
```

This creates a backup function that takes a target directory as an argument.

```bash
# Method 2
function name {
    commands
}

# Example
function show_help {
    echo "Usage: $0 [directory]"
}
```

This defines a help function using the alternative `function` keyword.

---

### Parameter Passing

Functions can take **arguments** just like scripts:

```bash
create_backup() {
    echo "Backing up to $1"
}
create_backup "/tmp/backup"
```

Here `$1` is the first parameter.

Special variables inside functions:

| Variable      | Meaning                         | Example                                    |
| ------------- | ------------------------------- | ------------------------------------------ |
| `$1, $2, ...` | Positional parameters           | `$1` = first parameter                     |
| `$0`          | Script name (not function name) | `echo "Running: $0"`                       |
| `$#`          | Number of parameters            | `count_params() { echo "Got $# params"; }` |
| `$@`          | All params as separate words    | `echo "Params: $@"`                        |
| `$*`          | All params as one string        | `echo "Params: $*"`                        |

---

### Return Values

Functions can **signal success/failure** or **produce output**:

1. **Using `return` (status codes)**

   ```bash
   check_dir() {
       if [ -d "$1" ]; then
           return 0   # success
       else
           return 1   # failure
       fi
   }

   check_dir "backup"
   if [ $? -eq 0 ]; then
       echo "Directory exists"
   else
       echo "Directory not found"
   fi
   ```

2. **Using `echo` (output values)**

   ```bash
   get_date() {
       echo $(date +%Y%m%d)
   }

   backup_dir=$(get_date)
   echo "Backup to $backup_dir"
   ```

Here, `return` is for **status codes (0–255)**, while `echo` is for **passing values**.

---

## Example Script – Backup Manager

```bash
#!/bin/bash
# Backup Manager with Functions

create_backup() {
    mkdir -p "$1"
    cp *.txt "$1/"
    echo "Backup completed in $1"
}

get_date() {
    echo $(date +%Y%m%d)
}

# Main script flow
backup_dir="backup_$(get_date)"
create_backup "$backup_dir"
```

This script creates a backup directory with today’s date and copies `.txt` files into it.

---

## Practice Exercises

1. Write a function `greet_user` that takes a name and prints:
   `"Hello <name>, welcome to shell scripting!"`
2. Create a function `is_even` that checks if a given number is even.

   * Return **0** if even, **1** if odd.
3. Write a function `sum_numbers` that takes multiple arguments and prints their sum.

---

## 3.8 Exit Codes and Status
Great — let’s wrap up the fundamentals with **Exit Codes and Status** in the same **book-style chapter format**.

---

One morning, Bhanu proudly ran his new backup script. It looked fine… but when he checked, **no files were copied**.

“Why didn’t it work?” Bhanu muttered in confusion.

Maheedhar explained:
“Every command leaves behind a **secret number** that tells you whether it succeeded or failed. Learn to read it, and your scripts will never mislead you again.”

That secret number is called the **exit status**.

---

## Concept Introduction

* Every command in Linux ends with an **exit code**.
* **0** means **success**.
* **Non-zero (1–255)** means **failure** or a specific error.
* Shell scripts use this to **decide what to do next**.

---

## Technical Deep Dive

### Exit Status Variable

```bash
ls /nonexistent
echo "Exit code: $?"
```

* `$?` → holds the exit status of the last command.
* `0` = success.
* Non-zero = error.

Examples:

| Command           | Output | Meaning             |
| ----------------- | ------ | ------------------- |
| `echo "Hi"`       | `0`    | Success             |
| `ls /nonexistent` | `2`    | Directory not found |
| `false`           | `1`    | General error       |

---

### Exit Command

You can **manually control** exit codes in your scripts:

```bash
# Exit with last command's status
if [ ! -d "$backup_dir" ]; then
    echo "Directory missing"
    exit
fi
```

```bash
# Exit with specific status code
if [ ! -f "$config_file" ]; then
    echo "Config missing"
    exit 2
fi
```

---

### Common Exit Codes

| Code               | Meaning                 | Example                         |
| ------------------ | ----------------------- | ------------------------------- |
| 0                  | Success                 | `exit 0` → Script ran fine      |
| 1                  | General error           | `exit 1` → Something went wrong |
| 2                  | Misuse of shell command | `exit 2`                        |
| 126                | Command not executable  | Permission issue                |
| 127                | Command not found       | Wrong command name              |
| 128+N              | Fatal error (signal N)  | `exit 130` → Ctrl+C (signal 2)  |
| Custom (e.g., 100) | Script-specific meaning | `exit 100` → Backup dir missing |

---

## Example Script – Exit Codes in Action

```bash
#!/bin/bash
# Backup Script with Exit Codes

backup_dir="backup_$(date +%Y%m%d)"

# Check if directory exists
if [ ! -d "$backup_dir" ]; then
    echo "Error: $backup_dir not found"
    exit 100   # custom error code
fi

cp *.txt "$backup_dir"/
if [ $? -ne 0 ]; then
    echo "Error: Failed to copy files"
    exit 1
fi

echo "Backup completed successfully"
exit 0
```

---

## Practice Exercises

1. Write a script that tries to `cd` into a directory:

   * Exit with **0** if successful, **1** if not.
2. Create a script that runs a command from user input:

   * Exit with **127** if the command is not found.
3. Modify your backup script to return **different custom codes** depending on the type of error (e.g., missing directory vs failed copy).

---

## Putting It All Together: Bhanu's Automated Backup Script

<img style="background: black" src="./image/Module3/code to image as a story flow creation - visual selection.png" style="display: block; margin: auto; width: 500px; height: 600px;" />

```bash
#!/bin/bash
# Bhanu's Automated Backup Script
# This script automates daily backup tasks and replaces manual commands

# Function to create backup directory
create_backup_dir() {
    local backup_dir="backup_$(date +%Y%m%d)"
    if [ -d "$backup_dir" ]; then
        echo "Backup directory $backup_dir already exists"
        return 1
    else
        mkdir -p "$backup_dir"
        echo "Created backup directory: $backup_dir"
        return 0
    fi
}

# Function to backup files
backup_files() {
    local backup_dir=$1
    local file_count=0
  
    # Check if source files exist
    if [ ! -d "reports" ]; then
        echo "Error: reports directory not found"
        return 2
    fi
  
    # Backup each file type
    for file_type in "txt" "csv" "xlsx"; do
        local files=($(find reports -name "*.$file_type" 2>/dev/null))
        if [ ${#files[@]} -gt 0 ]; then
            echo "Backing up $file_type files..."
            cp reports/*.$file_type "$backup_dir/"
            file_count=$((file_count + ${#files[@]}))
        fi
    done
  
    echo "Backed up $file_count files"
    return 0
}

# Function to check disk space
check_disk_space() {
    local threshold=90  # 90% threshold
    local usage=$(df . | tail -1 | awk '{print $5}' | sed 's/%//')
  
    if [ "$usage" -gt "$threshold" ]; then
        echo "Warning: Disk space is at ${usage}%"
        return 1
    else
        echo "Disk space is at ${usage}% (OK)"
        return 0
    fi
}

# Main script
echo "=== Automated Backup Script ==="
echo "Starting backup at $(date)"

# Create backup directory
if create_backup_dir; then
    backup_dir="backup_$(date +%Y%m%d)"
  
    # Backup files
    if backup_files "$backup_dir"; then
        echo "Backup completed successfully"
    else
        echo "Backup completed with errors"
        exit 1
    fi
else
    echo "Failed to create backup directory"
    exit 2
fi

# Check disk space
check_disk_space

echo "Backup process finished at $(date)"
exit 0
```

