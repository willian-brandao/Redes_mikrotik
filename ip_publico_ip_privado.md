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
