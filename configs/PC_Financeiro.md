## Teste de DHCP – VLAN 10 (Financeiro)

O host da VLAN 10 (Financeiro) obteve endereço IP automaticamente via DHCP configurado no pfSense.

### Comando executado no VPCS

VPCS> ip dhcp


### Resultado

DDORA IP 192.168.10.2/24 GW 192.168.10.1


### Explicação
- O pfSense está atuando como servidor DHCP para a VLAN 10  
- O host recebeu:
  - IP: 192.168.10.2  
  - Gateway: 192.168.10.1 (interface VLAN no pfSense)  
- Isso confirma que:
  - A VLAN está funcionando corretamente  
  - A comunicação entre switch e pfSense via trunk está correta  
  - O DHCP está ativo e configurado corretamente para a VLAN


## Testes de Conectividade – VLAN 10 (Financeiro)

Foram realizados testes de conectividade a partir de um host da VLAN 10 para validar acesso à rede interna e externa.

---

### Teste 1 – Conectividade com a Internet (IP público)

VPCS> ping 8.8.8.8

84 bytes from 8.8.8.8 icmp_seq=1 ttl=110 time=62.048 ms
84 bytes from 8.8.8.8 icmp_seq=2 ttl=110 time=62.753 ms
84 bytes from 8.8.8.8 icmp_seq=3 ttl=110 time=62.748 ms
84 bytes from 8.8.8.8 icmp_seq=4 ttl=110 time=63.211 ms


✅ Resultado: Conectividade com a Internet funcionando corretamente (NAT e WAN operacionais)

---

### Teste 2 – Resolução de DNS

VPCS> ping www.google.com

www.google.com
 resolved to 142.251.156.119

84 bytes from 142.251.156.119 icmp_seq=1 ttl=112 time=62.476 ms
84 bytes from 142.251.156.119 icmp_seq=2 ttl=112 time=70.641 ms
84 bytes from 142.251.156.119 icmp_seq=3 ttl=112 time=70.830 ms
84 bytes from 142.251.156.119 icmp_seq=4 ttl=112 time=73.935 ms


✅ Resultado: DNS funcionando corretamente

---

### Teste 3 – Comunicação entre VLANs

VPCS> ping 192.168.20.2

84 bytes from 192.168.20.2 icmp_seq=1 ttl=63 time=6.526 ms
84 bytes from 192.168.20.2 icmp_seq=2 ttl=63 time=9.608 ms
84 bytes from 192.168.20.2 icmp_seq=3 ttl=63 time=54.218 ms
84 bytes from 192.168.20.2 icmp_seq=4 ttl=63 time=66.787 ms


✅ Resultado: Comunicação entre VLAN 10 (Financeiro) e VLAN 20 (TI) permitida pelas regras de firewall

---

### Observações
- O acesso à Internet confirma:
  - NAT funcionando no pfSense  
  - WAN corretamente configurada  
- A comunicação entre VLANs indica que há regras permitindo esse tráfego