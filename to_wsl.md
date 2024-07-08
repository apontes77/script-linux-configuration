## Encaminhamento de Porta

Acesse o Powershell como admin.

Agora, execute estes comandos a seguir.

comando 1: 

`netsh interface portproxy add v4tov4 listenport=19000 listenaddress=0.0.0.0 connectport=19000 connectaddress=$($(wsl hostname -I).Trim()); `


comando 2: 

`New-NetFireWallRule -Profile Private -DisplayName 'MyRule ports for LAN development' -Direction Inbound -LocalPort 19000-19006 -Action Allow -Protocol TCP`


Fórum para referência futura:
 https://superuser.com/questions/1131874/how-to-access-localhost-of-linux-subsystem-from-windows