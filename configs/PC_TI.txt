## Teste de DHCP – VLAN 20 (TI)

O host da VLAN 20 (TI) obteve endereço IP automaticamente via DHCP configurado no pfSense.

### Comando executado no VPCS

PC_TI> ip dhcp


### Resultado

DDORA IP 192.168.20.2/24 GW 192.168.20.1


### Explicação
- O pfSense está atuando como servidor DHCP para a VLAN 20  
- O host recebeu:
  - IP: 192.168.20.2  
  - Gateway: 192.168.20.1 (interface VLAN no pfSense)  
- Isso confirma que:
  - A VLAN 20 está funcionando corretamente  
  - O DHCP está configurado corretamente para o setor de TI  
  - A segmentação entre as redes está operacional  

  ## Testes de Conectividade – VLAN 20 (TI)

Foram realizados testes de conectividade a partir de um host da VLAN 20 para validar acesso à rede interna e externa.

---

### Teste 1 – Conectividade com a Internet (IP público)

PC_TI> ping 8.8.8.8

84 bytes from 8.8.8.8 icmp_seq=1 ttl=110 time=60.080 ms
84 bytes from 8.8.8.8 icmp_seq=2 ttl=110 time=66.018 ms
84 bytes from 8.8.8.8 icmp_seq=3 ttl=110 time=69.465 ms
84 bytes from 8.8.8.8 icmp_seq=4 ttl=110 time=57.667 ms


✅ Resultado: Conectividade com a Internet funcionando corretamente

---

### Teste 2 – Resolução de DNS

PC_TI> ping www.google.com

www.google.com
 resolved to 142.251.153.119

84 bytes from 142.251.153.119 icmp_seq=1 ttl=110 time=62.631 ms
84 bytes from 142.251.153.119 icmp_seq=2 ttl=110 time=60.613 ms
84 bytes from 142.251.153.119 icmp_seq=3 ttl=110 time=62.255 ms
84 bytes from 142.251.153.119 icmp_seq=4 ttl=110 time=59.663 ms


✅ Resultado: DNS funcionando corretamente

---

### Teste 3 – Comunicação entre VLANs

PC_TI> ping 192.168.10.2

84 bytes from 192.168.10.2 icmp_seq=1 ttl=63 time=10.444 ms
84 bytes from 192.168.10.2 icmp_seq=2 ttl=63 time=31.128 ms
84 bytes from 192.168.10.2 icmp_seq=3 ttl=63 time=28.615 ms
84 bytes from 192.168.10.2 icmp_seq=4 ttl=63 time=3.834 ms


✅ Resultado: Comunicação entre VLAN 20 (TI) e VLAN 10 (Financeiro) permitida

---

### Observações
- A VLAN 20 possui acesso completo à Internet (NAT e WAN funcionando)  
- A resolução de nomes (DNS) está operacional  
- A comunicação entre VLANs está liberada pelas regras de firewall  