---
id: 24
title: SendInternetSms - Send SMS through websites, from your Windows Mobile or PC
date: 2010-05-17T02:55:52+02:00
permalink: /archives/24
categories:
  - Mobile Devices
  - Technology
---
I had always been fond of making a program that would automatically send SMS messages through websites that offer free SMS. This idea got even stronger when I saw solidu's [post](http://www.studentguru.gr/blogs/solidus/archive/2010/03/29/solidsms-sms-desktop.aspx). But I didn't want to use watiN, mainly because I wanted the process to be in the background. So I used Fiddler to find out which HTTP Requests and Responses were needed to send an SMS through a website. Then, I automated the process with C#.

This got me thinking a bit more: People just get bored of using either the SMS websites or a desktop application that automates the process. Because frankly, each time, you have to copy-paste one's phone number. So, a better solution would be for the mobile phone you already have. How about this: When you send a regular SMS with your Windows Mobile, the program will automatically pick it up and try to send it through an SMS website. At last, I've made it!

"SendInternetSms" is the name I gave to all the projects included. It contains the following Visual Studio 2008 solutions:

  * SendSmsLib: A .NET (Compact) Framework library that defines an ISmsService interface. It allows easy configuration and loading of ISmsServices from different assemblies (.dlls). After being configured, one can use SendSmsLibTester Windows Forms application to easily send a SMS message.
  * SendInternetSms: Contains the SmsRerouter program. It allows automatic interception of outgoing SMS messages from a Windows Mobile 5 or 6 device (either Smartphone or PocketPC). It uses SendSmsLib. It contains a native C++ project and a C# program.
  * WebSms: An ASP.NET website that uses SendSmsLib to send SMS messages. My many thanks to my friend Alexandros Sigaras (a.k.a. [mazohack](http://www.studentguru.gr/members/Mazohack.aspx)) who made the design of the website! Default username and password are "user" and "pass".

You can develop an ISmsService yourself, for any SMS website you can think of. The process of course is quite time-consuming, as you cope with Fiddler, cookies, and PHP/Ajax/Asp.Net quirks. If you create one, share it with us! Do note, it would be better if they're developed with .NET Compact Framework, so that they may work on Windows Mobile phones, and not just on PCs. Right now, there are two ISmsServices included in SendInternetSms:

  * SmsServiceOtenet: Implements ISmsService for the OTENET web sms website ([http://tools.otenet.gr](http://tools.otenet.gr/)).
  * SmsServiceOtenetCorporate: Implements ISmsService for Otenet Corporate web sms website ([http://corpmail.otenet.gr](http://corpmail.otenet.gr/)).

Now, a sneak preview of the three ways that one can send an SMS:

<p style="text-align: center;">
  <img alt="SendInternetSms Windows Mobile Screenshot" src="/assets/posts/2010-05-17-sendinternetsms/SendInternetSms_WM.jpg" /><br />Windows Mobile<br /><br />
  <img alt="SendInternetSms Web Screenshot" src="/assets/posts/2010-05-17-sendinternetsms/SendInternetSms_Web.jpg" /><br />Web<br /><br />
  <img alt="SendInternetSms PC Screenshot" src="/assets/posts/2010-05-17-sendinternetsms/SendInternetSms_PC.jpg" /><br />PC<br /><br />
</p>

To download the file with all my projects, click <a href="/assets/posts/2010-05-17-sendinternetsms/SendInternetSms.0.1.zip">here</a>. The files are under the GNU GPLv3 license. That means it's free and open source. There's a ReadMe.txt included with instructions on how to configure the programs and how to install SmsRerouter on Windows Mobile.

Last, I would like to point out some of the development issues addressed/showed in SendInternetSms for Windows Mobile:

  * .NET Compact Framework for Windows Mobile devices. How to make a background process.
  * How to use Windows Mobile native API. E.g. Implementing the IMAPIAdviseSink for intercepting outgoing SMS messages and using MAPI.
  * Multithreading using ManualResetEvent and the ThreadPool.
  * Platform Invoke: How the managed application calls the C++ project's functions. How callback functions can be used.
  * Smartphone/PocketPC compatibility. Detect the type of the current device and show accordingly either a taskbar notification or a message box.

I'm waiting for your comments, and maybe your ISmsServices. Enjoy!