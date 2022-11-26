---
id: 19
title: WebDAV for IIS 7 on Windows Server 2008 R2
date: 2009-11-21T17:52:48+01:00
permalink: /archives/19
categories:
  - Technology
  - Web
  - Windows
---
These days I'm trying to configure my new Windows Server 2008 R2. Of course, I would like to be able to access my files remotely and without any effort (such as downloading a third-party application). There were 3 options to use for accessing remotely files on Windows: VPN and SMB, FTP or FTPS and WebDAV. VPN is a bit complex and I ruled it out. FTPS is a great way to go but unfortunately Windows clients cannot directly map network drives to FTPS (it only supports plain FTP which is insecure). Fortunately, Windows clients can map network drives to WebDAV drives. So that's the way to go! It's also a standard and many systems can connect to WebDAV. It's also pretty "comfortable" as it relies on HTTP. And it becomes quite secure when you use HTTPS.

Fortunately, Microsoft has developed a great IIS 7 extension that adds WebDAV capabilities to websites. It's included automatically in R2, but for Windows Vista you have to download it from [here](http://www.iis.net/expand/WebDAV). There will be a WebDAV icon in the IIS which allows you to configure everything. So, when you need to configure a website's physical folder for WebDAV access, you just have to do the following:

  * If you want to enable HTTPS, you need to create a self-signed certificate for your server. This can be done easily if you go to your IIS server and click Server Certificates. **Unfortunately, IIS issues a certificate with a common name that is your server's name.** If you're using a dns address like "www.example.com", you'll find this unacceptable for most PCs, because they will be surmising that it's false. To create a custom self-signed certificate, [use this guide](http://www.robbagby.com/iis/self-signed-certificates-on-iis-7-the-easy-way-and-the-most-effective-way/).
  * Enable WebDAV on the parent site. You do not need to add access rules in the parent site, if you don't want WebDAV for all the website. If you want to have only HTTPS, go to the settings and turn "Require SSL Access" to true. Be sure that the website has an https binding, with the right certificate.
  * Go to the folder you want to enable WebDAV on. If you want only HTTPS, go to iis SSL Settings and check Require.
  * Now, you'll come to configure the permissions. First of all, there must be a way of authentication. Enable "Basic Authentication" (only works for SSL WebDAV) or something else if you want. Then you have to configure permissions in 3 places: 1) the IIS Authorization Rules, 2) WebDAV Authoring rules, 3) NTFS/File/Folder permissions.

After all these you'll be able to connect to your WebDAV! But there's another problem with most PC clients. If you're using a self-signed certficate like me, they'll automatically reject the connection. What to do? Open the website with Internet Explorer (be sure to open it with "Run as Administrator", else the "Install certificate" button won't show up later). Go to the webdav location e.g. https://www.example.com/webdav/. It will complain about the untrusted certificate. Do the following to install the certificate on the client PC:

  * It will complain about the certificate, click Continue.
  * In the address tab, click the certificate error icon.
  * Click View Certificates. Click Install Certificate... Click Next. Select "Place all certificates in the following store".
  * Click Browse and select Trusted Root Certification Authorities.
  * Click Next and then Finish.
  * On the Security Warning dialog box, click Yes.

After all the above steps, the computer can trust the location and you'll be able to map the network drive with the following command line:

```
net use * https://www.example.com/webdav
```

It will ask for username and password. You can also use Windows Explorer's map network drive wizard. One small problem you could stumble upon, is when trying to **move/copy large files**. There are two possible problems there:

  * Client Side: Windows may tell you that you cannot do that because of the file size. The "webdav redirector" on windows (client side, not server side) has a limit. It exists in the registry, in the key `HKLM\SYSTEM\CurrentControlSet\Services\WebClient\Parameters\FileSizeLimitInBytes`. The default is 50 MB. Change it to the maximum allowed and restart.
  * Server Side (thanks to Stefan's comment below): IIS7 has a default transfer limit of around 30 MB, which very much affects webdav. Execute the following command line to change the size:  
    `%windir%\system32\inetsrv\appcmd set config -section:requestFiltering -requestLimits.maxAllowedContentLength:xxx`
    where xxx is the number of bytes allowed.

One last problem you may stumble upon: Unfortunately, WebDAV for IIS has one major bug (at least for me): **You cannot add virtual directories that map to a whole hard disk.** For some reason, they are not shown when you're exploring the webdav remotely. To resolve that, you must create a folder in each hard disk e.g. "webdav" and put all your hard disk in there. Then add a virtual directory in IIS that points to that folder. It worked for me!

Conclusion: Webdav's a really nice way to connect to files remotely! I just wish Microsoft resolved the aforementioned problems and make the administrator's life easier.