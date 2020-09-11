https://itstuff.the-zabala.net/2014/07/linux-driver-for-canon-imageclass.html

Linux Driver for Canon ImageClass MF3110/3112
I recently stumbled upon a treasure trove while looking for ways to make my old Canon ImageClass MF3112 all-in-one laser printer work with the latest OS around.

Background of the situation

If you're looking for drivers of this printer at the Canon official website, it only provides drivers to support 32-bit Windows XP, Vista and 7... none for Linux nor MacOS. This is pretty much a bummer especially if you have up-to-date workstations that "need" 64-bit OS (the > 4GB RAM thing). In my case, all my workstations and laptops run a Windows 8.1 and an Ubuntu Gnome 14.04, both 64-bit.

Canon actually published a package to install printer drivers for Linux-based OS, called the "UFR II". However, this is only for their not-so-late models, and apparently the one I need is the one they developed prior to this. The older models seem to be an implementation based on a raster-like format that I have no particular clue how it differs.

After a day of two of digging around the Internet, and exploring the vast "Page 2 and 3" Google search results, I found a guy who made a custom linux driver to support this "rastertocups" print driver thing that Canon has done and left to rot. He has a GitHub repo page which sort of discussed what the driver is and what other canon printer models are supported.

Since there's no HowTo wiki entry to use his codes, I opted to share what I did in order to use and install it (credits to ondrej-zary for the source code).

Pre-work Requirements
			sudo rights (or root)
			gcc and compiler (e.g. make, build-essential) is installed
			cups, libcups2-dev, and libcupsimage2-dev is installed
even though it doesn't have the required drivers, I installed the UFR II Canon Linux Drivers because it seems that it is needed for the custom drivers to work
The Steps
			Download ondrej-zary's carps-cups source code (there's a zip file download link present)
			Extract it on the desired work-area folder (temporary use; mine was inside my home folder)
			Using the terminal, go to the location of the unzipped folder and run "make" 
			$ cd ~/carps-cups-master 
			$ make 

If there are errors of missing dependencies, you can try to use "apt-file search " to check which packages you need install before trying to make it.
If things look fine and there's no error, proceed with "sudo make install" (or make install for root users);
$ sudo make install
The Result

I've done this and made my printer work with Ubuntu Gnome 14.04 64-bit (cups 1.7.2) and Debian 7 Wheezy 32-bit (cups 1.5.3). I added printer and selected the compiled driver via the cups web interface (usually running at your linux machine "localhost:631").




Hope this helps somebody out there... and again a huge thanks to ondrej-zary!
Posted by Armand Z at 11:14 AM 
Email This
BlogThis!
Share to Twitter
Share to Facebook
Share to Pinterest
Labels: 14.04, canon, carps-cups, cups, debian, drivers, linux, mf3110, mf3112, ondrej-zary, ubuntu, ufr, ufrII, wheezy
21 comments:

Ihor KaharlichenkoNovember 10, 2014 at 3:29 PM
Hi. Thank you for this great tutorial! It really helped to get started with my MF 3110.

To simplify installation on Ubuntu I've made a PPA:

So now it is just a matter of running these commands:

sudo add-apt-repository ppa:madkinder/carps-cups
sudo apt-get update
sudo apt-get install printer-driver-carps

For now the packages are built only for Trusty. Feel free to contact me if you need other Ubuntu versions.

Reply
Replies

UnknownOctober 24, 2015 at 3:51 PM
Thank you a lot!
Now I can live with my (not so old) MF3110 and enjoy life :)

Be lucky and happy.


AnonymousNovember 16, 2015 at 3:31 PM
Hello, i need packages for KDE Linux...can you help me with this?


Ihor KaharlichenkoNovember 16, 2015 at 5:10 PM
It doesn't matter what desktop environment you use (GNOME, KDE, XFCE, whatever) for these packages to work.

Given you are on Ubuntu Trusty (14.04) just follow those three commands I posted above and that should do it. You don't even need a compiler.


AnonymousNovember 16, 2015 at 5:14 PM
I have Linux KDE.These commands will help me with the installation MF3110 Linus KDE?

Reply

Ihor KaharlichenkoNovember 10, 2014 at 3:35 PM
Also it turns out that "UFR II Canon Linux Drivers" are not needed, Ondrej's driver is sufficient.

Unfortunately my MF 3110 is very unstable with it: it works flawlessly after you plug printer in and add it to CUPS; but after reboot it doesn't work anymore.

The instructions in the repo's README suggesting to use usblp file uri didn't help. Any help would be appreciated very much.

Reply

imagestoreDecember 18, 2014 at 6:02 PM
Hello,
Your post is very helpful. Now I need not to call my tech person to get fix my Canon printers. Thanks for sharing.Keep in touch. Canon ImageClass MF3110/3112 is one of the best Canon printers in India.

Reply

UnknownJanuary 16, 2015 at 8:04 PM
This comment has been removed by the author.

Reply

UnknownJanuary 16, 2015 at 8:08 PM
Hello!
Thanks a lot ! Instruction is very simple and helpfull. All went ok, mf3110 works well (Ubuntu 12.4) though there was some errors/warnings during the compile process.
You've made my day, especially after "throw out this junk" solutions from our tech guys =)

Reply

UnknownAugust 19, 2015 at 7:34 PM
Works! Thank You for this manual, Ondřej Zarý for drivers, Madkinder for PPA and Google for its searching abilities:-)

Reply

UnknownOctober 15, 2015 at 1:53 AM
nice works like a charm just make sure that you have all the requirements

Reply

AnonymousNovember 16, 2015 at 2:53 PM
Hello...pls can you help me? i try to install craps-cups, but i see this errors...pls help!!! [root@reklama-6 carps-cups-master]# make install
gcc -Wall -Wextra --std=c99 -O2 rastertocarps.c -o rastertocarps -lcupsimage -lcups
/usr/bin/i586-alt-linux-gcc: No such file or directory
make: *** [rastertocarps] Ошибка 1
[root@reklama-6 carps-cups-master]# sudo make install
root is not in the sudoers file. This incident will be reported.

Reply
Replies

UnknownNovember 16, 2015 at 2:59 PM
you can try Madkinder's solution (check his comment) as he has compiled a package that already does most of the dirty-work to install the driver


AnonymousNovember 16, 2015 at 3:32 PM
ok, i'll try to making like this. thx

Reply

UnknownJanuary 29, 2016 at 10:45 PM
Hello and thank you for this post. I, like the rest of everyone here, just want to save a bit of money and utilize an existing printer. Although in my search for a solution, I have come to realize how unique Canon printers are in the way of making them work with Linux.

I also realize that Fedora and Ubuntu are quite different animals, but I wonder if anyone can help with a code error.

I ran 'make', and before it could even get going I got this error:

carps-decode.c: In function ‘decode_print_data’:
carps-decode.c:319:10: warning: format ‘%x’ expects argument of type ‘unsigned int’, but argument 7 has type ‘long int’ [-Wformat=]
printf("out_pos: 0x%x, line_num=%d, line_pos=%d (%d), len=%d, in_pos=0x%x ",
^
gcc -Wall -Wextra --std=c99 -O2 rastertocarps.c -o rastertocarps -lcupsimage -lcups
ppdc carps.drv

Now, I am certainly no programmer, and on a scale of one to ten, ten being a Linux guru and one being "Oh look, Penguins! How cute!", I'm a three or four at best.

Any help would be very appreciated.

Reply
Replies

Ihor KaharlichenkoJanuary 30, 2016 at 6:10 AM
John, what Fedora version do you use?

Reply

realcyborgMay 22, 2016 at 6:47 PM
THX a lot! Canon MF 3110 worx on ubuntu 16.04, 32 bit

Reply

tengelyiJuly 17, 2016 at 5:58 PM
Hello Madkinder, is there a a way to create version for Xenial? THX

Reply
Replies

Ihor KaharlichenkoJuly 19, 2016 at 7:12 AM
Done. Updated and rebuilt the package for both Trusty and Xenial.

Reply

upssMarch 16, 2017 at 4:29 PM
Hi Armand,
Thkn you for very nice article. I jost come around to find the solution for one of my Canon printers.

Unfortunately i see that it is not good for a MF3200 series printer. Can you tell me if it is possible somehow to change and have the driver for a MF3200 Series printers ?

Thank you in advance.

Reply
Replies

Armand ZApril 3, 2017 at 11:39 AM
Hi!

Sadly I'm not the original author of the source code/custom drivers. I think the MF3200 is also one of those printers that uses that raster protocol of sorts. Maybe you can reach out to the original author via his github account.

Cheers and good luck!

Reply

