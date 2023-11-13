# Set Up Firewalld on CentOS with Packet Forwarding and NAT Rules

## Install Firewalld (if not already installed):

```bash
sudo yum install -y firewalld
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

## Configure Firewalld:

3. **Allow incoming SSH traffic (optional)**

```bash
sudo firewall-cmd --permanent --add-service=ssh
```
4. **Enable Masquerade for NAT:**

```bash
sudo firewall-cmd --permanent --zone=public --add-masquerade
```

5. **Add Custom NAT Rules:**
Edit /etc/firewalld/before.rules:

```bash
sudo nano /etc/firewalld/before.rules
```
Add the following NAT rules at the top:

```bash
*nat
:POSTROUTING ACCEPT [0:0]

# MASQUERADE rule
-A POSTROUTING -s 10.0.0.0/24 -o ens160 -j MASQUERADE

# End of NAT table
COMMIT
```

Save and exit the editor.

6. **Reload Firewalld:**

```bash
sudo systemctl restart firewalld
```

## Verify NAT Rules:

```bash
sudo iptables -t nat -L -n -v
```
![ufw](https://github.com/Iamaguest5/Document-Document-Document/assets/148782286/9f5b0735-84cb-4794-ba82-119e52a51bd2)
