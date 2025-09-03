# Shell Scripting Curriculum

## Module 1: Introduction to Shell and Environment Setup

| Topic                                        | Subtopics                                                                                     |
| -------------------------------------------- | --------------------------------------------------------------------------------------------- |
| **1.1 What is Shell?**                 | • Bash, Zsh, Ksh, etc.<br />  • Shell history and evolution                                 |
| **1.2 Shell vs Terminal vs Bash**      | • Understanding the differences<br />• When to use each component                           |
| **1.3 Installing and Setting up Bash** | • Linux on AWS EC2 setup<br />• Environment configuration<br />• Basic shell customization |



## Module 2: Intermediate Scripting Techniques

| Topic                                            | Subtopics                                                                                                                               |
| ------------------------------------------------ | --------------------------------------------------------------------------------------------------------------------------------------- |
| **2.1 Working with Files and Directories** | •`ls`, `cp`, `mv`, `mkdir`<br />• `find` command <br />• File system navigation                                            |
| **2.2 String Manipulation**                | •`sed` for stream editing <br />• `awk` for pattern scanning <br />• `cut` and `tr` utilities                                |
| **2.3 File Permissions and Ownership**     | •`chmod` command <br />• `chown` command <br />• `umask` settings                                                              |
| **2.4 Input and Output Redirection**       | •`>` and `>>` redirection<br />• `<` input redirection <br />• `2>` and `&>` error redirection                             |
| **2.5 Process Management**                 | •`ps` and `top` commands<br />• `kill` command<br />• `nohup` and background jobs <br />• `jobs`, `fg`, `bg` commands |
| **2.6 Cron Jobs and Task Automation**      | •`crontab -e` configuration <br />• `at` command <br />• `systemd` timers                                                      |
| **2.7 Working with Logs**                  | •`tail -f` for monitoring <br />• `grep` for filtering <br />• `awk` for log parsing                                           |


## Module 3: Basic Scripting Skills

| Topic                                         | Subtopics                                                                                                                                                                                                                                                               |
| --------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **3.1 Writing Your First Shell Script** | • Creating .sh files<br />• Shebang `#!/bin/bash`• Basic script structure                                                                                                                                                                                          |
| **3.2 Executing Scripts**               | •`chmod +x script.sh<br>`• `./script.sh` execution <br />• `bash script.sh` execution <br />• [Execution Methods Guide](https://www.notion.so/x-scripts-sh-script-sh-bash-script-sh-25e02d139a5d80beadb3e1c8ee34dc33?pvs=21)                                     |
| **3.3 Variables and Data Types**        | • String variables<br />• Integer operations<br />• Array handling                                                                                                                                                                                                   |
| **3.4 Reading User Input**              | •`read` command usage<br />• Input validation <br />• Prompt customization                                                                                                                                                                                        |
| **3.5 Basic Operators**                 | • Arithmetic operators<br />• Relational operators <br />• Logical operators                                                                                                                                                                                         |
| **3.6 Control Flow**                    | •**Conditional Statements** <br />         - `if-else` constructs <br />         - `case` statements <br />• **Looping** <br />          - `for` loops <br />          - `while` loops <br />          - `until` loops |
| **3.7 Functions in Shell Scripting**    | • Function definition<br />• Parameter passing <br />• Return values                                                                                                                                                                                                 |
| **3.8 Exit Codes and Status**           | •`$?` variable <br />• `exit` command <br />• Custom exit codes                                                                                                                                                                                                  |



## Module 4: Advanced Scripting and Debugging

| Topic                                                    | Subtopics                                                                                                                  |
| -------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- |
| **4.1 Writing Robust Scripts with Error Handling** | •`set -e` for error detection <br />• `trap` command • `                                                            |
| **4.2 Debugging Techniques**                       | •`bash -x script.sh`• `set -x` and `set -v`<br />• Debugging best practices                                       |
| **4.3 Regular Expressions and Pattern Matching**   | •`grep -E` for extended regex <br />• `sed -r` for regex substitution <br />• Pattern matching techniques           |
| **4.4 Advanced File Processing**                   | • Advanced `awk` usage <br />• Complex `sed` operations <br />• `xargs`, `cut`, `paste` utilities             |
| **4.5 Networking with Shell Scripting**            | •`ping` for connectivity <br />• `curl` and `wget` for transfers <br />• `netstat` and `ss` for network stats |
| **4.6 Parallel Execution and Background Jobs**     | • Background job control (`&`)<br />• `wait` command <br />• `xargs -P` for parallelism                           |
| **4.7 Working with APIs in Shell Script**          | • cURL for REST API calls<br />• JSON parsing with shell tools <br />• Authentication methods                           |

## Module 5: Real-World Applications and Projects

| Topic                                       | Subtopics                                                                                                             |
| ------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| **5.1 Automating AWS Operations**     | • AWS CLI setup<br />• EC2 instance management <br />• S3 automation <br />• Security group configuration         |
| **5.2 Backup and Restore Automation** | • File backup strategies<br />• Database backups <br />• Automated restore procedures <br />• Backup verification |
| **5.3 Log Parsing and Analysis**      | • Log aggregation techniques<br />• Pattern extraction<br />• Report generation <br />• Anomaly detection         |

