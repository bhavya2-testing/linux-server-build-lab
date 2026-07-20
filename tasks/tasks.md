# Linux Server Build Lab - Project Tasks

## Project Goal

Build and configure a Linux server from scratch while practicing common DevOps system administration activities.

The goal is to simulate tasks performed by a Linux/DevOps engineer:

- Server preparation
- User management
- Permissions
- Service deployment
- Storage management
- Troubleshooting
- Documentation

---

# Phase 1: Server Baseline Assessment

## Task 1: Inspect the Linux Server

### Scenario

You have received access to a new Linux server.

Before making any changes, collect information about the environment.

### Objectives

Identify:

- Linux distribution
- Kernel version
- Current user
- CPU information
- Memory usage
- Disk usage
- Running processes
- Network information

### Deliverables

Document:

- Commands used
- System information collected
- Screenshots
- Observations

---

# Phase 2: User and Access Management

## Task 2: Create Development Users

### Scenario

A development team requires individual Linux accounts.

### Requirements

Create users:

```
developer1
developer2
tester1
```

Configure:

- Home directories
- User passwords
- Group membership

### Deliverables

Document:

- User creation steps
- User verification
- Group assignments

---

## Task 3: Create Shared Development Workspace

### Scenario

Developers need a shared project directory.

### Requirements

Create:

```
/opt/dev-project
```

Configure:

- Owner
- Group ownership
- Permissions
- Shared collaboration access

Test access using different users.

### Deliverables

Document:

- Permission decisions
- Ownership configuration
- Access testing results

---

# Phase 3: Linux File Permissions

## Task 4: Application File Security

### Scenario

An application contains different types of files requiring different access levels.

Create:

```
application/
├── config.txt
├── credentials.txt
└── deploy.sh
```

Configure permissions:

- Configuration file access
- Restricted credential access
- Executable deployment script

### Deliverables

Document:

- Permission settings
- Ownership
- Security considerations

---

# Phase 4: Web Server Deployment

## Task 5: Deploy Nginx Web Server

### Scenario

The development team needs a simple web server.

### Requirements

Install and configure Nginx.

Deploy:

```
/var/www/html/index.html
```

The page should display:

```
Linux Server Build Lab
```

Verify:

- Service status
- Web response
- Listening ports

### Deliverables

Document:

- Installation steps
- Configuration
- Verification
- Screenshots

---

## Task 6: Nginx Troubleshooting

### Scenario

The website becomes unavailable.

Simulate failures:

Examples:

- Stop the service
- Disable the service
- Modify permissions
- Change webpage content

Troubleshoot and restore service.

### Deliverables

Document:

- Problem
- Investigation steps
- Root cause
- Fix
- Verification

---

# Phase 5: Linux Logs and Monitoring

## Task 7: Analyze System Logs

### Scenario

The security team wants an investigation of authentication activity.

### Objectives

Analyze:

- Authentication logs
- Service logs
- System events

Find:

- Failed login attempts
- Service failures
- Important events

### Deliverables

Document:

- Log locations
- Commands used
- Findings

---

# Phase 6: Storage Management Using LVM

## Task 8: Create Additional Storage

### Scenario

The server needs additional storage for backups.

No physical disk is available, so simulate additional storage.

### Requirements

Create:

- Virtual disk
- Physical Volume
- Volume Group
- Logical Volume

Format and mount storage.

### Deliverables

Document:

- Storage architecture
- Commands used
- Verification output
- Screenshots

---

## Task 9: Expand Storage

### Scenario

The backup storage needs more capacity.

Increase the logical volume size.

Verify:

- New capacity
- Filesystem size
- Data preservation

### Deliverables

Document:

- Before state
- Expansion process
- After state

---

# Phase 7: Automation Basics

## Task 10: Create Server Setup Script

### Scenario

You want to automate repetitive server setup tasks.

Create a Bash script that performs selected setup activities.

Examples:

- Create directories
- Create users
- Install packages
- Verify services

### Deliverables

Document:

- Script purpose
- Script execution
- Output
- Improvements

---

# Phase 8: Production Troubleshooting Scenarios

## Task 11: Disk Full Scenario

### Scenario

A server reports:

```
Disk usage: 95%
```

Investigate.

Find:

- Large directories
- Large files
- Possible causes

Document:

- Investigation process
- Findings
- Recommended action

---

## Task 12: Service Down Scenario

### Scenario

A developer reports:

> Application is not reachable.

Troubleshoot:

- Service status
- Process status
- Network ports
- Logs
- Configuration

Document:

- Troubleshooting flow
- Root cause
- Resolution

---

# Final Capstone Task

## Task 13: Complete Linux Server Build

### Scenario

You are responsible for preparing a Linux server for a development team.

Complete:

✅ User setup  
✅ Group management  
✅ Permissions  
✅ Nginx deployment  
✅ Logs investigation  
✅ Storage configuration  
✅ Troubleshooting  
✅ Automation  

---

# Project Documentation Requirements

For every task include:

## Objective

What problem are you solving?

## Commands Used

Commands you executed.

## Verification

How did you confirm success?

## Screenshots

Evidence of completion.

## Troubleshooting

Problems encountered and fixes.

## Lessons Learned

Key concepts gained from the exercise.
