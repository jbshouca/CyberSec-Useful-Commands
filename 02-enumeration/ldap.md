# LDAP (389/tcp, 636/tcp)

```bash
# Anonymous bind
ldapsearch -x -H ldap://TARGET -b "DC=domain,DC=com"

# With credentials
ldapsearch -x -H ldap://TARGET -D "user@domain.com" -w 'pass' -b "DC=domain,DC=com"

# Users with descriptions (often contain passwords!)
ldapsearch -x -H ldap://TARGET -D "user@domain.com" -w 'pass' -b "DC=domain,DC=com" "(objectClass=user)" sAMAccountName description

# Kerberoasting targets
ldapsearch -x -H ldap://TARGET -D "user@domain.com" -w 'pass' -b "DC=domain,DC=com" "(servicePrincipalName=*)" sAMAccountName servicePrincipalName

# AS-REP Roasting targets
ldapsearch -x -H ldap://TARGET -D "user@domain.com" -w 'pass' -b "DC=domain,DC=com" "(userAccountControl:1.2.840.113556.1.4.803:=4194304)" sAMAccountName
```
