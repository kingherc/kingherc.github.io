---
id: 12
title: Motion detection - protect your home with a webcam
date: 2009-01-15T19:56:03+01:00
permalink: /archives/12
categories:
  - Technology
---
I've heard of many programs for motion detection, using only your webcam, but most of the free ones have many deficiencies. I finally found a program that not only detects motion, but also notifies you! Its name? Yawcam, the website of which you can find <a href="http://www.yawcam.com/">here</a>. And it's free and runs on any platform, as it's written in java.

<img src="http://www.yawcam.com/img/screen8.png" />

Yawcam has many surprising features. Firstly, it creates a web server and you can remotely (through http + javascript) view your webcam live! Moreover, it has the ability to send snapshots to a FTP server, through an email, and obviously it can store snapshots on your hard drive. It also has our desired motion detector that, when it detects motion, can send snapshots through ftp, emails, play a sound or call a program.

With a simple batch script (a ping command and yawcam), you can run it when you leave home, and have Yawcam started after 1 minute. And you can configure it to automatically start motion detection.

<img src="/assets/posts/2009-01-15-motion-detection/SendSkypeSms.jpg" />

What else can you do if you want more immediate updates? You can have a SMS sent to your mobile! How? By using Skype + Yawcam. Create a Skype account and charge it with money. Through Skype, you can send sms messages to mobile numbers. Furthermore, using the free Skype COM API, you can make a program that sends a sms, which Yawcam will call when it detects motion. It'd be best to configure Yawcam's flood control settings to call it only once in 15 minutes (only when, of course, it's needed).

I made such a program, which you can download <a href="/assets/posts/2009-01-15-motion-detection/SendSkypeSms.0.0.1.zip">here</a> and use it. I called it simply SendSkypeSms. I also included the source (.NET 2.0), even if it's quite short and scrappy.
