My Custom Shell
This is a custom shell I built from scratch in C. It mimics many of the core functionalities of bash, including foreground/background processes, I/O redirection, piping, and signal handling, while also adding several unique custom commands.

🚀 Getting Started
1. Compile the Shell
To create the executable, run:

Bash

make
2. Run the Shell
Execute the compiled program:

Bash

./a.out
3. Clean Up
To remove the executable and temporary files:

Bash

make clean
✨ Core Features
Custom Prompt: An informative prompt that shows username@hostname:~relative/path. It also displays the execution time for slow commands (>2s) and uses a * to indicate active background jobs.

System Commands: Execute any standard system command (like ls, grep, sleep, etc.) just as you would in bash.

Background Processes: Run any system command in the background by appending &.

Command Chaining: Combine multiple commands on one line using ; (sequential execution) and & (parallel/background execution).

I/O Redirection: Full support for input/output redirection using <, >, and >>.

Piping: Chain multiple commands together using |.

Job Control:

Ctrl+C: Interrupts the current foreground process (SIGINT).

Ctrl+Z: Stops and backgrounds the current foreground process (SIGTSTP).

Ctrl+D: Logs out of the shell cleanly.

fg <pid>: Brings a background job to the foreground.

bg <pid>: Resumes a stopped background job.

🛠️ Custom Commands
I've built several custom commands to extend the shell's functionality:

warp <path>

My equivalent of cd. It changes the current working directory.

Supports ~ for home, - for the previous directory, and standard paths.

Example: warp ~/projects

peek <flags> <path>

My equivalent of ls. It lists files and directories.

Supports -l (long listing) and -a (show hidden files).

Directories are colored blue, executables green, and files white.

Example: peek -la .

seek <flags> <search> <target_dir>

Searches for files or directories within a target directory.

-f: Search for files only.

-d: Search for directories only.

-e: If exactly one match is found, warp to it (if a dir) or print its contents (if a file).

Example: seek -f "README.md" .

pastevents

My command history (stores the last 15 commands).

pastevents: Displays all commands from history.

pastevents execute <index>: Executes the command at the given (1-based) index.

pastevents purge: Clears all command history.

iMan <command_name>

Fetches the man page for a command directly from man.he.net using a GET request and prints its Name, Synopsis, and Description.

Example: iMan grep

proclore <pid>

Prints detailed information about a process, including its PID, status, process group, virtual memory, and executable path. If no pid is given, it describes the shell itself.

activities

Lists all background processes spawned by this shell, showing their PID, command name, and current state (Running/Stopped).

ping <pid> <signal_number>

Sends a specific signal to a given process.

Example: ping 12345 9 (sends SIGKILL)

neonate -n <time>

Prints the process ID of the most recently created process on the system every <time> seconds (default is 1s). Press x to stop.

exit

Terminates all background processes and exits the shell cleanly.

💡 Unique Design Choices
Smart Parsing: The shell intelligently handles double quotes ("), allowing for strings that contain special characters. For example, echo "hello > world" will print the literal string, not perform redirection.

Normalized History: pastevents stores a "canonical" version of commands. This means sleep 5 and sleep "5" are treated as the same command, making history more consistent and useful.

Improved Piping: Unlike bash, my shell handles continuous pipes (e.g., cmd1 | | cmd2) by treating the empty space as a "void" command, allowing the pipeline to continue.

⚠️ Known Limitations
Tokenization: My parser splits by spaces, so it cannot handle file or directory names that contain spaces.

Quotes: Only double quotes ("...") are supported for strings; single quotes ('...') are not.

Backgrounding: Custom commands (like warp, peek, etc.) cannot be run in the background with &.