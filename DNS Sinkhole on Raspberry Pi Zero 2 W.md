
---

## Overview

This project focuses on DNS resolution. Using a Raspberry Pi to create a simple DNS sinkhole that blocks ads on my home network as well as malicious domains and trackers. This project will further my understanding of DNS and Networking.
 

---

## Goals

- Build a basic DNS sinkhole using a Raspberry Pi  
- Block unwanted or harmful domains
- Gain hands-on experience with networking  

---

## Tools & Equipment

**Hardware**
- Raspberry Pi Zero 2 W  
- microSD card 16 GB  
- Power supply  
- Wi-Fi  

**Software**
- Raspberry Pi OS Lite (x64) 
- [Pi-hole](https://pi-hole.net/)   
- SSH (PuTTY)

---

## Setup Summary  

1. The Raspberry Pi came packaged with the standard full OS pre installed on the SD card, however I erased it and instead installed Raspberry Pi OS Lite and will run the device headless.  

2. In the setup I pre configured the WiFi addressing. At my routers admin panel I can check the DHCP leases to see what IP my pi was assigned. We will change this to a static IP later. 

3. I will SSH into my pi using PuTTY, and run an update and upgrade command to ensure everything is up to date. 

4. After the updates, I set a reserved IP for the pi in my router settings to ensure I can use it as a DNS server.

5. I again SSH into my pi and install the PiHole software using 'curl -sSL https://install.pi-hole.net | bash' 
![[{F7AB367F-D3DF-4940-B169-9465A52F7301}.png]]

6. As part of the installer for PiHole, it asks if we want to set an upstream DNS server, I will take this opportunity to add some built in security at the DNS server end. I will set the upstream DNS server to 1.0.0.2 which is a CloudFlare DNS that has built in malware protection as well as fast speeds.

7. With the PiHole software installed, the first thing ill do is set a new password for PiHole to improve security.
![[{425AD002-FEB1-4F5C-B4B8-B12D866BFD18}.png]]

8. We will log into the pihole server in our browser and add more blocklists to the pi. Some great blocklists can be found on Firebog.net

9. Im going to add 2 lists for each category: Suspicious Lists, Advertising Lists, Tracking & Telemetry Lists and Malicious Lists. This will increase the security of my home network and devices massively.
![[{3CCAA280-C7E2-4DE5-8FB7-AC03324C6FEB}.png]]

10. Now we must run 'pihole -g' to update gravity. This retrieves the lists back down to the pi and allows it to block them.

11. When we go to the dashboard, we can see that we are actively blocking 320,907 domains.
![[{97D58768-B25A-43F4-B29B-A8CD71F9B774}.png]]

12. After tweaking a few minor settings we have the PI running how we want.

13. Now we must configure our router to look to the pihole as a DNS server. This is easily done on the Router Dashboard.


---
## Testing

Looking at the dashboard we can see that the pi is already blocking traffic.
![[{68B47858-5CBC-45B0-89E4-7A7939325DE1}.png]]

We can also test this using a tool called AdBlock Tester. The pi passes multiple tests but fails others like banner and gif ads. We will add more lists to the blocklist to help eliminate these failures. We will be sure to use 'pihole -g' to ensure the software grabs the lists.

After adding a few more lists focused towards advertisements, our score improves from 42/100 to 51/100.

I researched more up to date blocklists and imported to PiHole, after testing again we score 81/100. I am yet to receive any false positives or commonly used services blocked.

![[{889B3ADB-1E53-4672-81BA-6FAFB425812B}.png]]
One final check of the PiHole confirms that the DNS sinkhole is working well and blocking potentially dangerous traffic.

---

## Results

| Metric            | Result |
| ----------------- | ------ |
| Total DNS queries | 3171   |
| Blocked queries   | 1037   |
| Block rate        | 32.7%  |


---

## What I Learned

Write a few sentences about what you learned:  
- This helped me to further my knowledge of DNS as well as how ads on web pages are loaded and requested. 
- How to configure a Raspberry Pi as a network tool.  
- The basics of blocking malicious and suspicious domains.    

---

## Next Steps

- Learn how to monitor DNS traffic more closely  
- Explore integrating Unbound DNS server for upgraded privacy.  

---

## References

- [Pi-hole Documentation](https://docs.pi-hole.net/)  
- [Raspberry Pi OS Guide](https://www.raspberrypi.com/software/)  
- [StevenBlack’s Hosts Blocklist](https://github.com/StevenBlack/hosts)
- [The World's Greatest Pi-Hole](https://www.crosstalksolutions.com/the-worlds-greatest-pi-hole-and-unbound-tutorial-2023/)

---

