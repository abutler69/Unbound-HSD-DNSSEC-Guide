<!-- PROJECT LOGO -->
<br />
<p align="center">
  <a href="https://github.com/Cloudchain_Main/guides">
    <img src="images/hnslogo.png" alt="HNSLogo" width="80" height="80">
  </a>

  <h3 align="center">Unbound DNS with HSD full node setup</h3>

  <p align="center">
    Setting up Unbound as an authoritative, recursive, validating DNS server for LAN, ICANN and Handshake names with DNSSEC and AdBlock filtering.
    <br />
    <br />
    ·<a href="https://github.com/abutler69/Unbound-HSD-DNSSEC-Guide/issues">Report Issue</a>·
  </p>
</p>



<!-- TABLE OF CONTENTS -->
<details open="open">
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="./Start.md">Start Here (Intial Pi Setup)</a>
    </li>
        <li>
      <a href="./PI1-HSD_setup.md">PI1-HSD :HSD NS Full Node Setup</a>
    </li>
        <li>
      <a href="./PI2-Unbound_setup.md">PI2-NS1 :Unbound DNS Setup</a>
    </li>
    <li>
      <a href="./Testing_setup.md">Testing The Setup</a>
    </li>
  </ol>
</details>



<!-- ABOUT THE GUIDE -->
## About The Guide

These instruction are for setting up Unbound as an authoritative, recursive, validating DNS server for LAN, ICANN and Handshake names with DNSSEC and AdBlock filtering. <br/> 

This guide assumes you already have a internet connection attached to a router and a knowledge to change the router setting to make the new IP connections static (this will not be covered in this guide). I will explain a lot of the options as I go through the steps, but assuming a layman will try to implement these instructions I will not go to a deep dive.  Mostly I will present all the commands to get your private DNS server working; "copy & paste" style from start to finish, then give you some commands to test the DNS.  If you need to know more about DNS, HSD, Handshake, or any other topic presented, please search for the information with  your friend Dr. Google (knowledge is good).<br/><br/><u>Installed On/With:</u><br/> Raspberry Pi 4 with with 8g RAM & 128G SSD  <br/>
 OS: Ubuntu 64bit Server 20.04 LTS for ARM64 <br/>
 Unbound version: 1.16 <br/>
HSD version: 3.0.1 <br/>
<u>Tested With:</u> <br/>
Microsoft Edge 102.0.1245.39 (Official build) (64-bit) <br/> Firefox 101.0.1 (64-bit) <br/> & Google Chrome 102.0.5005.115 (Official Build) (64-bit)





<!--REQUIREMENTS -->
## Requirements
  - 2 raspberry pi's  
  - 1 will be the Unbound DNS resolving local zone (LAN) names
  - 1  will have Libunbound with HSD authoritative full node NS for resolving WAN names <br />
  (you can combine LAN with WAN but best practice is to keep these separate which this guide will focus on)



<!-- DONATIMG -->
## Support The Guide

If you feel this guide helped you in any way, please consider donating to my HNS wallet <br/>  `hs1qskr248ggtwvyc2zz48xq78c4nqfef2xdwqw09f`  <br/>
Sending coins other than HNS will result in permanent loss. There is no way to recover those funds.  
Please send HNS only, thank you.


<!-- CONTACT -->
## Contact

weedman./ - [pleazu69#9513](https://discordapp.com/users/786316515086827540)

<hr/>
<H3>
<BR/>

>>move onto <br/>
 [Start Here](./Start.md) Initial Pi Set Up (common for both Pi's) </h3>