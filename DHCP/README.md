# DHCP Server Setup Guide

This guide walks you through setting up a DHCP server on Ubuntu and CentOS.

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

6. **Assign DHCP Server to Connect Interface:**
Edit /etc/sysconfig/dhcpd to specify the interface.

```bash
# Example interface setting (/etc/sysconfig/dhcpd)
DHCPDARGS=ens33
```
# Set Up Virtual Client on VMware (Same VMnet)

## Configure VMnet:

1. Ensure both DHCP server and client are on the same VMnet.
2. Open VMware, navigate to `Edit` > `Virtual Network Editor`.
3. Note the VMnet number being used (e.g., VMnet2).

## Create Virtual Client:

1. Create a new virtual machine for the client.
2. During configuration, select the same VMnet as the DHCP server.

## Configure Client to Obtain IP via DHCP:

1. In the client's network settings, set it to obtain an IP address automatically.

## Test DHCP on Client:

1. Start the virtual client.
2. Check if the client successfully receives an IP address from the DHCP server.
