---
title: pfsense in IBM Cloud
date: 2020-01-04T15:04:10.000Z
description: >-
  Using IBM Cloud bare metal to provision any ISO
image: /img/firewall.unsplash.jpg
---

# pfsense in IBM Cloud

By way of introduction, I am a Customer Success Manager.  My role is to help clients leverage IBM Cloud in the most efficient and secure manner to accomplish their goals.  The cloud is complex and I hope to unravel some of the complexities and nuances that one may encounter.  I'm also a tinkerer, which bodes well with some of the perks of my job.

I've had various clients talk about their initial onroad to the IBM Cloud.  One of the first questions is always around the network and particularly, network security.  Network security in itself is a proverbial iceberg.  Personally, I believe the idea of [Zero Trust](https://www.cloudflare.com/learning/security/glossary/what-is-zero-trust/) will be mainstream in the next 5 years.  At the same time, organizations still require the concept of the basic Firewall to secure traffic.  Therefore, let's consider four basic solutions available in IBM Cloud:

- Flat Network
- Gateway Appliance / Firewall
- VPC
- Virtualized (VMW,K8's,etc)

These four concepts are the most basic solutions available in IBM Cloud today.  Each concept has advantages and disadvantages, but if you have the option to leverage a virtualized platform, the go toward VPC for simplicity and cost efficiencies.  Our [VPC](https://cloud.ibm.com/docs/vpc?topic=vpc-about-networking-for-vpc) is fairly well documented and can provide great getting started guides.  If you are looking for the traditional appliance to segment traffic for bare metal and virtual in a single datacenter (router), then the [Gateway Appliance](https://cloud.ibm.com/docs/gateway-appliance?topic=gateway-appliance-getting-started) or [Firewalls](https://cloud.ibm.com/docs/hardware-firewall-dedicated?topic=fortigate-10g-exploring-firewalls) are the most robust solutions available.

In addition to walking through the various options, I wanted to provide you with a quick walk through for the last option, the Flat Network.  Since the documentation on this is less available, likely due to assumptions of what is possible in any IT environment, I decided to spend extra time on the walk-thru.

### Logical Architecture for "Flat Network"

- WAN Interface - Static Public IP
- LAN Interface - Static Private IP
	- subnet A
	- subnet B
	- subnet C

Here are the basic steps one might take to setup a pfsense community edition router/firewall in IBM Cloud:

1. order bare metal server with NoOperatingSystem
2. KVM to bare metal host via Remote Management
3. Install .ISO for pfsense community edition on virtual drive and reboot
4. Follow instructions for setup and install of pfsense
5. Setup VLAN and interfaces with static IPv4
6. Order virtual server on same subnet >>> RDP/VNC to virtual host and hit pfsense GUI through browser
7. Start having fun with NAT tables and adding VLANs/subnets across network
