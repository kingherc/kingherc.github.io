---
id: 3
title: Pocket Control PC
date: 2004-10-29T19:00:17+02:00
permalink: /archives/3
categories:
  - Mobile Devices
  - Technology
---
### Description

<img src="/assets/posts/2004-10-29-pocket-control-pc/PocketControlPC_48.gif" />

Pocket Control PC is consisted of two programs. The first is run on a PC and the second, runs on a device. When the two programs connect, they can exchange and execute commands. In this way, you can control a PC's mouse, keyboard and programs remotely from a device like Smartphones/PocketPCs 2003 and PCs.

Pocket Control PC is divided in two programs, both essential for it to work. One program is called the client and the other the host. The host program is Pocket Control PC -- PC and always runs on a PC. The client one is Pocket Control PC -- NetCF which runs on Smartphones 2003, Pocket PCs 2003 and PCs. When both programs are run and connected, the remote user can send commands to the PC which are then executed. The current commands supported pertain to the following:

  * Mouse and Scroll commands: The remote user is able to control the PC's mouse (and mouse's vertical scroll).
  * Keyboard commands: The remote user is able to control the PC's keyboard. All usual keys are supported. Current keyboard layout is US (extended -- with media/browser/application keys e.g. next/previous track). The remote user can normally change languages in Windows.
  * Input text & keystrokes: The remote user can input text and keystrokes for the PC.
  * Input Mouse location: The remote user can input coordinates to move the PC's mouse.

For the connection between the device and the PC, the TCP/IP protocol is used. Microsoft's Activesync connection is adequate (through many ways like cable, bluetooth, network etc). You can find more info in the programs' readmes.

### Screenshots:

<p style="text-align: center;">
  <img src="/assets/posts/2004-10-29-pocket-control-pc/ControlPCScr_1.gif" />
  <img src="/assets/posts/2004-10-29-pocket-control-pc/ControlPCcf_2.gif" />
  <img src="/assets/posts/2004-10-29-pocket-control-pc/ControlPCcf_1.gif" />
  <img src="/assets/posts/2004-10-29-pocket-control-pc/ControlPCScr_2.gif" />
  <img src="/assets/posts/2004-10-29-pocket-control-pc/ControlPCcf_3.gif" />
  <img src="/assets/posts/2004-10-29-pocket-control-pc/ControlPCcf_4.gif" />
  <img src="/assets/posts/2004-10-29-pocket-control-pc/ControlPCcf_5.gif" />
</p>

### Requirements:

Pocket Control PC -- PC:

  * A PC which runs Pocket Control PC -- PC (for Windows platforms). Microsoft .NET Framework 1.1 or later must be installed on the PC. You can download it at Microsoft's website.
  * A device which runs Pocket Control PC -- NetCF. Supported devices: Smartphones 2003 or later, Pocket PCs 2003 or later, PCs.
  * Connection between PC and the device with TCP/IP. Microsoft's Activesync connection is adequate.

Pocket Control PC -- NetCF:

  * A device with .NET Compact Framework. It could be Smartphones 2003, Pocket PCs 2003 and PCs. In Smartphones and Pocket PCs, .NETCF is pre-installed. On PCs, you must download and install .NETCF or .NET Framework if you do not have it.
  * A PC which runs Pocket Control PC -- PC.
  * Connection between PC and the device with TCP/IP. Microsoft's Activesync connection is adequate.

### Troubleshooting for 1.1 version

I've got a lot of messages about people not being able to achieve a connection between the device and the PC with Pocket Control PC -- 1.1 and Pocket Control PC -- NetCF 1.0. So, here are some easy and general steps you can follow to achieve a connection. If the problem persists, please don't hesitate to email me.

As I've noted that the programs with the default options work/connect just fine and because reseting the options isn't yet supported, it's best to reset the options for each program manually.  
For the PC: Options: Validate Connection is checked. Also Ensure Connection is checked (but disabled if there's no connection). Configure IP is at 0.0.0.0 and at the max port. Auto-Listen is checked to none and Stop When Disconnect is not checked. Auto Listen/Minimize on start are not checked.  
For the device: Options: Validate Connection is checked. Also Ensure Connection is checked (but disabled if there's no connection). Configure IP is at ActiveSync's IP and at the max port.

There's another thing you have to be careful about: It's best to uncheck "Ensure active connection" on both the device and the PC when you first get a connection. When you uncheck it, restart the programs (or the devices) so that the options are saved. After this I think ther will not be another problem.  
If the above option is checked, you may be improperly disconnected without a reason sometimes.

With the above options, trying to connect is likely to succeed.  
Hope I've helped. If you still can't get a connection done, you could use the older versions of the program found at the bottom of this page which do not show any of the above errors.

### Download

Through this page you will download (free) Pocket Control PC -- PC and Pocket Control PC -- NetCF (**both must be downloaded**, because they depend on each other). The executable and source are distributed in a .zip file that be opened with WinZip or WinRar or with Windows ME (and newer) and other programs. Instructions are given inside to install the program on your device (Windows Mobile) and on your PC. Also, be sure to read the ReadMe and the license (GNU GPL) of the program.

**Quick Guide:** Download <a href="/assets/posts/2004-10-29-pocket-control-pc/PocketControlPC-PC1.1.zip">Pocket Control PC -- PC</a> and then <a href="/assets/posts/2004-10-29-pocket-control-pc/PocketControlPC-NetCF1.0.zip">Pocket Control PC -- NetCF</a>. Unzip them and read their ReadMes. Follow their installation instructions for each program. Then, connect the PC and the device through activesync (a small bluetooth guide is contained in the readme if you prefer it). Then, run both programs. On the PC, set the program to Listen (Connection > Begin Listening). Then, quickly click the Connect button on your smartphone. Now, you're ready to control your PC through your device (Menu > Modes).
