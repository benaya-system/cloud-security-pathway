# Day 2 — Auth Logs (Debian / systemd journal)

## Goal
Practice finding authentication/privilege-escalation evidence using system logs (journal), focusing on `sudo` activity.

## Why this matters (security context)
In incident response and auditing, you want to answer:
- WHO did it? (user)
- WHAT did they run? (command)
- WHEN did it happen? (timestamp)
- WHERE from? (TTY + working directory)
- WITH what privilege? (root / uid=0)

## What I searched for
I used the systemd journal as the source of truth (this system does not have `/var/log/auth.log`).

Commands used:

```bash
journalctl --since "today" | grep -Ei "sudo|sshd" | tail -n 120
journalctl --since "15 min ago" | grep -Ei "sudo|pam_unix" | tail -n 80

### Evidence
1) Generate a marker event

I ran a command that reliably creates an auth/privilege log entry:

sudo id

2) Find the marker in the logs

I searched the journal for sudo + PAM session events:
journalctl --since "15 min ago" | grep -Ei "sudo|pam_unix" | tail -n 80


3) Log snippet (paste lines here)

Paste the lines that include:

COMMAND=/usr/bin/id

pam_unix(sudo:session): session opened ...

pam_unix(sudo:session): session closed ...

Interpretation (what the log tells me)

From the sudo[...] line, I can extract:

Actor: the user initiating sudo (e.g., bruno)

Context: terminal (TTY=...) and working directory (PWD=...)

Privilege: action was executed as USER=root

Action: the exact command run (e.g., COMMAND=/usr/bin/id)

Time: timestamp at the beginning of the line

From the pam_unix(sudo:session) lines, I can confirm:

a privileged session opened for root (uid=0) initiated by the user (e.g., bruno (uid=1000))

the session closed normally (useful to detect unusual session behavior)

Conclusions (3 bullets)

I can reliably generate and locate evidence of privilege escalation by executing a real sudo command (e.g., sudo id) and searching for sudo + pam_unix entries in the systemd journal.

The sudo audit line provides strong forensic value: it ties together who ran the command, what command was executed as root, and the context (TTY + PWD), which helps correlate actions during investigations.

On this Debian setup, /var/log/auth.log is not present, so the journal is the primary log source; using focused filters (sudo|pam_unix|sshd) is an efficient way to triage auth-related activity.
