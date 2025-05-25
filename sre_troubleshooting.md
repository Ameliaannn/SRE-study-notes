
# Basic Troubleshooting Flow for SRE Beginners

This document outlines a basic troubleshooting flow when a host or service is unreachable.


## 1. Network Reachability

### Step 1: Ping the host

```bash
ping <IP_ADDRESS>
```

- If ping fails, the host may be down or the network is unreachable.

### Step 2: Check if the port is open

```bash
telnet <IP_ADDRESS> <PORT>
# or
nc -zv <IP_ADDRESS> <PORT>
```

### Step 3: Check local port listening

```bash
netstat -tuln
# or
ss -tuln
```

- Use `grep` to filter for specific ports.

---

## 2. Check Service Logs

If the host is reachable but the service is not responding:

```bash
tail -f /path/to/log/file.log
```

- Look for errors like `500`, timeouts, connection refused, etc.

You might need to access a logging platform (e.g., ELK, Grafana) depending on your environment.

---

## 3. Check via Browser (Frontend Failure)

Press **F12** in your browser to open Developer Tools.

### In the "Network" tab:
- Check if the request URL is correct.
- Look at HTTP status codes (e.g. 200 OK, 404 Not Found, 502 Bad Gateway).
- Inspect request headers, token, cookies, etc.

---

## 4. Verify URL and Routing

Ensure that the frontend is calling the correct backend service:

- Double-check domain, path, and parameters.
- Confirm no redirection or broken route.
- Validate service DNS resolution and accessibility.

---

## 5. Check Load Balancer (SLB / GELB)

### SLB (Server Load Balancer)
- A cloud load balancing service (e.g., by Alibaba Cloud).

### GELB
- Could refer to Global ELB or internal naming.
- Use it to distribute traffic to multiple backend servers.

### Actions:
- Check which backend instances are bound.
- Review health check status.
- Identify which backend server is down.

