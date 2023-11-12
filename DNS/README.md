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
Add the following lines to the end of the file:

```bash
zone "sysninja" IN {
    type master;
    file "/etc/named/sysninja.zone";
};
```
### Step 3: Create the Zone File
Create a new zone file for "sysninja":

```bash 
sudo nano /etc/named/sysninja.zone
```
Add the following content:
```bash
$TTL 86400
@   IN  SOA     ns.sysninja. root.sysninja. (
               2023111201  ; serial
               3600        ; refresh
               1800        ; retry
               604800      ; expire
               86400       ; minimum TTL
)

; Name Server Information
@           IN  NS  ns.sysninja.

; Default IP address for undefined subdomains
*           IN  A   YOUR_WEBSERVER_IP

```
### Step 4: Start and Enable BIND

```bash
sudo systemctl start named
sudo systemctl enable named
```

## Part B: Lets test TXT Verification to DNS clients!
### Step 5: Add TXT Record for Verification
Edit the sysninja.zone file:
```bash
sudo nano /etc/named/sysninja.zone
```
Add the TXT record under existing content
```bash
; TXT Verification Record
@           IN  TXT "ccLcw6J4v7SGdM2ZhzHBoyFdbVvKh6oGQLQQSEzC4vivBUz35Qz6KVUi6PGSAPJfVH7bNEMpACrKk"

```
### Step 6: Reload BIND
After adding the TXT record, reload BIND to apply the changes:

```bash
sudo systemctl reload named
```
## Part C: SPF Record for Outgoing Mail integration
### Step 7: Update sysninja.zone for SPF Record
Edit the sysninja.zone file once more

```bash
sudo nano /etc/named/sysninja.zone
```
Add the SPF record under the existing content:
```bash
; SPF Record for Outgoing Mail Integration with Google Apps (gmail)
@           IN  TXT "v=spf1 include:_spf.google.com ~all"
```
Step 8: Reload BIND
Reload BIND to apply the changes:
```bash
Reload BIND to apply the changes:
```
Now, you have set up a customized TLD with DNS zone configuration, TXT verification, and SPF record on CentOS using BIND. Replace YOUR_WEBSERVER_IP with the actual IP address of your web server.