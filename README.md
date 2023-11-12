# Network Services Using Centos 9
# Table of Contents
1. [Introduction](#intro)
2. [Install](#install)
3. [DNS](#dns)
4. [DHCP](#dhcp)
5. [UFW](#ufw)
6. [Squid Proxy](#squid-proxy)
## Introduction <a name="intro"></a>

### [Description of your server (appliance)](description.md)
[Provide a brief overview of your CentOS server and its purpose.]

### [Overview of network services](network-services.md)
[List the network services that your appliance provides.]

### [Supported network topology (interfaces)](network-topology.md)
[Describe the network topology and interfaces supported by your CentOS server.]

### [Special instructions for initial distro install](initial-install.md)
[Add any special instructions or configurations needed during the initial CentOS installation.]

---

## Install <a name="install"></a>

## 1. Download CentOS ISO:
- Go to [official CentOS download page](https://www.centos.org/centos-stream/).
- Download the ISO image for the desired version.

## 2. Set Up VMware Workstation:
- Open VMware Workstation on your host machine.
- Create a new virtual machine for CentOS.

## 3. Install CentOS on VMware:
- Attach the CentOS ISO to the virtual machine.
- Power on the virtual machine and start the CentOS installation.

## 4. Follow the CentOS Installation Process:
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

## 5. VMware Tools (Optional):
- After CentOS is installed, consider installing VMware Tools for better integration.
  - Mount the VMware Tools ISO.
  - Install the tools following VMware's instructions.

## 6. Post-Installation VMware Configuration (Optional):
- Configure additional settings within VMware Workstation.
  - Adjust display resolution, networking options, etc.

## 7. Done!
- Your CentOS 9 VM on VMware Workstation is now ready for use.

---

## DNS <a name="dns"></a>

[Instructions for DNS](DNS/dns-instructions)

[Include information about setting up and configuring DNS on your CentOS server.]

---

## DHCP <a name="dhcp"></a>

[Instructions for DHCP](DHCP/dhcp-Instructions)

[Include information about setting up and configuring DHCP on your CentOS server.]

---

## UFW <a name="ufw"></a>

[Instructions for DHCP](UFW/ufw-Instructions)

[Include information about setting up and configuring UFW on your CentOS server.]

---

## Squid Proxy <a name="squid-proxy"></a>

[Instructions for DHCP](SQUID/Squid-Instructions)

[Include information about setting up and configuring Squid on your CentOS server.]