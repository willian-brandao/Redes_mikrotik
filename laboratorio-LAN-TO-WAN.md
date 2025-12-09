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
   * Reservar IP no DHCP da CPE 


