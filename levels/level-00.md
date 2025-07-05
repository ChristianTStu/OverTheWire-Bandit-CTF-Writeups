# Level 0: SSH Connection

## Objective
Learn how to successfully SSH into the Bandit game server.

## Level Info
- **Host:** bandit.labs.overthewire.org
- **Port:** 2220
- **Username:** bandit0
- **Password:** bandit0

## Solution

### Step 1: Connect via SSH
```bash
ssh -p 2220 bandit0@bandit.labs.overthewire.org
```

### Step 2: Enter the password when prompted
```
bandit0@bandit.labs.overthewire.org's password: bandit0
```

## Command Breakdown

- `ssh`: Secure Shell command for remote login
- `-p 2220`: Specifies the port number (default SSH port is 22)
- `bandit0`: Username for this level
- `@`: Separator between username and hostname
- `bandit.labs.overthewire.org`: Server hostname

## What You'll See

After successful connection, you'll see something like:
```
bandit0@bandit:~$ 
```

This indicates you're logged in as `bandit0` on the `bandit` server in the home directory (`~`).

## Key Learning Points

- **SSH Basics**: Understanding how to connect to remote servers
- **Port Specification**: Using `-p` flag when SSH runs on non-standard ports
- **Authentication**: Basic password authentication

## Next Steps

Once connected, you're ready to proceed to [Level 1](level-01.md) where you'll find your first password file.

---

**Password for next level:** `bandit0` (This is just the connection password; Level 1 will have you find the actual first flag)

## Notes

- This is the entry point to the Bandit wargame
- The password `bandit0` is publicly known and used by everyone starting the game
- Each subsequent level will require you to find a new password to access the next level
- Always remember to SSH into the next level using the password you discover
