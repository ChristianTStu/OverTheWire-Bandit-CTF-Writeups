# Level 4 → 5: File Type Identification

## Objective
The password for the next level is stored in the only human-readable file in the `inhere` directory. Tip: if your terminal is messed up, try the "reset" command.

## Level Info
- **Username:** bandit4
- **Password:** 2WmrDFRmJIq3IPxneAaMGhap0pFhF3NJ
- **Host:** bandit.labs.overthewire.org
- **Port:** 2220

## Solution

### Step 1: Connect to the server
```bash
ssh -p 2220 bandit4@bandit.labs.overthewire.org
```

### Step 2: Check your current location and navigate
```bash
pwd
ls
cd inhere
```

### Step 3: List all files in the inhere directory
```bash
ls
```
**Output:** `-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09`

### Step 4: Check file types (Recommended method)
```bash
file ./-file*
```
**Output:**
```
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
```

### Step 5: Read the ASCII text file
```bash
cat ./-file07
```
**Output:** `4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw`

## Complete Command Sequence
```bash
bandit4@bandit:~$ pwd
/home/bandit4
bandit4@bandit:~$ ls
inhere
bandit4@bandit:~$ cd inhere
bandit4@bandit:~/inhere$ ls
-file00  -file01  -file02  -file03  -file04  -file05  -file06  -file07  -file08  -file09
bandit4@bandit:~/inhere$ file ./-file*
./-file00: data
./-file01: data
./-file02: data
./-file03: data
./-file04: data
./-file05: data
./-file06: data
./-file07: ASCII text
./-file08: data
./-file09: data
bandit4@bandit:~/inhere$ cat ./-file07
4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
```

## Alternative Method: Manual Checking

If you want to check each file manually:
```bash
cat ./-file00  # Shows binary data like: ��_��+J��2X1�M�O�g���Y����d�Ŧj
cat ./-file01  # More binary data
cat ./-file02  # More binary data
# ... continue until you find the readable one
cat ./-file07  # This one shows the password!
```

## Understanding File Types

### The `file` Command
- **Purpose**: Determines file type based on content, not extension
- **Usage**: `file filename` or `file *` for multiple files
- **Advantage**: Quick way to identify file types without opening them

### Common File Types You'll See:
- **ASCII text**: Human-readable text file
- **data**: Binary data (not human-readable)
- **executable**: Binary executable file
- **directory**: Folder/directory
- **symbolic link**: Link to another file

## Why Use `./` with Dashed Filenames?

Remember from Level 2: filenames starting with `-` need special handling because the shell interprets `-` as command options.

## Key Learning Points

- **File type identification**: Use `file` command before opening unknown files
- **Binary vs text**: Not all files are human-readable
- **Wildcards**: `*` matches multiple files (`./-file*` matches all files starting with `-file`)
- **Efficiency**: Check file types first to avoid opening binary files

## What Happens When You Open Binary Files?

Opening binary files with `cat` can:
- Display garbled characters
- Mess up your terminal display
- Trigger terminal beeps or strange behavior

**Solution**: Use the `reset` command to fix terminal issues:
```bash
reset
```

## Useful File Commands

| Command | Purpose |
|---------|---------|
| `file filename` | Show file type |
| `file *` | Show types of all files |
| `file ./-file*` | Show types of files with dashed names |
| `reset` | Reset terminal if display gets corrupted |

## Best Practices

1. **Always check file types** before opening unknown files
2. **Use wildcards** to check multiple files efficiently
3. **Keep `reset` in mind** if your terminal gets messed up
4. **Don't manually check** every file when you can use `file` command

## Next Steps

Use the password you found to connect to Level 5:
```bash
ssh -p 2220 bandit5@bandit.labs.overthewire.org
```

---

**Password for next level:** `4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw`

## Notes

- This level teaches the crucial skill of file type identification
- The `file` command is essential for security analysis and system administration
- Understanding binary vs text files prevents terminal issues
- Wildcards (`*`) are powerful tools for handling multiple files efficiently
