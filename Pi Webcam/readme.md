# Basic webcam service for Pi

## Tested on Raspbian Lite


```
sudo raspi-config
```
```
sudo apt install autoconf automake build-essential pkgconf libtool git libzip-dev libjpeg-dev gettext libmicrohttpd-dev libavformat-dev libavcodec-dev libavutil-dev libswscale-dev libavdevice-dev default-libmysqlclient-dev libpq-dev libsqlite3-dev libwebp-dev
```
```
sudo wget https://github.com/Motion-Project/motion/releases/download/release-4.5.1/$(lsb_release -cs)_motion_4.5.1-1_$(dpkg --print-architecture).deb
```
```
sudo dpkg -i $(lsb_release -cs)_motion_4.5.1-1_$(dpkg --print-architecture).deb
```
```
sudo nano /etc/motion/motion.conf
```

Find the following lines and ensure that they are set to the following values.

```
daemon off
stream_localhost off


Note: Change the following two lines from on to off if you’re having issues with the stream freezing whenever motion occurs.

picture_output off
movie_output off

Optional (Don’t include the text after the -)

stream_maxrate 100 - This change will allow for real-time streaming but requires more bandwidth & resources. Needs to be added to the config file, default is 1
framerate 100 - Changing this option will allow for 100 frames to be captured per second allowing for smoother video, default is 50
width 640 - This line changes the width of the image displayed, default is 640
height 480 - This option changes the height of the image displayed, default is 480
```

MotionEye server will now be running on the Pi

### These commands add the Pi camera module to the system, but that module seems to not work awesome. Maybe deprecated?

```
sudo modprobe bcm2835-v4l2
```
---OR---
```
sudo nano /etc/modules
```

And add this to the bottom
```
bcm2835-v4l2
```


## Sources

https://github.com/Motion-Project/motion

https://pimylifeup.com/raspberry-pi-webcam-server/

