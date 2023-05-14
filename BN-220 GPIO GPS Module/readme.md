# BN-220 GPIO GPS Module

Small form factor GPS module, works on Pi and Arduino and anything else that can handle serial data input I assume

## GPIO from GPS to Pi

![BN-220 Pinout](BN-220_pinout.jpg)

![GPS to Pi - Not BN-220 specific](rpi-gps_pinout.JPG)

GPIO connection diagrams for module and Pi. Note that the picture of the pi connecting to the GPS module is *not* BN-220 specific.

## Using on Raspbian

### You have to enable the Serial connection for GPIO on the Pi

```
sudo raspi-config
```

Select "Interfaces"

Select "Serial"

For "Serial login shell" choose whatever fits your needs

For "Serial interface" choose Enable

### Installing GPSD and Configuring

To check GPS activity on serial port - after running this command you should see data. If nothing happens the module may not be connected correctly.

```
cat /dev/serial0
```




## Source for Steps

https://maker.pro/raspberry-pi/tutorial/how-to-use-a-gps-receiver-with-raspberry-pi-4


## Purchase Link

https://www.amazon.com/dp/B086ZK9BT4?psc=1&ref=ppx_yo2ov_dt_b_product_details