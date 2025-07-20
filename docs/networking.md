# Networking

## Network settings

Display all network interfaces along with their configuration details.
``` sh
sudo ip addr show
sudo ip a  # Shortcut.
```

Assign an IP address to a network interface:
- ip: The command to manipulate routes and devices.
- addr add: Add an IP address to a device.
- 10.0.0.10/24: The IP address and subnet mask to assign to the interface.
- dev wlan0: Specify the device (network interface) to which the IP address will be added.

``` sh
sudo ip addr add 192.168.100.10/24 dev wlan0
```

Control the state of the network interface.
``` sh
sudo ip link set wlan0 up
sudo ip link set wlan0 down
```

Display the routing table.
``` sh
ip route show
ip r  # Shortcut.
```

Add a default gateway to the routing table.
``` sh
sudo ip route add default via 192.168.100.1 dev wlan0
```

## DNS

Set a custom DNS server.
```sh
sudo vim /etc/resolv.conf

# Add the following line:
# nameserver 8.8.8.8
# nameserver 8.8.4.4
```

## Wireless

The iwctl command is used to configure and manage wireless devices and connections.

``` sh
iwctl
device list
station wlan0 scan
station wlan0 get-networks
station wlan0 connect MY_NETWORK
exit
```

## Hostname

Install the hostname package.
``` sh
sudo pacman -S inetutils
```

Display the system's hostname.
``` sh
hostname
```
## Networking tools

### ping
This is used to test the reachability of a host on an IP network.
``` sh
ping google.com
ping -c 3 google.com
```

### ss
Display information about network connections and sockets. A "socket" is an endpoint of communication on a network. The sockets may be using different protocols, such as TCP or UDP.

This command is used to:
- What network connections are active on your computer.
- What programs are using the network.
- What network ports are in use and by what program.
- Statistics of how the network is being used.


``` sh
ss -t  # Display TCP sockets.
ss -u  # Display UDP sockets.

ss -a # Display all sockets in details (TCP and UDP).
ss -l # Display listening sockets.
ss -n # Display numerical addresses.
ss -p # Display process (programs) using the socket.

ss -tunap
```

### dig
Query DNS servers for information about domain names.
``` sh
dig google.com
```

### nmap
A network scanner used to discover hosts and services on a computer network.
``` sh
nmap -sn 192.168.1.0/24
```

## Persistent Networking

### NetworkManager

Install package and enable the service.
``` sh
sudo pacman -S networkmanager

sudo systemctl enable NetworkManager
sudo systemctl start NetworkManager
```

Set up a connection.
``` sh
nmcli device wifi list
sudo nmcli --ask device wifi connect MY_NETWORK
sudo nmcli connection modify MY_NETWORK connection.autoconnect yes
```
