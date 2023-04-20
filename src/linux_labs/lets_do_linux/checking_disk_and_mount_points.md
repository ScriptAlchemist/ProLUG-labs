# Checking disk and mount points 🐧

## Linux Commands for physical disks

> 💬 Check the physical disk information 🐧 🐧 🐧
>
> 🐧 Echo the number of physical disks you have into `/root/disks`
>
> 🐧 Echo the number of partitions of that disk into `/root/partitions`

---

## 🐧 Check disk information and count partitions

Input:

```bash
fdisk -l | grep -i vd
```

Example Output:

```
ubuntu $ fdisk -l | grep -i vd
Disk /dev/vda: 20 GiB, 21474836480 bytes, 41943040 sectors
/dev/vda1  227328 41943006 41715679 19.9G Linux filesystem
/dev/vda14   2048    10239     8192    4M BIOS boot
/dev/vda15  10240   227327   217088  106M EFI System
```

### 💬 Why do we use VD?

```text,editable
// What do you think?


```

## 🐧 Let's use another command to see that information another way

Input:

```bash
lsblk
```

Example Output:

```
ubuntu $ lsblk
NAME    MAJ:MIN RM  SIZE RO TYPE MOUNTPOINT
loop0     7:0    0 63.2M  1 loop /snap/core20/1634
loop1     7:1    0 67.8M  1 loop /snap/lxd/22753
loop2     7:2    0   48M  1 loop /snap/snapd/17336
vda     252:0    0   20G  0 disk 
|-vda1  252:1    0 19.9G  0 part /
|-vda14 252:14   0    4M  0 part 
`-vda15 252:15   0  106M  0 part /boot/efi
```

and

Input:

```bash
blkid
```

Example Output:

```
ubuntu $ blkid
/dev/vda1: LABEL="cloudimg-rootfs" UUID="666195bb-9c58-470d-9495-743ff99e48c8" TYPE="ext4" PARTUUID="1b586e7b-ba4c-4d6b-9ca6-2502f02cf595"
/dev/vda15: LABEL_FATBOOT="UEFI" LABEL="UEFI" UUID="B8F2-0510" TYPE="vfat" PARTUUID="27df778d-f6e2-4441-b310-124faa31cc3e"
/dev/loop0: TYPE="squashfs"
/dev/loop1: TYPE="squashfs"
/dev/loop2: TYPE="squashfs"
/dev/vda14: PARTUUID="aab173d6-e275-429d-bb29-e66fbfa1c06b"
```

## 🐧 After that we can run our disk information into `/root/disks` and `/root/partitions`

Input:

```bash
echo 1 > /root/disks
echo 3 > /root/partitions
```

---

## Linux Commands for filesystems and mountpoints

> 💬 Check filesystem type and mount points 🐧 🐧 🐧
>
> 🐧 Echo the filesystem type of the root partition into `/root/fstype`
>
> 🐧 Echo the name of the file that defines all the mount points into `/root/mountinfo`

## 🐧 Check what partition the root (/) filesystem is mounted from

Input:

```bash
mount | grep vda
```

Example Output:

```
ubuntu $ mount | grep vda
/dev/vda1 on / type ext4 (rw,relatime)
/dev/vda15 on /boot/efi type vfat (rw,relatime,fmask=0077,dmask=0077,codepage=437,iocharset=iso8859-1,shortname=mixed,errors=remount-ro)
```

### 💬 Check the filesystem written to that partition.

## 🐧 Let's use another command to see that information another way

Input:

```bash
blkid /dev/vda1
```

Example Output:

```
ubuntu $ blkid /dev/vda1
/dev/vda1: LABEL="cloudimg-rootfs" UUID="666195bb-9c58-470d-9495-743ff99e48c8" TYPE="ext4" PARTUUID="1b586e7b-ba4c-4d6b-9ca6-2502f02cf595"
```

## 🐧 You see the type is ext4. Write that out to `/root/fstype`

Input:

```bash
blkid /dev/vda1 > /root/fstype
```

## 🐧 Check the `/etc/fstab` to see how your system is mounting all it's partitions as it comes up.

Input:

```bash
cat /etc/fstab
```

Example Output:

```
ubuntu $ cat /etc/fstab
LABEL=cloudimg-rootfs   /        ext4   defaults        0 1
LABEL=UEFI      /boot/efi       vfat    umask=0077      0 1
```

## 🐧 But that mapping is strange, so to demystify it, use this command

Input:

```bash
ls -l /dev/disk/by-label
```

Example Output:

```
ubuntu $ ls -l /dev/disk/by-label
total 0
lrwxrwxrwx 1 root root 11 Apr 11 13:32 UEFI -> ../../vda15
lrwxrwxrwx 1 root root 10 Apr 11 13:32 cloudimg-rootfs -> ../../vda1
```

## 🐧 There are 4 ways to mount disk: label, partuuid, path, and uuid. You can verify this by looking in each of these locations. This gives you how the system is mapping to the underlying disks

Input:

```bash
for type in $(ls /dev/disk); do echo "type is $type"; ls -l /dev/disk/$type; done
```

Example Output:

```
ubuntu $ for type in $(ls /dev/disk); do echo "type is $type"; ls -l /dev/disk/$type; done
type is by-label
total 0
lrwxrwxrwx 1 root root 11 Apr 11 13:32 UEFI -> ../../vda15
lrwxrwxrwx 1 root root 10 Apr 11 13:32 cloudimg-rootfs -> ../../vda1
type is by-partuuid
total 0
lrwxrwxrwx 1 root root 10 Apr 11 13:32 1b586e7b-ba4c-4d6b-9ca6-2502f02cf595 -> ../../vda1
lrwxrwxrwx 1 root root 11 Apr 11 13:32 27df778d-f6e2-4441-b310-124faa31cc3e -> ../../vda15
lrwxrwxrwx 1 root root 11 Apr 11 13:32 aab173d6-e275-429d-bb29-e66fbfa1c06b -> ../../vda14
type is by-path
total 0
lrwxrwxrwx 1 root root  9 Apr 11 13:32 pci-0000:04:00.0 -> ../../vda
lrwxrwxrwx 1 root root 10 Apr 11 13:32 pci-0000:04:00.0-part1 -> ../../vda1
lrwxrwxrwx 1 root root 11 Apr 11 13:32 pci-0000:04:00.0-part14 -> ../../vda14
lrwxrwxrwx 1 root root 11 Apr 11 13:32 pci-0000:04:00.0-part15 -> ../../vda15
lrwxrwxrwx 1 root root  9 Apr 11 13:32 virtio-pci-0000:04:00.0 -> ../../vda
lrwxrwxrwx 1 root root 10 Apr 11 13:32 virtio-pci-0000:04:00.0-part1 -> ../../vda1
lrwxrwxrwx 1 root root 11 Apr 11 13:32 virtio-pci-0000:04:00.0-part14 -> ../../vda14
lrwxrwxrwx 1 root root 11 Apr 11 13:32 virtio-pci-0000:04:00.0-part15 -> ../../vda15
type is by-uuid
total 0
lrwxrwxrwx 1 root root 10 Apr 11 13:32 666195bb-9c58-470d-9495-743ff99e48c8 -> ../../vda1
lrwxrwxrwx 1 root root 11 Apr 11 13:32 B8F2-0510 -> ../../vda15
```

## 🐧 Remember to put the file that the system uses to mount the disks into `/root/mountinfo`

Input:

```bash
echo "/etc/fstab" > /root/mountinfo
```

---

## Linux Commands disk space and inodes

> 💬 Check disk size and usage 🐧 🐧 🐧
>
> 🐧 Find the size of the partition root (/) and put it in a file called `/root/size`
>
> 🐧 Place a single file that is 3G at location `/root/bigfile`
>
> 🐧 Place 10,000 files called file{1..10000} in `/root` directory

## 🐧 Check the overall current disk space

Input:

```bash
df -h
```

Example Output:

```
ubuntu $ df -h
Filesystem      Size  Used Avail Use% Mounted on
udev            975M     0  975M   0% /dev
tmpfs           199M  1.0M  198M   1% /run
/dev/vda1        20G  4.4G   15G  23% /
tmpfs           992M     0  992M   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs           992M     0  992M   0% /sys/fs/cgroup
/dev/loop0       64M   64M     0 100% /snap/core20/1634
/dev/loop1       68M   68M     0 100% /snap/lxd/22753
/dev/loop2       48M   48M     0 100% /snap/snapd/17336
/dev/vda15      105M  5.2M  100M   5% /boot/efi
```

## 🐧 Write out the size of just root (/) to `/root/size`

Input:

```bash
df -h / | grep -v Size | awk '{print $2}' > /root/size
```

### 💬 This command just cuts out the unnecessary information. You can check it's output by removing `> /root/size`, if you like

```bash
ubuntu $ df -h / | grep -v Size | awk '{print $2}'
20G
```

## 🐧 Let's make a giant file filled with 0's and then check available space

Input:

```bash
dd if=/dev/zero of=/root/bigfile bs=1024k count=3000
```

Example Output:

```
ubuntu $ dd if=/dev/zero of=/root/bigfile bs=1024k count=3000
3000+0 records in
3000+0 records out
3145728000 bytes (3.1 GB, 2.9 GiB) copied, 4.65708 s, 675 MB/s
```

## 🐧 Re-Check size to see that the filesystem is much more full now

Input:

```bash
df -h /
ls -lh /root/bigfile
```

Example Output:

```
ubuntu $ df -h /
Filesystem      Size  Used Avail Use% Mounted on
/dev/vda1        20G  7.3G   12G  38% /
```

```
ubuntu $ ls -lh /root/bigfile
-rw-r--r-- 1 root root 3.0G Apr 20 09:09 /root/bigfile
```

## 🐧 Let's write out 10,000 files and see how that affects out inode usage

Input:

```bash
df -i /
touch /root/file{1..10000}
ls /root | wc -l
df -i /
```

Example Output:

```
ubuntu $ df -i /
Filesystem      Inodes  IUsed   IFree IUse% Mounted on
/dev/vda1      2580480 115080 2465400    5% /
```

```
ubuntu $ touch /root/file{1..10000}
```

```
ubuntu $ ls /root | wc -l
10006
```

```
ubuntu $ df -i /
Filesystem      Inodes  IUsed   IFree IUse% Mounted on
/dev/vda1      2580480 125080 2455400    5% /
```

# Look at you, learning Linux! You looked at the disk space and usage! 🐧

