# nmap
An introduction to the basics of nmap and how to bypass some common firewall rules.

## What you will learn 
* How to install and use nmap.
* How to use nmap to build a subnet of the various hosts on a network.
* The different nmap flags you can use to find specific information about a host.
* An intro to source-port manipulation, IPv6 attacks, and bypassing filtered ports.

### How to install and use nmap
Nmap is a linux-based command-line tool used for network exploration and security auditing. Although it can be 
used on windows, it is easiest to use on linux. 
#### If your OS is a linux distro
You can simply type in the command 'sudo apt install nmap' in the terminal.
##### You will see something similar to the image:
![nmap-install](https://user-images.githubusercontent.com/62024377/111915218-7e3c6680-8a4b-11eb-8855-f4be8adfffae.png)


  * *Note that if you are running Kali Linux, nmap will be preinstalled.*
#### If your OS is Windows or other
The easiest and safest way is to use a virtual machine, or VM. I highly recommend using [virtualbox](https://www.virtualbox.org/) 
and installing Kali Linux on it. 
It is a free and open-source VM perfectly suited for this task. To install Kali linux on virtualbox please click [here](https://phoenixnap.com/kb/how-to-install-kali-linux-on-virtualbox)
### Using nmap
##### Note that I am using Ubuntu, but everything is the same regardless of which linux distro you use.
Now that you have nmap installed, open up the terminal, if you haven't already, and type in 'nmap' and hit 'enter'
on the keyboard. What you will see is a list of various commands and flags you can use with nmap. I will be 
showing you a general overview of certain ones for common tasks to get you started. 
#### Network scanning
Let's say I want to know whether my phone is up and running. I would use the command: 
![ping](https://user-images.githubusercontent.com/62024377/111915779-569acd80-8a4e-11eb-89e1-941650a5c36c.png) 
##### to stop pinging just press ctrl+c
  You can do the same thing with your network. Depending on your region, the format of your network will be 192.168.1.x. If it is not, use whatever 
format your region uses. 
##### Let's try it out!
![network](https://user-images.githubusercontent.com/62024377/111916494-91eacb80-8a51-11eb-9600-525e7cd55867.png)                                      
As you can see, my network is working. Presumably, yours is too. Normally, there are 256 possible hosts on a given network. To scan all of them, we can 
use $ping <device identification> which is 192.168.1.1 all the up to 192.168.1.256 to see which ones are active and which are not. 
 This is where nmap comes in. We can use nmap to see all the live hosts on a given network.
##### The way to do that is: 
![network-map](https://user-images.githubusercontent.com/62024377/111916839-41746d80-8a53-11eb-97ce-99622979f406.png)                               
  Please follow the above syntax correctly. Capitalization matters when using this tool!



