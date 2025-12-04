# 1. Configure o IP na interface LAN:
/ip address add address=10.0.0.1/24 interface=LAN


# 2. Configure o servidor DHCP:
bash
# Criar pool DHCP
/ip pool add name=lan-pool ranges=10.0.0.100-10.0.0.200

# Configurar rede DHCP
/ip dhcp-server network add address=10.0.0.0/24 gateway=10.0.0.1 dns-server=8.8.8.8,8.8.4.4

# Habilitar servidor DHCP na interface LAN
/ip dhcp-server add interface=LAN address-pool=lan-pool disabled=no

# 3. Configure NAT para a LAN:

# Adicionar NAT para tráfego da LAN (se já não tiver)
/ip firewall nat add chain=srcnat src-address=10.0.0.0/24 out-interface=WAN action=masquerade
