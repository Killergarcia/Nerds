## Linux Wi-Fi AP

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

