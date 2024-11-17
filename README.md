# Arch Linux SSH Setup Guide

```bash
# Prerequisites
# Ensure you have a stable internet connection and an up-to-date Arch Linux installation.

# System Update
pacman -Syu

# Install OpenSSH
pacman -S openssh

# Start and Enable SSH Service
systemctl start sshd
systemctl enable sshd

# Configure SSH Server
nano /etc/ssh/sshd_config

# Example Configurations (edit within the nano editor):
# Port 22                # Change the default SSH port (optional)
# PermitRootLogin no     # Disable root login for security
# AllowUsers username    # Allow only specific users (optional)

# After editing, restart SSH service
systemctl restart sshd

# Allow SSH Through Firewall
# If a firewall is active, allow SSH traffic:
# Using ufw:
ufw allow ssh
# Using iptables:
iptables -A INPUT -p tcp --dport 22 -j ACCEPT

# Test SSH Access
ssh username@your-server-ip

# Enable Key-Based Authentication (Optional)
# 1. Generate SSH Key Pair (on the client machine)
ssh-keygen -t rsa -b 4096
# Save the key to the default location (~/.ssh/id_rsa).

# 2. Copy Public Key to Server
ssh-copy-id username@your-server-ip

# 3. Verify Key-Based Login
ssh username@your-server-ip

# 4. Disable Password Authentication (Optional)
nano /etc/ssh/sshd_config
# Inside the file, update:
# PasswordAuthentication no
# Restart the SSH service
systemctl restart sshd

# Troubleshooting
# Check SSH Service Status
systemctl status sshd

# Debug SSH Connection
ssh -v username@your-server-ip

# Verify OpenSSH is Listening on Port
ss -tuln | grep 22

# Secure SSH Setup (Optional)
# Change the Default Port
# Update Port in /etc/ssh/sshd_config to a non-standard port.

# Install Fail2Ban (to block repeated failed login attempts)
pacman -S fail2ban

# Enable Two-Factor Authentication (Optional)
# Use tools like Google Authenticator for extra security.

# Final Steps
# Reboot your system to verify SSH starts on boot
reboot

# Test SSH setup again
ssh username@your-server-ip
