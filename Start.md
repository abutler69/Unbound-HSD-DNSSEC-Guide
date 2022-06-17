## Initial Pi Set Up (common for both Pi's)

Do this set up on BOTH your raspberry Pi's. When your finished - continue to [PI1-HSD Setup](./PI1-HSD_setup.md) before the [PI2-Unbound Setup](./PI2-Unbound_setup.md) 

<hr/>

### 1. Install Ubuntu 64bit Server 20.04 LTS for ARM64 From The Raspberry Pi Imager Onto Both Pi's (https://www.raspberrypi.com/software/)
Insert the SSD card that you just cloned from the Pi Imager and plug your PI into your LAN then
turn it on.<br/> Log in as user: ubuntu password: ubuntu <br/> You will be prompted to change the default password to something new (do not change the user name) <br/> You have to reboot now after changing the password <br/>  Input this command (commands are highlighted - don't copy the $):<br/>

$ `sudo reboot now`

### 2. Update The Installed Software, Free Up Space From Updates Then Reboot System:

After the system reboots, login with your new password then input these commands to update the software


  $ `sudo apt update`

  $ `sudo apt upgrade`

  $ `sudo apt autoremove`

  $ `sudo reboot now`

You can now SSH into the server if you are inclined, otherwise stay at the terminal and continue.
### 3. Change The Computer 'host name'
  The file '/etc/hostname' contains the current hostname.  Replace it with your new one: hsd for Pi1 & ns1 for Pi2

  $ `sudo nano /etc/hostname`

This is what the file should look like after making changes (you can cut and paste it into your file) <br/> reminder make Pi1 hsd and Pi2 make it ns1

  ```
  hsd

  ```
    
  Save the file & exit the editor

The file '/etc/hosts' maps hostnames to IP addresses. <br/> 

  $ `sudo nano /etc/hosts`
  

Copy and paste below into the editor for Pi1 and change the line 127.0.1.1 hsd to 127.0.1.1 ns1 for Pi2

```
127.0.0.1 localhost
127.0.1.1 hsd

# The following lines are desirable for IPv6 capable hosts
::1 ip6-localhost ip6-loopback
fe00::0 ip6-localnet
ff00::0 ip6-mcastprefix
ff02::1 ip6-allnodes
ff02::2 ip6-allrouters
ff02::3 ip6-allhosts
```

Save the file & exit the editor <br/>
Reboot the system

  $ `sudo reboot now`


 ### 4. Install Core Essentials On Both Pi's
These are not all required but they are very useful to have on the servers


#### install net tools:
  $ `sudo apt-get install -y net-tools`

#### install node.js 14.15.5 and NPM:
  $ ` curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -`

  $ `sudo apt-get install -y nodejs`

  $ ` sudo apt-get install alsa-utils`

#### install build essentials (includes GCC, G++ and MAKE):
  $ `sudo apt-get install build-essential`



#### install node-gyp:
  $ `sudo npm install -g node-gyp`

#### install PM2
  $ `sudo npm install -g pm2`

make PM2 startup on reboot

  $ `sudo pm2 startup`



### 5. Free Up Port #53 From systemd-resolve So Unbound Can Use It

To see if port 53 is in use on your system, use:

  $ `sudo lsof -i :53`
  
  In case you don't get any output, it means that port 53 is not in use.

#### 5a. edit '/etc/systemd/resolved.conf with a text editor (as root)



Uncomment (remove # from the front of the line) the DNS= line and the DNSStubListener= line.<br/> Next, change the DNS= value to 127.0.0.1 and also change the DNSStubListener= value from yes to no.

  $ `sudo nano /etc/systemd/resolved.conf`

This is what the file should look like after making changes (you can cut and paste it into your file)
```
[Resolve]	
DNS=127.0.0.1	
#FallbackDNS=	
#Domains=		
#LLMNR=no		
#MulticastDNS=no	
#DNSSEC=no
#DNSOverTLS=no		
#Cache=no		
DNSStubListener=no		
#ReadEtcHosts=yes
```

Save the file & exit the editor

#### 5b. create a symbolic link for '/run/systemd/resolve/resolv.conf' with '/etc/resolv.conf as the destination':

  $ `sudo ln -sf /run/systemd/resolve/resolv.conf /etc/resolv.conf`

#### reboot the  system
  
  $  `sudo reboot now`

Port 53 should now be free on your Ubuntu system, and you shouldn't be getting errors like "listen tcp 127.0.0.1:53: bind: address already in use" anymore.  <br/>

#### test - you should get no output

  $ `sudo lsof -i :53`

#### 6. Get Each Of The Rasp Pi IP#'s And Write Them Down For The Next Step

$ `hostname -I` <br/>

Log into your Router and make these IP's static for the NS1 and HSD servers

  <hr/>
  <H3> That's it for the initial set up of both Pi's </h3>
  <hr/>
<br/>

<h3>

>>move onto <br/>
  [PI1-HSD Full Node Setup](./PI1-HSD_setup.md) <br/>but  always start here <br/>
  [Start Here - Common for both Pi's](./Start.md)
  <br/>
  The Introduction <br/>
 [READ ME](./README.md)
</h3>

<br/><br/>

  ##  NOTE:
  Undoing changes to resolv.conf and port 53<br/>

1. Start by editing '/etc/systemd/resolved.conf' with a text editor (as root), e.g. open it with Nano console text editor:		
		
  $ `sudo nano /etc/systemd/resolved.conf`
		
Comment out (add # in front of the line) DNS= and DNSStubListener=no <br/> 

save the file.
		
2. Remove the /etc/resolv.conf symbolic link:		
		
  $ `sudo rm /etc/resolv.conf`
		
3. Reboot your system.		

  $ `sudo reboot now`
