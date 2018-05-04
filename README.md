IN PROGRESS, Needs orginizing and pictures.

# Final Project Documentation
My final project's documentation

`Project requirements`
http://www.ebredder.org/Docs/ETRDocumentationv2.pdf

## Introduction:
My project was to write a mouse driver for linux. It would have basic functionality that one would expect from a mouse. There were
three attempts and three failures. I wil divide this into two sections.

### _Section 1_

#### Milestone A:
The first hurdle was figuring out how to even begin. Knowing quite little about linux the first thing I did was start
googling.

I found this nice guide here:
http://freesoftwaremagazine.com/articles/drivers_linux/
That helped with the code needed, and how to make the files needed but that was it.

#### Milestone B:
I originally tried to use gcc as an interpreter to write the driver off of a suggestion from
a poster on stack overflow talking about a different driver, but it refused work as it was 
not seeing the required drivers I installed. Then, I started back on the vi thing many days later. After 
some hours spent searching on google, I learned vi is an interpreter that can be used for writing a driver. 
Using vi, I made two files, a .c file and a makefile.

The code for the makefile I used is:
`obj-m := <DRIVERNAME>.o`

and the code to run this was:
``make -c /usr/src/linux-headers-<CURRENTKERNELVERSION> M=`pwd` modules``

A bit later, I found I needed root access in order to store the driver in the module libraries.

#### Milestone C:
Several days later of google diving and testing, I learn how to actually install the files using "insmod" 
and can remove modules with `rmmod`. I also know now that of the files made during milestone A, the one with the .ko extension.
I can also check if it is installed with `lsmod | grep driver`, but I need to install the driver first.

After some hours using knowledge gained from an earlier tutorial assignment on the course, 
I learned about about linux to find the locations of where the files needed to go and how to launch them.
For the version from milestone A, I found this by using `uname -r` to get the version type I am using. and
successfully install the driver and uninstall it. Shortly later I found out how to move the .ko file to its home in the proper directory.



### Section 1 conclusion 
This was round 1 and 2. I learned a massive amount about linux with this project. I learned how to write a basic driver,
program using vi, working with the kernel, learning about root permissions, installing and removing drivers, then storing them
in the proper library. I also learned some more information on what needs to be turned on and off to enable or disable the mouse driver, though not enough to fully do it at this point.

### _Section 2_
So now that I can install and uninstall a driver in the right location, as well as put them in the right place, the next thing to do was make a mouse driver. The mouse guide I was given left out important details like addresses, so I went to open source.

After various fiddling, I found something that worked, made some very small modifications to it and got it to work.

##### Many hours later:


So it turns out that the mouse works even if it has no mouse driver installed seemingly. I am guessing either the mouse driver I am using does not work/matter, or there is another generic backup driver that is replacing it.

### _Days Later_

So I found out the locations of all the drivers I would suspect in question, such as the mouse folder for drivers and the hid modules.
I tried to troubleshoot by systematically removing _every_ single mouse driver installed. I did this by uninstalling the current
driver (in this case pcmouse) by using the code -lsmod (| grep mouse/hid/etc)- to find the code and remove it. Then I found the directory where the mouse drivers were, which (for this computer, version and flavor of linux) was
``/lib/modues/4.13.0-37-generic/kernel/driver/input/mouse/psmouse.ko
``
and

``the above path /drivers/hid/
``
I also tried to find installed drivers by using rmmod * to uninstall every single driver in the directories. interestingly, when I removed and plugged in the mouse or keyboard, three drivers kept rebooting while removing other non-hid devices (like a usb wireless adapter) would not reinstall the drivers.

Using notepad to compare and contract the listed drivers and what the terminal said was not loaded, there were only three drivers installed of all the drivers listed. They were hid-generic, /usbhid/usbhid (usbkbd.ko and usbmouse.ko in the same directory apparently were optional/ not required for the mouse or keyboard to operate) and hid.ko (which was in use by the other two, unable to be uninstalled.)

### Section 2 Conclusion

I am unsure of how to continue from here, as this means that both the keyboard and mouse are able to operate without any dedicated driver. Only these three hid drivers get restored when I plug in/unplug the mouse or keyboard while the other drivers are seemingly not critical for the mouse or keyboard to function. I do belive that the open source mouse driver I have will work. While it remains untested in any meaningful manner, using modinfo on the hid-generic driver will list three authors. One of these authors is the same author of my mouse driver I found, meaning it should work due to the fact another working driver is written by the same author.


## Conclusion

Having started with only ever seeing linux one other time in my life, I learned a massive amount about linux.
While I learned quite a bit, I think the things that will help me most outside of the classroom are:

1. Basics of using the terminal

2. Syntax to operate the terminal more in depth (like going through root)

3. Creating make files, learning how to use vi and how to make code and linux work together

4. Learning how to uninstall and install modules/driver both permanently and temporarily (rmmod restores modules on reboot.)

5. Familiarity with how to troubleshoot linux

6. Moving and installing files in the correct places

7. installing packages needed (or what I thought I needed) through terminal

8. Modifing permissions on files and changing ownership of files.

While the goal of the project was unmet, the knowledge gained along the way should prove invaluable in the future if I ever have to go this in depth with linux in my career.

#### Failures summarized

Trying to use gcc as an interpreter and using linux-headers to install the driver. This proved redunant and incorrect. I later learned that gcc made the .o file, but not the required data structures to make the .ko file. The "make file" process does both of these things at once rather than one at a time.

Trying to indirectly manipulate the mouse driver using console commands in a different driver. This defeated the point of the entire project and was more of a band aid on a hole in a ship.

Trying to figure out why the mouse was working reguardless of any drivers installed. My guess is the hid-generic driver is a failsafe used to cover missing drivers. Perhaps installing a mouse driver while removing this one could work, it remains untested and with all the other false mountaintops in this project, I would assume that it is not that simple.

## Citations used:
* http://freesoftwaremagazine.com/articles/drivers_linux/
* https://stackoverflow.com/questions/38857741/is-dynamic-linker-part-of-kernel-or-gcc-library-on-linux-systems
* Open scource code used: https://casper.berkeley.edu/svn/trunk/roach/sw/linux/drivers/hid/usbhid/usbmouse.c
