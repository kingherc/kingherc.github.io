---
id: 11
title: Ubuntu linux as NFS client of Windows Server 2008
date: 2008-06-26T01:44:44+02:00
permalink: /archives/11
categories:
  - Technology
  - Windows
---
I have installed Windows Server 2008 on my main machine and I have all my files there. But as I'm also developing PHP, I wanted to set up an ubuntu test server. I thought wonderfully, I could finally put my old laptop to use! So, I installed ubuntu server on my laptop. But my laptop doesn't have much hard disk space... And of course, I would rather have my files on the Windows Server machine, because I think they are more stable and secure there (you know linux, you can get them pretty messed up in a second if you do something nasty!).

So, how do I connect ubuntu to WS08? With NFS of course. As I only need my laptop to access files on Windows (like .php files, or even set up mysql database files there), the laptop only needs to be an NFS client to Windows Server's NFS Server. And that's where problems begin... The main one being how user identities are mapped between the two systems! I was rather impressed when I found out that Microsoft had a whole bunch of tools that provide interoperability with Unix systems!

So, what do you do? I'll only talk about my case which is simple: My Windows Server is my only Domain Controller and has Windows user identities there. In order to also manage Unix users, you have to install the Active Directory Role's feature named "Identity Management for UNIX" along with "Server for Network Information Services", included with Windows Server. Also install "Subsystem for UNIX-based Applications" which we'll need later. After this, WS will act as a NIS server. The NIS server holds uids and gids that a unix system can use. And that means that now, you can define usual windows AD users and groups as NIS users and groups!

In the most usual case, you'll only have one user you use on ubuntu with uid 1000 and gid 1000. So, create an AD user and group on WS (like "kingherc" and "kinghercgrp", names aren't important but they should be one word), or edit existing users and groups if you're already defined a user hierarchy. In the properties of the user, go to UNIX Attributes and there type 1000 for the uid. In the properties of the group, go to UNIX attributes and type 1000 for the gid, and add "kingherc" user to the members. Go back to the UNIX properties of the user, and check that the primary group is "kinghergrp".

OK, so now you have correllated your AD users with NIS users. You only need to install NIS client on ubuntu (check the internet for a guide), and connect it to the Windows Server NIS Server. Type "yptest" to check that it gets correct users from WS.

After solving the user stuff, you need to configure NFS Server on WS. Go to Administrative Tools > Services for NFS. Right-click "Services for NFS" and Properties. Here, check that for the user mapping, we use an AD Domain, and put in there the domain of your Windows Server (usually something like blabla.lan).  
Note: If your Windows Server isn't a Domain Controller, you're also presented with the option of using a "User Name Mapping" server. I believe this tool is provided free by Microsoft (check the internet), and acts a server which holds the uid and gid and you manually correllate them with Windows users.

Next, we need to export NFS shares. Go to a NTFS folder you wish to share. Go to Properties and you'll find a brand new NFS Sharing tab. Click it to define the share name (give the same as the folder name), and machine permissions. Now go to the Security tab, click Advanced, Owner tab, and define the owner as the AD user which is mapped to the ubuntu user. After this step, you should NOT alter permissions for the NFS folder from Windows Folder properties.

Here's how we modify the permissions of the folder: Start > Subsystem for UNIX > C Shell. This gives a unix-like shell for windows. "cd /dev/fs/J/ubuntufolder" where J is supposed to be a windows drive, and ubuntufolder the NFS share. "ls -laFh" will show you the owner of the folder and the group of the folder. It's crucial to change this to the ubuntu mapped user, so that ubuntu may access and alter this folder. Use the usual unix "chown" command to alter the folder's user and group to kingherc and kinghercgrp (use the names and not the uid and gid). After that, use "chmod" to define permissions.

You should all be done now. Go to your ubuntu machine, do a simple NFS mount command for the ubuntufolder, and you'll be able to access the remote NTFS folder!  
Note: If you see 4294967294 as the owner or group of the folder, then you didn't successfully changed the owner of the nfs share as described above.

Alas, Windows can live happily alongside a unix machine 🙂  
Resources you should check out:

  * <a href="http://blogs.msdn.com/sfu/">http://blogs.msdn.com/sfu/</a>
  * <a href="http://en.wikipedia.org/wiki/Microsoft_Windows_Services_for_UNIX">http://en.wikipedia.org/wiki/Microsoft_Windows_Services_for_UNIX </a>