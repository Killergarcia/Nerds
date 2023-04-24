# Kismet

## GPS

-Requires modification of the Kismet config file

--Located at /etc/kismet/kismet.conf

```
# GPS configuration
# gps=type:options
#
# Kismet supports multiple types of GPS.  Generally you should only activate one of these
# options at a time.
#
# Only one process can open a serial or USB device at the same time; if you are using GPSD,
# make sure not to configure Kismet on the same serial port.
#
# For more information about the GPS types, see the documentation at:
# https://www.kismetwireless.net/docs/readme/gps/
#
# gps=serial:device=/dev/ttyACM0,name=laptop
# gps=tcp:host=1.2.3.4,port=4352
# gps=gpsd:host=localhost,port=2947
# gps=virtual:lat=123.45,lon=45.678,alt=1234
# gps=web:name=gpsweb
```
