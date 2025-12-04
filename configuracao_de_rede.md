# Configurar WAN no Mikrotik

## 1. Ativa o DHCP Client na interface eth1

``
/ip 
dhcp-client
add interface=ether1 disable=no
``

## 1.1. Confirmar as configurações

``
/ip address print
``

## 1.2 Criar NAT para liberar internet para LAN
``
/ip firewall nat
add chain=srcnat out-interface=ether1 action=masquerade
``

## 1.3 Configurar IP da LAN
``
/ip address add adress=192.168.10.1/24 interface=ether2
``

## 1.4 Ativar o DHCP Server para sua LAN
``
/ip  pool add name=pool1 ranges=192.168.10.2-192.168.10.254
/ip dhcp-server
add name=dhcp1 interface=ether2 address-pool=pool1 disable=no
/ip dhcp-server network
add gateway=192.168.10.1 address=192.168.10.0/24
``

