# Active Directory Enumeration

## Without Credentials

```bash
# Null session
crackmapexec smb DC -u '' -p '' --shares
crackmapexec smb DC -u '' -p '' --users
crackmapexec smb DC -u '' -p '' --rid-brute
crackmapexec smb DC -u '' -p '' --pass-pol

# Kerbrute — find valid usernames (no lockout risk)
kerbrute userenum -d domain.com --dc DC users.txt

# LDAP anonymous
ldapsearch -x -H ldap://DC -b "DC=domain,DC=com"
```

## With Credentials

```bash
# Users, groups, shares
crackmapexec smb DC -u user -p pass --users
crackmapexec smb DC -u user -p pass --groups
crackmapexec smb DC -u user -p pass --shares
crackmapexec smb RANGE -u user -p pass                # check admin access (Pwn3d!)
crackmapexec smb RANGE -u user -p pass --loggedon-users

# BloodHound
bloodhound-python -u user -p pass -d domain.com -ns DC -c all
# Import .json files into BloodHound
# Key queries:
#   "Shortest Path to Domain Admin"
#   "Find All Kerberoastable Users"
#   "Find Principals with DCSync Rights"

# LDAP — users with descriptions (often contain passwords!)
ldapsearch -x -H ldap://DC -D "user@domain.com" -w 'pass' -b "DC=domain,DC=com" "(objectClass=user)" sAMAccountName description
```
