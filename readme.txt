
I.   Introduction

This is a remake of a game called Snake Byte by Sirius Software Inc. published
in 1982 for, according to Moby Games, the Commodore 64, Vic-20, Apple II & 
Atari 8-bit.  This remake has no audio.

From Wikipedia: The player controls a snake, crawling into a rectangular area.
The aim is to eat 10 apples per level. If an apple is not eaten during the
given deadline, three extra apples are to be eaten. The snake becomes longer
with each apple eaten. The snake loses a life when crashing a wall or its
tail. Higher levels have more fences, making the game more difficult. An
optional difficulty are the "plums" (one or two pieces), which kill the snake
when hitting its head.

It's a game I loved to play back in the 80's and it gave me a lot of pleasure
to recreate the game using cc65.

I uploaded a video on YouTube that shows the different versions and some 
gameplay.  http://www.youtube.com/watch?v=H7Y4HVXVzoI

II.  Distribution

The version packaged up here comes in a few different flavours:
1.  The 4-colour hi-res version that closely resembles the original
2.  A text-based, colour version for the Commodore 64
3.  A conio version that runs on several platforms (slow!)

The conio version was done so anyone that wants to attempt a port has
an easy starting-point.  It contains no assembly.  It's worth noting that
I wrote the game for the C64 but made it so it's as portable as I could.
If your conio display isn't at least 40x25, you will miss some info.  On
the Atari with 24 rows, for example, there's a screen that asks how many
plums right before the game starts.  That question is on the 25th line
and isn't seen so it looks like a blank screen.

III. Building from source

This distribution is available from the following svn repository:
svn://stewbc.dnsalias.com/snake

The Makefile is a variant on the one with the following credits:
#############################################################################
## Generic Makefile for cc65 projects - full version with abstract options ##
## V1.1.1 (w) 2010 - 2011 Oliver Schmidt & Patryk "Silver Dream !" Łogiewa ##
#############################################################################

I found it at the link:
http://wiki.cc65.org/doku.php?id=cc65:project_setup

I added something I call SKUs so that I can have variants for the same target.
Building the (default) C64 hi-res version is done with:
make 
Building other SKU's is done by adding SKUS on the command line, example:
make SKUS="c64 c64text conio"
Building other targets is done by adding TARGETS on the command line:
make SKUS=conio TARGETS="c64 c128 apple2 atari"
The conio SKU is the only one that will compile on all of these targets.
See the Makfile for what's possible.  It's the best-written Makefile I 
have seen (not that I spend a lot of time in Makefiles, but this was
easy to understand and modify).

IV.  Porting

The source files can be found in the src folder inside the project.  Inside
the src folder are other folders, namely c64, c64text and conio.  These are
the SKU-specific files that make up that SKU.  The file that's really needed
is the target or sku-specific implementation for the functions in plat.h.  If
those are provided, and some can have empty implementations, the game can be
made to work on a target.  These are the files and why they exist in the C64
folder:
c64
	crt0.s		- Moves DATA and RODATA segments into place
	logo64.c	- The graphical image of the snake logo
	logo64.h	- Accompanying header
	plat64.c	- Implementation of c64 specific functions
	snakec64.cfg	- Custom memory layout (VIC hi-res in the 0x4000 bank)

See the other folders for their files.  They all have less files.  Only a
plat.c is actually required to make a target go.  To add the nes as a target,
simply create src/nes and add a file, let's say platnes.c, and you are off
to the races.  The conio version complains about no cgetc() on the nes.  You
really should be able to make a target work by just working in the plat file,
no other editing should be required.

There is a Misc folder that contains a file SnakeLogo.txt.  This is a string
version of the snake logo with the pixel colours represented by the letters
y for yellow, G for dark green and g for light green.  This may help with the
creation of that logo in the native format of the target.

V.   Credits & Misc.

Credits for the Commodore 64 version:
Game design by Chuck Sommerville
Programmed by Dan Stanfield
Music & Sound effects by Ray Elzey

Links for the original:
http://en.wikipedia.org/wiki/Snake_Byte
http://www.mobygames.com/game/snake-byte

VI.  Contact

Feel free to send me an email if you have any comments.  If you do make a port
or something else, I would love to hear about it!

swessels@email.com

VII. Thanks

To people who did great work back in the 8-bit days, and now, making the tools
to make this possible.