Support for Cisco Small Business in RANCID
==========================================

Introduction
------------

I like using RANCID [1] to manage a backup of all the network devices of a 
network: switches, routers, firewalls,... However, RANCID lacks of "official"
support for Cisco SG300 series switches. These switches form part of 
Cisco's Small Business serie and although they are not based on Cisco IOS,
they are provided with a CLI with some similar commands to Cisco IOS's ones.

By Googling I found how to backup with RANCID a Cisco SRW2008P switch [2]. I
have modified those files to support not only a SRW switch but also a SG300
switch.

This files add support for:
- SRW series switches
- SG series switches
- SFE series switches

Installation
------------

- Download src/csblogin and src/csbrancid files and put them in the 
  RANCID's PATH (in my case, /opt/rancid/bin). Don't forget to give them 
  execution permissions.
- Edit rancid-fe file located in the RANCID's PATH (in my case,
  /opt/rancid/bin/rancid-fe) and insert a new item in the %vendortable
  dictionary:

		'cisco-sb'        => 'csbrancid',

Usage
-----

- Insert the device to backup in the router.db file:

		test.example.com:cisco-sb:up:

- Modify your .cloginrc file:

		add user test.example.com        {user}
		add password test.example.com     {password}
		add autoenable test.example.com    1
		add method test.example.com        ssh
		add userprompt test.example.com  {"User Name:"}

- Enjoy it!


Christian Pinedo

[1] http://www.cisco.com/en/US/products/ps10898/index.html  
[2] http://www.mork.no/%7Ebjorn/srw2008/  
