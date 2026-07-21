
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
