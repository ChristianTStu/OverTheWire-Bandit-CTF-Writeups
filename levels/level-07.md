# Level 6 → 7: Server-Wide File Search

## Objective
The password for the next level is stored **somewhere on the server** and has all of the following properties:
- Owned by user bandit7
- Owned by group bandit6
- 33 bytes in size

## Level Info
- **Username:** bandit6
- **Password:** HWasnPhtq9AVKe0dmk45nxy20cvUa6EG
- **Host:** bandit.labs.overthewire.org
- **Port:** 2220

## Solution

### Step 1: Connect and Analyze the Challenge
```bash
ssh -p 2220 bandit6@bandit.labs.overthewire.org
pwd
ls -la
```

**Key Observation:** The instructions state the password is stored "somewhere on the server" - not necessarily in the home directory like previous levels.

### Step 2: Use Find Command for Server-Wide Search
```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```
**Output:** `/var/lib/dpkg/info/bandit7.password`

### Step 3: Read the Password
```bash
cat /var/lib/dpkg/info/bandit7.password
```
**Output:** `morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj`

## Complete Command Sequence
```bash
bandit6@bandit:~$ find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
/var/lib/dpkg/info/bandit7.password
bandit6@bandit:~$ cat /var/lib/dpkg/info/bandit7.password
morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj
bandit6@bandit:~$
```

## Understanding the Find Command

### Command Breakdown
```bash
find / -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

| Component | Purpose |
|-----------|---------|
| `find` | The search command |
| `/` | Start search from root directory (entire server) |
| `-user bandit7` | Filter: files owned by user "bandit7" |
| `-group bandit6` | Filter: files owned by group "bandit6" |
| `-size 33c` | Filter: files exactly 33 bytes in size |
| `2>/dev/null` | Redirect error messages to trash (hide "Permission denied") |

### Why This Approach Works
- **Comprehensive search**: Searches the entire filesystem, not just home directory
- **Multiple criteria**: Combines all three required properties
- **Error filtering**: Hides permission errors to show only relevant results
- **Efficient**: Finds the file in seconds instead of manual searching

## Alternative Approaches (Less Efficient)

### Manual Directory Traversal
```bash
# This would be extremely time-consuming
cd /
ls -la
cd var
ls -la
cd lib
# ... continue through thousands of directories
```

### Home Directory Search (Incorrect)
```bash
# This would fail because the file isn't in the home directory
find . -user bandit7 -group bandit6 -size 33c
```

## Key Learning Points

- **Server-wide vs. local search**: Use `/` to search entire server, `.` for current directory
- **Multiple criteria filtering**: Combine `-user`, `-group`, and `-size` for precise searches
- **Error handling**: `2>/dev/null` is crucial for clean output when searching system directories
- **File location awareness**: Passwords can be anywhere on the system, not just user directories

## Understanding Error Redirection

### What `2>/dev/null` Does
- `2>` redirects error messages (stderr)
- `/dev/null` is like a "trash can" - discards anything sent to it
- Without this, you'd see hundreds of "Permission denied" errors

### Example Without Error Redirection
```bash
find / -user bandit7 -group bandit6 -size 33c
# Output would include:
# find: '/root': Permission denied
# find: '/home/bandit0': Permission denied
# ... hundreds of error messages
# /var/lib/dpkg/info/bandit7.password
```

## Common Find Command Patterns

```bash
# Find by multiple users
find / -user bandit7 -o -user bandit8

# Find files larger than specific size
find / -size +1M

# Find files modified in last 7 days
find / -mtime -7

# Find and execute command on results
find / -name "*.log" -exec ls -la {} \;
```

## File System Location Insight

The password was found in `/var/lib/dpkg/info/bandit7.password`:
- `/var/lib/`: System application data
- `dpkg/`: Debian package manager data
- `info/`: Package information files
- This shows passwords can be hidden in system directories

## Why Manual Search is Impractical

**Time Analysis:**
- **Manual approach**: Could take hours or days
- **Find command**: Takes seconds
- **Directories to check**: Thousands across the entire filesystem
- **Permission barriers**: Many directories are inaccessible

## Next Steps

Use the password to connect to Level 7:
```bash
ssh -p 2220 bandit7@bandit.labs.overthewire.org
```

---

**Password for next level:** `morbNTDkSW6jIlUc0ymOdMaLnOlFVAaj`

## Notes

- This level introduces **system-wide file searching** - essential for security analysis
- The `find` command is one of the most powerful tools for system administration
- Understanding error redirection improves command efficiency
- Real-world security often requires searching entire systems for specific files
- This technique is valuable for finding configuration files, logs, and other system resources
