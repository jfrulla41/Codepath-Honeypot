# Codepath-Honeypot
Unit 10 and 11 of the Codepath course. Created honeypot and collected data.

## Overview and Setup
I used Google Cloud Platform to create the MHN Admin VM and MHN Honeypot VMs by following the Codepath
Honeypot Project Assignment instructions fairly closely.

I started by setting up firewall rules for the MHN Admin machine with TCP ports 80, 3000, and 10000.
I then used the `gcloud compute instances create` command to create a VM on the Google Cloud Platform.

I used an updated version of Ubuntu, `--image "ubuntu-1404-trusty-v20190321`, and I changed the
machine type from `f1-micro` to `g1-small` in order to deal with the RAM issues I had from installing
the mhn-admin software the first time I attempted this.

The MHN Admin VM was created with the device name `mhn-admin` and I followed instructions to the letter for
installing the mhn admin software on it.
There was a few issues regarding mongodb and some of the python source code. The python code needed to be edited
to import the correct libraries. The original code had the incorrect case for the library names.
Once the services were up and running correctly, I connected to the assigned IP address and navigated to 
the Deploy tab

I deployed Dionaea with HTTP on a new VM named `mhn-honeypot-1`. This new VM used all the same instance values
as the MHN Admin VM did, but the honeypot VM had different firewall rules so that traffic would be allowed on all ports.

I also deployed the following additional virtual honeypots:

Shockpot on `mhn-honeypot-2`
ElasticHoney on `mhn-honeypot-3`
P0f on `mhn-honeypot-4`
Amun on `mhn-honeypot-5`

These honeypot deployments were selected arbitrarily at random just to get some variety.

Dionaea ran for a week by itsself and the rest of them were added a few days before this write up.
Data on all was collected over at least a 24-hour period prior to this writeup.

## Demonstration
##### Here is the results from collecting data over a 24-hour period

#### Overview
![](mhn.png)

#### Sensors Deployed
![](mhn-sensors.png)

#### Attacks Example
![](mhn-attks.png)

__The export of the raw data from mongodb to json is available in this repository as session.json__

## Conclusions

The most frequently attacked port is port 445.
port 445 is the preferred port for carrying Windows file sharing services AKA Samba over IP.
This port is frequently attacked, because it allows hackers to potentially gain remote access to the contents
of the hard disk directories and drives. Access to via remote Samba allows attackers to upload and run any software
or data of their choosing without the computer owner being aware. Not only is this port insecure, but it is also exposed
by default and is installed on every Windows system since Windows 2000.

The next most frequently attacked ports are ports 80, 8088, and 8080.
This is no surprise, because ports 80 and 8080 are for http, and are incredibly common ports to have open to the internet.
Sometimes these ports can be exploited, depending on the server software listening for connections.

The next most frequently attacked ports are ports 22 and 23.
This is also no surprise, because ports 22 and 23 are ssh and telnet, respectively. These services are for remote
console connections. With successful exploits to ssh and telnet services, the attacker is able to remotely access
the console or shell for target systems. This allows them to perform virtually any action on the target machines.



