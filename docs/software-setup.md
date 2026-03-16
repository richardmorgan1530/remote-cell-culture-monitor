# Software Setup

This guide describes how to install and configure the software required
to run the **Remote Cell Culture Monitor** system on a **Raspberry Pi
5** using **Raspberry Pi OS 64-bit Lite (headless)**.

The system uses:

-   Raspberry Pi OS Lite
-   Apache2 web server
-   Motion for USB camera streaming
-   Optional secure remote access

------------------------------------------------------------------------

# Hardware Platform

Tested configuration:

  Component               Specification
  ----------------------- -------------------------------
  Single board computer   Raspberry Pi 5
  Operating system        Raspberry Pi OS Lite (64-bit)
  Cameras                 USB microscope cameras
  Storage                 microSD card (32GB or larger)
  Network                 Ethernet or WiFi

------------------------------------------------------------------------

# Install Raspberry Pi OS (Headless)

Download the **Raspberry Pi Imager** from:

https://www.raspberrypi.com/software/

Insert your microSD card and select:

Raspberry Pi OS Lite (64-bit)

This version has **no desktop environment**, which reduces system
overhead and improves stability for server applications.

------------------------------------------------------------------------

# Configure Headless Access

Before flashing the OS, apply OS customisation settings **'EDIT SETTINGS'** in Raspberry Pi Imager.

General Tab Enable:

-   Set hostname (optional)
-   Set username and password
-   Configure wireless LAN (if not using ethernet)

Services Tab Enable:

-   Enable SSH (Use password authentication)

Flash the SD card and insert it into the Raspberry Pi.

Boot the Raspberry Pi and connect via SSH.

Example:
```
ssh pi@raspberrypi.local
```
or
```
ssh pi@192.168.1.50
```
------------------------------------------------------------------------

# Update the System

Once connected, update the OS:
```
sudo apt update sudo apt upgrade -y
```
------------------------------------------------------------------------

# Install Apache2 Web Server

Install Apache:
```
sudo apt install apache2 -y
```
Verify the service is running:
```
sudo systemctl status apache2
```
You should see something similar to:
```
Active: active (running)
```
------------------------------------------------------------------------

# Test the Web Server

Open a browser on your local network and navigate to:
```
http://`<raspberry-pi-ip>`{=html}
```
Example:
```
http://192.168.1.50
```
You should see the default Apache page:
```
Apache2 Debian Default Page
```
------------------------------------------------------------------------

# Web Root Directory

The default web root is:
```
/var/www/html
```
Example files:
```
/var/www/html/index.html
```
You can place your monitoring interface here.

------------------------------------------------------------------------

# Optional: Create a Web Project Directory

Example structure:
```
/var/www/html/camera
```
Create the directory:
```
sudo mkdir /var/www/html/camera
```
Set permissions:
```
sudo chown -R pi:www-data /var/www/html
```
------------------------------------------------------------------------

# Install Motion (USB Camera Streaming)

Install Motion:
```
sudo apt install motion -y
```
Verify installation:
```
motion -h
```
------------------------------------------------------------------------

# Motion Configuration Location

Motion configuration files are located in:
```
/etc/motion/
```
Example contents:
```
/etc/motion
├── motion.conf
├── thread1.conf
├── thread2.conf
├── thread3.conf
└── thread4.conf
```
Each **thread file** corresponds to one camera.

------------------------------------------------------------------------

# Enable Motion Service

Enable Motion to start automatically:
```
sudo systemctl enable motion
```
Start Motion:
```
sudo systemctl start motion
```
Check service status:
```
sudo systemctl status motion
```
------------------------------------------------------------------------

# Detect USB Cameras

List connected cameras:
```
ls /dev/video\*
```
Example:
```
/dev/video0
/dev/video1
/dev/video2
```
You can also use:
```
v4l2-ctl --list-devices
```
------------------------------------------------------------------------

# Test Camera Stream

Once Motion is running, open:
```
http://`<raspberry-pi-ip>`{=html}:8081
```
Example:
```
http://192.168.1.50:8081
```
Each thread exposes a separate port.

------------------------------------------------------------------------

# Typical Camera Ports

| Camera   | Stream Port |
| -------- | ----------- |
| Camera 1 | 8081        |
| Camera 2 | 8082        |
| Camera 3 | 8083        |
| Camera 4 | 8084        |

------------------------------------------------------------------------

# Next Steps

After completing the software setup:

1.  Configure Motion camera threads
2.  Integrate streams into the web interface
3.  Configure remote access
4.  Configure snapshot and timelapse capture

See additional documentation:
```
docs/hardware-setup.md 
docs/network-access.md
```
