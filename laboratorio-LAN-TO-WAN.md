# Configurando a rede LAN do roteador Mikrotik

## -> Ativar o romon (Router Management Overlay Network) recurso que permite acessar e administrar o equipamento da mikrotik
``  
/tool/romon/set enabled=yes secrets=123mudar 
``
## -> Atribuição de IP à interface LAN do roteador e nomear o pool de IPs
``
 /ip address add address=192.168.1.1/24 interface=LAN
 /ip pool name=LAN-POOL ranges=192.168.1.1-192.168.1.254
``
##  -> Configuração de dhcp server no roteador
    
    /ip dhcp-server network add address=192.168.1.0/24 gateway=192.168.1.1 dns-server=8.8.8.8,8.8.4.4
    
    /ip dhcp-server interface=LAN address-pool=lan-pool disabled=no
## -> Renomear roteador
``
    /system identity set name=004-ROTEADOR
``
## -> Renomear interfaces
``
    /interface ethernet set ether2 name=LAN
``

# Configurando CPE Mikrotik para se conectar a rede da empresa a rede de um ISP

A CPE pode estar em dois modos:
1. Bridge - Todas cconfigurações chegaam até o equipamento próprio e as configurações terão que ser realizadas pelo próprio usuário.
   * DHCP
   * PPPoE
   * IP FIXO
2. CPE em modo de Roteamento - Informações são de controle do ISP
   * Colocar IP fixo no equipamento habilitando a dmz para que ele tenha acesso a rede externa.
   * Reservar IP no DHCP da CPE.

## Ativar o modo roteavel  do roteador
Devido a regra já está criada, nesse caso para a ativação usa-se apenas o identificador da regra.
<img width="901" height="219" alt="image" src="https://github.com/user-attachments/assets/dcd06590-78f6-44d0-a841-bd6a002d67a3" />


``
/system/script/ run "ATIVAR_MODO_ROTEADO"
``

### Mudanças realizadas:
1. Ativação do PPPoE Client
 <img width="1239" height="385" alt="image" src="https://github.com/user-attachments/assets/b46d9c8f-388e-414c-9607-b03d26acfcf4" />

2. Desativação do DHCP Server
 <img width="818" height="181" alt="image" src="https://github.com/user-attachments/assets/3110f802-0185-4917-9500-d8149fa414a0" />

3. portas da bridge desativadas
<img width="1074" height="155" alt="image" src="https://github.com/user-attachments/assets/8f0fbb5e-d262-4c82-a849-e764d4bb27c9" />



