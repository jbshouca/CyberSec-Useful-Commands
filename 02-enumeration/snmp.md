# SNMP (161/udp)

```bash
onesixtyone -c /usr/share/seclists/Discovery/SNMP/snmp.txt TARGET   # brute community strings
snmpwalk -v2c -c public TARGET                                       # full walk
snmp-check TARGET -c public                                          # human-readable

# Useful OIDs
snmpwalk -v2c -c public TARGET 1.3.6.1.2.1.1.5.0          # hostname
snmpwalk -v2c -c public TARGET 1.3.6.1.2.1.25.4.2.1.2     # running processes
snmpwalk -v2c -c public TARGET 1.3.6.1.2.1.25.6.3.1.2     # installed software
snmpwalk -v2c -c public TARGET 1.3.6.1.2.1.4.20.1.1       # IP addresses
```
