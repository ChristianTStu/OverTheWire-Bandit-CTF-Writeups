# Level 5 → 6: Advanced File Search

## Objective
The password for the next level is stored in a file somewhere under the `inhere` directory and has all of the following properties:
- Human-readable
- 1033 bytes in size
- Not executable

## Level Info
- **Username:** bandit5
- **Password:** 4oQYVPkxZOOEOO5pTW81FB8j8lxXGUQw
- **Host:** bandit.labs.overthewire.org
- **Port:** 2220

## Solution

### Step 1: Connect and Navigate
```bash
ssh -p 2220 bandit5@bandit.labs.overthewire.org
pwd
ls
cd inhere
```

### Step 2: Explore the Directory Structure
```bash
ls
```
**Output:** 20 directories named `maybehere00` through `maybehere19`

### Step 3: Use Find Command to Search by Size
```bash
find . -size 1033c
```
**Output:** `./maybehere07/.file2`

### Step 4: Verify File Properties
```bash
# Check if it's human-readable
file ./maybehere07/.file2

# Check file permissions and size
ls -la ./maybehere07/.file2
```

### Step 5: Advanced Find Command (All Properties at Once)
```bash
find . -size 1033c ! -executable -exec file {} \; | grep "ASCII text"
```
**Output:** `./maybehere07/.file2: ASCII text, with very long lines (1000)`

### Step 6: Read the Password
```bash
cat ./maybehere07/.file2
```
**Output:** `HWasnPhtq9AVKe0dmk45nxy20cvUa6EG`

## Complete Command Sequence
```bash
bandit5@bandit:~$ pwd
/home/bandit5
bandit5@bandit:~$ ls
inhere
bandit5@bandit:~$ cd inhere
bandit5@bandit:~/inhere$ ls
maybehere00  maybehere02  maybehere04  maybehere06  maybehere08  maybehere10  maybehere12  maybehere14  maybehere16  maybehere18
maybehere01  maybehere03  maybehere05  maybehere07  maybehere09  maybehere11  maybehere13  maybehere15  maybehere17  maybehere19
bandit5@bandit:~/inhere$ find . -size 1033c
./maybehere07/.file2
bandit5@bandit:~/inhere$ file ./maybehere07/.file2
./maybehere07/.file2: ASCII text, with very long lines (1000)
bandit5@bandit:~/inhere$ ls -la ./maybehere07/.file2
-rw-r----- 1 root bandit5 1033 Apr 10 14:23 ./maybehere07/.file2
bandit5@bandit:~/inhere$ find . -size 1033c ! -executable -exec file {} \; | grep "ASCII text"
./maybehere07/.file2: ASCII text, with very long lines (1000)
bandit5@bandit:~/inhere$ cat ./maybehere07/.file2
HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
```

## Understanding the Find Command

### Basic Syntax
```bash
find [path] [options] [expression]
```

### Key Options Used
| Option | Purpose |
|--------|---------|
| `-size 1033c` | Find files exactly 1033 **c**haracters (bytes) |
| `! -executable` | Find files that are **NOT** executable |
| `-exec file {} \;` | Execute `file` command on each found file |

### Size Options in Find
- `c` = bytes (characters)
- `w` = words (2-byte units)
- `k` = kilobytes
- `M` = megabytes
- `G` = gigabytes

## Alternative Approaches

### Method 1: Step-by-Step Verification
```bash
# Find by size first
find . -size 1033c

# Then check each result
file ./maybehere07/.file2
ls -la ./maybehere07/.file2
```

### Method 2: Combined Find Command
```bash
# Find files that match ALL criteria at once
find . -size 1033c ! -executable -type f -exec file {} \; | grep "ASCII text"
```

### Method 3: Multiple Criteria Find
```bash
# More comprehensive search
find . -type f -size 1033c ! -executable -readable
```

## Key Learning Points

- **Recursive search**: `find` searches through all subdirectories
- **Multiple criteria**: Combine different search parameters
- **Negation**: Use `!` to find files that DON'T match criteria
- **Execution**: `-exec` runs commands on found files
- **Pipe filtering**: Use `|` and `grep` to filter results

## Understanding File Permissions

When you see: `-rw-r----- 1 root bandit5 1033`
- First character (`-`): Regular file (not directory)
- Next 3 (`rw-`): Owner permissions (read, write, no execute)
- Next 3 (`r--`): Group permissions (read only)
- Last 3 (`---`): Other permissions (no access)

## Why This Approach is Efficient

Instead of manually checking 20 directories × multiple files each:
- **Manual approach**: Could take 20+ minutes
- **Find command**: Takes seconds
- **Scalable**: Works even with thousands of files

## Common Find Command Patterns

```bash
# Find by name
find . -name "*.txt"

# Find by size range
find . -size +1M -size -5M

# Find by modification time
find . -mtime -7

# Find and delete
find . -name "*.tmp" -delete
```

## Next Steps

Use the password you found to connect to Level 6:
```bash
ssh -p 2220 bandit6@bandit.labs.overthewire.org
```

---

**Password for next level:** `HWasnPhtq9AVKe0dmk45nxy20cvUa6EG`

## Notes

- This level introduces the powerful `find` command - essential for system administration
- Learning to combine multiple search criteria is crucial for efficiency
- The `find` command is one of the most important tools for security professionals
- Understanding file permissions helps with system security analysis
