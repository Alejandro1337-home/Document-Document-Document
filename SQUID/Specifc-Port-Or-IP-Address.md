# Configure Squid to Listen on Specific IP Address and Port

By default, the Squid proxy service listens on the 3128 port on all network interfaces. This section describes [how to change the port and configuring Squid to listen on a specific IP address.](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/networking_guide/configuring-the-squid-service-to-listen-on-a-specific-port-or-ip-address#:~:text=By%20default%2C%20the%20Squid%20proxy,port%20on%20all%20network%20interfaces.)

## Prerequisites
+ Squid is installed.

## Edit Squid Configuration:

```bash
sudo nano /etc/squid/squid.conf
```

## Set the Port Number:

To set the port on which the Squid service listens, set the port number in the http_port parameter. For example, to set the port to 8080, set:

```bash
http_port 8080
```

## Configure IP Address and Port:

To configure on which IP address the Squid service listens, set the IP address and port number in the http_port parameter. For example, to configure that Squid listens only on the 192.0.2.1 IP address on port 3128, set:

```bash
http_port 192.0.2.1:3128
```
## Add Multiple Listen Configurations (Optional):

Add multiple http_port parameters to the configuration file to configure that Squid listens on multiple ports and IP addresses:

```bash
http_port 192.0.2.1:3128
http_port 192.0.2.1:8080
```

## Open Port in Firewall (if different from default):

```bash
sudo firewall-cmd --permanent --add-port=8080/tcp
sudo firewall-cmd --reload

sudo ufw allow 8080
sudo restart ufw
```

## Restart Squid:

```bash
sudo systemctl restart squid
```