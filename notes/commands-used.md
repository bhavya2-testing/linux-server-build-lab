# Phase 1: Server Baseline Assessment(Task 1: Inspect the Linux Server)

## Objective

Inspect the Linux server to gather baseline system information before making any configuration changes.

### Commands Used

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

## Phase 3 — Task 3: Application File Security(Task 3: Application File Security)
Scenario

A development team has deployed an application directory on a Linux server.

The application contains different types of files:

Configuration files (developers can view and update)
Sensitive credentials (only the application owner should access)
Deployment scripts (must be executable)

Your job is to configure Linux permissions correctly.

### Objective
Create the file structure

/opt/application
│
├── config.txt
├── credentials.txt
└── deploy.sh
and have each of the file with sample content.

### Permission Requirements
config.txt
- Purpose: Application configuration that developers need to update.
- Requirements:
  - Owner → read/write
  - Group → read/write
  - Others → no access

credentials.txt
- Purpose: Sensitive application credentials.
- Requirements:
    - Only owner can read/write
    - Group has no access
    - Others have no access

deploy.sh
- Purpose: Deployment script.
- Requirements:
   - Owner can read/write/execute
   - Group can read/execute
   - Others can read/execute

### Ownership Requirements
 
### Create a scenario where:

Application owner = developer1
Development team group = developers

(You may need to create the group and users if they don't already exist from your previous task.)

The **directory** should belong to:

`developer1:developers`

Verification Requirements

You should verify:

1. Directory ownership
- Check:
   - /opt/application

2. File permissions

- Verify:
  - config.txt
  - credentials.txt
  - deploy.sh

4. Test access

- Test using:
  - developer1
  - developer2
  - tester1

4. Confirm:
  - Who can edit config.txt?
  - Who can access credentials.txt?
  - Who can execute deploy.sh?

### Commands Used

For user and password creation , see Phase 2

`groupadd developers` - create group named developers

`gpasswd -a developer1 developers` - add develeoper1 to group developers

`mkdir /opt/application` - creates the directory

`ls -ld /opt/application/` - list the directory details

`chgrp developers /opt/application/` - change the group of directory to developers

`chown developer1 /opt/application/` - change the owner of directory to developer1

`chown developer1:developers /opt/application/*` - change ownership of complete directory

`vim /opt/application/config.txt` - create a file config.txt

`vim /opt/application/credentials.txt` - create a file credentials.txt

`vim /opt/application/deploy.sh` - create d a file deploy.sh

`chmod 660 /opt/application/config.txt` - change file permission to 'rw-rw----'

`chmod 600 /opt/application/credentials.txt` - change file permission to 'rw-------'

`chmod 755 /opt/application/deploy.sh` - change file permission to 'rwxrw-rw-'


### Permission Configuration

### Verification
Test using:

developer1
developer2
tester1

Confirm:

Who can edit config.txt?  
Who can access credentials.txt?
Who can execute deploy.sh?

| User | config.txt | credentials.txt | deploy.sh |
|------|------------|-----------------|-----------|
| developer1 | Read / Write | Read / Write | Read / Write / Execute |
| developer2 | Read / Write | No Access | Read / Execute |
| tester1 | No Access | No Access | Read / Execute |

### Screenshots

<img width="1496" height="231" alt="adduser-to-group" src="https://github.com/user-attachments/assets/2d6b8e0e-f3ff-4856-865f-4ebdda146d7a" />
<img width="1187" height="161" alt="change-dir-group" src="https://github.com/user-attachments/assets/fd7d2000-b58c-47d0-ac5d-4fc3a60a0813" />
<img width="1438" height="295" alt="dir-details" src="https://github.com/user-attachments/assets/6bd3a236-c1e7-41d8-83e6-86d22bcd3763" />
<img width="329" height="295" alt="Screen Shot 2026-07-22 at 10 01 48 AM" src="https://github.com/user-attachments/assets/0fe10fa0-838b-44be-ad86-f6dfff726e33" />








### Lessons Learned
- Linux permissions control access through owner, group, and others.
- `chmod` changes permissions while `chown` changes ownership.
- Sensitive files should follow the principle of least privilege.
- Testing permissions with different users helps confirm security settings.
---

## Phase 4: Web Server Deployment and Service Management
Scenario - Your development team needs a web server to host a simple application landing page.

As the Linux administrator, your responsibilities are to:
- Install and configure Nginx
- Manage the service using systemctl
- Verify the application is accessible
- Troubleshoot common service issues

### Task 4: Deploy an Nginx Web Server

Objectives
- Install Nginx (if it's not already installed).
- Start the Nginx service.
- Enable Nginx to start automatically on boot.
- Verify the service is running.
- Verify that port 80 is listening.
- Replace the default web page with your own custom page.
- Verify the page using curl localhost.

### Commands Used
`systemctl status nginx` - Will tell the status of the service(if not installed ,says service not found)

`sudo apt upgrade` - Updates the local package index with the latest package information

`sudo apt install nginx` - Downloads and installs a specific software package by name.

`systemctl start nginx` - Starts the nginx service

`systemctk is-enabled nginx` - Confirms if Nginx to enabled to automatically start on boot.  

`systemctl status nginx` - Provide information about service with status and other details 

`sudo ss -tunlp | grep 80` - Confirms that nginx is listening to tcp at port 80

`vim /var/www/html/index.html` - Is the default page created by nginx service

`curl localhost` - Confirms if a web server or service is running locally on your own computer


### Verification

Nginx is installed.
Service is active.
Service is enabled.
Port 80 is listening.
Web page is accessible. TO DO - Add a cutome page to show project related content

### Screenshots

<img width="969" height="446" alt="systemctl-status" src="https://github.com/user-attachments/assets/759ee7c5-e26c-4c27-9ac3-b4a72f2e36a9" />
<img width="2003" height="479" alt="systemctl-status" src="https://github.com/user-attachments/assets/8492dd70-7d8e-43af-b4b7-07f61a0807b3" />
<img width="1323" height="851" alt="reload-nginx" src="https://github.com/user-attachments/assets/f36c0b6b-f802-4534-8d42-143b31adf9c7" />


### Lessons Learned

- Nginx serves content from `/var/www/html` by default.
- `systemctl reload` applies configuration or content changes without stopping the service.
- `curl localhost` is a quick way to verify a web server from the command line.

### Phase 5: Linux Logs & System Monitoring( Task 5: Investigate Linux System Logs)

### Scenario

You are the Linux administrator for a web server.

A developer reports:

> "Users are unable to access the application, and we also noticed several failed login attempts."

Your task is to investigate the Linux server using system logs and monitoring commands.

---

## Objectives

Investigate the server by answering the following questions:

### Authentication Logs

- Locate the Linux authentication log.
- Identify recent failed login attempts.
- Display only the latest failed login attempts.
- Count the total number of failed login attempts.

---

### Nginx Logs

Locate the Nginx log files.

Determine:

- Access log location
- Error log location

View the latest entries from both logs.

---

### Service Logs

Inspect the Nginx service logs using `journalctl`.

Determine:

- Is the service running normally?
- Were there any recent warnings or errors?
- When was the service last started or reloaded?

---

### System Monitoring

Collect the following system information:

- Current memory usage
- Current disk usage
- Running Nginx process
- Listening ports

---

## Verification

Verify that you can answer the following:

- Is Nginx currently running?
- Is the web server listening on port 80?
- Are authentication failures present?
- Are there any recent Nginx errors?
- Is the server running low on memory or disk space?

---

## Deliverables

Include the following sections in your README:

### Objective

Explain the purpose of investigating Linux logs and monitoring system health.

### Commands Used

Document every command used during the investigation.

### Findings

Summarize your observations, including:

- Authentication activity
- Nginx logs
- Service status
- Resource utilization

### Verification

Explain how you confirmed your findings.

### Screenshots

Include only meaningful screenshots, such as:

- Authentication log output
- Nginx service status
- `journalctl` output
- System monitoring commands

### Lessons Learned

Reflect on what you learned about:

- Linux log files
- Service troubleshooting
- System monitoring
- Using logs to diagnose issues

---

## Bonus Challenge

Simulate a small issue and investigate it.

Examples:

- Stop Nginx and observe the logs.
- Restart Nginx and identify the restart event in `journalctl`.
- Modify the web page and verify the service continues to function.
- Trigger a failed login attempt (if supported in the lab) and locate it in the authentication log.

Document:

- The issue you created.
- The commands used to investigate it.
- The resolution.
