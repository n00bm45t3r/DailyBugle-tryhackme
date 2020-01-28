# writeups
This is my first write-up for the box Daily-Bugle on tryhackme.com
 
Running an nmap scan on the machine reveals the following:
![Screenshot](https://github.com/n00bmasterr/writeups/blob/master/nmapscan.png?raw=true)

Upon running gobuster we find that there is a couple of interesting directories.

![Screenshot](https://github.com/n00bmasterr/writeups/blob/master/gobuster.png?raw=true)

Taking a closer look at /administrator we see a login panel for joomla. Now we know that the server is running joomla on the box. Taking a look at README.txt we can see that it indicates that the joomla version  might be 3.7.0.
Looking around on the interwebs I stumbled upon this very interesting script on github called joomblah.py. https://github.com/XiphosResearch/exploits/tree/master/Joomblah
Running this script immediately returns the hashed password for jonah.

![Screenshot](https://github.com/n00bmasterr/writeups/blob/master/joomblah.png?raw=true)

Using john to crack the password can take a while. Took me around 20 mins, so be patient while johntheripper does its magic.
Eventually we get the password.

![Screenshot](https://github.com/n00bmasterr/writeups/blob/master/cracked.png?raw=true)

Using the username and the password we can then log into the joomlah cms. After doing some more  research I stumbled upon this article https://www.hackingarticles.in/joomla-reverse-shell/ that explains how we can gain a reverse shell, on the machine.
Following the article we gain an initial shell on the box by heading to the following link.

![Screenshot](https://github.com/n00bmasterr/writeups/blob/master/link.png?raw=true)

After looking around for a bit we can see that there is a configuration.php file in the /var/www/html directory.
After taking a look at the contents we see mysql db credentials.

![Screenshot](https://github.com/n00bmasterr/writeups/blob/master/configuration.png?raw=true)

Using these credentials we can log into the database, but also these credentials are used by the user in the home directory so by using su jjameson we get a shell as jjameson.
We can now go ahead and grab the user flag.
 From there after using sudo -l we can see that jjameson has the following sudo permissions.
 
![Screenshot](https://github.com/n00bmasterr/writeups/blob/master/nopasswd.png?raw=true)

Using gtfo bins and basically just copy pasting the commands we get a shell as root and can grab the root flag.

![Screenshot](https://github.com/n00bmasterr/writeups/blob/master/privesc.png?raw=true)

Thank you for reading my write-up.


