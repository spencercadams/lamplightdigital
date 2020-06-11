---
title: Testing FreePBX
date: 2020-03-04
description: >-
  FreePBX is a great tool, now let's make this work
image: /img/phone.unsplash.jpg
---

## Webex isn’t working…what now?

If you haven’t had a chance to view the Otter cam @ the [Monterray Bay Aquarium](https://www.montereybayaquarium.org/animals/live-cams), do it now, by far my favorite live feed. There are so many great live feeds across the world:
• [NASA International Space Station](http://www.ustream.tv/channel/live-iss-stream)
• [Virtual Tours/Activities](https://virtualschoolactivities.com/)
• [LiveStream](https://livestream.com/watch)
• [YouTube Live](https://www.youtube.com/live)
• [Forbes List](https://www.forbes.com/sites/carlieporterfield/2020/03/16/in-coronavirus-quarantine-you-can-virtually-tour-these-museums-from-home/#231f1c207a3a)

It is amazing to see Moore’s Law in action, as technology continues to improve at an exponential pace. A common theme for each of the live feeds is the networking and computing power required to support such a seemingly simple vessel of communication. Fortunately, I live in suburbia of America and have fiber running to my residence, but I am still amazed at the amazing power of the internet. At the same time…the internet doesn’t always function as we’d like. Just the other day, I was working on a new project with a few co-workers and discovered that Cisco Webex was having a bit of trouble under the increased load. We had to fall back to a more reliable solution, a PBX (Private Branch Exchange) system. Amazingly, I had this old school dial-in from 8 years ago…and sure enough, it still functioned as best it did back then.

After that experience, I thought about all the other solutions for communication (as backup options) and figured I’d walk through a quick FreePBX setup on IBM Cloud leveraging Twilio’s free trial account for Elastic SIP Trunk. Since I am setting this up after my kids have gone to bed, the setup shouldn’t take more than 2–3 glasses of wine. And…should be easy enough to walk-thru under that same alcohol-induced coma. These were my requirements.

Therefore, I went to work ordering things quickly…

Originally was going to grab the free IKS node and leverage [DockerHub](https://hub.docker.com/r/tiredofit/freepbx/dockerfile), but quickly realized creating the Manifest and configuring the egress was going to be past the 3 drink max requirement. For others, maybe not. But for me, yes. Therefore, I went back to my requirements and just figured I’d start with Github and CentOS. With a quick Google search I found what I was looking for, a [PBX deployment on top of CentOS Server](https://github.com/cameronbackus/doPBX). That is simple. You could also simply grab the ISO and load up on bare metal via IPMI, but the VSI seemed easier. If this were for production, I would advise Bare Metal.

Ordered VSI quickly with SLCLI script: `slcli vs create — hostname=ibmpbx — domain=sa.test.local -f B1_1X2X25 -o CENTOS_LATEST_64 — datacenter=dal12 — billing=hourly`

Then went over to Twilio and created a [free account](https://www.twilio.com/try-twilio). Then did another quick Google search for FreePBX Setup with Twilio, and found [this guide](https://twilio-cms-prod.s3.amazonaws.com/documents/TwilioElasticSIPTrunking-AsteriskPBX-Configuration-Guide-Version2-1-FINAL-09012018.pdf).

By now, I am one glass of wine in and just getting started. Head over to Twilio and configure the trunks Origination and Termination, while the VSI instantiates. Twilio makes my life easy and I simply follow the guide. When complete on Twilio’s end, I head over to SSH into the VSI and install Astericks and FreePBX, cause I like a GUI…then let the scripts run, this takes a while, glass two completes. Once SSH shows complete, I hit up the Public IP and login as Administrator for my FreePBX system. I then did another quick Google for FreePBX to Twilio setup and discover another [guide](https://www.nicolasmeloni.com/blog/2017/06/18/set-sip-trunk-freepbx-twilio/). It’s great to know I am not the first to do this…

After following both guides, I have Astericks 13 (outdated, I know), FreePBX and Twilio setup with a Conference line for my backup. Glass 3 complete.

If I continue to run this server, I estimate it’ll be about $20/month and another $15/month for Twilio. A total of $35 for my own personal system that I can configure as I see fit. There is an abundance of other resources available, which I will list below, but nothing that allows me to customize the conference call to fit me like this setup would.

Other VoIP communication vehicles:
• Free Conference Bridge — https://www.freeconferencecalling.com/phone-conference.html
• Free Trial 90 days — https://www.webex.com/go-covid19.html
• Free Trial no limit — https://zoom.us/docs/en-us/covid19.html
Best of luck during these trying time and look forward to hearing about your plans during the Shelter in place movement.

Cheers,

_Spencer
