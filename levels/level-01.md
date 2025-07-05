# Level 0 → 1: Reading Files

## Objective
Find the password for the next level stored in a file called `readme` located in the home directory.

## Level Info
- **Username:** bandit0
- **Password:** bandit0
- **Host:** bandit.labs.overthewire.org
- **Port:** 2220

## Solution

### Step 1: Connect to the server
```bash
ssh -p 2220 bandit0@bandit.labs.overthewire.org
```

### Step 2: Check your current location
```bash
pwd
```
**Output:** `/home/bandit0`

### Step 3: List files in the directory
```bash
ls
```
**Output:** `readme`

### Step 4: Read the file contents
```bash
cat readme
```
**Output:** `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`

## Complete Command Sequence
```bash
bandit0@bandit:~$ pwd
/home/bandit0
bandit0@bandit:~$ ls
readme
bandit0@bandit:~$ cat readme
ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
```

## Commands Explained

| Command | Purpose |
|---------|---------|
| `pwd` | **P**rint **W**orking **D**irectory - Shows your current location |
| `ls` | **L**i**s**t - Shows files and directories in current location |
| `cat` | Con**cat**enate - Displays file contents |

## Key Learning Points

- **Navigation awareness**: Always know where you are in the file system
- **File exploration**: Use `ls` to discover available files
- **File reading**: `cat` is the most common way to read text files
- **Home directory**: User directories are typically located in `/home/username`

## Alternative Commands

You could also use these commands to read the file:
```bash
more readme     # View file page by page
less readme     # Navigate through file content
head readme     # Show first 10 lines
tail readme     # Show last 10 lines
```

## Common Mistakes

- **Forgetting to check location**: Always verify you're in the right directory with `pwd`
- **Not listing files first**: Use `ls` to see what's available before trying to read files
- **Case sensitivity**: Linux is case-sensitive, so `readme` ≠ `README`

## Next Steps

Use the password you found to connect to Level 1:
```bash
ssh -p 2220 bandit1@bandit.labs.overthewire.org
```

---

**Password for next level:** `ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If`

## Notes

- This level introduces the fundamental Linux commands for file system navigation
- The `readme` file is a common convention for documentation
- These basic commands (`pwd`, `ls`, `cat`) are essential for all future levels
