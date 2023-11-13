# Set Up UFW on CentOS
On CentOS, the standard tool for configuring firewalls is firewalld. If you still want to use ufw on CentOS, you need to install it since it's not available by default.
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

6. **Reload UFW:**

```bash
sudo ufw reload
```

## Verify NAT Rules:

```bash
sudo iptables -t nat -L -n -v
```
