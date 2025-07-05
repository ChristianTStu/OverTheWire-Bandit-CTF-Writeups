# Level 2 → 3: Spaces in Filenames

## Objective
The password for the next level is stored in a file called `spaces in this filename` located in the home directory.

## Level Info
- **Username:** bandit2
- **Password:** 263JGJPfgU6LtdEvgfWU1XP5yac29mFx
- **Host:** bandit.labs.overthewire.org
- **Port:** 2220

## Solution

### Step 1: Connect to the server
```bash
ssh -p 2220 bandit2@bandit.labs.overthewire.org
```

### Step 2: Check your current location
```bash
pwd
```
**Output:** `/home/bandit2`

### Step 3: List files in the directory
```bash
ls
```
**Output:** `spaces in this filename`

### Step 4: Read the file (using quotes)
```bash
cat "spaces in this filename"
```
**Output:** `MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx`

## Complete Command Sequence
```bash
bandit2@bandit:~$ pwd
/home/bandit2
bandit2@bandit:~$ ls
spaces in this filename
bandit2@bandit:~$ cat "spaces in this filename"
MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx
```

## The Problem with Spaces in Filenames

When you try to use `cat spaces in this filename` directly:
```bash
bandit2@bandit:~$ cat spaces in this filename
cat: spaces: No such file or directory
cat: in: No such file or directory
cat: this: No such file or directory
cat: filename: No such file or directory
```

**Why this happens:**
- The shell interprets spaces as argument separators
- `cat spaces in this filename` is seen as `cat` with 4 separate arguments
- The shell tries to find 4 different files: `spaces`, `in`, `this`, and `filename`

## Solutions

### Method 1: Double Quotes (Recommended)
```bash
cat "spaces in this filename"
```

### Method 2: Single Quotes
```bash
cat 'spaces in this filename'
```

### Method 3: Escaping Spaces
```bash
cat spaces\ in\ this\ filename
```

### Method 4: Tab Completion
```bash
cat sp<TAB>
# Shell will auto-complete and escape the filename
```

## Key Learning Points

- **Shell parsing**: The shell uses spaces to separate command arguments
- **Quoting**: Quotes tell the shell to treat the enclosed text as a single argument
- **Escaping**: Backslashes can escape individual special characters
- **Tab completion**: Most shells can auto-complete and properly escape filenames

## Comparison of Methods

| Method | Pros | Cons |
|--------|------|------|
| Double quotes `"..."` | Clean, handles most cases | Variables get expanded inside |
| Single quotes `'...'` | Literal interpretation | Can't contain single quotes |
| Escaping `\ ` | Precise control | Tedious for long filenames |
| Tab completion | Automatic, no mistakes | Requires interactive shell |

## Common Mistakes

- **Not using quotes**: Results in "No such file or directory" errors
- **Mixing quote types**: Don't start with `"` and end with `'`
- **Forgetting to escape**: When using backslashes, escape every space

## Best Practices

1. **Avoid spaces in filenames** when possible (use underscores or dashes)
2. **Use quotes consistently** when dealing with spaces
3. **Test with `ls`** to see the exact filename first
4. **Use tab completion** to avoid typing errors

## Next Steps

Use the password you found to connect to Level 3:
```bash
ssh -p 2220 bandit3@bandit.labs.overthewire.org
```

---

**Password for next level:** `MNk8KNH3Usiio41PRUEoDFPqfxLPlSmx`

## Notes

- This level teaches fundamental shell quoting concepts
- Understanding how the shell parses commands is crucial for advanced usage
- These techniques work for any command, not just `cat`
- Proper filename handling prevents many common scripting errors
