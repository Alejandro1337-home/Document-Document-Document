# Network Services Using Centos 9
# Table of Contents
1. [Overview of CentOS](#Overview)
2. [Installation](#install)
3. [DNS](#dns)
4. [DHCP](#dhcp)
5. [UFW](#ufw)
6. [Squid Proxy](#squid-proxy)
7. [Hardening](#hardening)
## Overview of CentOS <a name="Overview"></a>

### CentOS (Community ENTerprise Operating System):

- CentOS is a free and open-source Linux distribution that is community-supported and derived from the source code of Red Hat Enterprise Linux (RHEL).
- It aims to provide a stable, reliable, and secure platform suitable for enterprise-level deployments.

### Purpose of CentOS:

- CentOS is designed to be a downstream, binary-compatible, and free alternative to RHEL, allowing users to enjoy the benefits of RHEL without the associated costs.
- It is well-suited for servers, workstations, and various computing environments where stability and compatibility are paramount.

## Network Services Overview:

CentOS can provide a range of network services, including:

1. **DNS (Domain Name System):**
   - CentOS can function as a DNS server, translating human-readable domain names into IP addresses and vice versa.

2. **DHCP (Dynamic Host Configuration Protocol):**
   - As a DHCP server, CentOS can dynamically assign IP addresses and network configuration parameters to devices on the network, simplifying network management.

3. **UFW (Uncomplicated Firewall):**
   - CentOS includes UFW for managing firewall rules. It helps control incoming and outgoing network traffic, enhancing the security of the system.

4. **Squid Proxy:**
   - CentOS can be configured as a Squid proxy server, facilitating caching and controlling access to web resources, improving network performance and security.

5. **Hardening:**
   - SSH Hardening:
   Restrict Root Access: Disable direct root login by setting PermitRootLogin no in /etc/ssh/sshd_config.
   Enhance Authentication: Enforce SSH key authentication (PasswordAuthentication no) and consider implementing Two-Factor Authentication (2FA).
   - User Rules:
   Limit Privileges: Use sudo to control user administrative access, minimizing the use of root privileges.
   Password Security: Enforce strong password policies (pam_pwquality) and implement account lockout mechanisms for added security.
   These succinct configurations enhance security by restricting access and implementing robust authentication measures.

## Supported Network Topology:

CentOS supports a flexible network topology with various interfaces:

1. **Ethernet Interfaces:**
   - CentOS supports Ethernet interfaces (e.g., eth0, eth1) for wired network connections.

2. **Wireless Interfaces:**
   - Wireless network interfaces (e.g., wlan0) are supported for wireless connectivity.

3. **Virtual Interfaces:**
   - CentOS can manage virtual interfaces (e.g., VLANs, bridges) to segment and control network traffic.

4. **Loopback Interface:**
   - The loopback interface (lo) is supported for communication between processes on the same system.

5. **Tunneling Interfaces:**
   - CentOS supports tunneling interfaces (e.g., tun, tap) for virtual private network (VPN) configurations.

**Description:**
- The supported network topology depends on the specific hardware and networking requirements. CentOS provides tools and configurations to manage and adapt to various network environments, ensuring connectivity and performance.

---

## Installation <a name="install"></a>

### 1. Download CentOS ISO:
- Go to [official CentOS download page](https://www.centos.org/centos-stream/).
- Download the ISO image for the desired version.

### 2. Set Up VMware Workstation:
- Open VMware Workstation on your host machine.
- Create a new virtual machine for CentOS.

### 3. Install CentOS on VMware:
- Attach the CentOS ISO to the virtual machine.
- Power on the virtual machine and start the CentOS installation.

### 4. Follow the CentOS Installation Process:
- Follow steps 5 to 15 in the general installation process.
  - Language and Localization
  - Date and Time
  - Installation Source
  - Installation Destination
  - Network Configuration
  - Software Selection
  - Begin Installation
  - Root Password
  - User Creation
  - Reboot
  - Post-Installation Configuration

### 5. VMware Tools (Optional):
- After CentOS is installed, consider installing VMware Tools for better integration.
  - Mount the VMware Tools ISO.
  - Install the tools following VMware's instructions.

### 6. Post-Installation VMware Configuration (Optional):
- Configure additional settings within VMware Workstation.
  - Adjust display resolution, networking options, etc.

### 7. Done!
- Your CentOS 9 VM on VMware Workstation is now ready for use.

---

## DNS <a name="dns"></a>

[Instructions for DNS](DNS/README.md)

Setting up DNS on CentOS involves installing the BIND software, configuring the main **named.conf** file, and creating forward and reverse zone files to map domain names to IP addresses. Customize the zone files to define the authoritative DNS server, domain, and associated IP addresses. Ensure that the configurations comply with the network's requirements and restart the BIND service for changes to take effect.

---

## DHCP <a name="dhcp"></a>

[Instructions for DHCP](DHCP/README.md)

Configuring DHCP (Dynamic Host Configuration Protocol) on CentOS streamlines network management by automatically assigning IP addresses and essential network parameters to connected devices. Install the DHCP server package using yum, edit the configuration file at **/etc/dhcp/dhcpd.conf** to define IP address ranges, subnet masks, and other settings. Ensure proper permissions, start the DHCP service with **systemctl start dhcpd**, and enable it to start at boot using **systemctl enable dhcpd**. DHCP simplifies network administration, providing dynamic and efficient IP address allocation to devices within the network.

---

## UFW <a name="ufw"></a>

[Instructions for UFW](UFW/README.md)

 user-friendly command-line utility for managing iptables, the default firewall management tool on CentOS. UFW simplifies the process of configuring firewall rules by providing an easy-to-understand syntax. Install UFW using yum, enable it to start at boot with **systemctl enable ufw**, and start the service with **systemctl start ufw**. Define rules for allowed and denied connections using straightforward commands like **ufw allow** or **ufw deny**. UFW enhances security on CentOS by providing a simplified interface for managing firewall settings, making it accessible for users with varying levels of expertise.

---

## Squid Proxy <a name="squid-proxy"></a>

[Instructions for Squid](SQUID/README.md)

Squid is a popular proxy server and web cache daemon that enhances network performance and security on CentOS. By caching frequently accessed web content, Squid accelerates browsing and reduces bandwidth usage. Install Squid using yum, configure access control lists (ACLs) in **/etc/squid/squid.conf** to define policies for network access, and start the service with **systemctl start squid**. Squid can also be configured as a transparent proxy, intercepting and redirecting web traffic seamlessly. With its robust features, Squid plays a crucial role in optimizing network resources and providing content filtering capabilities on CentOS systems.

---

## Hardening <a name="hardening"></a>

When hardening CentOS with a focus on SSH and user rules, administrators should take steps to secure remote access and user authentication. This involves configuring SSH to use key-based authentication, disabling root login, and specifying allowed users. Additionally, implement firewall rules, using tools like UFW or firewalld, to control incoming and outgoing network traffic. Enforce strong password policies, regularly audit user accounts, and consider employing tools like fail2ban to mitigate brute force attacks. By combining these measures, administrators can significantly enhance the security of SSH access and user accounts on a CentOS system.
