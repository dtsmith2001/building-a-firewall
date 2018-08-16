# Building a Firewall on a Raspberry Pi

The artice I found https://www.instructables.com/id/Raspberry-Pi-Firewall-and-Intrusion-Detection-Syst/ is rather old. I worked through the process myself. Here's the record of what I did.

The interesting thing about the process used is it doesn't require a second Ethernet connection. That's a good solution for me.

## MicroSD Card

I bought one with NOOBS installed for Raspberry PI. You can probably get this cheaper if you buy a card and put NOOBS on the card yourself.

After inserting the card into my iMac (it has a slot for an SD card), I looked in Finder. I saw two partitions mounted - _*boot*_ and _*RECOVERY*_.

The tutorials I've read require either ARCHLinux or CentOS, meaning I have to wipe out my card if I want to use it. So I made a copy of each partition. I took screenshots from Disk Utility so I can restore the card.

Then I decided to order a fast 16 gb blank card. It's just easier to manage. I'm going to install [Ubuntu](https://wiki.ubuntu.com/ARM/RaspberryPi).

## Power Requirements

The Raspberry PI is sensitive to power supplies. I tried 5V 1.6A but just got the flashing red light. Then I tried to plug into a powered USB hub connected to my iMac, but I still had a power problem. I am not sure why this solution won't work. I should take my MicroUSB cable back to the store, I guess.
