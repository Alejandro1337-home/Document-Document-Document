# Server Hardening

## Introduction

Hardening a system that may have already been compromised, either through standard usage, unnecessary software, or network exposure, is an exercise in futility.

1. **Systems Access:**

### Check for Root Accounts and Blank Passwords
```bash
# Check for accounts with UID 0 (root)
awk -F: '($3=="0"){print}' /etc/passwd
# Check for accounts with blank passwords
cat /etc/shadow | awk -F: '($2==""){print $1}'

# Lock an account
passwd -l accountName

# Check sudoers configuration
sudo visudo

# Check if a user is a member of the sudo group
groups USERNAME
```

2. **Stay Current with Updates**

```bash
# Update package list
sudo yum update

# Remove unused packages
yum list installed

# Upgrade CentOS
sudo yum upgrade

# Enable Unattended Upgrades
sudo yum install yum-cron
sudo systemctl start yum-cron
sudo systemctl enable yum-cron
```

3. **Lock down access to our server even further:**

```bash
# Change SSH port and enhance security
sudo nano /etc/ssh/sshd_config
# Update the following directives:
# Change port
Port 2222
# Limit to IPv4
AddressFamily inet
# Disable root login
PermitRootLogin no
# Disable password authentication
PasswordAuthentication no
```


```bash
# Restart SSH service
sudo systemctl restart sshd

# Allow the new SSH port through the firewall
sudo firewall-cmd --permanent --add-port=2222/tcp
sudo firewall-cmd --reload

# If you have ufw installed 
sudo ufw allow 2222
sudo systemctl restart ufw

# Check active firewall rules
sudo firewall-cmd --list-all
sudo ufw status
```

**Adjust SELinux**

```bash
semanage port -a -t ssh_port_t -p tcp 2222
```


4. **planning to use Rsync?**

When you run an [rsync server on a CentOS system](https://www.server-world.info/en/note?os=CentOS_Stream_9&p=rsync), it listens on port 873 by default.
Port 873 is used for the rsync protocol, a popular tool for synchronizing files and directories between different systems.


```bash
sudo ufw allow from private IP to any port 873
```