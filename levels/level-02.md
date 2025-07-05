# Level 1 → 2: Dashed Filenames

## Objective
The password for the next level is stored in a file called `-` located in the home directory.

## Level Info
- **Username:** bandit1
- **Password:** ZjLjTmM6FvvyRnrb2rfNWOZOTa6ip5If
- **Host:** bandit.labs.overthewire.org
- **Port:** 2220

## Solution

### Step 1: Connect to the server
```bash
ssh -p 2220 bandit1@bandit.labs.overthewire.org
```

### Step 2: Check your current location
```bash
pwd
```
**Output:** `/home/bandit1`

### Step 3: List files in the directory
```bash
ls
```
**Output:** `-`

### Step 4: Read the file (using relative path)
```bash
cat ./-
```
**Output:** `263JGJPfgU6LtdEvgfWU1XP5yac29mFx`

## Complete Command Sequence
```bash
bandit1@bandit:~$ pwd
/home/bandit1
bandit1@bandit:~$ ls
-
bandit1@bandit:~$ cat ./-
263JGJPfgU6LtdEvgfWU1XP5yac29mFx
```

## The Problem with Dashed Filenames

When you try to use `cat -` directly:
```bash
bandit1@bandit:~$ cat -
# The command hangs waiting for input from stdin
```

**Why this happens:**
- In Unix/Linux, `-` is a special symbol meaning "standard input"
- Commands interpret `-` as "read from keyboard input" instead of a filename
- You need to tell the command that `-` is actually a filename

## Solutions

### Method 1: Relative Path (Recommended)
```bash
cat ./-
```

### Method 2: Absolute Path
```bash
cat /home/bandit1/-
```

### Method 3: Using Different Commands
```bash
more ./-
less ./-
head ./-
tail ./-
```

## Key Learning Points

- **Special characters**: Some characters have special meanings in the shell
- **Relative paths**: `./` means "current directory"
- **Standard input**: `-` typically represents stdin in Unix commands
- **Path specification**: Be explicit about file paths when dealing with special characters

## Common Mistakes

- **Using `cat -` directly**: This will hang waiting for keyboard input
- **Not understanding stdin**: The `-` symbol has special meaning in Unix
- **Forgetting the `./`**: You need to specify it's a file in the current directory

## Alternative Characters to Watch For

Other characters that can cause similar issues:
- Files starting with `-` (like this level)
- Files with spaces in names
- Files with special characters like `*`, `?`, `&`, etc.

## Next Steps

Use the password you found to connect to Level 2:
```bash
ssh -p 2220 bandit2@bandit.labs.overthewire.org
```

---

**Password for next level:** `263JGJPfgU6LtdEvgfWU1XP5yac29mFx`

## Notes

- This level teaches an important concept about special characters in Unix/Linux
- The `./` prefix is a common solution for files with problematic names
- Understanding stdin/stdout concepts is crucial for command-line mastery
- This technique will be useful in many real-world scenarios
