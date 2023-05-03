# NFS Sharing and Persistent Connection 🐧

### Setup the NFS Share from node01

```admonish summary
🐧 Your team has determined they need an NFS share to facilitate filesystem
access across multiple servers from one central location.

🐧 Deploy the nfs server on node01

🐧 Share out a filesystem `/share` to any system

🐧 Verify that the sytem is being shared out

```

💬 Let's setup NFS Share 🐧🐧🐧

---

### 1. Connect to node01

~~~admonish example title="Input"
```bash
ssh node01
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
controlplane $ ssh node01
Last login: Sun Nov 13 17:27:09 2022 from 10.48.0.33
```
~~~

### 2. Verify there is no nfs package

~~~admonish example title="Input"
```bash
dpgk -l | grep -i nfs
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
node01 $ dpkg -l | grep -i nfs
node01 $ 
```
~~~

### 3. Deploy the nfs server package

~~~admonish example title="Input"
```bash
apt -y install nfs-kernel-server
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
node01 $ apt -y install nfs-kernel-server
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  keyutils libnfsidmap2 libtirpc-common libtirpc3 nfs-common rpcbind
Suggested packages:
  watchdog
The following NEW packages will be installed:
  keyutils libnfsidmap2 libtirpc-common libtirpc3 nfs-common nfs-kernel-server rpcbind
0 upgraded, 7 newly installed, 0 to remove and 101 not upgraded.
Need to get 504 kB of archives.
After this operation, 1938 kB of additional disk space will be used.
Get:1 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libtirpc-common all 1.2.5-1ubuntu0.1 [7712 B]
Get:2 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 libtirpc3 amd64 1.2.5-1ubuntu0.1 [77.9 kB]
Get:3 http://archive.ubuntu.com/ubuntu focal/main amd64 rpcbind amd64 1.2.5-8 [42.8 kB]
Get:4 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 keyutils amd64 1.6-6ubuntu1.1 [44.8 kB]
Get:5 http://archive.ubuntu.com/ubuntu focal/main amd64 libnfsidmap2 amd64 0.25-5.1ubuntu1 [27.9 kB]
Get:6 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 nfs-common amd64 1:1.3.4-2.5ubuntu3.4 [204 kB]
Get:7 http://archive.ubuntu.com/ubuntu focal-updates/main amd64 nfs-kernel-server amd64 1:1.3.4-2.5ubuntu3.4 [98.9 kB]
Fetched 504 kB in 1s (756 kB/s)         
Selecting previously unselected package libtirpc-common.
(Reading database ... 72924 files and directories currently installed.)
Preparing to unpack .../0-libtirpc-common_1.2.5-1ubuntu0.1_all.deb ...
Unpacking libtirpc-common (1.2.5-1ubuntu0.1) ...
Selecting previously unselected package libtirpc3:amd64.
Preparing to unpack .../1-libtirpc3_1.2.5-1ubuntu0.1_amd64.deb ...
Unpacking libtirpc3:amd64 (1.2.5-1ubuntu0.1) ...
Selecting previously unselected package rpcbind.
Preparing to unpack .../2-rpcbind_1.2.5-8_amd64.deb ...
Unpacking rpcbind (1.2.5-8) ...
Selecting previously unselected package keyutils.
Preparing to unpack .../3-keyutils_1.6-6ubuntu1.1_amd64.deb ...
Unpacking keyutils (1.6-6ubuntu1.1) ...
Selecting previously unselected package libnfsidmap2:amd64.
Preparing to unpack .../4-libnfsidmap2_0.25-5.1ubuntu1_amd64.deb ...
Unpacking libnfsidmap2:amd64 (0.25-5.1ubuntu1) ...
Selecting previously unselected package nfs-common.
Preparing to unpack .../5-nfs-common_1%3a1.3.4-2.5ubuntu3.4_amd64.deb ...
Unpacking nfs-common (1:1.3.4-2.5ubuntu3.4) ...
Selecting previously unselected package nfs-kernel-server.
Preparing to unpack .../6-nfs-kernel-server_1%3a1.3.4-2.5ubuntu3.4_amd64.deb ...
Unpacking nfs-kernel-server (1:1.3.4-2.5ubuntu3.4) ...
Setting up libtirpc-common (1.2.5-1ubuntu0.1) ...
Setting up keyutils (1.6-6ubuntu1.1) ...
Setting up libnfsidmap2:amd64 (0.25-5.1ubuntu1) ...
Setting up libtirpc3:amd64 (1.2.5-1ubuntu0.1) ...
Setting up rpcbind (1.2.5-8) ...
Created symlink /etc/systemd/system/multi-user.target.wants/rpcbind.service → /lib/systemd/system/rpcbind.service.
Created symlink /etc/systemd/system/sockets.target.wants/rpcbind.socket → /lib/systemd/system/rpcbind.socket.
Setting up nfs-common (1:1.3.4-2.5ubuntu3.4) ...

Creating config file /etc/idmapd.conf with new version
Adding system user `statd' (UID 115) ...
Adding new user `statd' (UID 115) with group `nogroup' ...
Not creating home directory `/var/lib/nfs'.
Created symlink /etc/systemd/system/multi-user.target.wants/nfs-client.target → /lib/systemd/system/nfs-client.target.
Created symlink /etc/systemd/system/remote-fs.target.wants/nfs-client.target → /lib/systemd/system/nfs-client.target.
nfs-utils.service is a disabled or a static unit, not starting it.
Setting up nfs-kernel-server (1:1.3.4-2.5ubuntu3.4) ...
Created symlink /etc/systemd/system/multi-user.target.wants/nfs-server.service → /lib/systemd/system/nfs-server.service.
Job for nfs-server.service canceled.

Creating config file /etc/exports with new version

Creating config file /etc/default/nfs-kernel-server with new version
Processing triggers for systemd (245.4-4ubuntu3.18) ...
Processing triggers for man-db (2.9.1-1) ...
Processing triggers for libc-bin (2.31-0ubuntu9.9) ...
```
~~~

### 4. Verify that the server is running but nothing is being shared out.

~~~admonish example title="Input"
```bash
systemclt status nfs-server.service --no-pager
ss -ntulp | grep 2049
showmount -e
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
node01 $ systemctl status nfs-server.service --no-pager
● nfs-server.service - NFS server and services
     Loaded: loaded (/lib/systemd/system/nfs-server.service; enabled; vendor preset: enabled)
     Active: active (exited) since Wed 2023-05-03 04:36:47 UTC; 1min 49s ago
   Main PID: 37794 (code=exited, status=0/SUCCESS)
      Tasks: 0 (limit: 2339)
     Memory: 0B
     CGroup: /system.slice/nfs-server.service

May 03 04:36:46 node01 systemd[1]: Starting NFS server and services...
May 03 04:36:47 node01 systemd[1]: Finished NFS server and services.

```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
node01 $ ss -ntulp | grep 2049
udp    UNCONN  0       0                   0.0.0.0:2049           0.0.0.0:*                                                                                     
udp    UNCONN  0       0                      [::]:2049              [::]:*                                                                                     
tcp    LISTEN  0       64                  0.0.0.0:2049           0.0.0.0:*                                                                                     
tcp    LISTEN  0       64                     [::]:2049              [::]:*                                                                                     

```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
node01 $ showmount -e
Export list for node01:
```
~~~

#### 💬 Notice the service is running, the ports 2049 are open for TCP and udp connections, and no shares are being shared out

### 5. Further verify that the firewall isn't running to complicate things

~~~admonish example title="Input"
```bash
ufw status
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
node01 $ ufw status
Status: inactive
```
~~~

### 6. Let's create a directory to share out. We also need to prep it for other systems to connect and write by changing permissions

~~~admonish example title="Input"
```bash
mkdir /share
chown nobody:nogroup /share
```
~~~

### 7. Add the line `/share *(rw,sync,no_subtree_check)` to `/etc/expots` to share out the directory

~~~admonish example title="Input"
```bash
vi /etc/exports
```
~~~

[vim](../../tools/vim/basic_vim.md)

### 8. After doing this, you will need to restart the service to see the share

~~~admonish example title="Input"
```bash
systemctl restart nfs-server.service
showmount -e
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
node01 $ systemctl restart nfs-server.service
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
node01 $ showmount -e
Export list for node01:
/share *
```
~~~

#### 💬 Once you see the share, you're ready to move on to the client connection

### 9. Remember to move back to controlplane node

~~~admonish example title="Input"
```bash
exit
```
~~~

---

### Setup the client and connect from controlplane

```admonish summary
🐧 So far you've set up an NFS server and share, now we have to
connect to it as another system

🐧 Install the nfs-common client

🐧 Mount the `node01:/share` to `/mnt` to test

🐧 Make the `node01:/share` to `/mnt` a permanent setting in
`/etc/fstab`

```

### 10. Install the nfs-common client

~~~admonish example title="Input"
```bash
apt -y install nfs-common
```
~~~

### 11. Test the mount point to verify we can connect

~~~admonish example title="Input"
```bash
mount node01:/share /mnt
```
~~~

### 12. Let's examine the mount point in our system

~~~admonish example title="Input"
```bash
df -h /mnt
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
controlplane $ df -h /mnt
Filesystem      Size  Used Avail Use% Mounted on
node01:/share    20G  5.4G   14G  29% /mnt
```
~~~

### 13. Let's verify we can write into this directory

~~~admonish example title="Input"
```bash
touch /mnt/test1
ls -l /mnt
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
controlplane $ touch /mnt/test1
controlplane $ ls -l /mnt
total 0
-rw-r--r-- 1 nobody nogroup 0 May  3 05:10 test1
```
~~~

### 14. Remove the mount point so we can mount it via `/etc/fstab`

~~~admonish example title="Input"
```bash
umount -l /mnt
```
~~~

### 15. Edit `/etc/fstab` and add the line `node:01/share /mnt nfs
defaults 0 0`

~~~admonish example title="Input"
```bash
vi /etc/fstab
```
~~~

[vim](../../tools/vim/basic_vim.md)


### 16. Now we use the `/etc/fstab` to ensure that the mount point correctly mounts on reboot. This is an old system administrator trick

~~~admonish example title="Input"
```bash
mount -a
```
~~~

### 17. If this works, the system is set up correctly. Let's check our mount point again

~~~admonish example title="Input"
```bash
df -h /mnt
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
controlplane $ df -h /mnt
Filesystem      Size  Used Avail Use% Mounted on
node01:/share    20G  5.4G   14G  29% /mnt
```
~~~

### 18. Let's do on last write check to ensure everything is working correctly

~~~admonish example title="Input"
```bash
touch /mnt/finalcheck
ls -l /mnt/finalcheck
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
controlplane $ touch /mnt/finalcheck
controlplane $ ls -l /mnt/finalcheck
-rw-r--r-- 1 nobody nogroup 0 May  3 05:15 /mnt/finalcheck
```
~~~

#### 💬 If that's all worked, then the system is correctly set up!

# Look at you, learning Linux Configuration! You created a NFS share and then connected to it from another system 🐧

Next up: [Apache Webserver Install and
Setup](apache_webserver_install_and_setup.md)
