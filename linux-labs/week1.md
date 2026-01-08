# Week 1 — Linux Essentials (Day 1)

## Commands I practiced (with examples)
1) pwd — show current directory  
2) ls -la — list files with details  
3) cd — change directory  
4) mkdir -p — create directories  
5) touch — create file  
6) cp / mv / rm — copy, move, remove  
7) cat / less — read files  
8) head / tail — view start/end of files  
9) grep -R "text" . — search text recursively  
10) find . -type f -name "*.md" — find files  
11) whoami / id — user info  
12) chmod / chown — permissions/ownership  
13) ps aux / top — processes  
14) systemctl status ssh — service status  
15) journalctl -xe — inspect logs

## What I learned
- (write 3–6 bullet points in your own words)

## Evidence

### pwd
```bash
pwd
/home/bruno/Projects/cloud-security-pathway

### ls -la
total 36
drwxrwxr-x 8 bruno bruno 4096 Jan  8 17:05 .
drwxrwxr-x 3 bruno bruno 4096 Jan  8 17:01 ..
drwxrwxr-x 2 bruno bruno 4096 Jan  8 17:02 aws-security-labs
drwxrwxr-x 2 bruno bruno 4096 Jan  8 17:07 docs
drwxrwxr-x 2 bruno bruno 4096 Jan  8 17:02 git-workflow
drwxrwxr-x 2 bruno bruno 4096 Jan  8 17:09 linux-labs
drwxrwxr-x 2 bruno bruno 4096 Jan  8 17:02 networking
drwxrwxr-x 2 bruno bruno 4096 Jan  8 17:02 python-security-automation
-rw-rw-r-- 1 bruno bruno  905 Jan  8 17:05 README.md

### whoami
bruno

### id
uid=1000(bruno) gid=1000(bruno) groups=1000(bruno),24(cdrom),25(floppy),27(sudo),29(audio),30(dip),44(video),100(users),101(netdev),102(scanner),106(bluetooth),108(lpadmin),984(ollama),985(docker)

### ps aux | head
```bash
ps aux | head
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.0  24688 15708 ?        Ss   16:25   0:02 /sbin/init
root           2  0.0  0.0      0     0 ?        S    16:25   0:00 [kthreadd]
root           3  0.0  0.0      0     0 ?        S    16:25   0:00 [pool_workqueue_release]
root           4  0.0  0.0      0     0 ?        I<   16:25   0:00 [kworker/R-kvfree_rcu_reclaim]
root           5  0.0  0.0      0     0 ?        I<   16:25   0:00 [kworker/R-rcu_gp]
root           6  0.0  0.0      0     0 ?        I<   16:25   0:00 [kworker/R-sync_wq]
root           7  0.0  0.0      0     0 ?        I<   16:25   0:00 [kworker/R-slub_flushwq]
root           8  0.0  0.0      0     0 ?        I<   16:25   0:00 [kworker/R-netns]
root          10  0.0  0.0      0     0 ?        I<   16:25   0:00 [kworker/0:0H-events_highpri]

### journalctl -xe | head -n 30
Hint: You are currently not seeing messages from other users and the system.
      Users in groups 'adm', 'systemd-journal' can see all messages.
      Pass -q to turn off this notice.
Jan 08 16:25:42 debian systemd[4549]: Listening on pk-debconf-helper.socket - debconf communication socket.
░░ Subject: A start job for unit UNIT has finished successfully
░░ Defined-By: systemd
░░ Support: https://www.debian.org/support
░░ 
░░ A start job for unit UNIT has finished successfully.
░░ 
░░ The job identifier is 19.
Jan 08 16:25:42 debian systemd[4549]: Listening on speech-dispatcher.socket - Speech Dispatcher Socket.
░░ Subject: A start job for unit UNIT has finished successfully
░░ Defined-By: systemd
░░ Support: https://www.debian.org/support
░░ 
░░ A start job for unit UNIT has finished successfully.
░░ 
░░ The job identifier is 27.
Jan 08 16:25:42 debian systemd[4549]: Starting ssh-agent.socket - OpenSSH Agent socket...
░░ Subject: A start job for unit UNIT has begun execution
░░ Defined-By: systemd
░░ Support: https://www.debian.org/support
░░ 
░░ A start job for unit UNIT has begun execution.
░░ 
░░ The job identifier is 23.
Jan 08 16:25:42 debian systemd[4549]: Listening on gpg-agent-ssh.socket - GnuPG cryptographic agent (ssh-agent emulation).
░░ Subject: A start job for unit UNIT has finished successfully
░░ Defined-By: systemd
░░ Support: https://www.debian.org/support
░░ 
░░ A start job for unit UNIT has finished successfully.








