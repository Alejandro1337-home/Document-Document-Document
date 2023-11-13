# Set Up Squid Proxy Server on CentOS

## Install Squid:

```bash
sudo yum install -y squid
```

## Configure Squid:

1. **Edit Squid Configuration:**

```bash
sudo nano /etc/squid/squid.conf
```

Add the following ACl for your private network:

```bash 
acl private_network src 10.0.0.0/24
```

2. **Create Denited Sites Configuration File:**

```bash
sudo touch /etc/squid/denied-sites.conf
sudo nano /etc/squid/denied-sites.conf
```

Add the denied sites (e.g., neverssl.com) to the file:

```bash
neverssl.com
example.com
```
Save and exit the editor.

Include the path to the denied sites configuration file inside '/etc/squid/squid.conf':

```bash 
acl denied_sites url_regex -i "/etc/squid/denied-sites.conf"
http_access deny denied_sites
```
![squid](https://github.com/Iamaguest5/Document-Document-Document/assets/148782286/77ec904f-de06-4e0f-b152-6d0273e7667a)

3. **Update UFW (Assuming you are using UFW):**

```bash
sudo ufw allow 3128
```

4. **Update Firewalld (Assuming you are using firewalld):**

```bash
firewall-cmd --permanent --zone=public --add-port=80/tcp
```

5. **Configure Squid as a Transparent Proxy:**

Add the following iptables rule:

```bash
sudo iptables -t nat -I PREROUTING -p tcp -s 10.0.0.0/24 --dport 80 -j REDIRECT --to-port 3128
```
![wd](https://github.com/Iamaguest5/Document-Document-Document/assets/148782286/d6aa648d-bb7a-4a5c-9360-4e103453157d)

6. **Reload Squid and iptables:**

```bash
sudo systemctl restart squid
sudo service iptables restart
sudo systemctl restart firewalld  # Assuming firewalld is in use, adjust accordingly
sudo systemctl restart ufw        # Assuming ufw is in use, adjust accordingly
```


