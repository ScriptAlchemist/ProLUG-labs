# Checking kernel and packages 🐧

### Linux Commands for Kernel and Packages

```admonish summary
🐧 Echo the number of kernel versions that are stored on this system into `/root/kernel`

🐧 Check all the kernel information
```

💬Let's check the kernel and package info on the system 🐧 🐧 🐧

---

### 1. Display information about the currently running operation system

~~~admonish example title="Input"
```bash
uname -a
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
ubuntu $ uname -a
Linux ubuntu 5.4.0-131-generic #147-Ubuntu SMP Fri Oct 14 17:07:22 UTC 2022 x86_64 x86_64 x86_64 GNU/Linux
```
~~~

### 2. Check for old versions of the kernel that are on the system.

~~~admonish example title="Input"
```bash
ls /boot/vm*
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
ubuntu $ ls /boot/vm*
/boot/vmlinuz  /boot/vmlinuz-5.4.0-131-generic  /boot/vmlinuz.old
```
~~~

### 3. Echo the number of version into `/root/kernel`

~~~admonish example title="Input"
```bash
echo 1 > /root/kernel
```
~~~

### 4. Next we will check how many packages are on the system.

~~~admonish example title="Input"
```bash
dpkg -l | wc -l
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
ubuntu $ dpkg -l | wc -l
724
```
~~~

### 5. What is the version of ssh on this system? Server and client.

~~~admonish example title="Input"
```bash
dpkg -l | grep -i ssh
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
ubuntu $ dpkg -l | grep -i ssh
ii  libssh-4:amd64                   0.9.3-2ubuntu2.2                  amd64        tiny C SSH library (OpenSSL flavor)
ii  openssh-client                   1:8.2p1-4ubuntu0.5                amd64        secure shell (SSH) client, for secure access to remote machines
ii  openssh-server                   1:8.2p1-4ubuntu0.5                amd64        secure shell (SSH) server, for secure access from remote machines
ii  openssh-sftp-server              1:8.2p1-4ubuntu0.5                amd64        secure shell (SSH) sftp server module, for SFTP access from remote machines
ii  ssh-import-id                    5.10-0ubuntu1                     all          securely retrieve an SSH public key and install it locally
ii  sshfs                            3.6.0+repack+really2.10-0ubuntu1  amd64        filesystem client based on SSH File Transfer Protocol
```
~~~

#### 💬 client is named **openssh-client**

#### 💬 server is named **openssh-server**

Next up: [Checking disk and mount points](./checking_disk_and_mount_points.md)

