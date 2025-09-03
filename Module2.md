# Module 2: Scripting Fundamentals

#### In computers, everything is represented as a files, and folders are just special files that contain references to other files.

<img src="./image/Module2/FolerVSfiles.png" alt="Understanding the Shell" style="display: block; margin: auto; width: 500px; height: auto;" />


Imagine your **computer** as a **magical kingdom**  where everything —

📂  **folders** , 📄  **files** , and ⚙️ **programs** — is neatly arranged like a giant  **library** .

# GUI vs. CLI – Two Ways to Rule the Digital Kingdom

Every file has its exact home, like a map:

```
📂 C:
 └── 📂 Users
     └── 📂 app
         └── 📄 hello.txt
```

## GUI (Graphical User Interface) is like a with a colorful.

Want a new folder? 👉 Right-click → New Folder

Want to rename? 👉 Double-click, type, press Enter

Want to read a file? 👉 Double-click again

It’s simple, friendly, and visual — perfect when you’re learning or doing light tasks.

---

## CLI – The Powerful

CLI (Command Line Interface) is the wise who doesn’t waste time flipping through pages.
Instead, he speaks in precise incantations (commands):

```
cd ~/Desktop
mkdir app
cd app
echo "Hello World!" > hello.txt
cat hello.txt
```

---

## (CLI > GUI)

 **Speed** → What takes 5 clicks in GUI can be 1 command in CLI.

 **Automation** → You can script repetitive tasks, saving hours of work.

 **Precision** → No guessing, no extra clicks — just exact instructions.

 **Remote Powe**r → Control servers and systems anywhere in the world with pure commands.

<img src="./image/Module2/GUI_CLI.png" alt="GUI VS CLI" style="display: block; margin: auto; width: 500px; height: auto;" />


| **Task**                   | **GUI (Windows / Linux Desktop)**                                 | **PowerShell**                                              | **Linux (Bash)**                   |
| -------------------------------- | ----------------------------------------------------------------------- | ----------------------------------------------------------------- | ---------------------------------------- |
| Go to Desktop                    | Double-click**Desktop** icon or open **Desktop** folder     | `cd ~/Desktop`                                                  | `cd ~/Desktop`                         |
| Create a folder `app`          | Right-click →**New → Folder** → type `app`                   | `mkdir app`                                                     | `mkdir app`                            |
| Open the folder `app`          | Double-click `app` folder                                             | `cd app`                                                        | `cd app`                               |
| Create a text file `Hello.txt` | Right-click →**New → Text Document** → rename to `Hello.txt` | `New-Item -Path "Hello.txt" -ItemType File`                     | `touch Hello.txt`                      |
| Add text inside the file         | Double-click → open in**Notepad/Text Editor** → type content    | `Set-Content -Path "Hello.txt" -Value "Hello from PowerShell!"` | `echo "Hello from Linux!" > Hello.txt` |
| View file content                | Double-click to open in**Notepad/Text Editor**                    | `Get-Content Hello.txt`                                         | `cat Hello.txt`                        |

---

# Basic Shell Commands Reference for Beginners

## 1. Working with Files and Directories

<img src="./image/Module2/Working with Files and Directories.png" alt="Working with Files and Directories" style="display: block; margin: auto; width: 500px; height: auto;" />

### File System Navigation
| Command          | Description                                  | Example & Explanation                                                                 |
|------------------|----------------------------------------------|----------------------------------------------------------------------------------------|
| `pwd`            | Show current directory path                 | `pwd` → Outputs: `/home/username/Documents` (where you are now)                        |
| `cd`             | Go to home directory                        | `cd` → Takes you to your personal folder (like `/home/username`)                       |
| `cd ..`          | Go up one directory level                    | `cd ..` → If you're in `/home/username/Documents`, takes you to `/home/username`       |
| `cd folder_name` | Go to a subdirectory                        | `cd Projects` → Enters the Projects folder inside current directory                    |
| `cd /path/to/dir`| Go to a specific directory (absolute path)   | `cd /var/log` → Takes you directly to the system logs folder                           |
| `cd -`           | Switch to previous directory                 | `cd -` → Toggle between two directories you've used recently                           |

### Listing and Managing Files
| Command          | Description                                  | Example & Explanation                                                                 |
|------------------|----------------------------------------------|----------------------------------------------------------------------------------------|
| `ls`             | List files in current directory             | `ls` → Shows basic file names like: `notes.txt report.jpg music/`                      |
| `ls -l`          | Detailed list with permissions, size, date  | `ls -l` → Shows: `-rw-r--r-- 1 user group 2048 May 15 10:30 notes.txt`                 |
| `ls -a`          | Show all files including hidden ones         | `ls -a` → Reveals hidden files like `.bashrc` and `.config`                            |
| `mkdir dir`      | Create new directory                        | `mkdir homework` → Creates a new folder named "homework"                               |
| `mkdir -p path`  | Create nested directories                   | `mkdir -p school/2023/math` → Creates all parent folders as needed                     |
| `cp src dest`    | Copy files or folders                       | `cp report.txt backup/` → Copies "report.txt" to the "backup" folder                   |
| `mv src dest`    | Move or rename files/folders                | `mv oldname.txt newname.txt` → Renames the file<br>`mv project.zip ~/Documents/` → Moves file |
| `rm file.txt`    | Delete files permanently                    | `rm temp.txt` → Deletes "temp.txt" (cannot be undone!)                                 |
| `rm -r dir`      | Delete folders and everything inside        | `rm -r old_projects/` → Deletes the entire folder and its contents                      |

### Finding Files
| Command          | Description                                  | Example & Explanation                                                                 |
|------------------|----------------------------------------------|----------------------------------------------------------------------------------------|
| `find . -name "*.txt"` | Find files by pattern              | `find . -name "*.txt"` → Finds all .txt files in current directory and subdirectories  |
| `find /home -type d` | Find directories by type           | `find /home -type d` → Finds all directories under /home                               |
| `find . -mtime -7` | Find files modified in last 7 days   | `find . -mtime -7` → Finds files modified in the past week                             |

## 2. String Manipulation

<img src="./image/Module2/String Manipulation.png" alt="String Manipulation" style="display: block; margin: auto; width: 500px; height: auto;" />

### Stream Editing with sed
| Command          | Description                                  | Example & Explanation                                                                 |
|------------------|----------------------------------------------|----------------------------------------------------------------------------------------|
| `sed 's/old/new/g' file` | Replace text in file          | `sed 's/hello/world/g' greeting.txt` → Replaces all "hello" with "world" in the file    |
| `sed -i 's/old/new/g' file` | Replace text in file (save changes) | `sed -i 's/error/warning/g' log.txt` → Replaces and saves changes to the file         |
| `sed '3d' file`   | Delete specific line                        | `sed '3d' data.txt` → Shows file content with line 3 removed                          |
| `sed '/pattern/d' file` | Delete lines matching pattern     | `sed '/temp/d' config.txt` → Shows file with lines containing "temp" removed           |

### Pattern Scanning with awk
| Command          | Description                                  | Example & Explanation                                                                 |
|------------------|----------------------------------------------|----------------------------------------------------------------------------------------|
| `awk '{print $1}' file` | Print first column of file       | `awk '{print $1}' names.txt` → Shows only the first word of each line                   |
| `awk -F: '{print $1}' file` | Print using colon separator   | `awk -F: '{print $1}' /etc/passwd` → Shows usernames from password file                 |
| `awk '{sum += $1} END {print sum}' file` | Sum values in column | `awk '{sum += $3} END {print sum}' grades.txt` → Adds all numbers in 3rd column        |
| `awk '/pattern/ {print}' file` | Print lines matching pattern | `awk '/error/ {print}' system.log` → Shows only lines containing "error"               |

### Text Processing Utilities
| Command          | Description                                  | Example & Explanation                                                                 |
|------------------|----------------------------------------------|----------------------------------------------------------------------------------------|
| `cut -d',' -f1 file` | Extract specific column (CSV)       | `cut -d',' -f1 data.csv` → Shows first column of comma-separated file                  |
| `cut -c1-5 file` | Extract specific characters                | `cut -c1-5 names.txt` → Shows first 5 characters of each line                          |
| `tr 'a-z' 'A-Z' < file` | Convert lowercase to uppercase  | `tr 'a-z' 'A-Z' < input.txt` → Shows file content in all uppercase                    |
| `tr -d '[:digit:]' < file` | Delete all digits              | `tr -d '[:digit:]' < data.txt` → Shows file with all numbers removed                  |

## 3. File Permissions and Ownership

<img src="./image/Module2/File Permissions and Ownership.png" alt="File Permissions and Ownership" style="display: block; margin: auto; width: 500px; height: auto;" />

### chmod Command
| Command          | Description                                  | Example & Explanation                                                                 |
|------------------|----------------------------------------------|----------------------------------------------------------------------------------------|
| `chmod 755 file` | Set permissions (rwxr-xr-x)                | `chmod 755 script.sh` → Makes script executable for everyone, writable only by owner   |
| `chmod u+x file` | Add execute permission for owner            | `chmod u+x myprogram` → Allows you to run the program                                  |
| `chmod go-w file` | Remove write permission for group/others | `chmod go-w important.txt` → Prevents group and others from modifying the file          |
| `chmod a=r file` | Set read-only for all users                | `chmod a=r readonly.txt` → Makes file readable by everyone, no other permissions        |

### chown Command
| Command          | Description                                  | Example & Explanation                                                                 |
|------------------|----------------------------------------------|----------------------------------------------------------------------------------------|
| `chown user file` | Change file owner                         | `chown john report.txt` → Makes John the owner of the file                              |
| `chown user:group file` | Change owner and group          | `chown mary:students project.doc` → Sets Mary as owner and "students" as group         |
| `chown -R user dir` | Change ownership recursively          | `chown -R john:users /home/john` → Changes ownership of all files in directory          |

### umask Settings
| Command          | Description                                  | Example & Explanation                                                                 |
|------------------|----------------------------------------------|----------------------------------------------------------------------------------------|
| `umask`          | Show current umask value                    | `umask` → Outputs: `0022` (default umask)                                              |
| `umask 027`      | Set new umask value                         | `umask 027` → Sets permissions so new files are rw-r----- (750) by default             |
| `umask -S`       | Show symbolic umask value                  | `umask -S` → Outputs: `u=rwx,g=rx,o=rx` (symbolic representation)                     |

## 4. Input and Output Redirection

<img src="./image/Module2/Input and Output Redirection.png" alt="Shell Scripting - Input and Output Redirection" style="display: block; margin: auto; width: 500px; height: auto;" />

### Standard Output Redirection
| Command          | Description                                  | Example & Explanation                                                                 |
|------------------|----------------------------------------------|----------------------------------------------------------------------------------------|
| `command > file` | Redirect output to file (overwrite)        | `ls -l > filelist.txt` → Saves directory listing to file, overwriting if exists       |
| `command >> file`| Redirect output to file (append)           | `date >> log.txt` → Appends current date/time to end of log file                       |
| `command | command` | Pipe output to another command      | `ls -l | grep ".txt"` → Lists files, then filters to show only .txt files              |

### Input Redirection
| Command          | Description                                  | Example & Explanation                                                                 |
|------------------|----------------------------------------------|----------------------------------------------------------------------------------------|
| `command < file` | Use file as input                          | `sort < names.txt` → Sorts lines from names.txt without modifying the file             |
| `command << EOF` | Here document (multi-line input)          | `cat << EOF > letter.txt` → Creates letter.txt with text until EOF marker              |

### Error Redirection
| Command          | Description                                  | Example & Explanation                                                                 |
|------------------|----------------------------------------------|----------------------------------------------------------------------------------------|
| `command 2> file`| Redirect error messages to file            | `ls /nonexistent 2> errors.txt` → Saves error message to file, not screen               |
| `command 2>> file`| Append errors to file                   | `find / -name "secret" 2>> search_errors.log` → Appends errors to log file              |
| `command &> file`| Redirect both output and errors          | `make &> build.log` → Saves all output and errors to build.log                         |
| `command > file 2>&1` | Redirect output and errors (alternative) | `ls -l /etc > listing.txt 2>&1` → Saves both normal output and errors to same file      |

## 5. Process Management
### Process Monitoring

<img src="./image/Module2/Process Management.png" alt="Understanding the Shell" style="display: block; margin: auto; width: 500px; height: auto;" />

| Command          | Description                                  | Example & Explanation                                                                 |
|------------------|----------------------------------------------|----------------------------------------------------------------------------------------|
| `ps aux`         | List all running processes                   | `ps aux` → Shows all programs running with details like CPU usage and PID              |
| `top`            | Monitor system processes in real-time       | `top` → Live updating list of processes (press 'q' to quit)                            |
| `htop`           | Interactive process viewer (if installed)   | `htop` → More user-friendly version of top with color coding                          |

### Process Control
| Command          | Description                                  | Example & Explanation                                                                 |
|------------------|----------------------------------------------|----------------------------------------------------------------------------------------|
| `kill PID`       | Stop a running process                      | `kill 1234` → Stops process with ID 1234 (find PID with `ps` or `top`)                  |
| `kill -9 PID`    | Force stop a process                        | `kill -9 1234` → Forces immediate termination of process 1234 (use as last resort)      |
| `killall name`   | Stop all processes with a given name        | `killall firefox` → Closes all Firefox windows                                         |
| `pkill pattern`  | Kill processes matching pattern             | `pkill -f "python script.py"` → Kills all processes running "python script.py"         |

### Background Jobs
| Command          | Description                                  | Example & Explanation                                                                 |
|------------------|----------------------------------------------|----------------------------------------------------------------------------------------|
| `command &`      | Run command in background                    | `sleep 60 &` → Starts a 60-second timer in background, returns prompt immediately     |
| `nohup command &`| Run command immune to hangups               | `nohup ./long_script.sh &` → Keeps script running even after you log out               |
| `jobs`           | List background jobs                        | `jobs` → Shows programs running in background with job numbers                         |
| `bg %1`          | Run a stopped job in background             | `bg %1` → Sends job number 1 to run in background                                      |
| `fg %1`          | Bring a background job to foreground        | `fg %1` → Brings job number 1 back to your active terminal                             |

## 6. Cron Jobs and Task Automation

<img src="./image/Module2/Cron Jobs and Task Automation.png" alt="Understanding the Shell" style="display: block; margin: auto; width: 450px; height: auto;" />

### Crontab Configuration
| Command          | Description                                  | Example & Explanation                                                                 |
|------------------|----------------------------------------------|----------------------------------------------------------------------------------------|
| `crontab -e`     | Edit user's cron jobs                       | `crontab -e` → Opens editor to schedule recurring tasks                                |
| `crontab -l`     | List user's cron jobs                       | `crontab -l` → Shows all scheduled tasks for current user                             |
| `crontab -r`     | Remove all cron jobs                        | `crontab -r` → Deletes all scheduled tasks (use with caution!)                         |
| `0 2 * * * /path/to/script` | Example cron entry          | `0 2 * * * /home/user/backup.sh` → Runs backup script every day at 2:00 AM            |

### One-Time Task Scheduling
| Command          | Description                                  | Example & Explanation                                                                 |
|------------------|----------------------------------------------|----------------------------------------------------------------------------------------|
| `at time`        | Schedule command to run once                | `at 10:30 PM` → Prompts for commands to run at 10:30 PM today                         |
| `atq`            | List pending at jobs                       | `atq` → Shows all scheduled one-time tasks with job numbers                           |
| `atrm jobnum`    | Remove a scheduled at job                  | `atrm 3` → Cancels job number 3 from the at queue                                     |
| `echo "command" | at now + 1 hour` | Schedule command in 1 hour | `echo "notify-send 'Meeting soon'" | at now + 1 hour` → Shows notification in 1 hour |

### Systemd Timers
| Command          | Description                                  | Example & Explanation                                                                 |
|------------------|----------------------------------------------|----------------------------------------------------------------------------------------|
| `systemctl list-timers` | List active systemd timers       | `systemctl list-timers` → Shows all active timers and when they'll next run            |
| `systemctl start timer` | Start a systemd timer             | `systemctl start backup.timer` → Manually starts the backup timer                      |
| `systemctl enable timer` | Enable timer at boot             | `systemctl enable weekly-report.timer` → Ensures timer runs automatically after reboot  |
| `systemctl status timer` | Check timer status               | `systemctl status cleanup.timer` → Shows whether timer is active and when it last ran   |

## 7. Working with Logs

<img src="./image/Module2/Working with Logs.png" alt="Understanding the Shell" style="display: block; margin: auto; width: 500px; height: auto;" />

### Log Monitoring
| Command          | Description                                  | Example & Explanation                                                                 |
|------------------|----------------------------------------------|----------------------------------------------------------------------------------------|
| `tail -f logfile` | Monitor log file in real-time             | `tail -f /var/log/syslog` → Shows new log entries as they appear                       |
| `tail -n 100 logfile` | Show last 100 lines of log          | `tail -n 100 /var/log/auth.log` → Shows most recent 100 authentication log entries     |
| `tail -f logfile | grep pattern` | Monitor for specific pattern | `tail -f /var/log/nginx/access.log | grep "404"` → Shows only 404 errors in real-time |

### Log Filtering
| Command          | Description                                  | Example & Explanation                                                                 |
|------------------|----------------------------------------------|----------------------------------------------------------------------------------------|
| `grep pattern logfile` | Search for pattern in log          | `grep "error" /var/log/syslog` → Shows all lines containing "error"                    |
| `grep -i pattern logfile` | Case-insensitive search         | `grep -i "warning" /var/log/messages` → Finds "warning", "Warning", "WARNING", etc.    |
| `grep -v pattern logfile` | Exclude lines with pattern        | `grep -v "debug" /var/log/app.log` → Shows all lines except those containing "debug"    |
| `grep -C 3 pattern logfile` | Show context lines (3 before/after) | `grep -C 3 "failed" /var/log/auth.log` → Shows failed logins with surrounding context |

### Log Parsing with awk
| Command          | Description                                  | Example & Explanation                                                                 |
|------------------|----------------------------------------------|----------------------------------------------------------------------------------------|
| `awk '{print $4}' logfile` | Extract specific column           | `awk '{print $4}' /var/log/nginx/access.log` → Shows IP addresses from access log     |
| `awk '/pattern/ {count++} END {print count}' logfile` | Count pattern matches | `awk '/error/ {count++} END {print count}' app.log` → Counts total error occurrences  |
| `awk '$NF > 500 {print}' logfile` | Filter by numeric condition | `awk '$NF > 500' response_times.log` → Shows lines where last field > 500ms           |
| `awk -F: '{print $1}' logfile | Parse using colon separator   | `awk -F: '{print $1}' /var/log/auth.log` → Extracts usernames from authentication log  |

## 8. Additional Useful Commands


### Help and Documentation
| Command          | Description                                  | Example & Explanation                                                                 |
|------------------|----------------------------------------------|----------------------------------------------------------------------------------------|
| `man command`    | Open manual page for a command              | `man grep` → Shows detailed documentation for the `grep` command (press 'q' to exit)   |
| `command --help` | Get quick help for a command                | `ls --help` → Shows common options and usage examples for `ls`                        |
| `info command`   | View detailed info documentation            | `info coreutils` → Shows in-depth documentation for core utilities                     |
| `whatis command` | Get brief description of a command         | `whatis cd` → Outputs: "cd - change the working directory"                            |
| `apropos topic`  | Find commands related to a topic            | `apropos "list files"` → Shows commands related to listing files                       |

### Command History and Shortcuts
| Command          | Description                                  | Example & Explanation                                                                 |
|------------------|----------------------------------------------|----------------------------------------------------------------------------------------|
| `history`        | Show your command history                   | `history` → Lists your recent commands with numbers                                    |
| `!n`             | Re-run command number n from history        | `!42` → Re-executes the 42nd command in your history                                   |
| `!!`             | Re-run your last command                    | `!!` → Repeats the exact command you just ran                                          |
| `Ctrl+R`         | Search through command history              | `Ctrl+R` then type "grep" → Finds your last command containing "grep"                  |
| `Ctrl+C`         | Cancel current command                      | `Ctrl+C` → Stops a running command (like a long search)                                |
| `Ctrl+Z`         | Pause current command                       | `Ctrl+Z` → Suspends a process so you can do something else (use `fg` to resume)        |
| `Tab`            | Auto-complete file/directory names          | `cd Doc<Tab>` → Automatically completes to `cd Documents/` if unique                    |