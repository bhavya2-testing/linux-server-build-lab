
## Troubleshooting Notes

### Issue

Nginx was not installed in the Killercoda environment.

### Investigation

Checked the service status using:

```bash
systemctl status nginx
```

The output indicated that the service was not installed.

### Resolution

Installed Nginx using:

```bash
sudo apt update
sudo apt install nginx
```

Started the service:

```bash
systemctl start nginx
```

Verified using:

```bash
curl localhost
```

---

### Issue

Needed to confirm whether the service was listening on the expected port.

### Investigation

Checked listening ports:

```bash
sudo ss -tulnp | grep :80
```

### Resolution

Verified that Nginx was listening on TCP port 80.
