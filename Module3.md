

# Module 3: Scripting Fundamentals - From Commands to Automation

## Bhanu's Journey: From File Explorer to Scripting Sorcerer

After mastering the art of file navigation, folder structures, and permissions in Module 2, Bhanu felt confident navigating the digital kingdom. But soon, Bhanu noticed something frustrating - having to type the same commands over and over again. Every morning, Bhanu would:

1. Create backup folders with `mkdir backup_$(date +%Y%m%d)`
2. Copy important files with `cp reports/*.txt backup_$(date +%Y%m%d)/`
3. Check disk space with `df -h`
4. Look for errors in logs with `grep -i error /var/log/system.log`


​<img src="./image/Module3/Bhanu Journey From File Explorer to Scripting Sorcerer.png" alt="Bhanu Journey From File Explorer to Scripting Sorcerer" />

"It's tedious doing this manually every day," Bhanu thought while sipping coffee at the Digital Café. "There must be a better way!"

That's when Bhanu met maheedhar, a seasoned Shell Scripting Sorcerer who noticed Bhanu's frustration.

"Ah, I see you're performing the same ritual daily," maheedhar said with a knowing smile. "Why not create a magic spell - a script - that does all this for you automatically?"

"A script?" Bhanu asked curiously. "Like a text file with commands?"

"Precisely!" maheedhar replied. "But with special powers. Let me show you how to transform from a file explorer into a scripting sorcerer..."

---

## 3.1 Writing Your First Shell Script

​<img src="./image/Module3/Writing Your First Shell Script.png" alt="Writing Your First Shell Script" style="display: block; margin: auto; width: 500px; height: auto;"/>

### Understanding Text Editors vs. Script Files
| Concept          | Description                                  | Example & Explanation                                                                 |
|------------------|----------------------------------------------|----------------------------------------------------------------------------------------|
| Text Editors     | Programs for creating and editing plain text | `nano`, `vim`, `gedit` - Tools to write and modify text files                          |
| Regular Text File| Contains human-readable text                 | `notes.txt` - Contains text like "Meeting at 3pm"                                      |
| Shell Script File| Special text file with executable commands   | `backup.sh` - Contains commands that can be executed as a program                       |

### Creating Your First Script
| Action           | Description                                  | Example & Explanation                                                                 |
|------------------|----------------------------------------------|----------------------------------------------------------------------------------------|
| `nano daily_backup.sh` | Create script with Nano editor     | `nano daily_backup.sh` → Opens Nano to create a new script file                        |
| `vim daily_backup.sh` | Create script with Vim editor       | `vim daily_backup.sh` → Opens Vim (more advanced) to create the script                  |
| `gedit daily_backup.sh`| Create script with Gedit (GUI)     | `gedit daily_backup.sh` → Opens graphical text editor (if available)                   |

### Shebang and Script Structure
| Component        | Description                                  | Example & Explanation                                                                 |
|------------------|----------------------------------------------|----------------------------------------------------------------------------------------|
| `#!/bin/bash`    | Shebang line - tells system which interpreter to use | `#!/bin/bash` → Must be first line, specifies Bash interpreter          |
| `# comment`      | Comment line - ignored during execution     | `# This script creates daily backups` → Notes for humans, not executed                   |
| `command`        | Any shell command                           | `mkdir backup_$(date +%Y%m%d)` → Creates backup directory with today's date            |

### Complete First Script Example
```bash
#!/bin/bash
# Bhanu's first backup script
# This script automates daily backup tasks

echo "Starting daily backup..."
mkdir -p backup_$(date +%Y%m%d)
cp reports/*.txt backup_$(date +%Y%m%d)/
echo "Backup completed on $(date)"
```

---

## 3.2 Executing Scripts

​<img src="./image/Module3/Executing Scripts - visual selection.png" alt="Executing Scripts - visual selection" />

### Understanding Script Permissions

| Concept            | Description                                   | Example & Explanation                                                                      |
| ------------------ | --------------------------------------------- | ------------------------------------------------------------------------------------------ |
| File Permissions   | Access rights for reading, writing, executing | `ls -l daily_backup.sh` → Shows permissions like `-rw-r--r--` (no execute permission) |
| Execute Permission | Special permission to run as program          | After `chmod +x daily_backup.sh` → Permissions become `-rwxr-xr-x` (executable)       |

### Making Scripts Executable

| Command                 | Description                           | Example & Explanation                                                             |
| ----------------------- | ------------------------------------- | --------------------------------------------------------------------------------- |
| `chmod +x script.sh`  | Add execute permission to script      | `chmod +x daily_backup.sh` → Adds execute permission for all users             |
| `chmod u+x script.sh` | Add execute permission for owner only | `chmod u+x daily_backup.sh` → Only owner can execute the script                |
| `ls -l script.sh`     | Verify script permissions             | `ls -l daily_backup.sh` → Shows `-rwxr--r--` or similar (x means executable) |

### Execution Methods

| Method               | Description                         | Example & Explanation                                                                    |
| -------------------- | ----------------------------------- | ---------------------------------------------------------------------------------------- |
| `./script.sh`      | Execute script in current directory | `./daily_backup.sh` → Runs the script (requires execute permission)                   |
| `bash script.sh`   | Execute with Bash interpreter       | `bash daily_backup.sh` → Runs script using Bash (no execute permission needed)        |
| `source script.sh` | Execute in current shell context    | `source daily_backup.sh` → Runs script in current shell (affects current environment) |

### Execution Flow

1. Create script file with text editor
2. Add shebang line `#!/bin/bash`
3. Write commands in the script
4. Save the file
5. Add execute permission: `chmod +x script.sh`
6. Execute with: `./script.sh`

---

## 3.3 Variables and Data Types

​<img src="./image/Module3/Shell Scripting Variables and Data Types - visual selection.png" alt="Variables and Data Types - visual selection" style="margin: auto; width: 500px; height: auto;"/>

### Understanding Variables in Scripts

| Concept        | Description                                | Example & Explanation                                                             |
| -------------- | ------------------------------------------ | --------------------------------------------------------------------------------- |
| Variable       | Named container for storing data           | `backup_dir="backup_$(date +%Y%m%d)"` → Stores directory name in variable      |
| Variable Name  | Identifier without spaces or special chars | `backupDir` or `backup_dir` → Valid names; `backup dir` → Invalid (space) |
| Variable Value | Data stored in the variable                | `echo $backup_dir` → Outputs the value stored in backup_dir                    |

### String Variables

| Syntax                                                                                                                                                       | Description               | Example & Explanation                                                      |
| ------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------- | -------------------------------------------------------------------------- |
| `name="value"`                                                                                                                                             | Assign string to variable | `backup_dir="backup_$(date +%Y%m%d)"` → Stores directory name with date |
| `echo $name`     | Access variable value                       | `echo $backup_dir` → Outputs: "backup_20231115" (if today is Nov 15, 2023)             |                           |                                                                            |
| `name="new"`                                                                                                                                               | Update variable value     | `backup_dir="backup_archive"` → Changes backup_dir to "backup_archive"  |
| `echo "${name}"` | Access with braces (recommended)            | `echo "${backup_dir}/reports"` → Outputs: "backup_20231115/reports" (avoids ambiguity) |                           |                                                                            |

### Integer Operations

| Syntax                                                                                             | Description                       | Example & Explanation                                           |
| -------------------------------------------------------------------------------------------------- | --------------------------------- | --------------------------------------------------------------- |
| `((result=expr))`                                                                                | Arithmetic evaluation             | `((backup_count=5+3))` → Sets backup_count to 8              |
| `echo $((expr))` | Output arithmetic result                   | `echo $((10-4))` → Outputs: 6 |                                   |                                                                 |
| `let "result=expr"`                                                                              | Alternative arithmetic evaluation | `let "file_count=5*4"` → Sets file_count to 20               |
| `expr $a + $b`                                                                                   | Traditional arithmetic (legacy)   | `expr 5 + 3` → Outputs: 8 (spaces required around operators) |

### Array Handling

| Syntax                                                                                                                               | Description          | Example & Explanation                                               |
| ------------------------------------------------------------------------------------------------------------------------------------ | -------------------- | ------------------------------------------------------------------- |
| `arr=(val1 val2)`                                                                                                                  | Declare array        | `file_types=("txt" "doc" "pdf")` → Creates array with 3 elements |
| `${arr[0]}`      | Access array element by index              | `echo ${file_types[0]}` → Outputs: "txt" (indexing starts at 0) |                      |                                                                     |
| `${arr[@]}`      | Access all array elements                  | `echo ${file_types[@]}` → Outputs: "txt doc pdf"                |                      |                                                                     |
| `${#arr[@]}`     | Get array length                           | `echo ${#file_types[@]}` → Outputs: 3                           |                      |                                                                     |
| `arr[2]="new"`                                                                                                                     | Modify array element | `file_types[2]="xlsx"` → Changes third element to "xlsx"         |

---

## 3.4 Reading User Input

### Basic read Command

| Syntax                   | Description                     | Example & Explanation                                                                  |
| ------------------------ | ------------------------------- | -------------------------------------------------------------------------------------- |
| `read var`             | Read input into variable        | `read username` → Waits for user input, stores in $username                         |
| `read -p "Prompt" var` | Read with custom prompt         | `read -p "Enter backup directory: " backup_dir` → Shows prompt before reading input |
| `read -s var`          | Read sensitive input (silent)   | `read -s -p "Password: " pass` → Hides input as user types (for passwords)          |
| `read -a arr`          | Read multiple values into array | `read -a file_names` → Input "report.txt notes.txt" stored as array                 |

### Input Validation

| Technique                                                                                                                                 | Description               | Example & Explanation                                                                  |
| ----------------------------------------------------------------------------------------------------------------------------------------- | ------------------------- | -------------------------------------------------------------------------------------- |
| `if [ -z "$var" ]` | Check if input is empty                 | `if [ -z "$backup_dir" ]; then echo "Directory cannot be empty"; fi`   |                           |                                                                                        |
| `if [[ $var =~ ^[0-9]+$ ]]`                                                                                                             | Check if input is numeric | `if [[ $days =~ ^[0-9]+$ ]]; then echo "Valid number"; else echo "Numbers only"; fi` |
| `case $var in`   | Validate against specific values          | `case $confirm in [yY]*) ;; *) echo "Invalid"; esac` → Checks for Y/y |                           |                                                                                        |

---

## 3.5 Basic Operators

​<img src="./image/Module3/Basic Operators - visual selection.png" style="margin: auto; width: 500px; height: auto;"/>

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

​<img src="./image/Module3/Control Flow.png" alt="String Manipulation" style="margin: auto; width: 500px; height: auto;"/>

### Conditional Statements

| Construct                                                                                                                                                             | Description         | Example & Explanation                                                                                    |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------- | -------------------------------------------------------------------------------------------------------- |
| `if [ condition ]`                                                                                                                                                  | Simple if statement | `if [ -f "report.txt" ]; then echo "File exists"; fi`                                                  |
| `if-else`                                                                                                                                                           | If with else clause | `if [ -f "report.txt" ]; then echo "File exists"; else echo "File not found"; fi`                      |
| `if-elif-else`                                                                                                                                                      | Multiple conditions | `if [ $count -gt 10 ]; then echo "Many"; elif [ $count -gt 5 ]; then echo "Some"; else echo "Few"; fi` |
| `case $var in`   | Multi-branch conditional                    | `case $file_type in txt) echo "Text file" ;; csv) echo "Data file" ;; *) echo "Unknown" ;; esac` |                     |                                                                                                          |

### Looping Constructs

| Construct                 | Description               | Example & Explanation                                                                                |
| ------------------------- | ------------------------- | ---------------------------------------------------------------------------------------------------- |
| `for var in list`       | Iterate through list      | `for file in *.txt; do echo "Processing $file"; done` → Processes each .txt file                  |
| `for ((i=0; i<5; i++))` | C-style for loop          | `for ((i=1; i<=3; i++)); do echo "Backup $i"; done` → Outputs Backup 1, 2, 3                      |
| `while [ condition ]`   | Loop while condition true | `count=1; while [ $count -le 3 ]; do echo "Processing $count"; ((count++)); done` → Counts 1 to 3 |
| `until [ condition ]`   | Loop until condition true | `count=1; until [ $count -gt 3 ]; do echo "Processing $count"; ((count++)); done` → Counts 1 to 3 |
| `break`                 | Exit loop immediately     | `for i in {1..10}; do if [ $i -eq 5 ]; then break; fi; echo $i; done` → Prints 1-4                |
| `continue`              | Skip to next iteration    | `for i in {1..5}; do if [ $i -eq 3 ]; then continue; fi; echo $i; done` → Prints 1,2,4,5          |

---

## 3.7 Functions in Shell Scripting

​<img src="./image/Module3/Functions in Shell Scripting - visual selection.png "style="margin: auto; width: 500px; height: auto;"/>

### Function Definition

| Syntax                          | Description        | Example & Explanation                                                             |
| ------------------------------- | ------------------ | --------------------------------------------------------------------------------- |
| `name() { commands; }`        | Define function    | `create_backup() { mkdir -p $1; cp *.txt $1/; }` → Creates backup function     |
| `function name { commands; }` | Alternative syntax | `function show_help { echo "Usage: $0 [directory]"; }` → Creates help function |

### Parameter Passing

| Technique                                                                                                                                            | Description                  | Example & Explanation                                                     |
| ---------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------- | ------------------------------------------------------------------------- |
| `$1, $2, ...`                                                                                                                                      | Access positional parameters | `create_backup() { echo "Backing up to $1"; }` → $1 is first parameter |
| `$0`             | Function name (script name in main)         | `echo "Running: $0"` → Shows script name                                       |                              |                                                                           |
| `$#`             | Number of parameters                        | `count_params() { echo "Received $# parameters"; }` → Counts parameters passed |                              |                                                                           |
| `$@`             | All parameters as separate words             | `show_all() { echo "Params: $@"; }` → Shows all parameters                    |                              |                                                                           |
| `$*`             | All parameters as single word                | `show_all() { echo "Params: $*"; }` → Shows parameters as one string          |                              |                                                                           |

### Return Values

| Technique                                                                                                                                                      | Description                            | Example & Explanation                                                                   |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------- | --------------------------------------------------------------------------------------- |
| `return value`                                                                                                                                               | Exit function with status code (0-255) | `check_dir() { if [ -d "$1" ]; then return 0; else return 1; fi }` → 0=exists, 1=not |
| `echo value`                                                                                                                                                 | Output value to capture                | `get_date() { echo $(date +%Y%m%d); }` → Function outputs date in YYYYMMDD format    |
| `result=$(func)` | Capture function output                      | `backup_dir=$(get_date); echo "Backup to $backup_dir"` → Stores output in variable      |                                        |                                                                                         |
| `$?`             | Get last return status                       | `check_dir "backup"; if [ $? -eq 0 ]; then echo "Directory exists"; fi` → Checks return |                                        |                                                                                         |

---

## 3.8 Exit Codes and Status

### Exit Status Variable

| Variable                                                                                                                                               | Description    | Example & Explanation                                            |
| ------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------- | ---------------------------------------------------------------- |
| `$?`             | Exit status of last command                  | `ls /nonexistent; echo "Exit code: $?"` → Outputs non-zero if directory missing |                |                                                                  |
| `0`                                                                                                                                                  | Success status | `echo "Success"; echo "Exit code: $?"` → Outputs: 0 (success) |
| `1-255`                                                                                                                                              | Error status   | `false; echo "Exit code: $?"` → Outputs: 1 (general error)    |

### Exit Command

| Syntax     | Description                            | Example & Explanation                                                                       |
| ---------- | -------------------------------------- | ------------------------------------------------------------------------------------------- |
| `exit`   | Exit script with last command's status | `if [ ! -d "$backup_dir" ]; then echo "Directory missing"; exit; fi` → Exits if missing  |
| `exit N` | Exit with specific status code         | `if [ ! -f "$config_file" ]; then echo "Config missing"; exit 2; fi` → Exits with code 2 |

### Custom Exit Codes

| Code         | Meaning                     | Example & Explanation                                             |
| ------------ | --------------------------- | ----------------------------------------------------------------- |
| `0`        | Success                     | `exit 0` → Script completed successfully                       |
| `1`        | General error               | `exit 1` → Generic error occurred                              |
| `2`        | Misuse of shell command     | `exit 2` → Command used incorrectly                            |
| `126`      | Command cannot execute      | `exit 126` → Permission problem or command not executable      |
| `127`      | Command not found           | `exit 127` → Command doesn't exist                             |
| `128+N`    | Fatal error with signal N   | `exit 130` → Script terminated by Ctrl+C (signal 2)            |
| Custom codes | Application-specific errors | `exit 100` → Custom error meaning "backup directory not found" |

---

## Putting It All Together: Bhanu's Automated Backup Script

​<img src="./image/Module3/code to image as a story flow creation - visual selection.png" style="display: block; margin: auto; width: 500px; height: 600px;" />


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

