# 1. Configurar IP da LAN
/ip address add address=10.0.0.1/24 interface=LAN

# 2. Configurar DHCP
/ip pool add name=lan-pool ranges=10.0.0.100-10.0.0.200
/ip dhcp-server network add address=10.0.0.0/24 gateway=10.0.0.1 dns-server=8.8.8.8,8.8.4.4
/ip dhcp-server add interface=LAN address-pool=lan-pool disabled=no

# 3. Configurar NAT específico para LAN
/ip firewall nat add chain=srcnat src-address=10.0.0.0/24 out-interface=WAN action=masquerade comment="NAT para LAN"

# 4. Regras de firewall
/ip firewall filter add chain=forward src-address=10.0.0.0/24 out-interface=WAN action=accept
/ip firewall filter add chain=forward dst-address=10.0.0.0/24 in-interface=WAN action=accept

# 5. Habilitar forwarding entre interfaces
/ip firewall filter add chain=forward action=fasttrack-connection connection-state=established,related
/ip firewall filter add chain=forward action=accept connection-state=established,related
