# MACL #
Macl.pl is a Perl script that I wrote that allows you to perform lookups of WAP MAC addresses, with the primary source of those MAC addresses being the NetworkList Registry key on Vista/Windows 7 systems.  The script can output the information provided in a Google Earth KML file, or in a Google Maps URL.

The development of this script is described in [this blog post](http://windowsir.blogspot.com/2011/11/tool-update-wifi-geolocation.html).

Please note that this script is not intended for _all_ MAC addresses.  It is commonly known within the DFIR community that Windows systems maintain their own MAC address(es) in specific locations within the Registry; that being said, this script is intended specifically for looking up WAP MAC addresses.

Also, this script requires that you have a WiGLE.net account already in order to perform the lookup, and run the script from an Internet-connected system.  WiGLE.net accounts are free.

## Dependencies ##
This script requires the use of the Net::Wigle Perl module.  If you have the ActiveState Perl distribution installed, you can update your system (must be Internet-connected) using the following command:

```
ppm install net-wigle
```

## Syntax ##
The following is the syntax for the script:

```
MACLookup v.1.0 - CLI MACLookup tool
macl [-f text file] [-m mac_addr] [-u username] [-p password] [-c][-k][-w][-h]
Use Wigle.net to attempt to lookup lat/long for WiFi MAC address(es).
You must have a Wigle.net username & password.

  -f file............parse flat text file containing MAC addresses
  -m mac_addr........look up this MAC address
  -c ................output list in CSV format
  -k ................output in KML format (open in Google Earth)
  -w ................output each point as a Google Maps URL
  -u username........Wigle.net username
  -p password........Wigle.net password
  -h.................Help (print this information)

Ex: C:\>macl.pl -u user -p pass -f macs.txt
    C:\>macl.pl -u user -p pass -m 00:11:22:33:44:55:66 -c

All output goes to STDOUT; use redirection (ie, > or >>) to output to a file.

copyright 2011 Quantum Analytics Research, LLC
```