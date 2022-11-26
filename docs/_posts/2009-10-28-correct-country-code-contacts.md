---
id: 16
title: Correct country code of your Window Mobiles contacts
date: 2009-10-28T12:15:04+01:00
permalink: /archives/16
categories:
  - Mobile Devices
  - Technology
---
I had a little problem with my phone's contacts. I have changed several mobile phones, Windows Mobile and not (e.g. Symbian). Each operating system had a different philosophy for storing the country code (+30) of each contact. One time, I synced my contacts from a Windows Mobile Smartphone 2003 to a Motorola phone and all +30 were converted to 30. Then I changed to a Windows Mobile 6 Professional device and I could not anymore call these contacts unless I added the plus (+) sign again at the beginning of the country code. Moreover, the desktop version of Outlook, adds a space between the country code and the number.

<img  src="/assets/posts/2009-10-28-correct-country-code-contacts/CorrectCountryCode.jpg" width="221" height="296" />

Alas, .NET Compact Framework 3.5 is ideal for such petty work! I made the following program in a snap. You can download it, it contains the source code (Visual Studio 2008) and the executable which you can just copy (along with the required .dlls) to your device and execute it. It just changes all your contacts' numbers with the following rules, so as to make them homogeneous.

For the given country code (e.g. +30 for Greece), it will do the following:  
-- Change 30xxxxxxxxxx to +30xxxxxxxxxx.  
-- Change +30 xxxxxxxxxx to +30xxxxxxxxxx.  
-- Change 0030xxxxxxxxxx to +30xxxxxxxxxx.  
-- Change 0030 xxxxxxxxxx to +30xxxxxxxxxx.  
-- Any other number which does not start with a plus sign (+), xxxxxxxxxx to +30xxxxxxxxxx.

Of course I have not added any validation or any peculiar cases, so proceed at your own risk! If you're interested in how to use Pocket Outlook to manage contacts, tasks, calendar etc., see an [older post of mine](/archives/6) where I note the most intriguing features of the namespace Microsoft.WindowsMobile.PocketOutlook.

### Download

Click <a href="/assets/posts/2009-10-28-correct-country-code-contacts/CorrectCountryCode.zip">here</a>.

### Introduction to Windows Mobile 6 programming

For an introduction in programming Windows Mobile 6, you can watch my webcast ["StudentGuru.gr -- Introduction to Windows Mobile 6 (greek)"](/archives/385).