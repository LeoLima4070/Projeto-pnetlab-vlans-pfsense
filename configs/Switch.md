## Configuração das VLANs no Switch

### VLAN 10 – Financeiro

Switch> enable
Switch# configure terminal

Switch(config)# vlan 10
Switch(config-vlan)# name Financeiro
Switch(config-vlan)# exit

Switch(config)# interface e0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
Switch(config-if)# exit


### VLAN 20 – TI

Switch(config)# vlan 20
Switch(config-vlan)# name TI
Switch(config-vlan)# exit

Switch(config)# int e0/2
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 20
Switch(config-if)# exit

## Configuração de Porta Trunk

A porta trunk é responsável por transportar múltiplas VLANs entre o switch e o pfSense (ou outro switch).

### Exemplo de configuração (porta conectada ao pfSense)


## Configuração de Porta Trunk (802.1Q)

A porta trunk utiliza o padrão **IEEE 802.1Q (dot1q)** para transportar múltiplas VLANs pela mesma interface.

### Exemplo de configuração


Switch> enable
Switch# configure terminal

Switch(config)# interface e0/0
Switch(config-if)# switchport trunk encapsulation dot1q
Switch(config-if)# switchport mode trunk
Switch(config-if)# switchport trunk allowed vlan 10,20
Switch(config-if)# no shutdown
Switch(config-if)# exit