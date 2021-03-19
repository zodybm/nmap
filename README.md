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
*Note that if you are running Kali Linux nmap will be preinstalled.*
#### If your OS is Windows or other
The easiest and safest way is to use a virtual machine, or VM. I highly recommend using [virtualbox](https://www.virtualbox.org/) I highly recommend using *virtualbox*.
It is a free and open-source VM perfectly suited for this task. To install Kali linux on virtualbox please click [here](https://phoenixnap.com/kb/how-to-install-kali-linux-on-virtualbox)
### Using nmap
Now that you have nmap installed, open up the terminal if you haven't already and type in 'nmap'. 
