---
layout: post
title:  "Why suckless is wrong"
date:   2016-10-19 13:13:13
categories: imho
---

Many people pointed me to this website [suckless](http://suckless.org/sucks/systemd) when a discussion about systemd
began. Now I got tired of summarizing why this blogpost is so wrong over
and over again. This time I want to write it down that other people have
arguments when they got pointed to this website. This can take a while
so feel free to grab a coffee or a cold mate.  
  
Let us begin with the second abstract:  
**What PID 1 Should Do**  
*When your system boots up the kernel is executing a given binary in its
known namespace. To see what are the only tasks the application running
as pid 1 has to do, see sinit. Just wait for child process to reap and
run some other init scripts.*  
  
First of all: **systemd** was **never**, is **not** and will **never**
be a init daemon. It is a system-**daemon**. Thats why it's called
system**d**. Moreover we don't live in 1980 anymore. The view and the
purpose of computers had changed completely since this time. We want to
have access on logs in pre-early-boot-time and we want to be sure that
several things are done during the boot process. Computers are not just
a server in some university anymore. Many people use GNU/Linux in their
workstations or notebooks nowadays.  

**systemd does {,U}EFI bootload**  
*Should systemd’s PID be changed from 1 to a negative, or imaginary,
number? It now exists before the kernel itself, during a bootup. See
also systemd-boot.*  
  
Again. system**d** is not only an init daemon. It's the same when I
would say:  
  
*Should grub's PID be changed from 4235 to a negative, or imaginary,
number? It Now exists before the kernel itself, during a bootup. See
also syslinux*  
  
As you see this sentence is absolutly ridiculous. Systemd has a
**module** and this **module** is managing the EFI entries in the EFI
bootloader. **systemd-boot** is not booting the system. It is just a
boot-manager! **EFI** does!  
  
**systemd replaces sudo and su**  
*Please note the command name, machinectl and its features at the
manpage. In exchange for a program which contains sudo, su and kill (and
does some functions which historically ssh/telnet did), bare metal users
have a tons of bloat and a lot of things to disable, if even possible,
useful only to people which deal with virtual machines.*  
  
First of all: **systemd-machined** or better **machinectl** will never
replace sudo or su. Do not worry. Secondly **machinectl** is totally
different than sudo or su. **machinectl** gets its information from
**polkit** via **dbus**. **polkit** is a much nicer way to define
permissions-rules. **sudo** and **su** has different weak points, one of
them is that **sudo** and **su** can not talk via **dbus** nor any other
IPC daemon. I think you know this moment when you forgot to type
**sudo** in front of a command. With **polkit** you don't have this
situation because the system service will just ask for a permission via
**IPC**. And yes.. you will need this for some stronger security
policies than just kernel-based permissions. You can find more about
this topic here:
[why-polkit](https://www.collabora.com/about-us/blog/2015/06/08/why-polkit-(or,-how-to-mount-a-disk-on-modern-linux))  
  



