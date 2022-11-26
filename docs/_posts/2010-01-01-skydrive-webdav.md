---
id: 21
title: Access SkyDrive from Windows Explorer through WebDAV
date: 2010-01-01T18:44:29+01:00
permalink: /archives/21
categories:
  - Technology
  - Windows
---
Nowadays the cloud services are blooming really fast. One very useful service that many hosts are offering is online storage. A notable example is Microsoft's [SkyDrive](http://skydrive.live.com/) service which offers 25GB of free online file storage. There's also a rumor about Google offering a similar service named GDrive, following the example of GMail.

One thing most people dislike about online storage is having to go to the host's website in order to upload, download, edit files. Fortunately, there are internet protocols to help us. And fortunately, Windows supports natively the WebDAV protocol for accessing remote file servers through Windows Explorer, plus supporting the HTTPS for solid security. All you need is have a SkyDrive account. Note: See [my previous article](/archives/379 "WebDAV for IIS 7 on Windows Server 2008 R2") if you're interested in creating _your_ WebDAV folders to access them remotely.

Before starting, I recommend creating a new private folder in your SkyDrive, e.g. named "Files" and do the following in that folder. If you do not want to create a new folder, remember that sometimes a folder in SkyDrive has a different name shown and a different real name that is shown in the address bar. We need the folder's name that appears in the address bar. Also, I must note that I haven't been able to map the SkyDrive's root folder, but only the folders shown in SkyDrive's homepage separately. We will continue with one folder, the "Files" folder we created. You can follow the same process to map all of your other SkyDrive folders.

Now we have to "discover" the WebDAV address which we will use for our SkyDrive: If you create/upload a new Office document (e.g. Powerpoint) in Live Documents, you can then "Edit" it with PowerPoint Web App. There, you will see a button called "Open in Powerpoint" which will open Powerpoint 2007/2010 and edit the online document. In your local powerpoint, click Save As and you will see the internet WebDAV address Powerpoint uses to upload the file. This is the address we need to connect Windows Explorer to SkyDrive's WebDAV features!

My address has the following pattern: Either you'll see `https://03wdfx.docs.live.net/{SkyDriveID}/Files` or `\\03wdfx.docs.live.net@SSL\DavWWWRoot\{SkyDriveID}\Files`, it doesn't matter. From this address we'll need to take the `{ServerURL}` part, that is `"03wdfx.docs.live.net"` in this example. Ignore this `{SkyDriveID}` as it may not be exact. Now, we need to take the real/full ID of your skydrive, which you see in the address line of your browser when you're browsing the homepage of SkyDrive. The address line has the following pattern: `http://cid-{SkyDriveID}.skydrive.live.com/`. This is the `{SkyDriveID}` we need!

Now we have the two pieces of information we need in order to map the skydrive folder "Files" to our Windows Explorer. Open the Command Prompt and execute the following command:

```
net use * \\{ServerURL}@SSL\DavWWWRoot\{SkyDriveID}\Files /SAVECRED /PERSISTENT:YES
```

It will create a new network drive in Windows Explorer and then you'll be able to access your SkyDrive files! You can also rename the mapped drive with a more friendly name like "Sky Files".

The only issue left is the one involving the Live ID credentials. If you restart your PC, the network connection won't work (except if you previously login to SkyDrive). We have to make Windows remember your Live ID. This is what you must do (tested in Windows 7): Go to Window's Control Panel and click Credential Manager. In the left panel of the Control Panel, you'll see a link named "Link Online IDs" (also can be found in Control Panel's User Accounts). There you'll be able to link your Windows account with your Live ID. Additionally, in the Credential Manager, you can add a "Generic Credential" with your live ID (this is usually your hotmail) and your password for the {ServerURL}, though I do not know if it's necessary to do that. After doing these things, you'll be able to access the skydrive network connection without having to previously login with the browser.

Finally, there is also a freeware application that does away with all the WebDAV hassle and does the same job: [http://skydriveexplorer.com/](http://skydriveexplorer.com/ "http://skydriveexplorer.com/").

As this is my post of the very first day of 2010, I wish you all a happy new year full of healthiness and creativity!

Sources:

  * [http://www.winmatrix.com/forums/index.php?/topic/16691-access-skydrive-from-windows-explorer/page\_\_st\_\_15](http://www.winmatrix.com/forums/index.php?/topic/16691-access-skydrive-from-windows-explorer/page__st__15 "http://www.winmatrix.com/forums/index.php?/topic/16691-access-skydrive-from-windows-explorer/page__st__15")