
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

### Q: What is Nginx?

- Nginx is a high-performance web server that can also act as a reverse proxy, load balancer, and HTTP cache.

---

### Q: What does `systemctl status nginx` show?

It displays:

- Service state (running/stopped)
- Process ID (PID)
- Uptime
- Recent log messages

---

### Q: Difference between `systemctl start` and `systemctl enable`?

- `start` starts the service immediately.
- `enable` configures the service to start automatically during system boot.

---

### Q: Why use `curl localhost`?

To verify that the web server is serving content locally without using a browser.

---

### Q: Why use `ss -tulnp`?

To verify:

- The service is listening
- Which port it is using
- Which process owns that port

---

### Q: Where does Nginx serve files from by default?

```
/var/www/html
```

---

### Q: What happens after modifying `index.html`?

The updated content is immediately served because it is a static file. A service reload is generally not required for content changes, though it is commonly used after configuration changes.
