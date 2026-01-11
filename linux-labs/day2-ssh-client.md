# Day 2 — SSH Client Setup (Debian)

## Goal
Configure SSH client safely and authenticate to GitHub using SSH keys.

## What I changed
- Created/edited `~/.ssh/config` for github.com
- Fixed permissions for SSH directory and keys

## Evidence

### SSH key loaded in agent
```text

256 SHA256:+0hDubR54xGKSUXLqYepWOoi65ugPIyVVQf9dzGI6RM bruno@advir.org (ED25519)

### SSH config
Host github.com
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519
  IdentitiesOnly yes
  AddKeysToAgent yes
  PreferredAuthentications publickey

### Permissions
total 28
drwx------  2 bruno bruno 4096 Jan 11 18:54 .
drwx------ 60 bruno bruno 4096 Jan 11 19:46 ..
-rw-------  1 bruno bruno  161 Jan 11 18:54 config
-rw-------  1 bruno bruno  464 Jan  8 16:37 id_ed25519
-rw-r--r--  1 bruno bruno   97 Jan  8 16:37 id_ed25519.pub
-rw-------  1 bruno bruno 2098 Jan  8 16:48 known_hosts
-rw-------  1 bruno bruno 1262 Dec  5 15:15 known_hosts.old

-rw------- 1 bruno bruno 161 Jan 11 18:54 /home/bruno/.ssh/config
-rw------- 1 bruno bruno 464 Jan  8 16:37 /home/bruno/.ssh/id_ed25519
-rw-r--r-- 1 bruno bruno  97 Jan  8 16:37 /home/bruno/.ssh/id_ed25519.pub

### GitHub SSH test
i benaya-system! You've successfully authenticated, but GitHub does not provide shell access.

### What I learned (3 bullets)
**Items to paste in the evidence section (commands):**
```bash
ssh-add -l
cat ~/.ssh/config
ls -la ~/.ssh
ls -la ~/.ssh/config ~/.ssh/id_ed25519 ~/.ssh/id_ed25519.pub
ssh -T git@github.com
