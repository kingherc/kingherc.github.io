---
id: 10
title: How to Mono 1.9.1 and PHP 5 on Ubuntu 8.04 (Hardy)
date: 2008-05-22T21:37:35+02:00
permalink: /archives/10
categories:
  - Linux
  - Technology
---
I've also published this in <a href="http://ubuntuforums.org/showthread.php?t=803743">ubuntu's forums</a>:

It got me a few days to find out how to solve this problem. And it was rather frustrating. But finally I got to run mod\_mono on apache, and get some asp.net 2.0 working on Ubuntu 8.04! I searched around the internet, and many have the same problem: It's annoying that Ubuntu Hardy doesn't let you install mod\_mono on apache 2 without uninstalling PHP, though it was possible on Ubuntu 7.10.

We'll assume a new Ubuntu 8.04 installation, with an apache 2 and php 5 installed and working fine. It's annoying that Ubuntu Hardy doesn't let you install libapache2-mod-mono without uninstalling libapache2-mod-php5 (which will then not serve php pages, and will only serve them as downloadable files), though it was possible on Ubuntu 7.10. It's further annoying that it's all too complicated to get mod_mono working! Let's solve the problem. I'm assuming you know a bit about linux commands, just enough to edit a file at least. I'll not explain all commands, but you can find some explanations about what we're doing in the referenced pages i've written in the bottom of the post.

**First steps:**

  * `sudo apt-get remove mono-common`
    That will remove all the extra packages that are installed with mono as they all depend on it. Be aware that it will also remove applications like f-spot and beagle, which will have to be re-installed after the mono upgrade if you wish to use them.
  * `cd ~`
  * `mkdir src`
  * `cd src`  
    This is where we'll download the mono source files and work with them.
  * `sudo vi /etc/apt/sources.list`  
    Remove the # characters from the universe and multiverse entries and save the file. That will allow the apt-get command to install packages from the universe and multiverse repositories.
  * `sudo apt-get update`
  * `sudo apt-get install build-essential pkg-config libglib2.0-dev bison libcairo2-dev libungif4-dev libjpeg62-dev libtiff4-dev`
    This will install required and optional packages for compiling and installing mono.

**Installing libgdiplus:** 

  * Go to http://go-mono.com/sources-stable/ to see the links for the files we'll be downloading and we'll compile and install. Note the version (if it's not 1.9.1 which we'll be using), and do something like the following to get the latest version from the links:
  * `wget http://ftp.novell.com/pub/mono/sources/libgdiplus/libgdiplus-1.9.tar.bz2`
  * `tar -xvf libgdiplus-1.9.tar.bz2`
  * `cd libgdiplus-1.9/`
  * `sudo ./configure --prefix=/usr/local`
  * `sudo make`
  * `sudo make install`
  * `sudo sh -c "echo /usr/local/lib >> /etc/ld.so.conf"`
  * `sudo /sbin/ldconfig`

**Installing mono:** 

  * `cd ~/src/`
  * `wget http://ftp.novell.com/pub/mono/sources/mono/mono-1.9.1.tar.bz2`
  * `tar -xvf mono-1.9.1.tar.bz2`
  * `cd mono-1.9.1`
  * `sudo ./configure --prefix=/usr/local`
  * `sudo make`
  * `sudo make install`
  * We'll now add mono to the bash path. Edit the following file:  
    `vi ~/.bashrc`
    And add the following lines at the end of the file:  
    `PATH=/usr/local/bin:$PATH`
    `LD_LIBRARY_PATH=/usr/local/lib/:$LD_LIBRARY_PATH`
    `PKG_CONFIG_PATH=/usr/local/lib/pkgconfig:$PKG_CONFIG_PATH`
  * bash  
    This command will reload bash, so that the mono command is available.

**Installing XSP (required, even if you'll only use mod_mono):** 

  * `cd ~/src/`
  * `wget http://ftp.novell.com/pub/mono/sources/xsp/xsp-1.9.1.tar.bz2`
  * `tar -xvf xsp-1.9.1.tar.bz2`
  * `cd xsp-1.9.1/`
  * `sudo ./configure --prefix=/usr/local`
  * `sudo make`
  * `sudo make install`

**Let's test XSP and see if everything works until now:** 

  * `cd /usr/local/lib/xsp/test`
  * `xsp2`
    This command will start the xsp web server which will most probably listen on port 8080. Because the command is run from this directory, this directory will serve as the root of the web server. Open up a browser and go to http://localhost:8080/. You should see the XSP test asp.net pages. If you see them, everything works fine until now, cheers!  
    Note: XSP is a great way to test and develop mono websites.

**Installing mod_mono module for apache 2:** 

  * `sudo apt-get install apache2 apache2-threaded-dev`  
    apache2-threaded-dev will be needed for apxs, which automates the loading of apache modules.
  * `cd ~/src/`
  * `wget http://ftp.novell.com/pub/mono/sources/mod_mono/mod_mono-1.9.tar.bz2`
  * `tar -xvf mod_mono-1.9.tar.bz2`
  * `cd mod_mono-1.9`
  * `sudo ./configure --prefix=/usr --with-apxs=/usr/bin/apxs2`
  * `sudo make`
  * `sudo make install`
  * `cp -r /usr/local/lib/xsp/test /var/www/test`
    This will copy the XSP test site to Apache's default root website (/var/www), so that we may later test mod_mono and see if everything works fine.
  * `sudo a2enmod mod_mono`
    `sudo vi /etc/apache2/mods-enabled/mod_mono.conf`
    and uncomment the aps.net version of mono server you want (I uncommented the 2.0 and commented the 1.0).EDIT: If the a2enmod command complains about not finding the module, then you'll have to activate mod_mono on apache manually:  
    Visit my first reference page at http://blog.ruski.co.za/page/Install-Mono-126-on-Ubuntu-710.aspx, and follow the steps of the section "Installing Mod_Mono" just after the "make install" command. Be careful to check the paths you write in those steps, because at some steps the paths should be /usr/lib/... and not /usr/local/lib/..., according to our guide. These steps are equivalent with the "a2enmod" step of my guide, and after you'll be able to continue to our next bullet point. I'm reproducing these steps for further assistance, but I've not tested them, if you have an error, please make a comment: 
      * `sudo vi /etc/apache2/apache2.conf`
        Add the following line at the end:  
        Include /etc/apache2/mod_mono.conf
      * `sudo vi /etc/apache2/mods-available/mod_mono.load`  
        Add the following line to the file:  
        `LoadModule mono_module /usr/lib/apache2/modules/mod_mono.so`
      * `sudo vi /etc/apache2/mods-available/mod_mono.conf`
        Add the following to the file:  
        `AddType application/x-asp-net .aspx .ashx .asmx .ascx .asax .config .ascx` 
        `DirectoryIndex index.aspx`  
        `include /usr/local/lib/mono/2.0/mono-server2-hosts.conf`
      * `sudo vi /usr/local/lib/mono/2.0/mono-server2-hosts.conf`  
        Add the following to the file:
        ```
        <IfModule mod_mono.c>
          MonoUnixSocket default /tmp/.mod_mono_server2
          MonoServerPath default /usr/local/lib/mono/2.0/mod-mono-server2.exe
          AddType application/x-asp-net .aspx .ashx .asmx .ascx .asax .config .ascx
          MonoApplicationsConfigDir default /usr/local/lib/mono/2.0
          MonoPath default /usr/local/lib/mono/2.0:/usr/local/lib
          
        </IfModule>
        Note: Be sure that `/usr/local/lib/mono/2.0/mod-mono-server2.exe` exists, else use `/usr/bin/mod-mono-server2` instead (thanks tiger2004 for this).

  * `sudo vi /etc/apache2/sites-enabled/000-default`
    and add the following at the end of the virtual host:
    ```
    MonoServerPath "/usr/local/bin/mod-mono-server2"  
    MonoApplications "/test:/var/www/test"  
    <Directory /var/www/test>  
    SetHandler mono  
    AddHandler mod_mono .aspx .ascx .asax .ashx .config .cs .asmx  
    DirectoryIndex index.html index.aspx default.aspx Default.aspx  
    Options Indexes FollowSymLinks MultiViews  
    AllowOverride None  
    Order allow,deny  
    allow from all  
    </Directory>
    ```
  * `sudo /etc/init.d/apache2 restart`
  * Now, go to http://localhost/test/. If you see the XSP test pages, then everything works fine! Maybe you'll see the XSP test site without graphics and images, but it's not an error (it's because paths in the source shouldn't start with a /)!  
    You can also test PHP pages, they should work fine too.

References:

  * <a href="http://blog.ruski.co.za/page/Install-Mono-126-on-Ubuntu-710.aspx">http://blog.ruski.co.za/page/Install-Mono-126-on-Ubuntu-710.aspx</a>
  * <a href="http://www.mono-project.com/Mod_mono">http://www.mono-project.com/Mod_mono</a>
  * <a href="https://help.ubuntu.com/community/MonoFromSource">https://help.ubuntu.com/community/MonoFromSource</a>