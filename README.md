IN PROGRESS

# Final_Project_Documentation
My final projects documentation

Project requirements
http://www.ebredder.org/Docs/ETRDocumentationv2.pdf

Introduction: My project was to write a linux driver. This driver would be capable of reponding when installed and removed.
It would respond with a print to console.

Milestone A: The first hurdle was figuring out how to even begin. Knowing quite little about linux the first thing I did was start
googling.

I found this nice guide here:
Picture here
That helped with the code needed, and how to make the files needed but that was it.

Milestone B: I originally tried to use gcc as an interpreter to write the driver off of a suggestion from
a poster on stack overflow talking about a different driver, but it refused work as it was 
not seeing the required drivers I installed. Then, I started back on the vi thing many days later. After 
some hours spent searching on google, I learned vi is an interpreter that can be used for writing a driver. 
Using vi, I made two files, a .c file and a makefile.

Code Pictures here

A bit later, I found I needed root access in order to store the driver in the module libraries.

Milestone C: Several days later of google diving and testing, I learn how to actually install the files using "insmod" 
and can remove modules with "rmmod." I also know now that of the files made during milestone A, the one with the .ko extension.
I can also check if it is installed with lsmod | grep driver, but I need to install the driver first.

After some hours using knowledge gained from an earlier tutorial assignment during week X, 
I learned about about linux to find the locations of where the files needed to go and how to launch them.
For the version from milestone A, I found this by using uname -r to get the version type I am using. and
successfully install the driver.

Picture here


Milestone D: and now it is uninstalled, and using the same path I can move the .ko file to the module libraries and reinstall it from
there with the same path.

Picture here
Location in terminal picture here.

This concludes the project. I learned a massive amount about linux with this project. I learned how to write a basic driver,
program using vi, working with the kernel, learning about root permissions, installing and removing drivers, then storing them
in the proper library.

Citations used:
http://freesoftwaremagazine.com/articles/drivers_linux/
https://stackoverflow.com/questions/38857741/is-dynamic-linker-part-of-kernel-or-gcc-library-on-linux-systems
