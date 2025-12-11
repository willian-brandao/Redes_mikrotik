# Configurando a rede LAN do roteador Mikrotik

## -> Ativar o romon (Router Management Overlay Network) recurso que permite acessar e administrar o equipamento da mikrotik
```bash  
/tool/romon/set enabled=yes secrets=123mudar 
```
## -> Atribuição de IP à interface LAN do roteador e nomear o pool de IPs
```bash
 /ip address add address=192.168.1.1/24 interface=LAN
 /ip pool name=LAN-POOL ranges=192.168.1.1-192.168.1.254
```
##  -> Configuração de dhcp server no roteador
    
    /ip dhcp-server network add address=192.168.1.0/24 gateway=192.168.1.1 dns-server=8.8.8.8,8.8.4.4
    
    /ip dhcp-server interface=LAN address-pool=lan-pool disabled=no
## -> Renomear roteador
```bash
    /system identity set name=004-ROTEADOR
```
## -> Renomear interfaces
```bash
    /interface ethernet set ether2 name=LAN
```

# Configurando CPE Mikrotik para se conectar a rede da empresa a rede de um ISP

A CPE pode estar em dois modos:
1. Bridge - Todas cconfigurações chegaam até o equipamento próprio e as configurações terão que ser realizadas pelo próprio usuário.
   * DHCP
   * PPPoE
   * IP FIXO
2. CPE em modo de Roteamento - Informações são de controle do ISP
   * Colocar IP fixo no equipamento habilitando a dmz para que ele tenha acesso a rede externa.
   * Reservar IP no DHCP da CPE.

## Ativar o modo roteavel  do CPE do ISP
Devido a regra já está criada, nesse caso para a ativação usa-se apenas o identificador da regra.
<img width="901" height="219" alt="image" src="https://github.com/user-attachments/assets/dcd06590-78f6-44d0-a841-bd6a002d67a3" />


```bash
/system/script/ run "ATIVAR_MODO_ROTEADO"
```

### Mudanças realizadas:
1. Ativação do PPPoE Client
 <img width="1239" height="385" alt="image" src="https://github.com/user-attachments/assets/b46d9c8f-388e-414c-9607-b03d26acfcf4" />

2. Desativação do DHCP Server
 <img width="818" height="181" alt="image" src="https://github.com/user-attachments/assets/3110f802-0185-4917-9500-d8149fa414a0" />

3. portas da bridge desativadas
<img width="1074" height="155" alt="image" src="https://github.com/user-attachments/assets/8f0fbb5e-d262-4c82-a849-e764d4bb27c9" />

### Realizar alteração de modo de dhcp dentro do roteador da empresa


Ativar o dhcp-client

```bash
/ip/dhcp-client/enable [find interface="ether1-link-vivo"]
```

Desativar o dhcp-client

```bash
/ip/dhcp-client/disable [find interface="ether1-link-vivo"]
```

### Habilitar o nat no roteador para que os computadores conectados possam navegar na internet

```bash
/ip/firewall/nat/add chain=srcnat out-interface="ether1-link-vivo" action=masquerade
```
# Ativando o link de Internet na CPE Bridge (dhcp e pppoe client)

Opções de recebimento de informações de rede da WAN

* PPPoE Cliente-> (cgnat/123) ou (publico/123)
* DHCP Cliente
* IP fixo e público sem VLAN
* IP fixo e público com VLAN

Etapas para configuração:

### Ativar o modo bridge na CPE

Essa configuração fará com que a cpe não tenha configurações pre-definidas e todas as configurações sejam administradas apenas pelo roteador que está conectada a CPE.

```bash
/system/script/ run "ATIVAR_MODO_BRIDGE"
```
Dentro do WINBOX:

Acessar System > Scripts > Selecionar Modo Bridge > Run Script

<img width="968" height="472" alt="image" src="https://github.com/user-attachments/assets/56d808c9-693f-4343-9d10-6cabb3cb09da" />

## Configurar a interface PPPoE 

1. Configure o roteador para receber as informações de WAN e de acordo com sua realidade.

1.1. Retirar a configuração de DHCP client do roteador alocado dentro da empresa que contratou o link

```bash
 /ip/dhcp-client/disable [find interface="ether1-1-link-vivo"]
```
1.2 - Criando a interface PPPoE de cliente dentro do roteador

```bash
/interface/pppoe-client/add name="pppoe-client-vivo" interface="ether1-link-vivo" user=USUARIO password=PASSWORD disable=no add-default-route=yes use-peer-dns=yes

name=pppoe-out1 → nome da interface PPPoE criada

interface=ether1 → interface física conectada ao modem

user= → usuário PPPoE fornecido pelo provedor

password= → senha PPPoE

add-default-route=yes → cria a rota default automaticamente

use-peer-dns=yes → recebe DNS do provedor

disabled=no → já ativa ao criar
```

1.3 Importante criar uma regra de firewall para a interface por meio de um NAT

```bash
/ip firewall nat add chain=srcnat out-interface=pppoe-out1 action=masquerade
```

O mesmo procedimento realizado pelo winbox:

1. Definição do nome da interface

<img width="1481" height="845" alt="image" src="https://github.com/user-attachments/assets/280079ea-2e9d-493b-94a2-8b35d5471659" />

1.2 - Configurar usuário e senha (cgnat/123) ou (publico/123)

<img width="501" height="465" alt="image" src="https://github.com/user-attachments/assets/ef2a9f45-8aad-434e-9946-dfee95d57b0a" />




3. Faça a regra de NAT.
4. Coloque IP na interface de LAN.
5. Crie o DHCP Server na interface de LAN.



