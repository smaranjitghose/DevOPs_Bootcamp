# Module 5: Scripting Mastery - Building Resilient Automation Systems

## Bhanu's Challenge: From Process Master to Scripting Virtuoso

<img src="image/Module5/Scripting Mastery - Building Resilient Automation Systems.png" alt="Scripting Mastery - Building Resilient Automation Systems"/>

After mastering process management in Module 4, Bhanu became the go-to automation expert at the university. His systems ran smoothly, handling complex tasks with precision. But as the university's digital infrastructure grew, so did the complexity of Bhanu's scripts.

During the university's online registration day, a critical script failed unexpectedly. The system crashed, causing chaos for thousands of students trying to enroll. Bhanu was called to an emergency meeting with the IT director.

"Your automation systems work perfectly when conditions are ideal," the director said, "but they crumble under pressure. We need scripts that don't just work - scripts that survive."

Bhanu realized that writing scripts was no longer enough. He needed to build resilient systems that could handle errors, adapt to unexpected conditions, and recover gracefully. This was the next level of mastery - creating bulletproof automation that could withstand any challenge.

---

## 5.1 Writing Robust Scripts with Error Handling 

<img src="image/Module5/Writing Robust Scripts with Error Handling - visual selection.png" alt="Writing Robust Scripts with Error Handling - visual selection"/>

### Building Fault-Tolerant Systems

| Technique               | Description                          | Example & Explanation                                                                                 |
| ----------------------- | ------------------------------------ | ----------------------------------------------------------------------------------------------------- |
| `set -e`              | Exit immediately on any error        | `set -e` → Script stops at first error (like stopping at first sign of trouble)                    |
| `set -u`              | Treat unset variables as errors      | `set -u` → Prevents using undefined variables (like checking all equipment before use)             |
| `set -o pipefail`     | Ensure pipeline errors are caught    | `set -o pipefail` → If any command in pipeline fails, whole pipeline fails (team effort)           |
| `trap command signal` | Execute command when signal received | `trap 'echo "Error at line $LINENO"' ERR` → Catches errors and shows location (emergency response) |

### Practical Error Handling Examples

```bash
#!/bin/bash
# Robust script with comprehensive error handling

# Enable strict error handling
set -euo pipefail

# Error handling function
error_handler() {
    echo "ERROR: Script failed at line $1 with command '$2'"
    echo "System: $(uname -a)"
    echo "User: $(whoami)"
    echo "Directory: $(pwd)"
    exit 1
}

# Set up error trap
trap 'error_handler $LINENO "$BASH_COMMAND"' ERR

# Critical operation with error checking
backup_directory="/data/backups/$(date +%Y%m%d)"
echo "Creating backup in $backup_directory"

# Create directory with error handling
if ! mkdir -p "$backup_directory"; then
    echo "CRITICAL: Failed to create backup directory"
    exit 2
fi

# Copy files with error handling
if ! cp -r /important/data/* "$backup_directory/"; then
    echo "WARNING: Some files failed to copy, continuing..."
    # Log failed files but continue execution
    find /important/data -type f ! -exec test -e "$backup_directory/{}" \; -print >> failed_copies.log
fi

echo "Backup completed with status $?"
```

---

## 5.2 Debugging Techniques 

<img src="image/Module5/Writing Robust Scripts with Error Handling.png" alt="Finding and Fixing Issues Efficiently"/>

### Finding and Fixing Issues Efficiently

| Technique             | Description                            | Example & Explanation                                                                         |
| --------------------- | -------------------------------------- | --------------------------------------------------------------------------------------------- |
| `bash -x script.sh` | Execute script with debug output       | `bash -x myscript.sh` → Shows each command before execution (like watching a play-by-play) |
| `set -x`            | Enable debug mode within script        | `set -x` → Turns on debugging for specific section (spotlight on particular action)        |
| `set +x`            | Disable debug mode                     | `set +x` → Turns off debugging (end of spotlight)                                          |
| `set -v`            | Enable verbose mode (show input lines) | `set -v` → Shows script lines as read (showing the playbook)                               |
| `logger` command    | Send debug messages to system log      | `logger "Processing user data"` → Sends message to system log (official record)            |

### Debugging Best Practices

```bash
#!/bin/bash
# Script with built-in debugging capabilities

# Debug flag (set to 1 for debugging)
DEBUG=${DEBUG:-0}

# Debug function
debug() {
    if [[ $DEBUG -eq 1 ]]; then
        echo "[DEBUG $(date '+%Y-%m-%d %H:%M:%S')] $*" >&2
    fi
}

# Enable debugging if requested
if [[ $DEBUG -eq 1 ]]; then
    set -xv
fi

# Main script with debug statements
debug "Starting script with PID $$"
debug "User: $(whoami)"
debug "Arguments: $*"

# Critical operation with debugging
debug "Attempting to connect to database"
if ! db_connection=$(mysql -u user -ppass db -e "SHOW TABLES;" 2>/dev/null); then
    debug "Database connection failed"
    echo "ERROR: Database connection failed" >&2
    exit 1
fi

debug "Successfully connected to database"
debug "Found $(echo "$db_connection" | wc -l) tables"

# Conditional debugging for specific sections
debug "Entering data processing section"
for file in data/*.csv; do
    debug "Processing file: $file"
    # Process file...
done

debug "Script completed successfully"
```

---

## 5.3 Regular Expressions and Pattern Matching 

### Advanced Text Processing Techniques

| Technique           | Description                    | Example & Explanation                                                                     |
| ------------------- | ------------------------------ | ----------------------------------------------------------------------------------------- |
| `grep -E`         | Extended regular expressions   | `grep -E 'error                                                                           |
| `grep -o`         | Show only matching part        | `grep -o '[0-9]\+' data.txt` → Shows only numbers (extracting specific info)           |
| `sed -r`          | Extended regex in sed          | `sed -r 's/([A-Z]+) ([0-9]+)/\2 \1/' file.txt` → Swaps words and numbers (rearranging) |
| `awk '/pattern/'` | Pattern matching in awk        | `awk '/error/ {print $1, $4}' log.txt` → Shows first and fourth fields of error lines  |
| `[[ =~ ]]`        | Regex matching in conditionals | `if [[ "$input" =~ ^[0-9]+$ ]]; then` → Checks if input is numeric (validation)        |

### Practical Regex Examples

```bash
#!/bin/bash
# Advanced pattern matching examples

# Extract IP addresses from logs
echo "Extracting IP addresses from access logs..."
grep -oE '[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}\.[0-9]{1,3}' /var/log/nginx/access.log | sort | uniq > ip_addresses.txt

# Find and replace dates in ISO format
echo "Converting dates to MM/DD/YYYY format..."
sed -r 's/([0-9]{4})-([0-9]{2})-([0-9]{2})/\2\/\3\/\1/g' dates.txt > formatted_dates.txt

# Validate email addresses
validate_email() {
    local email=$1
    if [[ "$email" =~ ^[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,}$ ]]; then
        echo "Valid email: $email"
        return 0
    else
        echo "Invalid email: $email"
        return 1
    fi
}

# Process log entries with complex patterns
process_logs() {
    local log_file=$1
    echo "Processing log file: $log_file"
  
    # Extract error messages with timestamps
    awk '/ERROR/ {
        timestamp = $1 " " $2
        message = substr($0, index($0, "ERROR"))
        print timestamp " | " message
    }' "$log_file" > error_summary.txt
  
    # Count different types of warnings
    echo "Warning counts:"
    grep -oE 'WARNING: [A-Z_]+' "$log_file" | sort | uniq -c | sort -nr
}

# Extract and process URLs from text
extract_urls() {
    local text=$1
    echo "Extracting URLs from text..."
  
    # Find all URLs
    echo "$text" | grep -oE 'https?://[^[:space:]]+' | while read -r url; do
        # Extract domain
        domain=$(echo "$url" | sed -r 's|https?://([^/]+).*|\1|')
        echo "Found URL: $url (Domain: $domain)"
    done
}
```

---

## 5.4 Parallel Execution and Background Jobs 

### Maximizing Performance Through Concurrency

| Technique     | Description                          | Example & Explanation                                                           |
| ------------- | ------------------------------------ | ------------------------------------------------------------------------------- |
| `command &` | Run command in background            | `long_task &` → Starts task and returns prompt immediately (delegating work) |
| `wait`      | Wait for background jobs to complete | `wait` → Pauses until all background jobs finish (gathering team)            |
| `xargs -P`  | Run commands in parallel             | `cat files.txt                                                                  |
| `jobs -p`   | Show PIDs of background jobs         | `jobs -p` → Lists process IDs of background jobs (roster check)              |
| `disown`    | Remove job from shell's job table    | `disown %1` → Job continues after shell exits (setting free)                 |

### Parallel Processing Examples

```bash
#!/bin/bash
# Parallel processing demonstration

# Maximum parallel processes
MAX_PARALLEL=4

# Function to process a single file
process_file() {
    local file=$1
    echo "Processing $file in background..."
  
    # Simulate processing time
    sleep $((RANDOM % 5 + 1))
  
    # Create output file
    echo "Processed: $file at $(date)" > "processed_${file##*/}"
  
    echo "Completed processing $file"
}

# Process files in parallel using xargs
process_with_xargs() {
    echo "Processing files with xargs -P..."
  
    # Find files and process in parallel
    find data/ -type f -name "*.dat" | xargs -P $MAX_PARALLEL -I {} bash -c 'process_file "$1"' _ {}
  
    echo "All files processed with xargs"
}

# Process files in parallel using background jobs
process_with_background_jobs() {
    echo "Processing files with background jobs..."
  
    # Process each file in background
    for file in data/*.dat; do
        process_file "$file" &
    
        # Control number of parallel jobs
        if [[ $(jobs -r | wc -l) -ge $MAX_PARALLEL ]]; then
            wait -n  # Wait for any job to finish
        fi
    done
  
    # Wait for all remaining jobs
    wait
  
    echo "All files processed with background jobs"
}

# Parallel processing with named pipes
process_with_named_pipes() {
    echo "Processing files with named pipes..."
  
    # Create named pipe
    mkfifo work_pipe
  
    # Start worker processes
    for ((i=0; i<MAX_PARALLEL; i++)); do
        while read -r file; do
            process_file "$file"
        done < work_pipe &
    done
  
    # Feed files to workers
    find data/ -type f -name "*.dat" > work_pipe
  
    # Close pipe and wait
    exec 3>&-  # Close file descriptor
    wait
  
    # Clean up
    rm -f work_pipe
  
    echo "All files processed with named pipes"
}

# Main execution
echo "Starting parallel processing demonstration..."
echo "Maximum parallel processes: $MAX_PARALLEL"
echo ""

# Choose method
case ${1:-xargs} in
    xargs)
        process_with_xargs
        ;;
    background)
        process_with_background_jobs
        ;;
    pipes)
        process_with_named_pipes
        ;;
    *)
        echo "Usage: $0 {xargs|background|pipes}"
        exit 1
        ;;
esac

echo "Parallel processing completed!"
```

---

## Bhanu's Transformation: From Process Master to Scripting Virtuoso

After implementing these advanced techniques, Bhanu's automation systems became remarkably resilient. The university's critical systems now handled peak loads gracefully, errors were caught and resolved before they caused problems, and performance improved dramatically through parallel processing.

During the next major registration event, Bhanu's systems processed three times the normal load without a single failure. The IT director was impressed.

"What changed?" the director asked.

Bhanu smiled. "I stopped writing scripts that just work. I started building systems that survive. I learned to anticipate errors, debug efficiently, process complex patterns, and maximize performance through parallel execution."

The director nodded. "You've not just mastered scripting - you've mastered resilience. That's the difference between a good automation engineer and a great one."

Bhanu had completed his journey from a novice script writer to a true scripting virtuoso, capable of building automation systems that could withstand any challenge. His systems were no longer just functional - they were bulletproof.

### primary outcomes

1. **Robust Error Handling** (`set -e`, `trap`) → Build scripts that survive failures
2. **Effective Debugging** (`bash -x`, `set -x`) → Find and fix issues efficiently
3. **Advanced Pattern Matching** (`grep -E`, `sed -r`) → Process complex text patterns
4. **Parallel Processing** (`xargs -P`, background jobs) → Maximize performance



