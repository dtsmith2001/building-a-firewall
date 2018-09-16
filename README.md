# Building a Firewall on a Raspberry Pi

The artice I found https://www.instructables.com/id/Raspberry-Pi-Firewall-and-Intrusion-Detection-Syst/ is rather old. I worked through the process myself. Here's the record of what I did.

The interesting thing about the process used is it doesn't require a second Ethernet connection. That's a good solution for me.

## MicroSD Card

NOOBS would not work on the latest Raspberry PI 3B+, so I downloaded headless Raspbian.

## Power Requirements

The Raspberry PI is sensitive to power supplies. I tried 5V 1.6A but just got the flashing red light. Then I tried to plug into a powered USB hub connected to my iMac, but I still had a power problem. I am not sure why this solution won't work. I should take my MicroUSB cable back to the store, I guess.

I got a 3 A power supply for the PI 3B+ and it works just fine. Someone gave me a 2, so I'm going to get a 2.5 A power supply for it and configure it as the firewall. The 2 doesn't have WiFi, and that's just fine.

## Use /etc/rc.local on Ubuntu and Raspbian

We have to use `/etc/rc.local`. Edit the file in the `etc` directory and change the interface, address, netmask, broadcast address, and gateway for your router. I'm using a box provided by my cable company, so I logged into the device and got this information. I also set the PI 2 so it has a static IP address. Go ahead and do this now.

## Edit /etc/hosts

Put the static address in the `hosts` file.

## Copy rc.local and hosts to /etc

Make sure you have backup copies of these files. You need to use `sudo` for this step.

```bash
sudo service network-manager restart
```
