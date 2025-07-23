# Credit goes to Helix over at ipfire.org - https://people.ipfire.org/~helix/auto-dnsbl/

## This directory contains test versions of Banish which has been re-written as an add-on for ipblocklist. 
The original version of Banish was an add-on for IPCop V1 but was abandoned by its author Sid McLaurin.

## ***** Banish-001.tar.gz  ******

2022-05-24

This version uses the ipblocklist ipset mechanisms instead of Banish's original 
iptables.

If you are using my original port of Banish to IPFire please backup your 
/var/ipfire/Banish files first and then uninstall Banish.

The original config files are compatible with this new version and can be 
restored.

Installation is the same as ipblocklist.

Get the latest version of banish and copy it to yout /tmp directory on your 
firewall.

    extract the tar file using "tar -xvf banish-xxx.tar.gz -C /" 
     
Regenerate the language cache with "update-lang-cache"
    
# Note:
this add-on will modify ipblocklists sources file by adding an additional source 'BANISH' to the menu.

See: https://github.com/Grantura/Banish-IPFire#readme for original port details.


## ******* Banish-002.tar.gz ********

2022-12-27

# Requirements IPFire 2.27 (x86_64) - Core-Update 170 or later.

## Info:

This version of Banish adds the facility to block on Autonomous System Number 
(ASN) as well as the earlier method of IP Address, CIDR or FQDN. 

Banish-002 uses the location database to derive the ip address associated with 
an ASN and combines these addresses with the other entries in the Banish 
blocklist in an ipset to generate a blocklist for ipblocklist 

This version is compatible with Banish-001 but make sure you backup: 
/var/ipfire/Banish/Banish_config 
/var/ipfire/ipblocklist/sources 
if upgrading from Banish-001

As extraction of ip addresses from the location database is slow they are cached in 
/var/ipfire/Banish/cache and the location database is checked hourly for updates 
and if changed the banish blocklist is updated with any new entries. This 
usually occurs once per week.

The ASN of a network can be found from a whois command or by interrogating the 
location database from the command line with "location lookup ip-address".

The ASN can then be entered into 'Banished Resource' window (as ASxxxxx) along with 
any remark if required and will be entered into to the Banish blocklist with the 
'add button'. The entry will become active on the next IP-blocklist update which 
is run every 15 minutes. 

## Banish-002 will add the following new files to IPfire:

/srv/web/ipfire/cgi-bin/BanishGeo.cgi

/srv/web/ipfire/cgi-bin/logs.cgi/Banishlog.dat /srv/web/ipfire/html/banish_list

/usr/local/bin/Banish_Sort.pl /var/ipfire/Banish/Banish_config

/var/ipfire/Banish/Banish-functions.pl /var/ipfire/Banish/Banish_settings

/var/ipfire/Banish/ip_Banishlist /var/ipfire/addon-lang/Banish.de.pl

/var/ipfire/addon-lang/Banish.en.pl /var/ipfire/addon-lang/Banish.es.pl

/var/ipfire/addon-lang/Banish.fr.pl /var/ipfire/addon-lang/Banish.it.pl

/var/ipfire/addon-lang/Banish.nl.pl /var/ipfire/addon-lang/Banish.pt.pl

/var/ipfire/menu.d/EX-Banishlog.menu /var/ipfire/menu.d/EX-banish.menu

## These IPFire files are modified:

/srv/web/ipfire/cgi-bin/logs.cgi/log.dat 
/var/ipfire/ipblocklist/sources

# To install.. 
Download Banish-002.tar.gz to /tmp

Extract the tar file using "tar -xvf banish-xxx.tar.gz -C /"

Regenerate the language cache with "update-lang-cache"

## Note 1:
this is an addon for IP Address Blocklists and the Banish blocklist 
needs to be enabled in the IP Address Blocklists menu and the firewall ruleset 
reloaded with the "Apply Changes" button in the "Firewall Rules" menu.

# Note 2: 
Banish entries are are updated every 15 minutes when IP-based blocking 
is updated.
