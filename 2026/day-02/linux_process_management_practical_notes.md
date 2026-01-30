# Linux Process Management – Practical Notes

## What is a Process?
- A **process** is a running instance of a program
- Each process has a **PID**, state, priority, and resource usage
- Process management is critical for **troubleshooting performance and service issues**

---

## Common Process States (Must Know)

- **Running (R)**
  - Process is actively using CPU
  - Example: a busy application handling requests

- **Sleeping (S)**
  - Waiting for I/O (disk, network, user input)
  - Most processes stay in this state normally

- **Uninterruptible Sleep (D)**
  - Waiting for disk or hardware I/O
  - Cannot be killed easily (red flag if stuck)

- **Stopped (T)**
  - Process paused manually or by debugger
  - Example: using `Ctrl + Z`

- **Zombie (Z)**
  - Process finished execution but parent didn’t clean it up
  - Uses no CPU, but too many zombies indicate a **buggy parent process**

---

## 5 Process Commands I Use Daily

**pwd – Show current directory**
pwd


**ls – List files & directories**
ls -l
ls -la

**cd – Change directory**
cd /var/log
cd ~


- **ps** – snapshot of processes
  ```bash
  ps -ef
  ```

- **top** – real-time process monitoring
  ```bash
  top
  ```

- **htop** – user-friendly interactive process viewer (if installed)
  ```bash
  htop
  ```

- **kill** – stop misbehaving processes
  ```bash
  kill -9 <PID>
  ```

- **systemctl** – manage service processes
  ```bash
  systemctl status <service>
  ```

---

## Practical DevOps Scenarios

- High CPU usage → check with `top`
- Application not responding → find PID using `ps`
- Service crashed → inspect via `systemctl status`
- Too many zombie processes → restart parent service

---

## Key Takeaway
Understanding process states helps you **quickly diagnose system and application issues** in production environments.

