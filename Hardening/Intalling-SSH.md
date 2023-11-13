# Enable and Configure SSH on CentOS 

## Introduction

Secure Shell (SSH) is a cryptographic protocol that allows a client to interact with a remote server in a secure environment. High-level encryption protects the exchange of sensitive information and allows file transfer or issue commands on remote machines securely.


## Prerequisites

- CentOS system to act as an SSH server
- A user with necessary permissions

## Installing and Enabling OpenSSH on CentOS 

1. **Install OpenSSH Server Software Package**

Enter the following command from your terminal to start the installation process:

```bash
sudo yum -y install openssh-server openssh-clients
```

This command installs both the OpenSSH client applications and the OpenSSH server daemon, sshd.

2. **Starting SSH Service:**

To start the SSH daemon on the OpenSSH server:

```bash
sudo systemctl start sshd
```

When active, sshd continuously listens for client connections from any of the client tools. When a connection request occurs, sshd sets up the correct connection.

3. **Check 'sshd' status:**

Check the status of the SSH daemon:

```bash
sudo systemctl status sshd
```

As we have previously started the service, the output confirms that it is active

**Check sshd status with systemctl command**

To stop the SSH daemon, enter:

```bash
sudo systemctl stop sshd
```
We can check if the service has stopped by verifying the status. The output shows that the service is inactive and the time and date when the status last changed.

4. **Enable OpenSSH Service:**

Enable SSH to start automatically after each system reboot by using the systemctl command:

```bash
sudo systemctl enable sshd
```

To disable SSH after reboot, enter:

```bash
sudo systemctl disable sshd
```
