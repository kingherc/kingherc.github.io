---
id: 15
title: Solution to Windows Server locking up after 15 minutes of inactivity
date: 2009-09-16T11:54:56+02:00
permalink: /archives/15
categories:
  - Technology
  - Windows
---
I have Windows Server 2008 installed on my main desktop machine, and I usually work on a Windows Vista installed as a Hyper-V virtual machine on Windows Server. I have to note that I don't have a Windows Server Domain infrastructure, and thus I do not have any Active Directory users or settings. My Windows Server locks up after a few minutes of inactivity (15 I believe), effectively showing the blue login screen where I have to press ctrl + alt + del to log in to my session again. This is very annoying while watching a video clip. Of course these settings were meant for real servers, but because I use Windows Server mainly for development, I would like to change them to be more workstation-like. The following may also apply to a workstation (Vista, 7 etc.) if their settings were tampered with, but usually the default settings do not result in locking out.

After searching for a while on the internet, and trying out stuff, I found the following combination to solve my problem: In the Start Run box type "gpedit.msc" to open up "Local Group Policy Editor". In the"Local Computer Policy", find the following nodes:

  * Computer Configuration > Windows Settings > Security Settings > Local Policies > Security Options > Interactive logon: Do not require CTRL+ALT+DEL. Enable this and you will not be required to press these keys before logging in.
  * Computer Configuration > Windows Settings > Security Settings > Local Policies > Security Options > Microsoft network server: Amount of idle time required before suspending a session. The pre-filled value is 45 minutes for servers and 15 minutes for workstations (Vista, 7 etc.). The default value is Not Configured, which means 15 minutes for servers and indefinite for workstations. So, this one is a value to change for Windows Server not to lock up. I changed it to 60 minutes.
  * User Configuration > Administrative Templates > Control Panel > Display > Screen Saver timeout. Even if you have not defined a screen saver, even if the rest of the nodes in the Display category are Not Configured, I found that enabling this and setting it to 0 seconds (effectively disabling any screen saver) helps.

After these, go to the Start Run box again and execute the command "gpupdate /force". Restart your PC. Again at the Start Run box you can type "rsop.msc" to open up "Resultant Set of Policy". Here you may assure that the above settings are applied.

Of course, if the above didn't help you consider searching:

  * Control Panel, such as Screen Saver settings.
  * Security policies. Both Local Policies for the current machine and Group Policies for Windows Domains infrastructures (apply them to client PCs and restart them).
  * Local Users (Control Panel > Administrative Tools > Computer Management > System Tools > Local Users and Groups). In Windows Server, you'll find Session settings etc.
  * Active Directory User's settings, if you have a Windows Domain infrastructure.
  * Power Settings, if your problem is that your screen turns off.
  * The notorious Registry!

Hope the above helps.