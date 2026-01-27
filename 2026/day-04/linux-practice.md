To check running processes in Linux, the primary commands are ps (process status) for a static snapshot and top or htop for real-time monitoring. 
Practice Note: Checking Running Processes

1. Using the ps command
The ps command provides a snapshot of current processes. Without options, it only shows processes tied to the current shell. 
ps aux
# or
ps -ef

Example Output (ps aux):
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.3  21696 12644 ?        Ss   07:33   0:10 /sbin/init
root           2  0.0  0.0   3028  2048 ?        Sl   07:33   0:00 /init
root           7  0.0  0.0   3028  1804 ?        Sl   07:33   0:00 plan9 --control-socket 7 --log-
root          70  0.0  0.5  66820 19656 ?        S<s  07:33   0:10 /usr/lib/systemd/systemd-journa

PID: The unique process ID.
%CPU / %MEM: CPU and memory utilization percentages.
VSZ / RSS: Virtual memory size and resident set size (physical memory used).
TTY: The terminal associated with the process (? means no terminal, usually a background/system process).
STAT: The process status code (e.g., R for running, S for sleeping).
START / STIME: The time or date the process started.
TIME: Total CPU time consumed.
COMMAND: The name/path of the command that launched the process.

To view a process hierarchy (parent/child relationships):
pstree
# or
ps -e --forest

Using the top command
The top command provides a dynamic, real-time view of running processes, sorting them by CPU usage by default. 
top

top - 18:10:29 up 10:37,  1 user,  load average: 0.03, 0.01, 0.00
Tasks:  22 total,   1 running,  21 sleeping,   0 stopped,   0 zombie
%Cpu(s):  0.1 us,  0.1 sy,  0.0 ni, 99.8 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :   3767.3 total,   3317.4 free,    341.8 used,    182.1 buff/cache
MiB Swap:   1024.0 total,   1024.0 free,      0.0 used.   3425.4 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
   2367 lenovo    20   0    9260   5504   3456 R   1.3   0.1   0:00.05 top
      1 root      20   0   21696  12644   9316 S   0.0   0.3   0:10.81 systemd
      2 root      20   0    3028   2048   1920 S   0.0   0.1   0:00.40 init-systemd(Ub
      7 root      20   0    3028   1804   1792 S   0.0   0.0   0:00.01 init
     70 root      19  -1   66820  19656  18760 S   0.0   0.5   0:10.65 systemd-journal

Key interactive shortcuts within top:
Press q to quit.
Press k to kill a process (requires entering the PID).
Press M to sort by memory usage.
Press P to sort by CPU usage (default). 

Using the htop command (interactive alternative) 
htop is an enhanced, more user-friendly alternative to top. It typically needs to be installed first (e.g., sudo apt install htop on Debian/Ubuntu systems). 
htop

htop provides a color-coded interface, allows vertical and horizontal scrolling, and enables process management using function keys (e.g., F9 to kill a process). 

This practice note demonstrates how to use the systemctl command to inspect a systemd service, using the sshd.service (OpenSSH server) as an example. 
Practice Note: Inspecting a Systemd Service

1. Command
The primary command for viewing the status of a systemd service is systemctl status followed by the service name. On some systems, you may need sudo privileges.

systemctl status sshd.service

2 Expected Output (Example)
When you run the command, the output provides detailed information, including whether the service is running, its process ID (PID), memory usage, and recent log entries. The exact output may vary slightly depending on your Linux distribution and the service's current state. 
Here is an example of what you might see if the sshd service is active and running:

● sshd.service - OpenBSD Secure Shell server
     Loaded: loaded (/lib/systemd/system/sshd.service; enabled; vendor preset: enabled)
     Active: active (running) since Wed 2026-01-27 10:00:00 UTC; 1h 15min ago
       Docs: man:sshd(8)
             man:sshd_config(5)
   Main PID: 1234 (sshd)
      Tasks: 1 (limit: 2219)
     Memory: 1.5M
     CGroup: /system.slice/sshd.service
             └─1234 "/usr/sbin/sshd -D [listener] 0 of 10-100 startups"

Jan 27 10:00:00 yourhostname systemd[1]: Starting OpenBSD Secure Shell server...
Jan 27 10:00:01 yourhostname systemd[1]: Started OpenBSD Secure Shell server.
# ... (additional log lines may follow)


3. Key Information Captured
The output provides several critical pieces of information for a system administrator: 
Loaded: Shows the path to the unit file (/lib/systemd/system/sshd.service) and whether the service is enabled (configured to start at boot) or disabled.
Active: Indicates the high-level unit activation state. A status of active (running) means the service is currently operational. Other states could be inactive, failed, or active (exited).
Main PID: The Process ID of the main process associated with the service.
CGroup: The control group the service belongs to.
Log Entries: The last few log messages are displayed, which are useful for quick troubleshooting. For more detailed logs, you can use the journalctl command, specifically journalctl -u sshd.service. 
This process allows for a quick and effective inspection of any systemd service on a modern Linux system. 


Practice Note: Troubleshooting Basic Web Connectivity (Linux/macOS)
Scenario: Cannot connect to example.com.
1. Verify DNS Resolution (nslookup)
Command: nslookup example.com
Observation:

Server:		192.168.1.1
Address:	192.168.1.1#53

Non-authoritative answer:
Name:	example.com
Address: 93.184.216.34

Conclusion: DNS is working; the domain resolves to IP \(93.184.216.34\).

2. Test Network Path (ping)Command: ping -c 4 93.184.216.34Observation:

PING 93.184.216.34 (93.184.216.34): 56 data bytes
64 bytes from 93.184.216.34: icmp_seq=0 ttl=55 time=15.2 ms
...
4 packets transmitted, 4 packets received, 0.0% packet loss

Conclusion: Network connection is active, no packet loss.

3. Check HTTP Service (curl)
Command: curl -I http://example.com
Observation:
HTTP/1.1 200 OK
Age: 543321
Cache-Control: max-age=604800
Content-Type: text/html; charset=UTF-8

Conclusion: The server responded with \(200\) OK. The web service is running correctly. If this failed, the issue could be server-side or a blocked port.

