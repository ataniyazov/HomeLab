WireGuard_Installation

https://browserleaks.com/ip - test ip and dns leak

### Installation

#### On Debian/Ubuntu

1. **Update the system:**
   ```bash
   sudo apt update
   sudo apt upgrade -y
   ```

2. **Install WireGuard:**
   ```bash
   sudo apt install wireguard -y
   ```

3. **Install additional tools:**
   ```bash
   sudo apt install wireguard-tools -y
   ```

### Configuration

#### Generate Keys

On each device (server and clients), generate private and public keys:

```bash
wg genkey | tee privatekey | wg pubkey > publickey
```

#### Server Configuration

1. **Create the configuration file:**
   ```bash
   sudo nano /etc/wireguard/wg0.conf
   ```

2. **Edit the server configuration:**

   ```ini
   [Interface]
   Address = 10.0.0.1/24, fd86:ea04:1115::1/64
   SaveConfig = true
   PrivateKey = <server-private-key>
   ListenPort = 51820
   
   [Peer]
   # Client 1
   PublicKey = <client1-public-key>
   AllowedIPs = 10.0.0.2/32, fd86:ea04:1115::2/128
   
   [Peer]
   # Client 2
   PublicKey = <client2-public-key>
   AllowedIPs = 10.0.0.3/32, fd86:ea04:1115::3/128
   ```

3. **Start and enable WireGuard:**
   ```bash
   sudo systemctl start wg-quick@wg0
   sudo systemctl enable wg-quick@wg0
   ```

#### Client Configuration

**Client 1:**

1. **Create the configuration file:**
   ```bash
   sudo nano /etc/wireguard/wg0.conf
   ```

2. **Edit the client 1 configuration:**

   ```ini
   [Interface]
   Address = 10.0.0.2/24, fd86:ea04:1115::2/64
   PrivateKey = <client1-private-key>
   DNS = 1.1.1.1

   [Peer]
   PublicKey = <server-public-key>
   Endpoint = <server-ip>:51820
   AllowedIPs = 0.0.0.0/0, ::/0
   PersistentKeepalive = 25
   ```

**Client 2:**

1. **Create the configuration file:**
   ```bash
   sudo nano /etc/wireguard/wg0.conf
   ```

2. **Edit the client 2 configuration:**

   ```ini
   [Interface]
   Address = 10.0.0.3/24, fd86:ea04:1115::3/64
   PrivateKey = <client2-private-key>
   DNS = 1.1.1.1

   [Peer]
   PublicKey = <server-public-key>
   Endpoint = <server-ip>:51820
   AllowedIPs = 0.0.0.0/0, ::/0
   PersistentKeepalive = 25
   ```

3. **Start and enable WireGuard on clients:**
   ```bash
   sudo systemctl start wg-quick@wg0
   sudo systemctl enable wg-quick@wg0
   ```

### Firewall Configuration

#### On the Server

1. **Allow WireGuard traffic:**
   ```bash
   sudo ufw allow 51820/udp
   ```

2. **Enable IP forwarding:**
   ```bash
   echo "net.ipv4.ip_forward=1" | sudo tee -a /etc/sysctl.conf
   echo "net.ipv6.conf.all.forwarding=1" | sudo tee -a /etc/sysctl.conf
   sudo sysctl -p
   ```

3. **Set up NAT for IPv4 and IPv6:**
   ```bash
   sudo iptables -t nat -A POSTROUTING -s 10.0.0.0/24 -o eth0 -j MASQUERADE
   sudo ip6tables -t nat -A POSTROUTING -s fd86:ea04:1115::/64 -o eth0 -j MASQUERADE
   ```

4. **Make the NAT rules persistent:**
   ```bash
   sudo apt install iptables-persistent
   sudo netfilter-persistent save
   sudo netfilter-persistent reload
   ```

### Enable IPv4 and IPv6 Tunneling

1. **Ensure IPv4 and IPv6 forwarding are enabled:**
   ```bash
   sudo sysctl -w net.ipv4.ip_forward=1
   sudo sysctl -w net.ipv6.conf.all.forwarding=1
   ```

2. **Confirm the settings are persistent across reboots:**
   ```bash
   sudo nano /etc/sysctl.conf
   ```
   - Ensure the following lines are present:
     ```
     net.ipv4.ip_forward=1
     net.ipv6.conf.all.forwarding=1
     ```

### Hide IPv6

To hide IPv6 addresses:

1. **Use IPv4 for main communication and set up NAT for IPv6 as mentioned.**

2. **Add the following to the server configuration to avoid exposing the actual IPv6 address:**
   ```bash
   ip6tables -t nat -A POSTROUTING -o wg0 -j MASQUERADE
   ```

### Hide Personal IP When Using

To mask the personal IP of the clients:

1. **Ensure all traffic is routed through the VPN:**
   - This is already configured in the client’s AllowedIPs setting `0.0.0.0/0, ::/0`.

### Common Commands on Using WireGuard

1. **Check WireGuard status:**
   ```bash
   sudo wg show
   ```

2. **Bring up the WireGuard interface:**
   ```bash
   sudo wg-quick up wg0
   ```

3. **Bring down the WireGuard interface:**
   ```bash
   sudo wg-quick down wg0
   ```

4. **Enable WireGuard service:**
   ```bash
   sudo systemctl enable wg-quick@wg0
   ```

5. **Disable WireGuard service:**
   ```bash
   sudo systemctl disable wg-quick@wg0
   ```

6. **Restart WireGuard service:**
   ```bash
   sudo systemctl restart wg-quick@wg0
   ```

By following these steps, you'll have a fully functional WireGuard VPN with proper IPv4 and IPv6 tunneling, firewall configurations, and measures to hide IPv6 addresses and personal IPs.
