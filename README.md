# 🐚 My Custom Shell

This is a custom shell I built from scratch in **C**.  
It mimics many of the core functionalities of **bash**, including foreground/background processes, I/O redirection, piping, and signal handling — while also adding several **unique custom commands**.

---

## 🚀 Getting Started

### 1. Compile the Shell
To create the executable, run:
```bash
make
```

### 2. Run the Shell
Execute the compiled program:
```bash
./a.out
```

### 3. Clean Up
To remove the executable and temporary files:
```bash
make clean
```

---

## ✨ Core Features

### 🧭 Custom Prompt
An informative prompt showing:
```
username@hostname:~relative/path
```
- Displays execution time for slow commands (>2s)  
- Uses `*` to indicate active background jobs  

### ⚙️ System Commands
Execute any standard system command (`ls`, `grep`, `sleep`, etc.) just like in bash.

### 🧵 Background Processes
Run commands in the background using `&`.

### 🔗 Command Chaining
Combine multiple commands:
- Sequential: `;`
- Parallel (background): `&`

### 📤 I/O Redirection
Full support for:
- Input: `<`
- Output: `>`
- Append: `>>`

### 🧩 Piping
Chain multiple commands using `|`.

### 🧠 Job Control
| Shortcut | Description |
|-----------|-------------|
| **Ctrl+C** | Interrupts current foreground process (`SIGINT`) |
| **Ctrl+Z** | Stops and backgrounds the current process (`SIGTSTP`) |
| **Ctrl+D** | Exits the shell cleanly |
| **fg <pid>** | Brings background job to foreground |
| **bg <pid>** | Resumes a stopped background job |

---

## 🛠️ Custom Commands

### 🔹 `warp <path>`
- Equivalent to `cd`  
- Supports `~` (home), `-` (previous directory), and relative/absolute paths  
- Example:  
  ```bash
  warp ~/projects
  ```

---

### 🔹 `peek <flags> <path>`
- Equivalent to `ls`  
- Supports:
  - `-l`: Long listing  
  - `-a`: Show hidden files  
- Colors:
  - Blue → directories  
  - Green → executables  
  - White → files  
- Example:  
  ```bash
  peek -la .
  ```

---

### 🔹 `seek <flags> <search> <target_dir>`
Search for files or directories within a target directory.  
Flags:
- `-f`: Search files only  
- `-d`: Search directories only  
- `-e`: If exactly one match found, `warp` (if dir) or print contents (if file)  

Example:
```bash
seek -f "README.md" .
```

---

### 🔹 `pastevents`
Command history manager (stores last 15 commands).

- `pastevents` → Display history  
- `pastevents execute <index>` → Re-run command at index  
- `pastevents purge` → Clear history  

---

### 🔹 `iMan <command_name>`
Fetches and prints the **man page** for a command from **man.he.net**, showing:
- Name
- Synopsis
- Description  

Example:
```bash
iMan grep
```

---

### 🔹 `proclore <pid>`
Shows detailed process info:
- PID  
- Status  
- Process group  
- Virtual memory  
- Executable path  

If no PID is given, shows info for the shell itself.

---

### 🔹 `activities`
Lists all background processes:
- PID  
- Command name  
- Current state (Running/Stopped)

---

### 🔹 `ping <pid> <signal_number>`
Sends a specific signal to a process.  
Example:
```bash
ping 12345 9
```

---

### 🔹 `neonate -n <time>`
Prints PID of the **most recently created process** every `<time>` seconds (default 1s).  
Press `x` to stop.  

---

### 🔹 `exit`
Terminates all background processes and exits the shell cleanly.

---

## 💡 Unique Design Choices

- **Smart Parsing:** Handles double quotes (`"..."`) so commands like `echo "hello > world"` print literally.  
- **Normalized History:** `pastevents` stores canonical versions (e.g., `sleep 5` and `sleep "5"` are identical).  
- **Improved Piping:** Handles cases like `cmd1 | | cmd2` gracefully, treating the gap as a no-op.

---

## ⚠️ Known Limitations

- **Tokenization:** Cannot handle filenames/directories with spaces.  
- **Quotes:** Only double quotes (`"`) are supported, not single quotes (`'`).  
- **Backgrounding:** Custom commands (like `warp`, `peek`, etc.) cannot run in the background.

---

🧑‍💻 **Author:** Akshith Mavurapu , Varun Edachali
📍 **Project Type:** Custom Linux Shell (C)
