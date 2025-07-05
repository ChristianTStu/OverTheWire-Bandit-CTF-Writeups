# Level 3 → 4: Hidden Files

## Objective
The password for the next level is stored in a hidden file in the `inhere` directory.

## Level Info
- **Username:** bandit3
- **Password:** MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
- **Host:** bandit.labs.overthewire.org
- **Port:** 2220

## Solution

### Step 1: Connect to the server
```bash
ssh -p 2220 bandit3@bandit.labs.overthewire.org
```

### Step 2: Check your current location
```bash
pwd
```
**Output:** `/home/bandit3`

### Step 3: List directories
```bash
ls
```
**Output:** `inhere`

### Step 4: Navigate to the inhere directory
```bash
cd inhere
```

### Step 5: List files (no hidden files shown)
```bash
ls
```
**Output:** *(empty - no files shown)*

### Step 6: List all files including hidden ones
```bash
ls -a
```
**Output:** `.  ..  ...Hiding-From-You`

### Step 7: Read the hidden file
```bash
cat ./...Hiding-From-You
```
**Output:** `2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ`

## Complete Command Sequence
```bash
bandit3@bandit:~$ pwd
/home/bandit3
bandit3@bandit:~$ ls
inhere
bandit3@bandit:~$ cd inhere
bandit3@bandit:~/inhere$ ls
bandit3@bandit:~/inhere$ ls -a
.  ..  ...Hiding-From-You
bandit3@bandit:~/inhere$ cat ./...Hiding-From-You
2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
```

## Understanding Hidden Files

In Unix/Linux systems:
- **Hidden files** start with a dot (`.`)
- **Regular `ls`** doesn't show hidden files by default
- **`ls -a`** shows **a**ll files, including hidden ones

### What you see with `ls -a`:
- `.` = Current directory
- `..` = Parent directory  
- `...Hiding-From-You` = The actual hidden file

## Why Use `./` Before the Filename?

The filename `...Hiding-From-You` starts with multiple dots, which can be confusing to some commands. Using `./` makes it explicit that this is a file in the current directory.

## Common `ls` Options

| Command | Purpose |
|---------|---------|
| `ls` | List visible files and directories |
| `ls -a` | List **a**ll files (including hidden) |
| `ls -l` | **L**ong format (detailed info) |
| `ls -la` | Long format + all files |
| `ls -lah` | Long format + all files + **h**uman readable sizes |

## Alternative Commands to Find Hidden Files

```bash
# Show all files with details
ls -la

# Find files starting with dots
find . -name ".*" -type f

# Show only hidden files (excluding . and ..)
ls -A
```

## Key Learning Points

- **Hidden files concept**: Files starting with `.` are hidden by default
- **Directory navigation**: Use `cd` to move between directories
- **File discovery**: `ls -a` is essential for finding hidden content
- **Path specification**: Using `./` clarifies file location

## Common Mistakes

- **Forgetting `-a` flag**: Won't see hidden files with just `ls`
- **Not checking subdirectories**: The file isn't always in the home directory
- **Ignoring special characters**: Files can have unusual names like `...Hiding-From-You`

## Hidden Files in the Real World

Hidden files are commonly used for:
- **Configuration files**: `.bashrc`, `.vimrc`, `.gitconfig`
- **Application data**: `.ssh/`, `.cache/`
- **System files**: `.DS_Store` (macOS), `.thumbs.db` (Windows)

## Next Steps

Use the password you found to connect to Level 4:
```bash
ssh -p 2220 bandit4@bandit.labs.overthewire.org
```

---

**Password for next level:** `2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ`

## Notes

- This level introduces the important concept of hidden files in Unix/Linux
- The `ls -a` command is fundamental for system administration and security work
- Hidden files are often used to store configuration and sensitive data
- Understanding directory navigation with `cd` is essential for future levels
