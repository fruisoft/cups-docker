# Current version

CUPS 2.2.1

# What is CUPS?

CUPS is an open source printing system that supports IPP along with other protocols. More information can be found at [cups.org](http://cups.org/)

# About this image

This image is based off [ticosax/cups-in-docker](https://github.com/ticosax/cups-in-docker) with a few specific tweaks:

* Debian testing is used as the base image. Most of the cups updates are put into testing fairly quickly so no need for unstable. This may change in future if versions start lagging behind.
* Adds USB backend for Brother printer.

# Running this image

## Way 1 : `docker run`

```
docker run -e CUPS_USER_ADMIN=admin \
-e CUPS_USER_PASSWORD=secr3t \
-e PRINTER_MODEL=HL-L2300D
-p 631:631/tcp \
-v /path/to/cupsd.conf:/etc/cups/cupsd.conf \
--device=/dev/bus/usb/xxx/yyy \
monkeydri/cups-docker:latest
```

## Way 2 : `docker compose`

See provided `docker-compose.yml` file.
Don't forget to set the `PRINTER_ADDRESS` var and change the `PRINTER_MODEL` value according to your model of Brother printer.

## Way 3 : startup script `start_cups_docker.sh`

The provided startup script `start_cups_docker.sh` automatically gets the printer address /dev/bus/usb/xxx/yyy by looking at any connected Brother printer. Thus, be careful if you have more than one Brother printer connected.
Don't forget to change the `PRINTER_MODEL` value according to your model of Brother printer.

Access the CUPS server at http://127.0.0.1:631.
To access it remotely at http://server-ip:631, add the line `DefaultEncryption IfRequested` to `cupsd.conf`.