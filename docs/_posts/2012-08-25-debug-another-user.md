---
id: 29
title: Debug a process of another user using gdb, Eclipse and Ubuntu
date: 2012-08-25T00:18:43+02:00
permalink: /archives/29
categories:
  - Linux
  - Technology
---
We assume that we (_user1_) need to attach gdb to an already executing process of another user (_user2_). Simply doing that, however, does not work, as gdb is ran by user1 and is not allowed to attach to a process of user2. Specifically, ptrace complains that the operation is not permitted. To successfully debug the process, we either have to:

  * Use remote debugging, using gdbserver. You start gdbserver under user2 and start listening for connections. Then, you start gdb under user1 and connect to the gdbserver.
  * Run gdb as root. This provides a faster and smoother debugging experience than using gdbserver. We will continue with this solution.

If we run gdb as root, we can successfully attach to the process of user2 (or any process). But, just typing "sudo gdb" usually prompts for your password. This makes things difficult to debug under an IDE, such as Eclipse. To overcome this problem, we need to allow user1 to run gdb under root without requiring a password. That can be done by editing the `/etc/sudoers` file. We can easily modify this file through the recovery console of Ubuntu. Reboot your machine, and press+hold Shift before Ubuntu starts loading. GRUB shows up and you can select the Recovery mode of Ubuntu. In the recovery options, select "root", which opens up a shell for the superuser. Do the following:

  * `chmod +w /etc/sudoers`
  * `vi /etc/sudoers`
  * At the bottom of the file, add the line `user1 ALL=(root) NOPASSWD: /usr/bin/gdb` (assuming gdb is at this location). This will allow you to "sudo gdb" without requiring a password. As a note, if you write `NOPASSWD:ALL` instead, it will allow you to execute any program with sudo without requiring a password. Save the file.
  * chmod -w /etc/sudoers
  * reboot now

Now, try "sudo gdb" and try "attach [pid]" to attach to the process of user2. It should work. To make it work with Eclipse, you need to make a new Debug Configuration of type "C++ Attach to Application". In the Debug panel, replace "gdb" with "sudo gdb". This will allow you to select any process to attach to, when Eclipse asks you.