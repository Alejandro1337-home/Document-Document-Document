# DHCP Server Setup Guide

This guide walks you through setting up a DHCP server  on CentOS.

To learn more about DHCP on CentOS click here:

[Running a DHCP server on CentOS](https://hostingultraso.com/help/centos/running-dhcp-server-centos)

## CentOS DHCP Configuration

1. **Add Additional Adapter:**
   - Edit VM settings and add an extra network adapter if not done previously.

2. **Identify New Interface:**
   - Run `ip addr` to show the new interface. Note its name (e.g., `ens33`).

3. **Configure Static IP with nmcli:**

```bash
sudo nmcli connection modify ens33 ipv4.addresses "10.0.0.250/24" ipv4.gateway "10.0.0.1" ipv4.dns "8.8.8.8, 8.8.4.4"
sudo nmcli connection up ens33
```

4. **Install DHCP Server:**

```bash
sudo dnf -y install dhcp-server
```
5. **Configure DHCP Server:**
Edit /etc/dhcp/dhcpd.conf and define scopes.
```bash
# Example DHCPd configuration (/etc/dhcp/dhcpd.conf)
subnet 10.0.0.0 netmask 255.255.255.0 {
  range 10.0.0.1 10.0.0.100;
  range 10.0.0.201 10.0.0.215;
  option routers 10.0.0.1;
  option domain-name-servers 8.8.8.8, 8.8.4.4;
  option domain-name "sysninja";
  default-lease-time 3600;
  max-lease-time 7200;
  authoritative;
}
```
![dhcp](https://github.com/Iamaguest5/Document-Document-Document/assets/148782286/658fb28b-1f2f-4111-be6a-e81683e27f28)


6. **Assign DHCP Server to Connect Interface:**
Edit /etc/sysconfig/dhcpd to specify the interface.

```bash
# Example interface setting (/etc/sysconfig/dhcpd)
DHCPDARGS=ens33
```
7. **Restart the service:**

```bash
sudo systemctl enable dhcpd.service
sudo systemctl restart dhcpd.service
```

## Testing

[I suggest clicking this link to test your dhcp service.](Set-up-DHCP-to-a-Virtual-Client.md)
