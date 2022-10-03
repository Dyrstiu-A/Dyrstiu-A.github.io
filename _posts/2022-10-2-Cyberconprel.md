---
layout: post
title: "Cybercon Preliminary CTF 2022"
date : 2022-10-2
image: ../../assets/img/Posts/cybercon.png
categories : [CTF-Writeups]
tags : [web,forensics,cryptography]
description : In this article , we have a look at some challenges in Cybercon 2022 ..
---
[CyberConKe](https://materializecss.com/) is holding its inaugural conference this year. A Preliminary CTF challenge in which I took part as team Rez3r0-students preceded the conference. The challenges were good, and this write-up is for the few I solved.

### Crypt0nite
For this challenge, they provided an audio file with the question. How do dead men lie? The audio file was morse code and by using a [Morse decoder](https://morsecode.world/international/decoder/audio-decoder-adaptive.html) you will get the flag `ccke{7H3Y_L13_5711L.}`. I can say this was a relatively easy challenge considering that they showed the flag format.

### Insecure
![insecure png](/assets/img/Posts/insecure.png)
This was a web challenge that required you to detect that there was an issue with the host header sent to the server. To solve this challenge, look at the host-name assigned on the SSL certificate and then replace the same on the host header sent to the server.
![request](/assets/img/Posts/insecure1.png)
After replacing the IP with the host-name we find it on the SSL certificate.
![request](/assets/img/Posts/insecure2.png)
Here is the Flag. ![Flag](/assets/img/Posts/insecure3.png)
> I solved this challenge after the competition ended unfortunately 😂😂. My initial thought was that the apache version of the website was a vulnerable one, the insecure statement on the landing page contributed to this. Let me try this in the future😂.
### Linux Incident response
In this challenge, they provided us with a Linux authentication log file. It was an easy challenge to some extent as we were required to analyze the log file manually ,to get the flags to the questions. For the manual analysis, I made use of the find feature on web browsers.
### Conclusion
This was a wonderful event, looking forward to more in the future. I am also glad I got to learn something from the entire event. This being my first CTF write-up I look forward to improving more in the future. Comments on areas of improvement are welcome. You can play some substantial challenges by visiting [Ctfroom](https://ctfroom.com).