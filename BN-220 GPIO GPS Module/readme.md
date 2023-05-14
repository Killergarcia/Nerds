# BN-220 GPIO GPS Module

Small form factor GPS module, works on Pi and Arduino and anything else that can handle serial data input I assume

## GPIO from GPS to Pi

![BN-220 Pinout](BN-220_pinout.jpg)(rpi-gps_pinout.JPG)

![GPS to Pi - Not BN-220 specific](rpi-gps_pinout.JPG)

GPIO connection diagrams for module and Pi. Note that the picture of the pi connecting to the GPS module is *not* BN-220 specific.

## Using on Raspbian

### You have to enable the Serial connection for GPIO on the Pi

```
sudo raspi-config
```

Select "Interfaces" -> "Serial"

For "Serial login shell" choose whatever fits your needs

For "Serial interface" choose Enable

### Installing GPSD and Configuring

To check GPS activity on serial port - after running this command you should see data. If nothing happens the module may not be connected correctly.

```
cat /dev/serial0
```


### Reading the Position Data

# I want to check these to see what's actually necessary

Stop the GPSD service that runs by default so we can change settings

```
sudo systemctl stop gpsd.socket
```

Note that you'll have to type this command every time you boot up the system. Alternatively, you can also disable it entirely:

```
sudo systemctl disable gpsd.socket
```

Start a new gpsd instance that redirects the data of the correct serial port to a socket: 

# Might be able to manually change gpsd.sock settings to force it to use serial0?

```
sudo gpsd /dev/serial0 -F /var/run/gpsd.sock
```

Display the GPS data

```
sudo cgps -s
```



## Source for Steps

https://maker.pro/raspberry-pi/tutorial/how-to-use-a-gps-receiver-with-raspberry-pi-4


## Purchase Link

https://www.amazon.com/dp/B086ZK9BT4?psc=1&ref=ppx_yo2ov_dt_b_product_details