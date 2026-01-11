## CPE Roteada e com IP Público 

Primeiramente, é preciso mudar o modo de configuração de CPE que atende o cliente. Para determinado serviços a CPE estava em modo bridge, mas para essa atividade a cpe ficará em modeo roteável. 

NA CPE DO CLIENTE

no winbox
- system>scripts> "ativar modo roteado"
run script
- Desativar a interface de pppoe client
- Ativar a interface de dhcp de client
---
Validar se o usuario está com IP público
- interfaces > interface de conexão 
- status  > local address

IP Público da CPE:  200.10.1.153
---
Criar regra para que os serviços sejam acessados de fora da rede

IP > Firewall > NAT 

General 
  - chain: dstnat
  - protocol: tcp
  - dst port: 8291
  - in interface: pppoe-cliente
Action
  - action: dst-nat
  - to addresses: endereço da rede local

---
Criar Redirecionamento dentro da CPE e dentro do roteador para poder acessar o 
servidor web que está hospedado dentro da rede local de fora da rede.

---

Criar a dmz no mikrotik

Dentro da regra de NAT no firewall não especificar porta apenas a chain, interface, action 
e IP.

Feito isso todos os protocolos estarão direcionados ao IP do servidor
- dstnat
- interface : pppoe
- to addresses: 192.168.15.254



