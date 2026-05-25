---
title: "Organizing Remote Work: SSH, tmux, and Security"
date: 2026-05-16
summary: "A practical guide to setting up secure remote access to servers, managing sessions with tmux, and protecting connections."
tags:
  - "ssh"
  - "tmux"
  - "security"
  - "remote-work"
  - "linux"
external_link: ""
---

## Introduction

Remote work with servers is an integral part of a researcher's and developer's workflow. Proper SSH configuration, using tmux for long-running sessions, and adhering to security measures allow you to work efficiently and not lose progress even when connections are interrupted.

## SSH: Secure Connection to a Remote Server

SSH (Secure Shell) is a protocol for secure remote server management.

### Basic connection command

ssh username@server_ip_or_domain

### Setting up SSH keys for passwordless login

Generate a key pair (on the local machine):
ssh-keygen -t ed25519 -C "your_email@example.com"

Copy the public key to the server:
ssh-copy-id username@server_ip

After this, login will proceed without a password prompt.

### Disabling password login on the server (for enhanced security)

Edit the file /etc/ssh/sshd_config:
PasswordAuthentication no
PubkeyAuthentication yes

Then restart SSH: sudo systemctl restart sshd

### Port forwarding (tunneling)

Local forwarding (access a remote service via a local port):
ssh -L 8080:localhost:80 username@server_ip

Remote forwarding (access a local service from the server):
ssh -R 9090:localhost:3000 username@server_ip

## tmux: Terminal Multiplexer

tmux allows you to create and manage multiple terminal sessions that continue running after disconnecting from the server.

### Basic commands

Create a new session: tmux new -s session_name

Detach from a session (session remains in the background): Ctrl+B, then D

List sessions: tmux ls

Attach to an existing session: tmux attach -t session_name

Kill a session: tmux kill-session -t session_name

### Hotkeys inside a session (prefix Ctrl+B by default)

Create a new window: Ctrl+B, then C

Switch between windows: Ctrl+B, then window number (0, 1, 2...) or Ctrl+B, then N (next) / P (previous)

Split panel horizontally: Ctrl+B, then "

Split panel vertically: Ctrl+B, then %

Switch between panels: Ctrl+B, then arrow keys

Close the current panel: Ctrl+B, then X (confirm with Y)

### Example workflow

Connect to the server via SSH, run tmux new -s research, inside run a long computation (e.g., python train_model.py), detach from the session (Ctrl+B, then D), close the SSH connection. After a few hours, reconnect to the server via SSH and run tmux attach -t research to see the computation progress.

## Additional Security Measures

Use a non-standard port for SSH (change Port 22 to Port 2222 in /etc/ssh/sshd_config). Disable root login (PermitRootLogin no). Use Fail2ban to block IPs after several failed login attempts. Regularly update the SSH server (sudo apt update && sudo apt upgrade openssh-server). Set up two-factor authentication (google-authenticator).

## Useful Diagnostic Commands

Check active SSH connections on the server: who | grep pts

Check SSH logs: sudo journalctl -u ssh -f

Test connection with verbose output: ssh -vvv username@server_ip

## Results

Secure SSH access to the server has been configured using keys with password login disabled. A workflow with tmux for long-running computational tasks has been established. Additional security measures have been implemented: port change, root login prohibition, Fail2ban.

## Useful Links

OpenSSH Documentation (https://www.openssh.com/), tmux handbook (https://github.com/tmux/tmux/wiki), Fail2ban Guide (https://www.fail2ban.org/), SSH best practices (https://infosec.mozilla.org/guidelines/security/remote-access.html)
