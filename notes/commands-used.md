# Phase 1: Server Baseline Assessment(Task 1: Inspect the Linux Server)

## Objective

Inspect the Linux server to gather baseline system information before making any configuration changes.

## Commands Used

- `uname -a` -  Provides the Kernel version and other details
- `cat /etc/os-release` -  Provides the OS distribution information
- `whoami` - Provides the current user information
- `cat /proc/cpuinfo` -  Provides CPU information
- `free -h` -  Provides memory usage information
- `df -h` - Provides the disk usage information
- `htop` - Provides live running processes information
- `sudo ss -tulnp` - Provides network inforamtion of listening ports

## Verification

Verified the operating system, kernel version, CPU, memory, disk usage, running processes, and listening network ports.

### Document: Screenshots

<img width="1440" height="900" alt="Screen Shot 2026-07-21 at 9 21 37 AM" src="https://github.com/user-attachments/assets/9791d1e8-3f90-430c-bd7d-dbedaadc0ef9" />
<img width="1440" height="900" alt="Screen Shot 2026-07-21 at 9 22 10 AM" src="https://github.com/user-attachments/assets/d3e73c56-0b4b-44ec-81ac-38cc92c0cd42" />
<img width="1440" height="900" alt="Screen Shot 2026-07-21 at 9 22 24 AM" src="https://github.com/user-attachments/assets/fe3b1e10-427c-4e77-97d8-84eb5a78b536" />

## Lessons Learned

- `uname` provides kernel information.
- `/etc/os-release` provides distribution details.
- `df` reports filesystem usage.
- `htop` is useful for monitoring system resources in real time.
  
---
# Phase 2: User and Access Management(Task 2: Create Development Users)

### Objective

Create individual Linux user accounts for a development team and configure them for basic access.

### Scenario

A new development team is joining the project. Each team member requires a dedicated Linux account to securely access the server.

### Requirements

Create the following users:

```
developer1
developer2
tester1
```

Ensure each user:

- Has a home directory
- Can successfully log in (or has a password configured if applicable)
- Is assigned to the appropriate defualt group(s)

### Verification

Confirm that:

- All user accounts exist
- Home directories have been created
- Default Group memberships are configured correctly

### Documentation

After completing the task, include:

## Commands used

- Creates users named developer1/2 and tester1 with home directories and  - Set password for the above created users
  ```
    useradd -m developer1
    passwd
    
    useradd -m developer2
    passwd 
    
    useradd -m tester1
    passwd 
  ```
  
## Verification steps
 - `cat /etc/passwd` - Shows the creation of users
 - `cat /etc/group` OR `groups developer1 && groups developer2 && groups tester1` - Shows the creation of respective groups
   
## Screenshot(s)

<img width="1207" height="367" alt="groups" src="https://github.com/user-attachments/assets/00a9ccf2-7c15-437c-a6a1-4f05ead783d8" />
<img width="1140" height="236" alt="usersadded" src="https://github.com/user-attachments/assets/11f703d5-e7f8-446c-bf6b-815e79353fd4" />

## Lessons learned

- I learned that creating a user with `useradd -m` automatically creates a home directory.
- I discovered that each new user is assigned a default primary group with the same name.
- I practiced verifying user creation instead of assuming the command succeeded.
- I learned the difference between creating a user and configuring their password.
---
