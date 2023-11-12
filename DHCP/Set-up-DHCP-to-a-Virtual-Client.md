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
![windwos](https://github.com/Iamaguest5/Document-Document-Document/assets/148782286/4fd6cc68-1304-4853-8293-959e245d1c24)

## Check out the Lease Info!

```bash
cd /var/lib/dhcpd
```
![image](https://github.com/Iamaguest5/Document-Document-Document/assets/148782286/a0e5a938-be16-4daf-8b18-56f323d7b870)
