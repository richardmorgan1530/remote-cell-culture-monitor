# Remote Cell Culture Monitor

![Platform](https://img.shields.io/badge/platform-Raspberry%20Pi-red)
![Language](https://img.shields.io/badge/python-3.11-blue)
![License](https://img.shields.io/badge/license-MIT-green)
![Status](https://img.shields.io/badge/status-active%20development-brightgreen)

Remote Cell Culture Monitor is an open-source Raspberry Pi--based
platform for remotely observing cell cultures using a USB microscope
camera over a secure internet connection.

The system enables live visual inspection of cell cultures, spheroids,
organoids, or microfluidic systems without requiring physical access to
the laboratory or repeated disturbance of incubator conditions.

Designed to be low-cost, reproducible, and extensible, the platform
combines commodity hardware, open-source software, and a browser-based
interface to support laboratory monitoring, teaching, and open lab
automation.

------------------------------------------------------------------------

# Overview

Routine inspection of cell cultures is an essential component of
experimental biology. However, frequent manual observation can introduce
disturbances to culture environments and requires researchers to be
physically present in the laboratory.

This project provides a remote microscopy monitoring platform that
allows researchers to:

-   view live microscope images from a Raspberry Pi
-   inspect cultures remotely through a web browser
-   capture snapshots for documentation
-   optionally generate timelapse image series
-   securely access the system over the internet

The system is intended for research and educational environments where
low-cost and reproducible monitoring solutions are valuable.

------------------------------------------------------------------------

# Key Features

-   Live microscope image streaming
-   Browser-based viewer interface
-   Raspberry Pi compatible
-   USB microscope camera support
-   Snapshot image capture
-   Optional timelapse imaging
-   Secure remote access via HTTPS or tunnel
-   Modular architecture for extension
-   Fully reproducible open hardware and software setup

------------------------------------------------------------------------

# System Architecture

The platform consists of four main components:

1.  Imaging hardware
2.  Raspberry Pi streaming server
3.  Web interface
4.  Secure remote access

Typical architecture:

USB Microscope Camera → Raspberry Pi (streaming server) → Web Server
(Apache / Nginx) → Secure Tunnel / Reverse Proxy → Remote Browser Viewer

------------------------------------------------------------------------

# Example Applications

Possible use cases include:

-   monitoring adherent cell cultures
-   organoid growth observation
-   spheroid formation tracking
-   remote laboratory teaching
-   incubator monitoring
-   low-cost lab automation
-   open-source microscopy platforms

------------------------------------------------------------------------

# Hardware Requirements

Minimum tested configuration:

  Component               Example
  ----------------------- ---------------------------------------
  Single-board computer   Raspberry Pi 4 or Raspberry Pi 5
  Camera                  USB microscope camera or macro webcam
  Storage                 32--128 GB microSD
  Network                 Ethernet or WiFi
  Mount                   microscope stand or custom holder
  Power                   5V / 3A power supply

Optional hardware:

-   LED illumination ring
-   incubator-compatible camera mount
-   temperature sensors
-   environmental monitoring modules

Detailed hardware setup instructions are available in:

docs/hardware-setup.md

------------------------------------------------------------------------

# Software Requirements

Required software components:

-   Raspberry Pi OS
-   Python 3.10+
-   Motion for USB camera streaming and web-based monitoring
-   Apache or Nginx web server
-   Optional secure tunnel (e.g. Cloudflare Tunnel)

Installation instructions:

docs/software-setup.md

------------------------------------------------------------------------

# Quick Start

Clone the repository:

git clone
https://github.com/richardmorgan1530/remote-cell-culture-monitor.git cd
remote-cell-culture-monitor

Install dependencies:

bash scripts/install.sh

Start the camera stream:

bash scripts/start_stream.sh

Open the web viewer:

http://`<raspberry-pi-ip-address>`{=html}

For secure internet access configuration see:

docs/network-access.md

------------------------------------------------------------------------

# Web Interface

The system provides a lightweight browser interface that allows users
to:

-   view live microscope feed
-   capture snapshots
-   access archived images
-   monitor system status

Example interface:

web/index.html

------------------------------------------------------------------------

# Snapshot and Timelapse Imaging

The platform supports image capture for experiment documentation.

Example snapshot command:

bash scripts/capture_snapshot.sh

Optional timelapse:

bash scripts/timelapse.sh

Captured images are stored in:

data/images/

------------------------------------------------------------------------

# Security Considerations

This system should not be exposed directly to the internet without
appropriate security measures.

Recommended deployment includes:

-   HTTPS encryption
-   password authentication
-   firewall restrictions
-   reverse proxy hardening
-   secure tunneling (e.g. Cloudflare Tunnel)

Security documentation:

docs/security.md

------------------------------------------------------------------------

# Reproducibility

The goal of this project is to provide a fully reproducible monitoring
platform for laboratory environments.

The repository therefore includes:

-   hardware bill of materials
-   tested software configuration
-   installation scripts
-   example configurations
-   validation images

Detailed documentation can be found in:

docs/

------------------------------------------------------------------------

# Validation

Example validation parameters (tested configuration):

  Parameter                   Result
  --------------------------- ---------------
  Raspberry Pi model          Pi 5
  Camera resolution           1080p
  Stream latency              \~1--2 s
  Continuous runtime tested   72 hours
  Network access              secure tunnel

Example images are available in:

examples/sample-images/

------------------------------------------------------------------------

# Limitations

This platform is designed for research and educational use only.

Limitations include:

-   image quality depends on camera optics
-   not suitable for diagnostic use
-   not designed for sterile incubator environments without modification
-   continuous illumination may affect some culture conditions

Users should ensure compliance with institutional biosafety and
laboratory safety guidelines.

------------------------------------------------------------------------

# Project Structure

remote-cell-culture-monitor │ ├── README.md ├── LICENSE ├── CITATION.cff
│ ├── docs/ ├── scripts/ ├── configs/ ├── web/ ├── app/ ├── hardware/
├── examples/ └── tests/

------------------------------------------------------------------------

# Contributing

Contributions are welcome.

Possible areas of development include:

-   multi-camera support
-   autofocus integration
-   automated confluence detection
-   contamination detection
-   image analysis pipelines
-   environmental sensor integration
-   improved web interface

Please see:

CONTRIBUTING.md

------------------------------------------------------------------------

# Citation

If you use this project in research or teaching, please cite it.

Example citation:

Morgan R. Remote Cell Culture Monitor: an open-source Raspberry Pi
platform for remote microscopy-based culture monitoring. GitHub
repository.

Formal citation metadata is provided in:

CITATION.cff

------------------------------------------------------------------------

# License

This project is released under the MIT License.

See:

LICENSE

------------------------------------------------------------------------

# Contact

Project maintainer:

Richard Morgan\
MSc Regenerative Medicine\
University of Galway
