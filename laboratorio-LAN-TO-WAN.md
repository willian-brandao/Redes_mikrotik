# Configurando a rede LAN


# Ativar o romon (Router Management Overlay Network) recurso que permite acessar e administrar o equipamento da mikrotik
``  
/tool/romon/set enabled=yes secrets=123mudar 
``
# atribuição de IP à interface LAN do roteador e nomear o pool de IPs
``
 /ip address add address=192.168.1.1/24 interface=LAN
 /ip pool name=LAN-POOL ranges=192.168.1.1-192.168.1.254
``
# configuração de dhcp server no roteador
    
    /ip dhcp-server network add address=192.168.1.0/24 gateway=192.168.1.1 dns-server=8.8.8.8,8.8.4.4
    
    /ip dhcp-server interface=LAN address-pool=lan-pool disabled=no
# renomear roteador
``
    /system identity set name=004-ROTEADOR
``
# renomear interfaces
``
    /interface ethernet set ether2 name=LAN
``
