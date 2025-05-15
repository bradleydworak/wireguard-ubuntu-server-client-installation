# wireguard-ubuntu-server-client-installation
## Install WireGuard VPN on Ubuntu 24.04 with iOS Peer Configuration

**Note:** These instructions are intended for IPv4 only. For IPv6 addresses please visit [How To Set Up WireGuard on Ubuntu 20.04](https://www.digitalocean.com/community/tutorials/how-to-set-up-wireguard-on-ubuntu-20-04#step-2-choosing-ipv4-and-ipv6-addresses)

### Step 1: Install WireGuard on Ubuntu (as server)

* `sudo apt install wireguard`

* `sudo apt autoremove`

### Step 2: Choosing an IPv4 range and listen port for server and peers

[See link](https://www.digitalocean.com/community/tutorials/how-to-set-up-wireguard-on-ubuntu-20-04#step-2-a-choosing-an-ipv4-range)

### Step 3: Generate WireGuard configuration files for server and peers

[Configuration site](https://www.wireguardconfig.com)

* Enter listening post number (ex. 51820)
* Enter number of clients (ensure you specify a sufficient amount, otherwise you will need to reconfigure Wirecutter)
* Enter CIDR address block for the internal IP range for the clients (ex. 10.0.0.0/24)
* Enter mask for the Client Allowed IP range (ex. if you want no restrictions on IP accessibility, you can enter : 0.0.0.0/0, ::/0 )
* Enter Endpoint IP, which is the public IP address of your server, and append the listening port number from above (ex. 123.456.78.90:51820)
* Enter DNS if you want to route all traffic through the VPN, so that the clients can access external sites (ex. Google DNS is 8.8.8.8, 8.8.4.4)
* Ensure that the Post-Up and Post-Down firewall rules match your network interface name (ex. check eth0 by default is the desired network interface)
* Check Use Pre-Shared Keys for enhanced security
* Click Generate Config button
* A list of configurations for the server and clients will appear on the page below (may need to scroll down to see them)

### Step 4: Server configuration
* Copy the complete server configuration ([Interface] and all [Peer]) text generated above to the WireGuard configuration file on the server (ex. /etc/wireguard/wg1.conf)
* Add any other desired firewall settings for PostUp and PostDown
* Start the service `sudo systemctl start wg-quick@wg1.service`

### Step 5: Configure your clients (using the QR code)
* Open Wireguard app, select add tunnel, and use the QR code feature to import client configuration file
* Ensure the settings match the configuration list
* Start the client VPN
* Ensure that all traffic is being routed through VPN



