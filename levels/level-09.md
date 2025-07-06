# Level 8 → 9: Finding Unique Lines with Sort and Uniq

## Objective
The password for the next level is stored in the file **data.txt** and is the only line of text that occurs only once

## Level Info
- **Username:** bandit8
- **Password:** dfwvzFQi4mU0wfNbFOe9RoWskMLg7eEc
- **Host:** bandit.labs.overthewire.org
- **Port:** 2220

## Solution

### Step 1: Connect and Explore
```bash
ssh -p 2220 bandit8@bandit.labs.overthewire.org
pwd
ls
```
**Output:** Confirms `data.txt` exists in the home directory

### Step 2: Understanding the Problem
The challenge requires finding a line that appears exactly once among potentially many duplicate lines.

### Step 3: Research Command Requirements
```bash
man uniq
```
**Key Discovery:** "Output the unique lines from a input or file. Since it does not detect repeated lines unless they are adjacent, we need to sort them first."

### Step 4: Execute Combined Command
```bash
sort data.txt | uniq --unique
```
**Output:** `4CKMh1JI91bUIZZPXDqGanal4xvAg0JM`

## Complete Command Sequence
```bash
bandit8@bandit:~$ sort data.txt | uniq --unique
4CKMh1JI91bUIZZPXDqGanal4xvAg0JM
bandit8@bandit:~$
```

## Understanding the Command Pipeline

### Command Breakdown
```bash
sort data.txt | uniq --unique
```

| Component | Purpose |
|-----------|---------|
| `sort data.txt` | Alphabetically sorts all lines in the file |
| `uniq --unique` | Shows only lines that appear exactly once |

### Why This Sequence Works
1. **Sort first**: Groups identical lines together
2. **Pipe output**: Sends sorted data to next command
3. **Filter unique**: Only shows lines with no duplicates

## Understanding the Uniq Command

### Basic Uniq Options
```bash
# Show only unique lines (appear once)
uniq --unique file.txt

# Show only duplicate lines  
uniq --repeated file.txt

# Count occurrences of each line
uniq --count file.txt

# Show all lines (default behavior)
uniq file.txt
```

### Why Sorting is Required
```bash
# Without sorting - INCORRECT
$ cat example.txt
apple
banana
apple
cherry
banana

$ uniq --unique example.txt
apple    # Wrong! This appears twice total
cherry
banana   # Wrong! This appears twice total
```

```bash
# With sorting - CORRECT
$ sort example.txt | uniq --unique
cherry   # Correct! Only appears once
```

## Alternative Approaches

### Method 1: Step-by-Step Approach
```bash
# First sort the file
sort data.txt > sorted_data.txt

# Then find unique lines
uniq --unique sorted_data.txt
```

### Method 2: Using Uniq with Count
```bash
# Count occurrences and find lines that appear once
sort data.txt | uniq -c | grep "^ *1 "
```

### Method 3: Using Awk (Advanced)
```bash
# Count occurrences and print lines that appear once
sort data.txt | uniq -c | awk '$1 == 1 {print $2}'
```

## Understanding Pipes in Linux

### What Pipes Do
- **Symbol**: `|`
- **Function**: Connects output of one command to input of another
- **Data flow**: Command1 → Pipe → Command2

### Common Pipe Patterns
```bash
# Count lines in a file
cat file.txt | wc -l

# Search and count
grep "pattern" file.txt | wc -l

# Sort and display top results
sort file.txt | head -10

# Multiple pipes
cat file.txt | grep "error" | sort | uniq -c
```

## File Structure Analysis

### Data.txt Contents (Conceptual)
```
password1
password2
password1
password3
password2
password4  # This appears only once
password1
password3
```

### After Sorting
```
password1
password1
password1
password2
password2
password3
password3
password4  # Still appears only once
```

### After Uniq --unique
```
password4  # Only this line appears exactly once
```

## Why This Method is Efficient

**Comparison Analysis:**
- **Manual approach**: Impossible with large files
- **Grep approach**: Would require knowing what to search for
- **Sort + Uniq**: Handles any file size automatically
- **Time complexity**: O(n log n) for sorting, O(n) for uniqueness check

## Command Efficiency Breakdown

| Step | Time Complexity | Memory Usage | Purpose |
|------|-----------------|--------------|---------|
| Sort | O(n log n) | O(n) | Group identical lines |
| Uniq | O(n) | O(1) | Filter unique occurrences |
| Pipe | O(1) | O(1) | Connect commands |

## Real-World Applications

### Log Analysis
```bash
# Find unique error messages
sort error.log | uniq --unique

# Find most common errors
sort error.log | uniq -c | sort -nr
```

### Data Deduplication
```bash
# Remove duplicate entries
sort data.csv | uniq > clean_data.csv

# Find duplicate entries
sort data.csv | uniq -d
```

### System Administration
```bash
# Find unique users in log files
cut -d' ' -f1 access.log | sort | uniq --unique

# Analyze unique IP addresses
grep "Failed login" auth.log | awk '{print $11}' | sort | uniq -c
```

## Problem-Solving Methodology

### Step-by-Step Analysis
1. **Identify requirement**: Find line that appears exactly once
2. **Research tools**: Understand `uniq` command requirements
3. **Plan approach**: Sort first, then filter unique
4. **Execute**: Use pipe to combine commands
5. **Verify**: Single result confirms success

### Key Learning Points
- **Read documentation**: Man pages provide crucial implementation details
- **Understand dependencies**: Some commands require specific input formats
- **Use pipes effectively**: Combine simple commands for complex tasks
- **Test understanding**: Verify why each step is necessary

## Common Pitfalls and Solutions

### Pitfall 1: Forgetting to Sort
```bash
# Wrong - may miss duplicates that aren't adjacent
uniq --unique data.txt

# Right - ensures all duplicates are detected
sort data.txt | uniq --unique
```

### Pitfall 2: Using Wrong Uniq Option
```bash
# Wrong - shows all non-consecutive duplicates
sort data.txt | uniq

# Right - shows only lines that appear exactly once
sort data.txt | uniq --unique
```

## Next Steps

Use the password to connect to Level 9:
```bash
ssh -p 2220 bandit9@bandit.labs.overthewire.org
```

---

**Password for next level:** `4CKMh1JI91bUIZZPXDqGanal4xvAg0JM`

## Notes

- This level introduces **data deduplication** and **pipeline processing** - essential for data analysis
- The combination of `sort` and `uniq` is one of the most powerful patterns in Linux
- Understanding command dependencies (sort before uniq) is crucial for reliable results
- Pipes enable complex data processing by chaining simple commands
- This technique is invaluable for log analysis, data cleaning, and system administration tasks
- Reading man pages and understanding command requirements prevents common mistakes
