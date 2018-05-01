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
Picture here
That helped with the code needed, and how to make the files needed but that was it.

#### Milestone B:
I originally tried to use gcc as an interpreter to write the driver off of a suggestion from
a poster on stack overflow talking about a different driver, but it refused work as it was 
not seeing the required drivers I installed. Then, I started back on the vi thing many days later. After 
some hours spent searching on google, I learned vi is an interpreter that can be used for writing a driver. 
Using vi, I made two files, a .c file and a makefile.

A bit later, I found I needed root access in order to store the driver in the module libraries.

#### Milestone C:
Several days later of google diving and testing, I learn how to actually install the files using "insmod" 
and can remove modules with "rmmod." I also know now that of the files made during milestone A, the one with the .ko extension.
I can also check if it is installed with lsmod | grep driver, but I need to install the driver first.

After some hours using knowledge gained from an earlier tutorial assignment on the course, 
I learned about about linux to find the locations of where the files needed to go and how to launch them.
For the version from milestone A, I found this by using uname -r to get the version type I am using. and
successfully install the driver and uninstall it. Shortly later I found out how to move the .ko file to its home in the proper directory.



### Section 1 conclusion 
This was round 1 and 2. I learned a massive amount about linux with this project. I learned how to write a basic driver,
program using vi, working with the kernel, learning about root permissions, installing and removing drivers, then storing them
in the proper library.

### _Section 2_
So now that I can install and uninstall a driver in the right location, as well as put them in the right place, the next thing to do was make a mouse driver. The mouse guide I was given left out important details like addresses, so I went to open source.

After various fiddling, I found something that worked, made some very small modifications to it and got it to work.

Many hours later:

So it turns out that the mouse works even if it has no mouse driver installed, either the mouse driver I am using does not work/matter, or there is another generic backup driver that is replacing it.

### _Days Later_

So I found out the locations of al the drivers I would suspect in question, such as the mouse folder for drivers and the hid modules.
I tried to troubleshoot by systematically removing _every_ single mouse driver installed. I did this by uninstalling the current
driver (in this case pcmouse) by using the code -lsmod | grep mouse- to find the code and remove it. Then I found the directory where
the mouse drivers were, which (for this computer, version and flavor of linux) was
``/lib/modues/4.13.0-37-generic/kernel/driver/input/mouse/psmouse.ko
``
and

``the above path /drivers/hid/
``

Of the hid folder, there were only three drivers installed of al the drivers listed. They were hid-generic, /usbhid/usbhid (usbkbd.ko and usbmouse.ko in the same directory apparently were optional) and hid.ko (which was in use by the other two, unable to be uninstalled.)




Citations used:
http://freesoftwaremagazine.com/articles/drivers_linux/
https://stackoverflow.com/questions/38857741/is-dynamic-linker-part-of-kernel-or-gcc-library-on-linux-systems
Open scource code used
