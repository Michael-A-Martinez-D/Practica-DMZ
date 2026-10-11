Video: https://youtu.be/iT1PmYgGK1I 

El proposito de esta topologia es demostrar el funcionamiento de una LAN DMZ y como gestionarla.

## Direccionamiento VLSM 

Matricula: 2025-1410

Red base: `14.10.0.0/16` (últimos 4 dígitos de la matrícula)

| # | Segmento | Red | Máscara | Prefijo | Hosts | Rango útil | Broadcast |
|---|----------|-----|---------|---------|-------|------------|-----------|
| 1 | VLAN 10 (Usuarios) | 14.10.10.0 | 255.255.255.128 | /25 | 126 | 14.10.10.1 - 14.10.10.126 | 14.10.10.127 |
| 2 | VLAN 20 (Admin) | 14.10.20.0 | 255.255.255.128 | /25 | 126 | 14.10.20.1 - 14.10.20.126 | 14.10.20.127 |
| 3 | DMZ (Servidores) | 14.10.30.0 | 255.255.255.240 | /28 | 14 | 14.10.30.1 - 14.10.30.14 | 14.10.30.15 |

### Asignación de IPs

| Dispositivo | Red | IP | Gateway |
|-------------|-----|----|---------|
| FortiGate (VLAN10) | VLAN 10 | 14.10.10.1/25 | - |
| FortiGate (VLAN20) | VLAN 20 | 14.10.20.1/25 | - |
| FortiGate (DMZ) | DMZ | 14.10.30.1/28 | - |
| Usuarios VLAN 10 (DHCP) | VLAN 10 | 14.10.10.10 - 14.10.10.120 | 14.10.10.1 |
| Usuarios VLAN 20 (DHCP) | VLAN 20 | 14.10.20.10 - 14.10.20.120 | 14.10.20.1 |
| Web Server: Sistema de Caja | DMZ | 14.10.30.2/28 | 14.10.30.1 |
| Web Server: Sistema de Inventario | DMZ | 14.10.30.3/28 | 14.10.30.1 |
| DB Server | DMZ | 14.10.30.4/28 | 14.10.30.1 |




## Topología

![Topología](imagenes/Topologia.png)

---

## Configuración en el FortiGate (GUI)

### Interfaces

![Interfaces general](imagenes/GUI%20FORTIGATE/InterfacesGeneral.png)

![VLAN 10](imagenes/GUI%20FORTIGATE/VLAN10.png)

![VLAN 20](imagenes/GUI%20FORTIGATE/VLAN20.jpg)

![LAN DMZ](imagenes/GUI%20FORTIGATE/LANDMZ.jpg)

### DHCP

![DHCP VLAN 10](imagenes/GUI%20FORTIGATE/dhcpvlan10.jpg)

![DHCP VLAN 20](imagenes/GUI%20FORTIGATE/dhcpvlan20.jpg)

![DHCP VLAN 20 (rango)](imagenes/GUI%20FORTIGATE/dhcppvlan20.jpg)

![DHCP PC](imagenes/GUI%20FORTIGATE/dhcppc.jpg)

### Rutas estáticas

![Ruta estática 1](imagenes/GUI%20FORTIGATE/RutaEstatica.jpg)

![Ruta estática 2](imagenes/GUI%20FORTIGATE/RutaEstatica2.jpg)

### Objetos de dirección y FQDN

![Addresses 1](imagenes/GUI%20FORTIGATE/ADDRESSES1.jpg)

![Addresses 2](imagenes/GUI%20FORTIGATE/ADDRESSES2.jpg)

![FQDNs](imagenes/GUI%20FORTIGATE/FDQNs.jpg)

### Políticas de firewall

![Políticas general](imagenes/GUI%20FORTIGATE/PoliticasGeneral.jpg)

![Política 1](imagenes/GUI%20FORTIGATE/Politica1.jpg)

![Política 2](imagenes/GUI%20FORTIGATE/Politica2.jpg)

![Política 3](imagenes/GUI%20FORTIGATE/Politica3.jpg)

![Política 4](imagenes/GUI%20FORTIGATE/Politica4.jpg)

![Política 5](imagenes/GUI%20FORTIGATE/Politica5.jpg)

![Política 6](imagenes/GUI%20FORTIGATE/Politica6.jpg)

![Política 7](imagenes/GUI%20FORTIGATE/Politica7.jpg)

![Política 8](imagenes/GUI%20FORTIGATE/Politica8.jpg)

---

## Pruebas

### DMZ sin acceso abierto a Internet

![DMZ Internet 1](imagenes/Pruebas/DMZ_Internet1.png)

![DMZ Internet 2](imagenes/Pruebas/DMZ_Internet2.png)

![DMZ Internet 3](imagenes/Pruebas/DMZ_Internet3.png)

### SSH solo desde la VLAN 20

![SSH VLAN 20 - 1](imagenes/Pruebas/SSH_VLAN20_1.png)

![SSH VLAN 20 - 2](imagenes/Pruebas/SSH_VLAN20_2.png)

![SSH VLAN 20 - 3](imagenes/Pruebas/SSH_VLAN20_3.png)

![SSH VLAN 20 - 4](imagenes/Pruebas/SSH_VLAN20_4.png)

![SSH VLAN 20 - 5](imagenes/Pruebas/SSH_VLAN20_5.png)

### VLAN 10 restringida al Web Server de Inventario

![VLAN 10 restringido 1](imagenes/Pruebas/Vlan10Restringido1.png)

![VLAN 10 restringido 2](imagenes/Pruebas/Vlan10Restringido2.png)

![VLAN 10 restringido 3](imagenes/Pruebas/Vlan10Restringido3.png)

---

## Detalles de los equipos

### Web Server: Sistema de Caja

![Detalles Web Caja](imagenes/Detalles_Web_Caja.png)

### Web Server: Sistema de Inventario

![Detalles Inventario](imagenes/Detalles_Inventario.png)

### DB Server

![Detalles DB](imagenes/Detalles_DB.png)

### Usuarios VLAN 10

![Detalles VLAN 10](imagenes/Detalles_VLAN10.png)

### Usuarios VLAN 20

![Detalles VLAN 20](imagenes/Detalles_VLAN20.png)
