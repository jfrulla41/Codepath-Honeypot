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
