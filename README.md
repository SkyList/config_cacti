## __srv-apps__ - Servidor que será monitorado
Para monitorar este host, é necessário instalar o SNMP (protocolo de monitoramento) que permitirá ao Cacti capturar os dados desta máquina

1. Instalar o snmp
   ```bash 
   $apt install snmp snmpd
   ```

Após instalar é necessário configurar o serviço snmpd para permitir a captura de dados remotamente via UDP. Para isso é necessário editar o arquivo `/etc/snmp/snmpd.conf`

2. Configurar o snmpd
   ```bash
	$vim /etc/snmp/snmpd.conf
	$systemctl restart nmpd
	```
	> neste arquivo sera necessario comentar a linha 15, `agentAddress udp:127.0.0.1:161` e descomentar a linha 17, `agentAddress udp:161, udp6:[::1]:161`.

	> É necessário adicionar a linha referente ao método de acesso remoto entre a linha 50 e 60, esta linha deverá seguir esta estrutura `rocommunity public <endereço IP de rede com mask>`.


3. Para verificar se o serviço está funcionando pode-se verificar o status do serviço e verificar se a socket udp (161) está aberto.

	```bash
	$systemctl status snmpd
	$netstat -nlup
	```
__________________________________________________________________
## ___monitor-unitins___ - Servidor contendo programa de monitoramento Cacti.

### Configurando host no Cacti
Primeiramente é necessário adicionar o host que será monitorado.
Na tela inicial já é apresentado o botão **Create devices**, clicando nele, o usuário será direcionado à página referente aos hosts.

![cacti_1](i1.jpg)

Nesta página existe um botão **Add** localizado na extremidade direita da barra azul que vai redirecionar o usuário à página para adicionar um novo host.

![cacti_2](i2.jpg)

Nesta tela basta preencher os dados do servidor **srv-apps**

![cacti_3](i3.jpg)

### Configurando os gráficos
