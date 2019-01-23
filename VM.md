
# CS 196 Virtual Machine Guide

### What is a virtual machine?
A **virtual machine** (VM) is an emulation of a physical computer. Regardless of what physical computer architecture or operating system is running the emulation, a VM can simulate a common environment. This is very useful for us as software developers, since it allows a single developer to ensure that their software works smoothly across a variety of platforms.

The physical machine running the emulation is called a **host machine**, and each virtual machine is called a **guest machine**. These emulations must be run using a piece of software called a **hypervisor**, like VirtualBox or VMWare.

### Why are we using a virtual machine?
The course material in CS 196 spans multiple languages and platforms, and we have found that in the past, students working on Windows have encountered problems setting up Python, and different system setups make troubleshooting difficult for course staff. The virtual machine for this class runs Debian, which is a user-friendly and lightweight distribution of Linux. This will also serve as an introduction to using Linux, since many classes later on in the curriculum assume this understanding. Since we cannot reasonably ask every student to install Linux on their machine, emulating one is the next best solution.

## Installing VirtualBox
VirtualBox is a popular hypervisor distributed by Oracle that can be used on Windows, OS X, and Linux. Install the hypervisor using the appropriate commands from the official VirtualBox website [here](https://www.virtualbox.org/wiki/Downloads).

## Downloading the Debian VDI
Much like versions of Windows or OS X, distributions of Linux are also periodically released with version numbers and names. We'll be using **Debian 9.5 Stretch**, which is the most recent release of Debian (as of the time of writing). The virtual disk image (VDI) is a copy of a physical disk that can be distributed. Multiple virtual machines using the same VDI file will be exactly the same; this uniformity makes resolving installation/setup/configuration issues much easier. The VDI can be downloaded from OSBoxes [here](https://www.osboxes.org/debian/#debian-9-vbox). Make sure to download the 64-bit version of Debian 9.5 Stretch for VirtualBox.

This file will be downloaded as a `.7z` compressed archive file and must be unzipped before it can be used. After unzipping using your tool of choice (eg. 7-Zip for Windows, Unarchiver for OS X, or 7zr for Linux), a file named `Debian 9.5 (64-bit).vdi` will be created. It is a good idea to keep a copy of this file somewhere in case you make a mistake and need to restore the initial state of your VM.

## Creating a Virtual Machine in VirtualBox
Now we get to the interesting part. First, launch VirtualBox and press the **New** button in the top left-hand corner. Enter the following information:
```
Name: cs196
Type: Linux
Version: Debian (64 bit)
```
Press `Next >` to enter the Memory Size screen. The default 1GB should be plenty for the purposes of this class.

Press `Next >` again to enter the Hard disk screen. Click the `Use an existing virtual hard disk file` option, and select the VDI file downloaded in the previous section.

Finally, click `Create` and the `cs196` virtual machine will be created. Congratulations; you now have a bootable virtual machine!

## Tour of the Virtual Machine
To start up the virtual machine, press the **Start** button on the top right-hand section of the VirtualBox window. This will launch a separate window which will show the virtual machine itself. The first screen that you will see is a login screen; the user is named `osboxes.org` and the password is `osboxes.org`. Feel free to change those to your preferred username and (secure) password.

The user interface installed by default is called **GNOME**. For those of you coming from a Windows or an OS X environment, it may seem a bit unintuitive but also aesthetically pleasing. To launch programs, click the **Activities** text button in the top left-hand corner to view all installed applications. For the purposes of this course, it will be enough to locate a web browser (Firefox), the file manager, the Software and the command prompt (Terminal). The pre-installed text editor is called **gedit** and has the same functionality as Notepad in Windows.

Unlike other operating systems, both Python 2.7 and 3.5 are installed by default, and can be used by typing `python` and `python3` into the command prompt, respectively. Be careful to use only Python 3.5 for this class.

Feel free to play around with the other features of your virtual machine and personalize it with your favorite text editor or IDE, a new desktop background, and custom configuration of the GNOME desktop environment.