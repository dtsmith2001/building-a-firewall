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

Make sure you have backup copies of these files. You need to use `sudo` for this step to copy everything in the `etc` directory to `/etc`. I did not keep my IP address or other networking information in GitHub. I edited manually and then did a `git checkout -- <file>`.

Restart the PI. Note - do not use `ifconfig <interface> down` if you are logged in via ssh. If you are using the console, use

```bash
ifconfig <interface> down
ifconfig <interface> up
```

Otherwise, just use

```bash
sudo shutdown -r now
```

This will close your ssh connection and restart the PI.

# Package Installation

Install `tcpdump`.

# Changes to /etc/sysctl.conf

I made the following changes

- Spoof protection

```
net.ipv4.conf.default.rp_filter=1
net.ipv4.conf.all.rp_filter=1
```

- TCP/IP SYN cookies

```
net.ipv4.tcp_syncookies=1
```

- Ignore ICMP broadcasts

```
net.ipv4.icmp_echo_ignore_broadcasts=1
```

- Ignore bogus ICMP errors

```
net.ipv4.icmp_ignore_bogus_error_responses=1
```

- Do not accept ICMP redirects (put your own interface name for `eth0`)

```
net.ipv4.conf.all.accept_redirects = 0
net.ipv4.conf.eth0.accept_redirects = 0
```

- Do not send ICMP redirects

```
net.ipv4.conf.all.send_redirects = 0
net.ipv4.conf.default.send_redirects = 0
net.ipv4.conf.eth0.send_redirects = 0
```

- Do not accept IP source route packets

```
net.ipv4.conf.all.accept_source_route = 0
```

- Log (https://en.wikipedia.org/wiki/Martian_packet)[Martian Packets]

```
net.ipv4.conf.all.log_martians = 1
```

- Router functionality

```
net.ipv4.ip_forward = 1
```

- Minimum free kb

```
vm.min_free_kbytes=8192
```

Make sure you use your own interface name for `eth0`. Apply changes using `sudo sysctl -p`.
