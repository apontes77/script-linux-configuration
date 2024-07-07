## Encaminhamento de Porta

O encaminhamento de porta permite que você crie um túnel virtual que conecta o ambiente de rede do WSL ao ambiente de rede do Windows. Dessa forma, você "mapeia" a porta 8080 do WSL para uma porta específica no Windows, tornando a aplicação Java acessível no navegador da sua máquina.

### Passos:

1. Identifique o endereço IP do WSL: Abra o prompt de comando do WSL e digite o comando ip addr. Procure pela interface de rede com nome eth0 ou wlan0. O endereço IP será exibido ao lado da interface. Anote-o.

2. Crie a regra de encaminhamento de porta no WSL: Utilize o seguinte comando no prompt de comando do WSL, substituindo <endereço_IP_WSL> pelo endereço IP que você anotou na etapa 1:

`sudo iptables -t nat -A PREROUTING -i eth0 -p tcp --dport 8080 -j DNAT --to-destination <endereço_IP_WSL>:8080`

3. Encaminhe a porta no Windows: Abra o prompt de comando do Windows como administrador e execute o seguinte comando, substituindo <número_porta_Windows> por uma porta não utilizada no seu sistema (por exemplo, 8081):

`netsh int ip portproxy add v4to4 listenport=<número_porta_Windows> connectaddress=<endereço_IP_WSL> connectport=8080`

Acesse a aplicação no navegador: No navegador da sua máquina Windows, acesse o endereço http://localhost:<número_porta_Windows>. A aplicação Java em execução no WSL deve ser exibida!