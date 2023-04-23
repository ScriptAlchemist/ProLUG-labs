# IP and Open Port Information

### Linux Commands for network information

```admonish summary
🐧 Put the name of your network interface into a file called `/root/interface`

🐧 Put the ip address of your network interface into a file called `/root/primary-ip`

🐧 Write the default route out to a file called `/root/default`
```

💬 Check network information 🐧 🐧 🐧

---

### 1. Check your ip address

~~~admonish example title="Input"
```bash
ip addr
```
~~~

~~~admonish collapsible=true title="Example Output"
```
ubuntu $ ip addr 
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host 
       valid_lft forever preferred_lft forever
2: enp1s0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1460 qdisc fq_codel state UP group default qlen 1000
    link/ether f2:05:f6:3f:86:80 brd ff:ff:ff:ff:ff:ff
    inet 172.30.1.2/24 brd 172.30.1.255 scope global dynamic enp1s0
       valid_lft 86293029sec preferred_lft 86293029sec
3: docker0: <NO-CARRIER,BROADCAST,MULTICAST,UP> mtu 1500 qdisc noqueue state DOWN group default 
    link/ether 02:42:bb:ac:49:d3 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever
```
~~~

### 2. What is the name of your interface?

~~~admonish example title="Input"
```bash
ip addr | grep enp | grep mtu | awk '{print $2}'
```
~~~

~~~admonish collapsible=true title="Example Output"
```
ubuntu $ ip addr | grep enp | grep mtu | awk '{print $2}'
enp1s0:
```
~~~

### 3. Put that value in a file `/root/interface`

~~~admonish example title="Input"
```bash
ip addr | grep enp | grep mtu | awk '{print $2}' > /root/interface
```
~~~

#### 💬 There are other ways to do this, but this will do it with one command

### 4. What is the ip of your interface?

~~~admonish example title="Input"
```bash
ip addr | grep enp | grep inet | awk '{print $2}'
```
~~~

~~~admonish collapsible=true title="Example Output"
```
ubuntu $ ip addr | grep enp | grep inet | awk '{print $2}' 
172.30.1.2/24
```
~~~

### 5. Put that value in a file `/root/prinary-ip`

~~~admonish example title="Input"
```bash
ip addr | grep enp | grep inet | awk '{print $2}' > /root/primary-ip
```
~~~

### 6. Let's pull the default route for your system

~~~admonish example title="Input"
```bash
ip route
```
~~~

~~~admonish collapsible=true title="Example Output"
```
ubuntu $ ip route
default via 172.30.1.1 dev enp1s0 
172.17.0.0/16 dev docker0 proto kernel scope link src 172.17.0.1 linkdown 
172.30.1.0/24 dev enp1s0 proto kernel scope link src 172.30.1.2 
```
~~~

### 7. What is the default route for your system? Write this out to `/root/default`

~~~admonish example title="Input"
```bash
ip route | grep -i default | awk '{print $3}' > /root/default
```
~~~

### 8. Ping the default gateway 3 times and verify that you get a response back

~~~admonish example title="Input"
```bash
ping -c3 `ip route | grep -i default | awk '{print $3}'`
```
~~~

~~~admonish collapsible=true title="Example Output"
```
ubuntu $ ping -c3 `ip route | grep -i default | awk '{print $3}'`
PING 172.30.1.1 (172.30.1.1) 56(84) bytes of data.
64 bytes from 172.30.1.1: icmp_seq=1 ttl=64 time=0.113 ms
64 bytes from 172.30.1.1: icmp_seq=2 ttl=64 time=0.177 ms
64 bytes from 172.30.1.1: icmp_seq=3 ttl=64 time=0.217 ms

--- 172.30.1.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2034ms
rtt min/avg/max/mdev = 0.113/0.169/0.217/0.042 ms
```
~~~

---

### Linux Commands for open ports

```admonish summary
🐧 Can you find sshd and containerd listening on your system?

🐧 If you can, write yes into the file `/root/ports`
```

💬 Let's check open ports on the system 🐧 🐧 🐧

### 9. Check what ports are open on your system

~~~admonish example title="Input"
```bash
ss -ntulp
```
~~~

~~~admonish collapsible=true title="Example Output"
```
ubuntu $ ping -c3 `ip route | grep -i default | awk '{print $3}'`
PING 172.30.1.1 (172.30.1.1) 56(84) bytes of data.
64 bytes from 172.30.1.1: icmp_seq=1 ttl=64 time=0.113 ms
64 bytes from 172.30.1.1: icmp_seq=2 ttl=64 time=0.177 ms
64 bytes from 172.30.1.1: icmp_seq=3 ttl=64 time=0.217 ms

--- 172.30.1.1 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2034ms
rtt min/avg/max/mdev = 0.113/0.169/0.217/0.042 ms
```
~~~

~~~admonish example title="Input"
```bash
ss -ntulp | grep -E "sshd|containerd"
```
~~~

~~~admonish collapsible=true title="Example Output"
```
ubuntu $ ss -ntulp | grep -E "sshd|containerd"
tcp    LISTEN  0       128                 0.0.0.0:22             0.0.0.0:*      users:(("sshd",pid=614,fd=3))                                                  
tcp    LISTEN  0       4096              127.0.0.1:38185          0.0.0.0:*      users:(("containerd",pid=13689,fd=14))                                         
tcp    LISTEN  0       128                    [::]:22                [::]:*      users:(("sshd",pid=614,fd=4))                                                  
```
~~~

### 10. Echo "yes" if you can see sshd and containerd listening to `/root/ports`

#### 💬 We can see them, so we'll set that to yes

~~~admonish example title="Input"
```bash
echo "yes" > /root/ports
```
~~~

### 11. Another way to look at the `ports/processes` for sshd and containerd

~~~admonish example title="Input"
```bash
lsof -i :22
```
~~~

~~~admonish collapsible=true title="Example Output"
```
ubuntu $ lsof -i :22
COMMAND PID USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
sshd    614 root    3u  IPv4  20882      0t0  TCP *:ssh (LISTEN)
sshd    614 root    4u  IPv6  20893      0t0  TCP *:ssh (LISTEN)
```
~~~

### 12. Connect to port 22. Timeout just causes it to drop after 3 seconds

~~~admonish example title="Input"
```bash
timeout 3 nc 127.0.0.1 22
```
~~~

~~~admonish collapsible=true title="Example Output"
```
ubuntu $ timeout 3 nc 127.0.0.1 22
SSH-2.0-OpenSSH_8.2p1 Ubuntu-4ubuntu0.5
```
~~~

### 13. So let's stop containerd and verify that the process is no longer running. First let's check the status

~~~admonish example title="Input"
```bash
systemctl status containerd
```
~~~

~~~admonish collapsible=true title="Example Output"
```
ubuntu $ systemctl status containerd
● containerd.service - containerd container runtime
     Loaded: loaded (/lib/systemd/system/containerd.service; enabled; vendor preset: en>
     Active: active (running) since Tue 2023-04-11 13:35:13 UTC; 1 weeks 1 days ago
       Docs: https://containerd.io
   Main PID: 13689 (containerd)
      Tasks: 8
     Memory: 12.8M
     CGroup: /system.slice/containerd.service
             └─13689 /usr/bin/containerd

Apr 11 13:35:13 ubuntu containerd[13689]: time="2023-04-11T13:35:13.932667312Z" level=i>
Apr 11 13:35:13 ubuntu containerd[13689]: time="2023-04-11T13:35:13.933048326Z" level=i>
Apr 11 13:35:13 ubuntu systemd[1]: Started containerd container runtime.
Apr 11 13:35:13 ubuntu containerd[13689]: time="2023-04-11T13:35:13.947444377Z" level=i>
Apr 11 13:35:13 ubuntu containerd[13689]: time="2023-04-11T13:35:13.948147815Z" level=i>
Apr 11 13:35:13 ubuntu containerd[13689]: time="2023-04-11T13:35:13.960280418Z" level=i>
Apr 11 13:35:13 ubuntu containerd[13689]: time="2023-04-11T13:35:13.960666171Z" level=i>
Apr 11 13:35:13 ubuntu containerd[13689]: time="2023-04-11T13:35:13.960931006Z" level=i>
Apr 11 13:35:13 ubuntu containerd[13689]: time="2023-04-11T13:35:13.961135447Z" level=i>
Apr 11 13:35:13 ubuntu containerd[13689]: time="2023-04-11T13:35:13.949109643Z" level=i>
```
~~~

### 14. You might need to click "q" to escape and we'll stop it. Stop containerd

~~~admonish example title="Input"
```bash
systemctl stop containerd
```
~~~

### 15. Verify that you no longer see containerd running or the port open on the system

~~~admonish example title="Input"
```bash
ss -ntulp | grep containerd
```
~~~

---

### Linux Commands to monitor traffic

```admonish summary
🐧 Look at the throughput to your interfaces

🐧 Create a file `/root/ubuntu.pcap` with 200 packets that can be read by wireshark later. (We don't look at it in the lab. We just create it)
```


💬 Let's check network traffic to our open system 🐧 🐧 🐧

### 16. Check network throughput to your system for 20 seconds

~~~admonish example title="Input"
```bash
ifstat 2 10
```
~~~

~~~admonish collapsible=true title="Example Output"
```
ubuntu $ ifstat 2 10
      enp1s0             docker0      
 KB/s in  KB/s out   KB/s in  KB/s out
    0.20      0.28      0.00      0.00
    0.19      0.60      0.00      0.00
    0.20      0.45      0.00      0.00
    0.17      0.31      0.00      0.00
    0.24      0.40      0.00      0.00
    0.13      0.35      0.00      0.00
    0.17      0.31      0.00      0.00
    0.20      0.45      0.00      0.00
    0.17      0.33      0.00      0.00
    0.13      0.35      0.00      0.00
```
~~~

#### 💬 Note: There is very little traffic (in size) into or out of your system

### 17. Do a tcpdump to inspect the actual traffic into your system. Capture 1000 packets against your `enp1s0` interface

~~~admonish example title="Input"
```bash
tcpdump -ni enp1s0 -s0 -c 1000
```
~~~

~~~admonish collapsible=true title="Example Output"
```
Cutting off beginning...

12:32:44.680485 IP 172.30.1.2.40200 > 10.57.2.9.34616: Flags [P.], seq 161968:162139, ack 1, win 501, options [nop,nop,TS val 3131427640 ecr 3052573401], length 171
12:32:44.680616 IP 172.30.1.2.40200 > 10.57.2.9.34616: Flags [P.], seq 162139:162310, ack 1, win 501, options [nop,nop,TS val 3131427641 ecr 3052573401], length 171
12:32:44.680746 IP 172.30.1.2.40200 > 10.57.2.9.34616: Flags [P.], seq 162310:162481, ack 1, win 501, options [nop,nop,TS val 3131427641 ecr 3052573401], length 171
12:32:44.680860 IP 172.30.1.2.40200 > 10.57.2.9.34616: Flags [P.], seq 162481:162652, ack 1, win 501, options [nop,nop,TS val 3131427641 ecr 3052573401], length 171
12:32:44.680996 IP 172.30.1.2.40200 > 10.57.2.9.34616: Flags [P.], seq 162652:162823, ack 1, win 501, options [nop,nop,TS val 3131427641 ecr 3052573401], length 171
12:32:44.681127 IP 172.30.1.2.40200 > 10.57.2.9.34616: Flags [P.], seq 162823:162994, ack 1, win 501, options [nop,nop,TS val 3131427641 ecr 3052573401], length 171
12:32:44.681256 IP 172.30.1.2.40200 > 10.57.2.9.34616: Flags [P.], seq 162994:163165, ack 1, win 501, options [nop,nop,TS val 3131427641 ecr 3052573401], length 171
12:32:44.681392 IP 172.30.1.2.40200 > 10.57.2.9.34616: Flags [P.], seq 163165:163336, ack 1, win 501, options [nop,nop,TS val 3131427641 ecr 3052573401], length 171
12:32:44.681524 IP 172.30.1.2.40200 > 10.57.2.9.34616: Flags [P.], seq 163336:163507, ack 1, win 501, options [nop,nop,TS val 3131427641 ecr 3052573401], length 171
12:32:44.681655 IP 172.30.1.2.40200 > 10.57.2.9.34616: Flags [P.], seq 163507:163678, ack 1, win 501, options [nop,nop,TS val 3131427642 ecr 3052573401], length 171
1000 packets captured
1024 packets received by filter
24 packets dropped by kernel
```
~~~

### 18. Let's generate a `.pcap` file that can be used by wireshark to inspect traffic. (We don't have wireshark on this system)

~~~admonish example title="Input"
```bash
for i in $(seq 1 5); do ping -c 10 www.google.com & done; tcpdump -ni enp1s0 -s0 -c 200 -w $(hostname).pcap
```
~~~

~~~admonish collapsible=true title="Example Output"
```
ubuntu $ for i in $(seq 1 5); do ping -c 10 www.google.com & done; tcpdump -ni enp1s0 -s0 -c 200 -w $(hostname).pcap
[1] 32253
[2] 32254
[3] 32255
[4] 32256
[5] 32257
PING www.google.com (172.253.62.99) 56(84) bytes of data.
PING www.google.com (172.253.62.99) 56(84) bytes of data.
PING www.google.com (172.253.62.99) 56(84) bytes of data.
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=1 ttl=111 time=1.01 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=1 ttl=111 time=0.696 ms
PING www.google.com (172.253.62.99) 56(84) bytes of data.
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=1 ttl=111 time=0.600 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=1 ttl=111 time=0.638 ms
PING www.google.com (172.253.62.99) 56(84) bytes of data.
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=1 ttl=111 time=0.626 ms
tcpdump: listening on enp1s0, link-type EN10MB (Ethernet), capture size 262144 bytes
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=2 ttl=111 time=0.717 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=2 ttl=111 time=0.657 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=2 ttl=111 time=0.587 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=2 ttl=111 time=0.695 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=2 ttl=111 time=0.621 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=3 ttl=111 time=0.725 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=3 ttl=111 time=0.670 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=3 ttl=111 time=0.683 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=3 ttl=111 time=0.580 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=3 ttl=111 time=0.795 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=4 ttl=111 time=0.667 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=4 ttl=111 time=0.743 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=4 ttl=111 time=0.660 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=4 ttl=111 time=0.669 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=4 ttl=111 time=0.593 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=5 ttl=111 time=0.735 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=5 ttl=111 time=0.669 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=5 ttl=111 time=0.678 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=5 ttl=111 time=0.705 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=5 ttl=111 time=0.724 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=6 ttl=111 time=0.777 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=6 ttl=111 time=0.717 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=6 ttl=111 time=0.599 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=6 ttl=111 time=0.676 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=6 ttl=111 time=0.659 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=7 ttl=111 time=0.715 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=7 ttl=111 time=0.563 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=7 ttl=111 time=0.608 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=7 ttl=111 time=0.648 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=7 ttl=111 time=0.711 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=8 ttl=111 time=0.735 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=8 ttl=111 time=0.596 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=8 ttl=111 time=0.542 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=8 ttl=111 time=0.683 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=8 ttl=111 time=0.765 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=9 ttl=111 time=0.703 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=9 ttl=111 time=0.656 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=9 ttl=111 time=0.681 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=9 ttl=111 time=0.664 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=9 ttl=111 time=0.742 ms
200 packets captured
228 packets received by filter
0 packets dropped by kernel
ubuntu $ 64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=10 ttl=111 time=0.705 ms

--- www.google.com ping statistics ---
10 packets transmitted, 10 received, 0% packet loss, time 9043ms
rtt min/avg/max/mdev = 0.667/0.749/1.012/0.091 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=10 ttl=111 time=0.814 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=10 ttl=111 time=0.724 ms


--- www.google.com ping statistics ---
--- www.google.com ping statistics ---
10 packets transmitted, 10 received, 0% packet loss, time 9073ms
rtt min/avg/max/mdev = 0.596/0.668/0.724/0.033 ms
10 packets transmitted, 10 received, 0% packet loss, time 9072ms
rtt min/avg/max/mdev = 0.563/0.645/0.814/0.071 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=10 ttl=111 time=0.679 ms

--- www.google.com ping statistics ---
10 packets transmitted, 10 received, 0% packet loss, time 9098ms
rtt min/avg/max/mdev = 0.542/0.666/0.795/0.069 ms
64 bytes from bc-in-f99.1e100.net (172.253.62.99): icmp_seq=10 ttl=111 time=0.713 ms

--- www.google.com ping statistics ---
10 packets transmitted, 10 received, 0% packet loss, time 9119ms
rtt min/avg/max/mdev = 0.593/0.692/0.765/0.048 ms
^C
[1]   Done                    ping -c 10 www.google.com
[2]   Done                    ping -c 10 www.google.com
[3]   Done                    ping -c 10 www.google.com
[4]-  Done                    ping -c 10 www.google.com
[5]+  Done                    ping -c 10 www.google.com
```
~~~

### 19. Verify the size and creation of the file

~~~admonish example title="Input"
```bash
ls -lh /root/ubuntu.pcap
```
~~~

~~~admonish collapsible=true title="Example Output"
```
ubuntu $ ls -lh /root/ubuntu.pcap
-rw-r--r-- 1 tcpdump tcpdump 25K Apr 20 12:36 /root/ubuntu.pcap
```
~~~

# Look at you, learning Linux! You looked at the disk space and usage! 🐧

Next up: [Connecting to systems and pushing or pulling files](./connecting_to_systems_and_pushing_or_pulling.md)
