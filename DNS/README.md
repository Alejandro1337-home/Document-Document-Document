# Instructions on setting up DNS on your CentOS machine

---

# Setting Up a Custom TLD with DNS on CentOS

## Part A: Configuring DNS for Customized TLD

### Step 1: Install BIND

```bash
sudo dnf install bind bind-utils
```
### Step 2: Configure BIND
Edit the BIND main configuration file:

```bash
sudo nano /etc/named.conf
```