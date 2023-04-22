# Look around a Linux System 🐧

### Linux Commands to gather information

```admonish summary
Follow along and look around a new Linux system for the first time
```

💬 Let's take a look around, shall we? 🐧 🐧 🐧

---

### 1. First we check what version of Linux we're on:

~~~admonish example title="Input"
```bash
cat /etc/*release
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
ubuntu $ cat /etc/*release
DISTRIB_ID=Ubuntu
DISTRIB_RELEASE=20.04
DISTRIB_CODENAME=focal
DISTRIB_DESCRIPTION="Ubuntu 20.04.5 LTS"
NAME="Ubuntu"
VERSION="20.04.5 LTS (Focal Fossa)"
ID=ubuntu
ID_LIKE=debian
PRETTY_NAME="Ubuntu 20.04.5 LTS"
VERSION_ID="20.04"
HOME_URL="https://www.ubuntu.com/"
SUPPORT_URL="https://help.ubuntu.com/"
BUG_REPORT_URL="https://bugs.launchpad.net/ubuntu/"
PRIVACY_POLICY_URL="https://www.ubuntu.com/legal/terms-and-policies/privacy-policy"
VERSION_CODENAME=focal
UBUNTU_CODENAME=focal
```
~~~

### 2. Next we check the kernel version:


~~~admonish example title="Input"
```bash
uname -r
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
ubuntu $ uname -r
5.4.0-131-generic
```
~~~

### 3. We might want to know how long the system has been up:

~~~admonish example title="Input"
```bash
uptime
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
ubuntu $ uptime
 05:23:23 up  1:21,  0 users,  load average: 0.01, 0.08, 0.05
```
~~~

### 4. Next we see how the system booted

#### 💬 What kernel parameters were passed when the system was started?

~~~admonish example title="Input"
```bash
cat /proc/cmdline
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
ubuntu $ cat /proc/cmdline
BOOT_IMAGE=/boot/vmlinuz-5.4.0-131-generic root=LABEL=cloudimg-rootfs ro
console=tty1 console=ttyS0
```
~~~

---

### Linux Commands to dig into the system

## 🐧 That was cool, but let's dig deeper 🧙

```admonish summary
Do each command command and really think about the output you're looking
at. You may run into them multiple times. If needed, you can compare the
output.
```

### 5. Look at the virtual memory usage of this system:

~~~admonish example title="Input"
```bash
vmstat 1 5
```
~~~

~~~admonish collapsible=true title="Example Output"
```
ubuntu $ vmstat 1 5
procs -----------memory---------- ---swap-- -----io---- -system-- ------cpu-----
 r  b   swpd   free   buff  cache   si   so    bi    bo   in   cs us sy id wa st
 0  0    780 106992 115796 1501412    0    0   106   666  197  359  3  1 95  1  0
 0  0    780 107024 115796 1501412    0    0     0     0  288  208  0  0 100  0  0
 0  0    780 107024 115796 1501412    0    0     0     0  273  182  0  0 100  0  0
 0  0    780 107024 115804 1501404    0    0     0    20  311  217  2  0 98  0  0
 1  0    780 107024 115804 1501412    0    0     0     0  291  202  0  1 99  0  0
```
~~~

#### 💬 What are you seeing here? Is this system under high memory usage or not?

```text,editable
// What do you think?


```

### 6. We can check the overall CPI usage of the system every second for 5 seconds:

~~~admonish example title="Input"
```bash
mpstat 1 5
```
~~~

~~~admonish collapsible=true title="Example Output"
```
ubuntu $ mpstat 1 5
Linux 5.4.0-131-generic (ubuntu)        04/20/23        _x86_64_        (1 CPU)

05:50:53     CPU    %usr   %nice    %sys %iowait    %irq   %soft  %steal  %guest  %gnice   %idle
05:50:54     all    0.00    0.00    1.00    0.00    0.00    0.00    0.00    0.00    0.00   99.00
05:50:55     all    0.00   13.27    1.02    0.00    0.00    0.00    0.00    0.00    0.00   85.71
05:50:56     all    0.00    1.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00   99.00
05:50:57     all    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00    0.00  100.00
05:50:58     all    0.00    0.99    0.99    0.00    0.00    0.00    0.00    0.00    0.00   98.02
Average:     all    0.00    3.01    0.60    0.00    0.00    0.00    0.00    0.00    0.00   96.39
```
~~~

#### 💬 Is this system under high load or not?

```text,editable
// What do you think?


```

### 7. Next we check what processes are running on the system:

~~~admonish example title="Input"
```bash
ps -ef
```
~~~

~~~admonish collapsible=true title="Example Output"
```
ubuntu $ ps -ef
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 04:02 ?        00:00:14 /sbin/init
root           2       0  0 04:02 ?        00:00:00 [kthreadd]
root           3       2  0 04:02 ?        00:00:00 [rcu_gp]
root           4       2  0 04:02 ?        00:00:00 [rcu_par_gp]
root           6       2  0 04:02 ?        00:00:00 [kworker/0:0H-events_highpri]
root           8       2  0 04:02 ?        00:00:00 [mm_percpu_wq]
root           9       2  0 04:02 ?        00:00:00 [ksoftirqd/0]
root          10       2  0 04:02 ?        00:00:00 [rcu_sched]
root          11       2  0 04:02 ?        00:00:00 [migration/0]
root          12       2  0 04:02 ?        00:00:00 [idle_inject/0]
root          14       2  0 04:02 ?        00:00:00 [cpuhp/0]
root          15       2  0 04:02 ?        00:00:00 [kdevtmpfs]
root          16       2  0 04:02 ?        00:00:00 [netns]
root          17       2  0 04:02 ?        00:00:00 [rcu_tasks_kthre]
root          18       2  0 04:02 ?        00:00:00 [kauditd]
root          19       2  0 04:02 ?        00:00:00 [khungtaskd]
root          20       2  0 04:02 ?        00:00:00 [oom_reaper]
root          21       2  0 04:02 ?        00:00:00 [writeback]
root          22       2  0 04:02 ?        00:00:00 [kcompactd0]
root          23       2  0 04:02 ?        00:00:00 [ksmd]
root          24       2  0 04:02 ?        00:00:00 [khugepaged]
root          70       2  0 04:02 ?        00:00:00 [kintegrityd]
root          71       2  0 04:02 ?        00:00:00 [kblockd]
root          72       2  0 04:02 ?        00:00:00 [blkcg_punt_bio]
root          73       2  0 04:02 ?        00:00:00 [tpm_dev_wq]
root          74       2  0 04:02 ?        00:00:00 [ata_sff]
root          75       2  0 04:02 ?        00:00:00 [md]
root          76       2  0 04:02 ?        00:00:00 [edac-poller]
root          77       2  0 04:02 ?        00:00:00 [devfreq_wq]
root          78       2  0 04:02 ?        00:00:00 [watchdogd]
root          81       2  0 04:02 ?        00:00:00 [kswapd0]
root          82       2  0 04:02 ?        00:00:00 [ecryptfs-kthrea]
root          84       2  0 04:02 ?        00:00:00 [kthrotld]
root          85       2  0 04:02 ?        00:00:00 [irq/24-aerdrv]
root          86       2  0 04:02 ?        00:00:00 [irq/25-aerdrv]
root          87       2  0 04:02 ?        00:00:00 [irq/26-aerdrv]
root          88       2  0 04:02 ?        00:00:00 [irq/27-aerdrv]
root          89       2  0 04:02 ?        00:00:00 [irq/28-aerdrv]
root          90       2  0 04:02 ?        00:00:00 [irq/29-aerdrv]
root          91       2  0 04:02 ?        00:00:00 [acpi_thermal_pm]
root          92       2  0 04:02 ?        00:00:01 [kworker/0:1H-events_highpri]
root          93       2  0 04:02 ?        00:00:00 [vfio-irqfd-clea]
root          94       2  0 04:02 ?        00:00:00 [ipv6_addrconf]
root         103       2  0 04:02 ?        00:00:00 [kstrp]
root         106       2  0 04:02 ?        00:00:00 [kworker/u3:0]
root         119       2  0 04:02 ?        00:00:00 [charger_manager]
root         158       2  0 04:02 ?        00:00:00 [scsi_eh_0]
root         159       2  0 04:02 ?        00:00:00 [scsi_tmf_0]
root         162       2  0 04:02 ?        00:00:00 [cryptd]
root         180       2  0 04:02 ?        00:00:00 [scsi_eh_1]
root         182       2  0 04:02 ?        00:00:00 [scsi_tmf_1]
root         184       2  0 04:02 ?        00:00:00 [scsi_eh_2]
root         185       2  0 04:02 ?        00:00:00 [scsi_tmf_2]
root         188       2  0 04:02 ?        00:00:00 [scsi_eh_3]
root         190       2  0 04:02 ?        00:00:00 [scsi_tmf_3]
root         192       2  0 04:02 ?        00:00:00 [scsi_eh_4]
root         193       2  0 04:02 ?        00:00:00 [ttm_swap]
root         195       2  0 04:02 ?        00:00:00 [scsi_tmf_4]
root         197       2  0 04:02 ?        00:00:00 [scsi_eh_5]
root         198       2  0 04:02 ?        00:00:00 [scsi_tmf_5]
root         201       2  0 04:02 ?        00:00:00 [scsi_eh_6]
root         203       2  0 04:02 ?        00:00:00 [scsi_tmf_6]
root         238       2  0 04:02 ?        00:00:00 [raid5wq]
root         278       2  0 04:02 ?        00:00:00 [jbd2/vda1-8]
root         279       2  0 04:02 ?        00:00:00 [ext4-rsv-conver]
root         349       1  0 04:02 ?        00:00:00 /lib/systemd/systemd-journald
root         385       1  0 04:02 ?        00:00:01 /lib/systemd/systemd-udevd
systemd+     395       1  0 04:02 ?        00:00:00 /lib/systemd/systemd-networkd
root         469       2  0 04:02 ?        00:00:00 [kaluad]
root         470       2  0 04:02 ?        00:00:00 [kmpath_rdacd]
root         471       2  0 04:02 ?        00:00:00 [kmpathd]
root         472       2  0 04:02 ?        00:00:00 [kmpath_handlerd]
root         473       1  0 04:02 ?        00:00:00 /sbin/multipathd -d -s
root         481       2  0 04:02 ?        00:00:00 [loop0]
root         483       2  0 04:02 ?        00:00:00 [loop1]
root         486       2  0 04:02 ?        00:00:00 [loop2]
root         538       1  0 04:02 ?        00:00:00 /usr/lib/accountsservice/accounts-da
message+     539       1  0 04:02 ?        00:00:01 /usr/bin/dbus-daemon --system --addr
root         551       1  0 04:02 ?        00:00:00 /usr/bin/python3 /usr/bin/networkd-d
root         557       1  0 04:02 ?        00:00:00 /usr/sbin/cron -f
root         559       1  0 04:02 ?        00:00:00 /usr/lib/policykit-1/polkitd --no-de
syslog       561       1  0 04:02 ?        00:00:00 /usr/sbin/rsyslogd -n -iNONE
root         568       1  0 04:02 ?        00:00:00 /lib/systemd/systemd-logind
root         570       1  0 04:02 ?        00:00:00 /usr/lib/udisks2/udisksd
daemon       584       1  0 04:02 ?        00:00:00 /usr/sbin/atd -f
root         598       1  0 04:02 ?        00:00:00 /usr/sbin/ModemManager
root         599       1  0 04:02 ttyS0    00:00:00 /sbin/agetty -o -p -- \u --keep-baud
root         609       1  0 04:02 tty1     00:00:00 /sbin/agetty -o -p -- \u --noclear t
root         614       1  0 04:02 ?        00:00:00 sshd: /usr/sbin/sshd -D [listener] 0
root         636       1  0 04:02 ?        00:00:00 /usr/bin/python3 /usr/share/unattend
root        5955       2  0 04:03 ?        00:00:00 bpfilter_umh
root        7414       1  0 04:03 ?        00:00:00 /usr/bin/dockerd -H fd:// --containe
root       13689       1  0 04:04 ?        00:00:06 /usr/bin/containerd
root       21622       1  0 04:05 ?        00:00:05 /opt/theia/node /opt/theia/browser-a
root       21634       1  0 04:05 ?        00:00:00 bash -c while true; do /bin/kc-termi
root       21636   21634  0 04:05 ?        00:00:00 /bin/kc-terminal -p 40200 -t disable
root       21655     614  0 04:06 ?        00:00:00 sshd: kc-internal@notty
root       21714       1  0 04:06 ?        00:00:01 /usr/libexec/fwupd/fwupd
root       21737       1  0 04:06 ?        00:00:00 dhclient -v
root       21785       1  0 04:06 ?        00:00:00 dhclient -v
root       21832       1  0 04:06 ?        00:00:00 gpg-agent --homedir /var/lib/fwupd/g
root       21834       1  0 04:06 ?        00:00:00 dhclient -v
systemd+   21882       1  0 04:06 ?        00:00:00 /lib/systemd/systemd-timesyncd
root       21935       1  0 04:06 ?        00:00:00 bash -c export RV_SCRIPT_DIR=/var/ru
root       21938   21935  0 04:06 ?        00:00:00 /bin/runtime-scenario-service
root       21973       1  0 04:06 ?        00:00:01 /bin/runtime-info-service
root       22521       2  0 04:20 ?        00:00:00 [kworker/u2:0-events_power_efficient
root       22773       2  0 04:47 ?        00:00:00 [kworker/u2:1-events_unbound]
root       23574   21636  0 05:13 pts/0    00:00:00 bash
root       23636   21622  0 05:13 ?        00:00:07 /opt/theia/node /opt/theia/node_modu
root       23659   21622  0 05:13 ?        00:00:00 /opt/theia/node /opt/theia/node_modu
root       23667   21622  0 05:13 pts/1    00:00:00 /bin/bash
root       24636       2  0 05:23 ?        00:00:00 [kworker/0:3-memcg_kmem_cache]
root       25268       2  0 05:29 ?        00:00:00 [kworker/0:1-events]
root       26268       2  0 05:39 ?        00:00:00 [kworker/0:0-events]
root       26269       2  0 05:39 ?        00:00:00 [kworker/u2:2-events_power_efficient
systemd+   26405       1  0 05:40 ?        00:00:00 /lib/systemd/systemd-resolved
root       26406       2  0 05:40 ?        00:00:00 [kworker/u2:3]
root       26436   23574  0 05:41 pts/0    00:00:00 ps -ef
```
~~~

#### 💬 Maybe check unique values return inside of `ps -ef`.

~~~admonish example title="Input"
```bash
ps -ef | awk '{print$1}' | sort | uniq -c
```
~~~

~~~admonish collapsible=true title="Example Output"
```
ubuntu $ ps -ef | awk '{print $1}' | sort | uniq -c
      1 UID
      1 daemon
      1 message+
    116 root
      1 syslog
      3 systemd+
```
~~~

#### 💬 What user is using the most processes?

#### 💬 Do you think this system is doing any real work or just sitting there running an OS?

```text,editable
// What do you think?


```

### 8. Next let's check what processes are executing on the processor every second.

~~~admonish example title="Input"
```bash
pidstat 1 5
```
~~~


~~~admonish collapsible=true title="Example Output"
```
ubuntu $ pidstat 1 5
Linux 5.4.0-131-generic (ubuntu)        04/20/23        _x86_64_        (1 CPU)

06:00:32      UID       PID    %usr %system  %guest   %wait    %CPU   CPU  Command

06:00:33      UID       PID    %usr %system  %guest   %wait    %CPU   CPU  Command
06:00:34        0     23636    0.00    1.00    0.00    0.00    1.00     0  node
06:00:34        0     28185    0.00    1.00    0.00    0.00    1.00     0  pidstat

06:00:34      UID       PID    %usr %system  %guest   %wait    %CPU   CPU  Command
06:00:35        0     21636    0.00    1.00    0.00    0.00    1.00     0  kc-terminal

06:00:35      UID       PID    %usr %system  %guest   %wait    %CPU   CPU  Command
06:00:36        0         1    1.00    0.00    0.00    0.00    1.00     0  systemd
06:00:36        0     28185    0.00    1.00    0.00    1.00    1.00     0  pidstat

06:00:36      UID       PID    %usr %system  %guest   %wait    %CPU   CPU  Command
06:00:37        0     21622    1.00    0.00    0.00    0.00    1.00     0  node
06:00:37        0     21636    1.00    0.00    0.00    0.00    1.00     0  kc-terminal
06:00:37        0     23636    1.00    0.00    0.00    0.00    1.00     0  node

Average:      UID       PID    %usr %system  %guest   %wait    %CPU   CPU  Command
Average:        0         1    0.20    0.00    0.00    0.00    0.20     -  systemd
Average:        0     21622    0.20    0.00    0.00    0.00    0.20     -  node
Average:        0     21636    0.20    0.20    0.00    0.00    0.40     -  kc-terminal
Average:        0     23636    0.20    0.20    0.00    0.00    0.40     -  node
Average:        0     28185    0.00    0.40    0.00    0.20    0.40     -  pidstat
```
~~~

#### 💬 Why do these have different length output?

#### 💬 What processes were using the most CPU?

#### 💬 Which is showing up the most often?

```text,editable
// What do you think?


```

### 9. Next we may want to see more CPU and Disk usage on the system in 1 second increments. Do you think you could modify this to run for 30 seconds?

~~~admonish example title="Input"
```bash
iostat -xz 1 5
```
~~~

~~~admonish collapsible=true title="Example Output"
```
ubuntu $ iostat -xz 1 5
Linux 5.4.0-131-generic (ubuntu)        04/20/23        _x86_64_        (1 CPU)

avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           1.48    1.06    1.21    0.42    0.15   95.68

Device            r/s     rkB/s   rrqm/s  %rrqm r_await rareq-sz     w/s     wkB/s   wrqm/s  %wrqm w_await wareq-sz     d/s     dkB/s   drqm/s  %drqm d_await dareq-sz  aqu-sz  %util
loop0            0.24      0.28     0.00   0.00    1.62     1.17    0.00      0.00     0.00   0.00    0.00     0.00    0.00      0.00     0.00   0.00    0.00     0.00    0.00   0.01
loop1            0.01      0.15     0.00   0.00    0.62    14.22    0.00      0.00     0.00   0.00    0.00     0.00    0.00      0.00     0.00   0.00    0.00     0.00    0.00   0.00
loop2            0.01      0.05     0.00   0.00    0.34     5.97    0.00      0.00     0.00   0.00    0.00     0.00    0.00      0.00     0.00   0.00    0.00     0.00    0.00   0.00
loop3            0.00      0.00     0.00   0.00    0.00     1.00    0.00      0.00     0.00   0.00    0.00     0.00    0.00      0.00     0.00   0.00    0.00     0.00    0.00   0.00
vda              2.76     76.80     0.61  18.02    1.81    27.83    5.84    486.62    11.46  66.25   11.01    83.31    0.12   2686.87     0.00   0.00    0.72 21966.24    0.06   1.00


avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           0.00    0.00    1.01    0.00    0.00   98.99

Device            r/s     rkB/s   rrqm/s  %rrqm r_await rareq-sz     w/s     wkB/s   wrqm/s  %wrqm w_await wareq-sz     d/s     dkB/s   drqm/s  %drqm d_await dareq-sz  aqu-sz  %util


avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           0.00    0.00    0.00    0.00    0.00  100.00

Device            r/s     rkB/s   rrqm/s  %rrqm r_await rareq-sz     w/s     wkB/s   wrqm/s  %wrqm w_await wareq-sz     d/s     dkB/s   drqm/s  %drqm d_await dareq-sz  aqu-sz  %util


avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           0.00    0.00    0.00    0.00    0.00  100.00

Device            r/s     rkB/s   rrqm/s  %rrqm r_await rareq-sz     w/s     wkB/s   wrqm/s  %wrqm w_await wareq-sz     d/s     dkB/s   drqm/s  %drqm d_await dareq-sz  aqu-sz  %util


avg-cpu:  %user   %nice %system %iowait  %steal   %idle
           0.00    0.00    0.00    0.00    0.00  100.00

Device            r/s     rkB/s   rrqm/s  %rrqm r_await rareq-sz     w/s     wkB/s   wrqm/s  %wrqm w_await wareq-sz     d/s     dkB/s   drqm/s  %drqm d_await dareq-sz  aqu-sz  %util
vda              0.00      0.00     0.00   0.00    0.00     0.00    2.00     24.00     4.00  66.67    0.50    12.00    0.00      0.00     0.00   0.00    0.00     0.00    0.00   0.80


```
~~~

#### 💬 Let's do one for 30 seconds every 5 seconds. I won't post the output. It's longer than we need.

~~~admonish example title="Input"
```bash
iostat -xz 5 6
```
~~~

---

### Linux Commands to see networking traffic and load

#### 💬 Now let's dig a little deeper into networking 🧙

```admonish summary
Do each command and think about what output you're looking at. You may run them multiple times. If needed to compare the output.
```

### 10. Look at the network usage and load of the system.

~~~admonish example title="Input"
```bash
sar -n DEV 1 5
```
~~~

~~~admonish collapsible=true title="Example Output"
```
ubuntu $ sar -n DEV 1 5
Linux 5.4.0-131-generic (ubuntu)        04/20/23        _x86_64_        (1 CPU)

06:17:04        IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s   %ifutil
06:17:05           lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
06:17:05       enp1s0      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
06:17:05      docker0      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00

06:17:05        IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s   %ifutil
06:17:06           lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
06:17:06       enp1s0      9.00      9.00      0.58      1.71      0.00      0.00      0.00      0.00
06:17:06      docker0      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00

06:17:06        IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s   %ifutil
06:17:07           lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
06:17:07       enp1s0      5.00      5.00      0.34      1.05      0.00      0.00      0.00      0.00
06:17:07      docker0      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00

06:17:07        IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s   %ifutil
06:17:08           lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
06:17:08       enp1s0      7.00      7.00      0.45      1.27      0.00      0.00      0.00      0.00
06:17:08      docker0      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00

06:17:08        IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s   %ifutil
06:17:09           lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
06:17:09       enp1s0      4.00      4.00      0.26      0.99      0.00      0.00      0.00      0.00
06:17:09      docker0      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00

Average:        IFACE   rxpck/s   txpck/s    rxkB/s    txkB/s   rxcmp/s   txcmp/s  rxmcst/s   %ifutil
Average:           lo      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
Average:       enp1s0      5.00      5.00      0.33      1.01      0.00      0.00      0.00      0.00
Average:      docker0      0.00      0.00      0.00      0.00      0.00      0.00      0.00      0.00
```
~~~

#### 💬 What are you seeing here? What devices are showing up? Do any devices seem to be under high load? Which one had the most traffic?


```text,editable
// What do you think?


```

### 11. Next we check tcp packets and errors.

~~~admonish example title="Input"
```bash
sar -n TCP,ETCP 1 5
```
~~~

~~~admonish collapsible=true title="Example Output"
```
ubuntu $ sar -n TCP,ETCP 1 5
Linux 5.4.0-131-generic (ubuntu)        04/20/23        _x86_64_        (1 CPU)

06:19:07     active/s passive/s    iseg/s    oseg/s
06:19:08         0.00      0.00      0.00      0.00

06:19:07     atmptf/s  estres/s retrans/s isegerr/s   orsts/s
06:19:08         0.00      0.00      0.00      0.00      0.00

06:19:08     active/s passive/s    iseg/s    oseg/s
06:19:09         0.00      0.00      3.00      3.00

06:19:08     atmptf/s  estres/s retrans/s isegerr/s   orsts/s
06:19:09         0.00      0.00      0.00      0.00      0.00

06:19:09     active/s passive/s    iseg/s    oseg/s
06:19:10         0.00      0.00      3.00      3.00

06:19:09     atmptf/s  estres/s retrans/s isegerr/s   orsts/s
06:19:10         0.00      0.00      0.00      0.00      0.00

06:19:10     active/s passive/s    iseg/s    oseg/s
06:19:11         0.00      0.00      3.00      3.00

06:19:10     atmptf/s  estres/s retrans/s isegerr/s   orsts/s
06:19:11         0.00      0.00      0.00      0.00      0.00

06:19:11     active/s passive/s    iseg/s    oseg/s
06:19:12         0.00      0.00      6.00      6.00

06:19:11     atmptf/s  estres/s retrans/s isegerr/s   orsts/s
06:19:12         0.00      0.00      0.00      0.00      0.00

Average:     active/s passive/s    iseg/s    oseg/s
Average:         0.00      0.00      3.00      3.00

Average:     atmptf/s  estres/s retrans/s isegerr/s   orsts/s
Average:         0.00      0.00      0.00      0.00      0.00
```
~~~

#### 💬 Do we appear to be seeing any large numbers of errors? Why might retransmits be a big problem?

```text,editable
// What do you think?


```

# Look at you, learning Linux 🐧! You looked around the OS!

Next up: [Checking kernel and packages](./checking_kernel_and_packages.md)
