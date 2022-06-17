# Pi #2 - The Unbound DNS NS1 Setup

These instructions are for the Pi #2 after you already ran the intial set up in the [Start Here section](./Start.md)


When done you can move onto [Testing The DNS Setup](./Testing_setup.md)
<HR/>

### 1. Install Unbound 
log onto PI2 - the one we called NS1 in the previous instructions and start inputting these commands <br/>

$ `sudo apt install unbound -y`

### 2. Edit/Create The 'root.hints' File 
Adding the A record for the PI1-HSD makes unbound look for an authoritative answer from the HSD NS whenever a user calls out to WAN <br/><br/>
The IP for the HSD server you wrote down in the previous step is required here. If you don't have it, go to the HSD server PI#1 and get it.... type:
$ `hostname -I` on that server and write it down. Use it in the next command (we will use 10.10.0.35 in the examples below)

now we can edit/create the root.hints file
<br/>
$   `sudo nano /etc/unbound/root.hints`

Delete any lines already in the file then cut & paste this into the text editor <br/>(change the IP below to your HSD Server's IP)
<br/>
```
;       This file holds the information on root name servers needed to
;       initialize cache of Internet domain name servers
;       (e.g. reference this file in the "cache  .  <file>"
;       configuration file of BIND domain name servers).
;
.       3600000         NS      .
.       3600000         A       10.10.0.35
```

Save and Exit the Editor 

### 3. Edit/Create The 'root.key' File
This file contains the public KSK key for HSD NS and is required for DNSSEC to determine the authenticity of the source domain name. <br/>

$   `sudo nano /var/lib/unbound/root.key`

Delete any lines already in the file and cut & paste this into the text editor<br/> (it's a long key so double check you have it all)
<br/>

```
; autotrust trust anchor file
;;id: . 1
;;last_queried: 1655402534 ;;Thu Jun 16 18:02:14 2022
;;last_success: 1655402534 ;;Thu Jun 16 18:02:14 2022
;;next_probe_time: 1655407511 ;;Thu Jun 16 19:25:11 2022
;;query_failed: 0
;;query_interval: 5400
;;retry_time: 3600
.       9471    IN      DNSKEY  257 3 13 T9cURJ2M/Mz9q6UsZNY+Ospyvj+Uv+tgrrWkLtPQwgU/Xu5Yk0l02Sn5ua2xAQfEYIzRO6v5iA+BejMeEwNP4Q== ;{id = 35215 (ksk), size = 256b} >

```
Save and Exit the Editor

### 4. Edit/Create The Unbound Config File
This file contains all the options Unbound will use on startup <br/>
The config file listed below is for an authoritative, validating, recursive caching DNS with Adblocking <br/>

The config file I provided is well documented  <br/>
Under the local-zone: this is just an example of an internal LAN structure.  Change it to fit your LAN. <br/>Under the AdBlocking Section you can redirect any domains your want, or create a separate blacklist file and call out to it. <br/>
<br/>now let's edit/create the file

$   `sudo nano  /etc/unbound/unbound.conf` 

Delete any lines already in the file and cut & paste this into the text editor

[cut and paste this config file into the text editor <---click here](./configs/myunbound.conf)	

Save and Exit the Editor <br/> 
Quickly Check the config file for errors before starting Unbound Services


$ `unbound-checkconf /etc/unbound/unbound.conf`



### 5. Start/Re-Start Unbound And Test It
Start the Unbound service<br/>

$   `sudo service unbound restart`

There should be no output on the screen when the Unbound service starts healthy.

Test to see if the service is running

$ `systemctl status unbound.service`

 <hr/>
  <H3> That's it for the Unbound set up on Pi #2 </h3>
  This server is complete 
  <hr/>
<br/>
<h3>

>>move onto <br/>
  [Testing The DNS Setup](./Testing_setup.md) <br/>
    The Introduction <br/>
 [READ ME](./README.md)<br/>
  but  always start here <br/>
   [Start Here - Common for both Pi's](./Start.md)
</h3>

<br/><br/>

