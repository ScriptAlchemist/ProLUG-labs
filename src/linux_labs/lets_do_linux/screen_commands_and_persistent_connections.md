# Screen Commands and persistent connections 🐧

### Screen Commands to create windows

```admonish summary
🐧 Inspect out `/root/.screenrc` file

🐧 Start screen

🐧 Create multiple screen windows, rename them, and move between them
```

💬 Let's learn all about Screen! 🐧🐧🐧

---

### 1. Verify your `/root/.screenrc` file

~~~admonish example title="Input"
```bash
cat /root/.screenrc
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
controlplane $ cat /root/.screenrc
# GNU Screen - main configuration file
# # All other .screenrc files will source this file to inherit settings.
# # Author: Christian Wills - cwills.sys@gmail.com
#
# # Allow bold colors - necessary for some reason
 attrcolor b ".I"
#
# # Tell screen how to set colors. AB = background, AF=foreground
 termcapinfo xterm 'Co#256:AB=\E[48;5;%dm:AF=\E[38;5;%dm'
#
# # Enables use of shift-PgUp and shift-PgDn
 termcapinfo xterm|xterms|xs|rxvt ti@:te@
#
# # Erase background with current bg color
 defbce "on"
#
# # Enable 256 color term
 term xterm-256color
#
# # Cache 30000 lines for scroll back
 defscrollback 30000
#
# # New mail notification
# backtick 101 30 15 $HOME/bin/mailstatus.sh
#
 hardstatus alwayslastline
# # Very nice tabbed colored hardstatus line
 hardstatus string '%{= Kd} %{= Kd}%-w%{= Kr}[%{= KW}%n %t%{= Kr}]%{= Kd}%+w %-= %{KG} %H
%{KW}|%{KY}%101`%{KW}|%D %M %d %Y%{= Kc} %C%A%{-}'
#
# # change command character from ctrl-a to ctrl-b (emacs users may want this)
#escape ^Bb
#
# # Hide hardstatus: ctrl-a f
 bind f eval "hardstatus ignore"
# # Show hardstatus: ctrl-a F
 bind F eval "hardstatus alwayslastline"
```
~~~

### 2. Create a screen session

~~~admonish example title="Input"
```bash
screen
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash

GNU Screen version 4.08.00 (GNU) 05-Feb-20

Copyright (c) 2018-2020 Alexander Naumov, Amadeusz Slawinski
Copyright (c) 2015-2017 Juergen Weigert, Alexander Naumov, Amadeusz Slawinski
Copyright (c) 2010-2014 Juergen Weigert, Sadrul Habib Chowdhury
Copyright (c) 2008-2009 Juergen Weigert, Michael Schroeder, Micah Cowan, Sadrul Habib Chowdhury
Copyright (c) 1993-2007 Juergen Weigert, Michael Schroeder
Copyright (c) 1987 Oliver Laumann

This program is free software; you can redistribute it and/or modify it under the terms of the GNU
General Public License as published by the Free Software Foundation; either version 3, or (at your
option) any later version.

This program is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without
even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU
General Public License for more details.

You should have received a copy of the GNU General Public License along with this program (see the
file COPYING); if not, see https://www.gnu.org/licenses/, or contact Free Software Foundation,
Inc., 51 Franklin Street, Fifth Floor, Boston, MA  02111-1301  USA.

Send bugreports, fixes, enhancements, t-shirts, money, beer & pizza to screen-devel@gnu.org


Capabilities:
+copy +remote-detach +power-detach +multi-attach +multi-user +font +color-256 +utf8 +rxvt
+builtin-telnet



















                                  [Press Space or Return to end.]

```
~~~


### 3. Verify that you are attached in screen

~~~admonish example title="Input"
```bash
screen -ls
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
controlplane $ screen -ls
There is a screen on:
        111343.pts-0.controlplane       (04/24/23 10:10:46)     (Attached)
1 Socket in /run/screen/S-root.
```
~~~

### 4. Split the screen horizontally

```admonish example title="Keystroke"
Ctrl A + S (Control A and S): split screen horizontally
```

~~~admonish collapsible=true title="Example Output"
```bash
controlplane $






















   0 bash                                                                                           
























  --                                                                                                
```
~~~

### 5. Jump between the horizontal screen sessions

~~~admonish example title="Keystroke"
```bash
Ctrl A + Tab (Control A and Tab key): move over horizontal screens
```
~~~

### 6. Rename the window you're in "Window1"

~~~admonish example title="Keystroke"
```bash
Ctrl A + A (Control A and A): rename window
```
~~~

### 7. Create a new window and name it "Window2"

~~~admonish example title="Keystroke"
```bash
Ctrl A + C (Control A and C): new window
Ctrl A + A (Control A and A): rename window
```
~~~

---

### Screen Commands for logging sessions

```admonish summary
🐧 Detach from screen session and verify it is still there

🐧 Reconnect and then kill the session

🐧 Create a new screen session with logging enabled to
`/root/screenlog.log`
```

### 8. Detach from screen session

```admonish example title="Keystroke"
Ctrl A + D D (Control A and D and D): detach from screen
```

### 9. Verify that screen session is still running

~~~admonish example title="Input"
```bash
screen -ls
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
controlplane $ screen -ls
There is a screen on:
        111343.pts-0.controlplane       (04/24/23 10:10:46)     (Detached)
1 Socket in /run/screen/S-root.
```
~~~

### 10. Reconnect to that session

~~~admonish example title="Input"
```bash
screen -r
```
~~~

### 11. Kill each window sessions

```admonish example title="Keystroke"
Ctrl A + K (Control A and K)
y  #To really kill the window
```

### 12. Create a screen session with logging enabled to `/root/screenlog.log`

~~~admonish example title="Input"
```bash
screen -L -Logfile /root/screenlog.log
```
~~~

### 13. Execute a command to log it out

~~~admonish example title="Input"
```bash
for i in $(seq 100); do uptime; sleep 1; done
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
controlplane $ for i in $(seq 100); do uptime; sleep 1; done
 10:33:07 up  3:08,  1 user,  load average: 0.35, 0.37, 0.44
 10:33:08 up  3:08,  1 user,  load average: 0.35, 0.37, 0.44
 10:33:09 up  3:08,  1 user,  load average: 0.35, 0.37, 0.44
 10:33:10 up  3:08,  1 user,  load average: 0.32, 0.37, 0.44
 10:33:11 up  3:08,  1 user,  load average: 0.32, 0.37, 0.44
 10:33:12 up  3:08,  1 user,  load average: 0.32, 0.37, 0.44
 10:33:13 up  3:08,  1 user,  load average: 0.32, 0.37, 0.44
 10:33:14 up  3:08,  1 user,  load average: 0.32, 0.37, 0.44
 10:33:15 up  3:08,  1 user,  load average: 0.53, 0.41, 0.45
 10:33:16 up  3:08,  1 user,  load average: 0.53, 0.41, 0.45
 10:33:17 up  3:08,  1 user,  load average: 0.53, 0.41, 0.45

```
~~~

### 14. Detach the screen

~~~admonish example title="Keystroke"
Ctrl A + D D (Control A and D and D): detach from screen
~~~

### 15. Check log file

~~~admonish example title="Input"
```bash
cat /root/screenlog.log
```
~~~

~~~admonish collapsible=true title="Example Output"
```bash
controlplane $ cat /root/screenlog.log
controlplane $ for i in $(seq 100); do uptime; sleep 1; done
 10:33:07 up  3:08,  1 user,  load average: 0.35, 0.37, 0.44
 10:33:08 up  3:08,  1 user,  load average: 0.35, 0.37, 0.44
 10:33:09 up  3:08,  1 user,  load average: 0.35, 0.37, 0.44
 10:33:10 up  3:08,  1 user,  load average: 0.32, 0.37, 0.44
 10:33:11 up  3:08,  1 user,  load average: 0.32, 0.37, 0.44
 10:33:12 up  3:08,  1 user,  load average: 0.32, 0.37, 0.44
 10:33:13 up  3:08,  1 user,  load average: 0.32, 0.37, 0.44
 10:33:14 up  3:08,  1 user,  load average: 0.32, 0.37, 0.44
 10:33:15 up  3:08,  1 user,  load average: 0.53, 0.41, 0.45
 10:33:16 up  3:08,  1 user,  load average: 0.53, 0.41, 0.45
 10:33:17 up  3:08,  1 user,  load average: 0.53, 0.41, 0.45
^C
```
~~~


# Look at you, learning Linux 🐧! You used Screen to run different sessions!

Next up: [DNS and Finding Resources](./dns_and_finding_resources.md)
