# nmap
An introduction to the basics of nmap

## What you will learn 
* How to install and use nmap.
* How to use nmap to build a subnet of the various hosts on a network.
* The different nmap flags you can use to find specific information about a host.

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
The -sP flag tells nmap to scan for hosts, but not to scan for ports. Thus, you get a list of all of the devices that are active on your network.
##### You created a subnet of your network! That's awesome!
 Now, what else can we do with that information? 
 ### Finding more specific information
 You discovered which hosts are on your network. What else can you find out about them? 
 ##### Let's figure out what operating system they are using!
 To do this, follow the code below:                                                                                                  
 ![operatingsystem](https://user-images.githubusercontent.com/62024377/111917439-64ece780-8a56-11eb-8bfe-e36952b8a8cb.png)                                                             
 Oh no! That didn't work! Why? Sometimes, a device will be live but is configured not to respond to pings. Nmap, by default, tries to ping the device 
 and when it doesn't recieve a response back you get the problem as noted above. Not to worry! Nmap already gives us the solution. So, let's try it out.           
 ![OSdetection](https://user-images.githubusercontent.com/62024377/111917720-e4c78180-8a57-11eb-903d-5f9734004699.png)                                                                   
 AHA! It works! But why? Since nmap, by default, tries to ping a device that is configured not to respond back, it doesn't. Thus, nmap says "Well,
 they aren't responding. They must be down, I'm quitting.". By using the -Pn flag, we are telling nmap that we want you to scan it regardless of 
 whether you get a response back or not. When it does, nmap realizes that the host is alive and we get the information we wanted. 
 In this case, I discovered that my laptop (identified by the IP address 192.168.1.56) is running on Linux (Ubuntu to be exact). 
 What operating system did you get back? 
 ##### Note that the OS detection is not always 100% reliable on nmap. 
 
 
 
 
 
 
 

 



