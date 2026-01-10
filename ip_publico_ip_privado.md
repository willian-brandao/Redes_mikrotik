# IP Público x IP de CGNAT

<img width="1197" height="735" alt="image" src="https://github.com/user-attachments/assets/41b0c3dd-bfa6-4ba8-b2e3-fa64ed579dfe" />

## Índice
* CPE em Bridge e IP Público no Mikrotik
* CPE e Bridge e IP de CGNAT no Mikrotik
* CPE Roteada e com IP Público
* CPE Roteada e com IP de CGNAT

##  Troubleshoot para validar se uma porta de um serviço está aberta usando telnet.

1. Habilitar telnet no Windows

   1.1 windows + r

   1.2 digitar appwiz.cpl

   1.3 Ativar ou desaticar recursos do Windows

   1.4 Ativar Client Telnet

2. Testar por meio da  CLI

   2.1 No CMD, digitar telnet

   2.2 Digitar comando: telnet [Endereço IP] [Porta]

3. Testar o Telent no Mikrotik
   3.1 Digitar o comando

   ```bash
       /system/telnet address=192.168.1.254 port=80 
   ```
## Configuração da CPE em Modo Bridge 

### Objetivo

O objetivo deste laboratório é configurar uma CPE em modo bridge para que o roteador mikrotik por meio de usuário PPPoE receba IP público direto do ISP.  Com esse IP público será possível acessar serviços hospedados na rede local de fora da rede. 

1. Ativar o modo bridge da CPE
   A CPE do laboratório possui um script para ativar o modo bridge, nesse caso   somente o script será executado. Acessando a CPE digite o comando:

```
   system/script/run ATIVAR_MODO_BRIDGE
```
Exemplo do script:

```
  name="ATIVAR_MODO_BRIDGE" owner="admin"
     policy=ftp,reboot,read,write,policy,test,password,sniff,sensitive,romon
     dont-require-permissions=no run-count=0 source=
       #ATIVA O MODO BRIDGE
       /interface/bridge/port enable [find]

       /interface/pppoe-client/disable pppoe-cliente

       /ip/dhcp-server/disable dhcp1
```
2. Acessando o roteador e fazer a configuração de PPPoE.
```
/interface pppoe-client add  name=pppoe-client interface=ether1  user=mudei password=123 disabled=no
```

## CPE Roteada e com IP Público 

Primeiramente, é preciso mudar o modo de configuração de CPE que atende o cliente. Para determinado serviços a CPE estava em modo bridge, mas para essa atividade a cpe ficará em modeo roteável. 

no winbox
- system>scripts> "ativar modo roteado"
run script
- Desativar a interface de pppoe client
- Ativar a interface de dhcp de client

 
