# Set Up UFW on CentOS
On CentOS, the standard tool for configuring firewalls is [firewalld](CentOS Firewalld.md). If you still want to use ufw on CentOS, you need to install it since it's not available by default.
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
![ctl](https://github.com/Iamaguest5/Document-Document-Document/assets/148782286/69f7fa50-4607-48d5-a13a-12435c6db4bb)

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
![network](https://github.com/Iamaguest5/Document-Document-Document/assets/148782286/135b0c29-4986-4d76-8248-b7162194ead4)

Restart the network service:

```bash
sudo systemctl restart network
```
## Configure UFW:

3. **Allow incoming SSH Traffic (Optional):**

```bash
sudo ufw allow OpenSSH
```

4. **Enable UFW:**

```bash
sudo ufw enable
```

5. **Add NAT Rules:**

Edit '/etc/ufw/before.rules':

```bash
sudo nano /etc/ufw/before.rules
```

Add the following NAT rules at the top:

```bash
# NAT table rules
*nat
:POSTROUTING ACCEPT [0:0]

# MASQUERADE rule
-A POSTROUTING -s 10.0.0.0/24 -o ens160 -j MASQUERADE

# End of NAT table
COMMIT
```
Save and exit the editor.
![ufww](https://github.com/Iamaguest5/Document-Document-Document/assets/148782286/a627b71c-a536-414b-a15e-a5c5d0b3da3a)

6. **Reload UFW:**

```bash
sudo ufw reload
```

## Verify NAT Rules:

```bash
sudo iptables -t nat -L -n -v
```
![ufw](https://github.com/Iamaguest5/Document-Document-Document/assets/148782286/9f5b0735-84cb-4794-ba82-119e52a51bd2)
