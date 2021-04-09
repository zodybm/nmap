# Nmap
The goal of this documentation is to familiarize you with the basics of Nmap and its capabilities.

- [Nmap](#nmap)
  * [What you will learn](#what-you-will-learn)
    + [System Requirements](#system-requirements)
    + [Installing Nmap on a Debian-based Linux Distro](#installing-nmap-on-a-debian-based-linux-distro)
    + [If your OS is Windows](#if-your-os-is-windows)
    + [Using Nmap](#using-nmap)
    + [Network scanning](#network-scanning)
    + [Finding more specific information](#finding-more-specific-information)
    + [More with Nmap](#more-with-nmap)
    + [Legal disclaimer!](#legal-disclaimer-)
    + [Licensing](#licensing)
    + [Want to contribute to nmap?](#want-to-contribute-to-nmap-)
                                                                                                                                                                      
## What you will learn 
* How to install and use Nmap.
* How to use Nmap to build a subnet of the various hosts on your network.
* The different Nmap flags you can use to find specific information about a host.
                                                                                                                                                                    
### System Requirements
You only need to have about 8 MB available for storage and the best part is Nmap will run on practically any computer or laptop!
                                                                                                                                                                    
### Installing Nmap on a Debian-based Linux Distro
Nmap is a linux-based command-line tool used for network exploration and security auditing. Although it can be 
used on Windows, it is easiest to use on a Debian-based Linux distro. 
                                                                                                                                                                                                                                                                                              
**To install** type in the command below in your terminal then follow the prompt:
```bash
~$ sudo apt install nmap
```
                                                                                                                              
 **You will see something similar to the image:** 
                                                                                                                                     
![nmap-install](https://user-images.githubusercontent.com/62024377/111915218-7e3c6680-8a4b-11eb-8855-f4be8adfffae.png)


  **Note that if you are running Kali Linux, Nmap will be preinstalled.**
### If your OS is Windows
The easiest and safest way is to use a virtual machine, or VM. I highly recommend using [virtualbox](https://www.virtualbox.org/) 
and installing Kali Linux on it. 
It is a free and open-source VM perfectly suited for this task. To install Kali linux on virtualbox please click [here.](https://phoenixnap.com/kb/how-to-install-kali-linux-on-virtualbox)

### Using Nmap

 **Note that I am using Ubuntu, but everything is the same regardless of which Debian-based Linux distro you use.**                                                

Now that you have Nmap installed, open up the terminal and type in the command below:
```bash
~$ nmap
```
What you will see is a list of various commands and flags you can use with Nmap. I will be 
showing you a general overview of certain ones for common tasks to get you started. 

### Network scanning

Let's say I want to know whether my phone is up and running. I would use the command: 
```bash
~$ ping <devices ip address>
```
![ping](https://user-images.githubusercontent.com/62024377/111915779-569acd80-8a4e-11eb-89e1-941650a5c36c.png) 

 **to stop pinging just press ctrl+c**                                                                                                 
 What you are doing is sending packets to the device to see if it is responding back. If it is, you will recieve a package back along with the response time of that device. If you recieve nothing back, check to make sure your device is on.                                     
                                                                                                                                           
You can do the same thing with your network. Depending on your region, the format of your network will be 192.168.1.x. If it is not, use whatever format your region uses. 
                                                                                                                                          
**Let's try it out!**                                                                                                                       
The command is just like before:
```bash
~$ ping 192.168.1.1
```
![network](https://user-images.githubusercontent.com/62024377/111916494-91eacb80-8a51-11eb-9600-525e7cd55867.png)                                                                                                          
As you can see, my network is working. Presumably, yours is too. I will assume that your network has space allocated
for a maximum of 256 hosts. Not all of them will be used, the majority probably are not. So, if we wanted 
to see which IP addresses are being used we could ping all 256 possible addresses one by one, but that is very time consuming.
A much better way to do this is to use Nmap. That is one of its main uses afterall! 
                                                                                                                                         
**To do that, use the command below:**                                                                                                 
```bash
~$ nmap -sP 192.168.1.0/24
```
**The 0/24 at the end of the IP Address indicates all 256 possible addresses to scan** 
                                                                                                                                                            
![network-map](https://user-images.githubusercontent.com/62024377/111916839-41746d80-8a53-11eb-97ce-99622979f406.png)                                             
                                                                                                                                                                 
The -sP flag tells Nmap to scan for all active hosts, but not to scan for ports. Thus, you get a list of all of the devices that are active on your network.
Mine currently has 4 hosts active.
This is called a subnet of a network. 
 
### Finding more specific information
 
You discovered which hosts are on your network. What else can you find out about them? 
                                                                                                                                         
**Let's figure out what Operating System they are using!**
                                                                                                                                         
To do this, follow the command:                                               
```bash
~$ sudo nmap -O <devices IP Address>
```

![operatingsystem](https://user-images.githubusercontent.com/62024377/111917439-64ece780-8a56-11eb-8bfe-e36952b8a8cb.png)                                                             
Oh no! That didn't work! Why? Sometimes, a device will be live but is configured not to respond to pings. Nmap, by default, tries to ping the device 
and when it doesn't recieve a response back you get the problem as noted above. Not to worry! Nmap already gives us the solution. So, let's try it out.              
Enter this command:
```bash
~$ sudo nmap -O -Pn <devices IP Address>
```
![OSdetection](https://user-images.githubusercontent.com/62024377/111917720-e4c78180-8a57-11eb-903d-5f9734004699.png)                                                                   
AHA! It works! But why? Since Nmap, by default, tries to ping a device that is configured not to respond back, it doesn't. Thus, Nmap says "Well,
they aren't responding. They must be down, I'm quitting.". By using the -Pn flag, we are telling Nmap that we want to scan the device  regardless of 
whether we get a response back. When it does, Nmap realizes that the host is alive and we get the information we wanted. 
In this case, I discovered that my laptop (identified by the IP address 192.168.1.56) is running on Linux (Ubuntu to be exact). 
What operating system did you get back? 
**Note that the OS detection is not always 100% reliable on Nmap.**                                                                                               

### What if we want to know which devices, if any, are on or are attempting to use the internet?
You can do this with the command:                                                                                                       
```bash
~$ nmap -sT -p 80,443 192.168.1.0/24
```
![portscan](https://user-images.githubusercontent.com/62024377/111922505-88bd2700-8a70-11eb-815a-44c63224a880.png)                                             
The -sT flag uses a 'Three-way handshake' to establish whether a connection exists. What this means is Nmap sends a SYN, the host (if active) sends 
an ACK back, and then Nmap finishes by sending its' own ACK back to secure the connection. In other words, Nmap says "hey, are you listening!", the host replies back with "yeah, what's up?", and Nmap says "nice, you're alive!". This scan, although effective, poses some risks. A configured firewall may catch on to all of these requests and say "hmmm that doesn't seem right..." and can log your activites and may even prevent your scan from completing.                               
**You don't even need the full three-way handshake to determine if a connection exists**                                                                                                                                                                                    
You can use the -sS flag wich is much stealthier, faster and is refered to as a SYN scan.                                                                         
The command is below:
```bash
~$ nmap -sS -p 80,443 192.168.1.0/24
```
It differs from -sT in that Nmap will send a SYN to the host, the host will send back an ACK (just like before) but instead of ackwoledging with another ACK, Nmap will just cut communications. Think of it like walking away from a conversation mid-sentence. The -p flag tells Nmap to scan for particular ports, in this case we scanned for ports 80 and 443 (ports used to communicate over the internet). If these ports are open, then the host is communicating over the internet, if closed then it is not. In the image above, my laptop and my router are communicating over the internet, which makes sense because I'm using my laptop to write this over the internet and my laptop connects to the internet through my router. 

### More with Nmap
So, now you have a basic idea of how to use Nmap to get information such as knowing which devices are connected to a given network, how to obtain more specific information about those devices (like what operating system they are running) and what some common flags are used for in Nmap. This is only the tip of the iceburg with what you can do with this tool, for more information about what to use Nmap for please visit their official site [here](https://nmap.org/).
 
### Legal disclaimer!
Only use Nmap on devices that **YOU** own or have permission from the owner to use Nmap on. Although it is not necessarily illegal to "test" the security of a given network, it is highly suspicious to do so and may get you in legal trouble if you are not the explicit owner. 
 
### Licensing
Nmap is distributed under the terms of the *Nmap Public Source Lincense*. Please refer to their HTML version [here](https://nmap.org/npsl/npsl-annotated.html) or their plain text version [here](https://svn.nmap.org/nmap/LICENSE).
 
### Want to contribute to nmap?
If you feel you have some worthy contributions to Nmap, such as a discovery of a bug or a new probe, check out their website [here](https://nmap.org/book/vscan-community.html) or visit their github [here](https://github.com/nmap/nmap/contribute).
 
