# Set Up UFW on CentOS

## Install UFW (if not already installed):

```bash
sudo yum install -y ufw
```
## Enable Packet Forwarding:

1. **Edit sysctl.conf:**

```bash
sudo nano /etc/sysctl.conf
```

Uncomment or add the following line to enable packet forwarding:

```bash
net.ipv4.ip_forward=1
```

Apply changes

```bash
sudo sysctl -p
```

2. **Edit sysconfig/network:**

```bash
sudo nano /etc/sysconfig/network
```

Add or modify the following line:

```bash
FORWARD_IPV4=True
```

Restart the network service:

```bash
sudo systemctl restart network
```