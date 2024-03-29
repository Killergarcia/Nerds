## Linux Wi-Fi AP

## This is using hostapd and dnsmasq on a Pi Zero W
Had to install hostapd and dnsmasq

```
sudo apt install hostapd
sudo apt install dnsmasq
```

I created a directory to hold my config files, so for me it's:

```
mkdir /home/user/wifi-ap
cd /home/user/wifi-ap
```

### Create hostapd config

```
nano hostapd.conf
```

My hostapd.conf has the following:

```
interface=wlan0

ssid=Hotspot-AP
channel=1

auth_algs=3
wpa=3
wpa_passphrase=password
wpa_key_mgmt=WPA-PSK
wpa_pairwise=CCMP
rsn_pairwise=CCMP
```

### Edit dnsmasq config

```
sudo nano /etc/dnsmasq.conf
```

```
interface=wlan0
dhcp-range=192.168.10.3,192.168.10.10,12h
```

## Order of Operations

1. Login
2. Check dnsmasq status - ensure it's got the log saying what IP range it's serving so you know it's bueno 

```
sudo systemctl status dnsmasq
```

5. Set wlan0 interface IP Address

You could probably automate this but I'm lazy

```
sudo ip link set wlan0 down # Shouldn't need this but I do it to be sure
sudo ip addr add 192.168.10.1/24 dev wlan0
sudo ip link set wlan0 up
```

7. cd into config folder we made

```
cd /home/user/wifi-ap
```

9. Command to start AP

```
sudo hostapd -B hostapd.conf
```

At this point I can connect, receive an address within the 192.168.10.3-10 range and can SSH.


I stole this from here - had to tweak some stuff but the gist is the same:

https://unix.stackexchange.com/questions/77530/setting-up-an-ad-hoc-network-on-boot


<3

# This is using some DUMB SHIT
## Like for real this is way harder than above
### Find wlan device names

```
ip link show / ifconfig / iwconfig
```
### Creating Hotspot Connection

```
IFNAME="[interfacename]"
CON_NAME="myhotspot"
nmcli con add type wifi ifname $IFNAME con-name $CON_NAME autoconnect yes ssid $CON_NAME
```

### Share the connection we just made
```
nmcli con modify $CON_NAME 802-11-wireless.mode ap 802-11-wireless.band bg ipv4.method shared
```

### Set Password on AP
```
nmcli con modify $CON_NAME wifi-sec.key-mgmt wpa-psk
nmcli con modify $CON_NAME wifi-sec.psk "MyStrongHotspotPass"
```

### Bring the connection up
```
nmcli con up $CON_NAME
```

### Confirm 
```
nmcli connection show
```
```
ip ad show [interfacename]
```

