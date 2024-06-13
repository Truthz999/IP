# IP
**Nos da la IP Privada y Publica del dispositivo**


# Code

```python

# Importamos los modulos que usaremos

import platform
import subprocess
import re

def ip_public():
     publica = subprocess.getoutput("nslookup myip.opendns.com resolver1.opendns.com")
     er = "\\b(?:(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\\.){3}(?:25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\\b"
     publica= re.findall(er, publica)
     
     return publica[1]

def ip_priv():
     if platform.system() == 'Windows':
         privada = subprocess.getoutput("""for /f "tokens=2 delims=[]" %a in ('ping -n 1 -4 "%computername%"') do @echo %a""")        
        
     else:
         privada = subprocess.getoutput("ifconfig | grep 'inet ' | grep -Fv 127.0.0.1 | awk '{print $2}'")
    
     return  privada
 
print("IP Privada : " , ip_priv())
print("IP Publica : " , ip_public())

```

