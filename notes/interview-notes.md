
#### What's the difference between uname -a and cat /etc/os-release?
- `uname` (short for unix name) uname reports information directly from the Linux kernel, such as the kernel version, architecture, and hostname.
- `cat /etc/os-release` is a configuration file provided by the Linux distribution that contains information like the distribution name, version, and ID (for example, Ubuntu 24.04 or Debian 12).

                Linux Server

        +-------------------------+
        | Ubuntu 24.04            |
        | Debian 12               |
        | RHEL 9                  |
        +-------------------------+
                 ▲
                 │
         cat /etc/os-release
                 │
        +-------------------------+
        | Linux Kernel            |
        | 6.8.x                   |
        | x86_64                  |
        +-------------------------+
                 ▲
                 │
              uname -a
