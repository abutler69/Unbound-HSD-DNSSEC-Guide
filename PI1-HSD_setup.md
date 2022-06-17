# Pi #1 - The HSD full Node Authoritative NS Setup

These instructions are for the Pi #1 after you already ran the initial set up in the [Start Here section](./Start.md)


When done you can move onto [PI2-Unbound Setup](./PI2-Unbound_setup.md)
<HR/>

### 1. Install Libunbound/HSD 
HSD includes native bindings to libunbound <br/>-- we will make use of this, by installing libunound  on your system before installing HSD <br/><br/>
log onto PI2 - the one we called HSD in the previous instructions and start inputting these commands

$   `sudo apt install libunbound-dev`

$   `git clone https://github.com/handshake-org/hsd`

$ `cd hsd`

$ `npm i`

### 2. install the HSD-CLI client globally

$ `sudo npm install -g hs-client`


### 3. Start Up The HSD Node with PM2



The IP for the HSD server you wrote down in the previous step is required here. If you don't have it, go to the HSD server PI#1 (the server your on now) and get it.... type:
$ `hostname -I` on that server and write it down. Use it in the next command (we will use 10.10.0.35 in the examples below)

$   `sudo pm2 start ./bin/hsd -- --ns-host=10.10.0.35 --ns-port=53`

Save the PM2 project to restart the HSD node on power failure or on a reboot

$ `sudo pm2 save`

Monitor the HSD NODE with the PM2 GUI

$   `sudo pm2 monit`

If you exit the PM2 monit with 'ctrl-c' the HSD node will still be running in the background, and continue to run even on a reboot, unless you do the steps below to shut down the project.  just use `sudo pm2 monit` to view the node again

To stop the HSD node on the PM2 project

$   `sudo pm2 del hsd`

$   `sudo pm2 save --force`

use $ `pm2 --help` for more commands 

<br/>

The HSD full node can take awhile to download so be patient.<br/>  We can move onto setting up Unbound on NS1 (Pi2)<br/>
To check what the block height of the chain your at, use the CLI command on the HSD server

  $ ` hsd-cli info`


 <hr/>
  <H3> That's it for the HSD set up on Pi #1 </h3>
  This server is complete 
  <hr/>
<br/>
<h3>

>>move onto <br/>
 [PI2-Unbound DNS Setup](./PI2-Unbound_setup.md) <br/>but  always start here <br/>
 [Start Here - Common for both Pi's](./Start.md)
 <br/>The Introduction <br/>
 [READ ME](./README.md)
  
</h3>



