# Raspberry Pi Deployment

## Installation
As usual, flash the Rasbian image onto an SD card, add the required ssh and wpa_supplicant files to the boot partition, and power on the device. You will need to find the IP address from your router or NMAP or something.

## Initialization
First, check the group_vars to set the desired static IP, gateway IP, username, etc. You will also need to define the variables for several passwords for your user account, etc. on the Pi, preferably using ansible-vault.

Then, run the following command:

`ansible-playbook init.yml -i '1.2.3.4' --ask-pass`

Use the DHCP assigned address of the Pi here instead of 1.2.3.4. The default password is `raspberry`

At this point, your pi will have only the assigned IP address.

## Role Installation
To install all roles, use the command `ansible-playbook -i inventory.yml playbook.yml`

To exclude certain roles, comment out those lines in `playbook.yml` before running to playbook.

### Access Point
This requires 2 wireless adapters. It will setup one adapter as an access point, using the information in group_vars, then configure the Pi to pass all traffic through a VPN service to the internet. You will need to replace `default.j2` with an OpenVPN config file from your own VPN service in addition to filling in your credentials as variables.

### Speed Test
This will install a simple webpage and script to check the internet bandwidth from the Pi every hour and display a graph of it on a webpage at the Pi's IP address.

### Samba
This will setup a samba server at /srv/share
