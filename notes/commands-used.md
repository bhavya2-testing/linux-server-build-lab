# Phase 1: Server Baseline Assessment(Task 1: Inspect the Linux Server)

## Objective

Inspect the Linux server to gather baseline system information before making any configuration changes.

### Scenario 
>
>

--- 
### Commands Used

- `uname -a` -  Provides the Kernel version and other details
- `cat /etc/os-release` -  Provides the OS distribution information
- `whoami` - Provides the current user information
- `cat /proc/cpuinfo` -  Provides CPU information
- `free -h` -  Provides memory usage information
- `df -h` - Provides the disk usage information
- `htop` - Provides live running processes information
- `sudo ss -tulnp` - Provides network inforamtion of listening ports
---
## Verification

Verified the operating system, kernel version, CPU, memory, disk usage, running processes, and listening network ports.

---
### Document: Screenshots

<img width="1440" height="900" alt="Screen Shot 2026-07-21 at 9 21 37 AM" src="https://github.com/user-attachments/assets/9791d1e8-3f90-430c-bd7d-dbedaadc0ef9" />
<img width="1440" height="900" alt="Screen Shot 2026-07-21 at 9 22 10 AM" src="https://github.com/user-attachments/assets/d3e73c56-0b4b-44ec-81ac-38cc92c0cd42" />
<img width="1440" height="900" alt="Screen Shot 2026-07-21 at 9 22 24 AM" src="https://github.com/user-attachments/assets/fe3b1e10-427c-4e77-97d8-84eb5a78b536" />

--- 
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

> A new development team is joining the project. Each team member requires a dedicated Linux account to securely access the server.

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
---

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
--- 

## Verification steps
 - `cat /etc/passwd` - Shows the creation of users
 - `cat /etc/group` OR `groups developer1 && groups developer2 && groups tester1` - Shows the creation of respective groups
---

## Screenshots

<img width="1207" height="367" alt="groups" src="https://github.com/user-attachments/assets/00a9ccf2-7c15-437c-a6a1-4f05ead783d8" />
<img width="1140" height="236" alt="usersadded" src="https://github.com/user-attachments/assets/11f703d5-e7f8-446c-bf6b-815e79353fd4" />

---

## Lessons learned

- I learned that creating a user with `useradd -m` automatically creates a home directory.
- I discovered that each new user is assigned a default primary group with the same name.
- I practiced verifying user creation instead of assuming the command succeeded.
- I learned the difference between creating a user and configuring their password.
---

## Phase 3 — Task 3: Application File Security(Task 3: Application File Security)

### Objective
Create the file structure

/opt/application
│
├── config.txt
├── credentials.txt
└── deploy.sh
and have each of the file with sample content.

### Scenario

>A development team has deployed an application directory on a Linux server.
>The application contains different types of files:
>  - Configuration files (developers can view and update)
>  - Sensitive credentials (only the application owner should access)
>  - Deployment scripts (must be executable)

Your job is to configure Linux permissions correctly.

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

### Create a scenario where:

Application owner = developer1
Development team group = developers

(You may need to create the group and users if they don't already exist from your previous task.)

The **directory** should belong to:

`developer1:developers`

--- 
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
--- 

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

--- 

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

## Phase 4: Web Server Deployment and Service Management (Task 4: Deploy an Nginx Web Server)

### Objectives
- Install Nginx (if it's not already installed).
- Start the Nginx service.
- Enable Nginx to start automatically on boot.
- Verify the service is running.
- Verify that port 80 is listening.
- Replace the default web page with your own custom page.
- Verify the page using curl localhost.

### Scenario - Your development team needs a web server to host a simple application landing page.

 > As the Linux administrator, your responsibilities are to:
 > - Install and configure Nginx
 > - Manage the service using systemctl
 > - Verify the application is accessible
 > - Troubleshoot common service issues
  
---
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

---

### Screenshots

<img width="969" height="446" alt="systemctl-status" src="https://github.com/user-attachments/assets/759ee7c5-e26c-4c27-9ac3-b4a72f2e36a9" />
<img width="2003" height="479" alt="systemctl-status" src="https://github.com/user-attachments/assets/8492dd70-7d8e-43af-b4b7-07f61a0807b3" />
<img width="1323" height="851" alt="reload-nginx" src="https://github.com/user-attachments/assets/f36c0b6b-f802-4534-8d42-143b31adf9c7" />

--- 
### Lessons Learned

- Nginx serves content from `/var/www/html` by default.
- `systemctl reload` applies configuration or content changes without stopping the service.
- `curl localhost` is a quick way to verify a web server from the command line.
---

### Phase 5: Linux Logs & System Monitoring( Task 5: Investigate Linux System Logs)

## Objectives - Investigate the server by answering the following questions:

### Authentication Logs

- Locate the Linux authentication log.
- Identify recent failed login attempts.
- Display only the latest failed login attempts.
- Count the total number of failed login attempts.
  
### Scenario

You are the Linux administrator for a web server.
A developer reports:
> "Users are unable to access the application, and we also noticed several failed login attempts."
Your task is to investigate the Linux server using system logs and monitoring commands.

---

### Nginx Logs (Locate the Nginx log files)

- Determine:
  - Access log location
  - Error log location
  - View the latest entries from both logs.

---

### Service Logs (Inspect the Nginx service logs using `journalctl`)

- Determine:
  - Is the service running normally?
  - Were there any recent warnings or errors?
  - When was the service last started or reloaded?

---

### System Monitoring

- Collect the following system information.
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

### Commands Used

`ls /var/log/auth.log` - locate authentication log

`grep -i "failed" /var/log/auth.log | tail -10` - view latest failed login attempts

`grep -i "failed" /var/log/auth.log | wc -l` - count failed login attempts

`tail -20 /var/log/auth.log`  - View latest authentication log entries

`ls -l /var/log/nginx/` - locate log files

`tail -20 /var/log/nginx/access.log` -  view access log

`systemctl status nginx` - check service status

`free -h` -  system memory monitoring

`df -h` - disk monitoring

`pgrep -a nginx` - check running nginx process

`sudo ss -tulnp | grep :80` - listening port

---

### Screenshots

- Authentication log output
<img width="1002" height="627" alt="authentication-logs" src="https://github.com/user-attachments/assets/c29bbe1d-4461-4b01-9cef-31ce120996d2" />

- nginx logs
<img width="1002" height="441" alt="nginx-service-logs" src="https://github.com/user-attachments/assets/59810e1a-164f-445c-ac5d-a46d19446511" />

- System monitoring commands
<img width="1000" height="376" alt="system-monitoring" src="https://github.com/user-attachments/assets/72ff8858-0e6c-48e7-8ed9-57642fa66b32" />

---

### Lessons Learned

- Linux stores different types of logs in separate locations, making it easier to investigate authentication, service, and application-related events.
- `journalctl` provides a centralized way to view service logs and helps troubleshoot service startup, shutdown, and restart events.
- System monitoring commands such as `free`, `df`, `ps`, and `ss` provide a quick overview of the server's health and resource utilization.
- Reviewing logs before making configuration changes helps identify the root cause of issues instead of relying on assumptions.
- Combining log analysis with service status and system monitoring provides a structured approach to diagnosing Linux server problems.
  
---

# Phase 6: Logical Volume Manager (LVM) (Task 6: Configure and Manage Logical Volumes)

---

## Objectives

- Complete the following tasks:

### 1. Prepare a Virtual Disk - If using Killercoda or WSL without an extra disk, create a virtual disk image to simulate a new storage device.

---

### 2. Create a Physical Volume (PV)

- Initialize the new disk as an LVM Physical Volume.
- Verify the Physical Volume has been created successfully.
---

### 3. Create a Volume Group (VG)
 - Create a Volume Group named:

```
vg_data
```

 - Verify the Volume Group.

---

### 4. Create a Logical Volume (LV)

- Create a Logical Volume named:

```
lv_storage
```

- Use approximately 500 MB (or an appropriate size based on the available virtual disk).
- Verify the Logical Volume.

---

### 5. Create a Filesystem

- Format the Logical Volume with the ext4 filesystem.

- Verify the filesystem was created successfully.

---

### 6. Create a Mount Point

- Create the directory:

```
/mnt/storage
```

- Mount the Logical Volume.
- Verify that the filesystem is mounted.

---

### 7. Verify Storage

- Confirm:
  - Physical Volume
  - Volume Group
  - Logical Volume
  - Mounted filesystem
  - Available disk space

### Scenario

Your Linux server is running low on storage, and a new application requires additional disk space.

As the Linux administrator, you must configure a new Logical Volume Manager (LVM) storage stack, create a filesystem, mount it, and verify that it is available for use.

---

## Verification

- Verify each of the following:
  - Physical Volume exists.
  - Volume Group exists.
  - Logical Volume exists.
  - Filesystem is mounted.
  - Disk space is available.
  - Mount point is accessible.

---

### Commands Used

 - Document every command used during the exercise.
```
# Create a 1GB blank disk image
dd if=/dev/zero of=/tmp/disk1.img bs=1M count=1024

# Attach the image as a loop device
losetup -fP /tmp/disk1.img

# Confirm which loop device was assigned
losetup -a

sudo pvcreate /dev/loop0
sudo pvs

sudo vgcreate devops-vg /dev/loop0
sudo vgs

sudo lvcreate -L 500M -n lv_storage vg_data
sudo lvs

# Format with ext4 filesystem
sudo mkfs.ext4 /dev/devops-vg/lv_storage

# Create the mount point
sudo mkdir -p /mnt/lv_storage

# Mount the LV
sudo mount /dev/vg_data/lv_storage /mnt/lv_storage

# Verify
df -h /mnt/lv_storage

```

---

### Verification

Explain how you confirmed:

- PV creation - Used pvcreate with loop device name to create and pvs to verify it have been created
- VG creation - Used vgcreate with volume group name  and vgs to verify it have been created
- LV creation - Used lvcreate with logical voume name and lvs to verify it have been created
- Filesystem creation - Used lsblk -f to verify the filesystem creation
- Mount status - Used df -h command
- Disk availability - Used df -h command

---

### Screenshots

Include meaningful screenshots, such as:

- Physical Volume information/Volume Group information / Logical Volume information

<img width="1632" height="898" alt="volumes-info" src="https://github.com/user-attachments/assets/38be916f-7bc0-4a24-8fee-4254cb4681fd" />

- Mounted filesystem /  Disk usage

<img width="1234" height="623" alt="mount-info" src="https://github.com/user-attachments/assets/696f44e7-d3cd-414f-8517-d4d74d30fa36" />

---

### Lessons Learned

Reflect on what you learned about:

- Physical Volumes (PV) / Volume Groups (VG) / Logical Volumes (LV) - These work together to create scalable storage.
- Filesystem creation - LVM provides a flexible way to manage storage without relying on fixed disk partitions. 
- Mounting storage - A Logical Volume must be formatted with a filesystem before it can be mounted and used.
- Why LVM is useful in production environments - LVM makes it easier to extend storage in production environments with minimal disruption

---

# Phase 7: Bash Automation (Task 7: Automate Basic Linux Server Administration)

## Objectives

- Create a Bash script named: server_setup.sh . The script should perform the following tasks:

### 1. Display basic server information
- Display:
  - Hostname
  - Current user
  - Current date and time
  - Linux kernel version

---

### 2. Display system resources
- Show:
  - Memory usage
  - Disk usage

---

### 3. Verify Nginx
- Check whether Nginx is installed. If installed: Display service status.
- If not installed: Display an informative message.

---

### 4. Verify Docker

- Check whether Docker is installed. Display an appropriate message.

---

### 5. Display listening ports
 - Show currently listening TCP/UDP ports.

---

### 6. Print a completion message
- Example: Linux server health check completed successfully.

### Scenario

- Your team frequently provisions new Linux servers for development and testing.Instead of manually running the same commands every time, you have been asked to automate the process using a Bash script.The script should perform common system administration tasks and display useful server information.
---

## Verification
Verify:

- The script executes successfully.
- All commands display expected information.
- Informative messages appear when software is not installed.

---

### Commands Used

- Script creation
  ```
  mkdir /devops/bhavya
  cd /devops/bhavya
  vim server_setup.sh
```
#!/bin/bash

echo "===== Linux Server Information ====="

echo "Hostname:"
hostname

echo

echo "Current User:"
whoami

echo

echo "Current Date:"
date

echo

echo "Kernel Version:"
uname -r

echo
echo "===== Memory Usage ====="
free -h

echo
echo "===== Disk Usage ====="
df -h

echo
echo "===== Nginx Status ====="

if systemctl list-unit-files | grep -q nginx; then
    systemctl status nginx --no-pager
else
    echo "Nginx is not installed."
fi

echo
echo "===== Docker Status ====="

if command -v docker >/dev/null 2>&1; then
    docker --version
else
    echo "Docker is not installed."
fi

echo
echo "===== Listening Ports ====="

ss -tuln

echo
echo "Linux server health check completed successfully."

 ```
- Permission changes
  `chmod +x server_setup.sh`
  
- Script execution
  `./server_setup.sh`

---

### Verification

Explain how you confirmed the script worked correctly.

---

### Screenshots

Include:

- Script contents

<img width="1440" height="900" alt="script" src="https://github.com/user-attachments/assets/ebd71346-aa6c-423a-af57-fa1bd42c2920" />

- Script execution

<img width="684" height="79" alt="script-execute" src="https://github.com/user-attachments/assets/efaab467-dd3e-4aa8-86f5-b013ad97b3e0" />

- Output
<img width="1440" height="900" alt="output" src="https://github.com/user-attachments/assets/2dd41508-ba61-436b-b0f5-6dd20eb6b662" />

---

### Lessons Learned

- Bash scripts automate repetitive Linux administration tasks.
- Making a script executable with `chmod +x` allows it to run like a program.
- Conditional statements enable scripts to handle different system states gracefully.
- Automating system checks saves time and reduces manual effort.
- Bash scripting is a foundational skill for DevOps and system administration.

---

# Phase 8: Production Troubleshooting Capstone

## Objective

Troubleshoot and resolve a simulated web application outage on a Linux server using service management, networking, logs, file permissions, and system monitoring.

## Scenario

A web application was reported as unavailable.

The goal was to investigate the server systematically, identify the root cause, resolve the issue, and verify that the application was accessible again.

## Investigation

The following areas were investigated:

* Nginx service status
* Port 80 availability
* Local web application response
* Nginx service and application logs
* Web directory and file permissions
* Disk space
* Memory usage
* Running Nginx processes
--- 
## Commands Used

### Service and Application Checks

* `systemctl status nginx` — Check Nginx service status
* `ss -tlnp` — Check listening TCP ports
* `curl localhost` — Verify local web application availability
---
### Log Investigation

* `journalctl -u nginx -n 20 --no-pager` — Review recent Nginx service events
* `tail -20 /var/log/nginx/error.log` — Review recent Nginx errors
* `tail -20 /var/log/nginx/access.log` — Review recent web requests
--- 
### System and File Checks

* `ls -ld /var/www/html` — Check web directory permissions
* `ls -l /var/www/html/index.html` — Check web page file permissions
* `free -h` — Check memory usage
* `df -h` — Check disk usage
* `ps -ef | grep nginx` — Check running Nginx processes
---
### Resolution

* `systemctl start nginx` — Start the Nginx service
---
## Findings

The initial investigation showed that the server resources, web files, and Nginx configuration were not showing obvious problems.

The Nginx service was found to be inactive, and port 80 was no longer listening. As a result, the local web application could not be accessed.

## Root Cause

Nginx was stopped/inactive, which caused the web application to become unavailable.

## Resolution

The Nginx service was started:

```bash
sudo systemctl start nginx
```
----

## Verification

The following checks were performed after resolving the issue:

* Confirmed Nginx was active using `systemctl status nginx`.
* Confirmed port 80 was listening using `ss`.
* Confirmed the web application was accessible using `curl localhost`.

The application successfully responded after Nginx was restarted.
--- 
## Screenshots

<img width="1998" height="1249" alt="nginxservice-failure" src="https://github.com/user-attachments/assets/50e7e6b3-e032-439e-a066-df6d30b4095b" />

### Nginx Service Failure

<!-- Add screenshot showing Nginx in an inactive/stopped state -->

### Verification After Resolution

<!-- Add screenshot showing Nginx active, port 80 listening, and curl response -->
--- 
## Lessons Learned

* Troubleshooting should begin by gathering evidence before making changes.
* Checking service status, listening ports, logs, and application availability helps narrow down the root cause.
* A stopped service can make an otherwise healthy server application unavailable.
* `systemctl`, `ss`, and `curl` provide useful information when troubleshooting Linux services.
* Logs may not always contain errors, so troubleshooting should combine multiple sources of evidence.
* After making a change, the issue should be verified from the application's perspective.
* A structured troubleshooting process helps identify the root cause without making unnecessary changes.

---
