---
share: "true"
---
# Routers
## Métodos para conectarse:

1. Modo de configuración de línea: Consola, SSH, Telnet o acceso auxiliar.
2. Modo de configuración de interfaz: Se utiliza para configurar un puerto de router o una interfaz de red de router.​
## Modos de configuraciones de comandos:

1. Modo sin privilegios: Se simboliza con un `>` después del nombre (hostname) del router
2. Modo EXEC privilegiado: Se simboliza con un `#` después del nombre (hostname) del router
3. Modo de configuración global: Se simboliza con un `(config)#` después del nombre (hostname) del router (debe estar en el modo de privilegio para ser usado)
4. Modo de configuraciones específicas: Se simboliza con un `(config-modo)#` (modo puede ser por ejemplo line) después del nombre (hostname) del router (debe estar en el modo de configuración global para ser usado)

> Se recomienda ejecutar el comando `hostname(config)# no ip domain-lookup` para que al equivocamos en un comando no busque ese comando en otra IP

> Para guardar la configuración del router en la memoria NVRAM se debe ejecutar el comando `hostname# copy running-config startup-config`

## Conexión segura en los modos de configuración
1. `hostname> enable`
   `hostname# configure terminal`
   `hostname(config)# enable secret class`   (class es la contraseña)
   `hostname(config)# line con 0`
   `hostname(config-line)# password cisco`   (cisco es la contraseña)
   `hostname(config-line)# login`
   `hostname(config-line)# exit`
2. 
3. 
4. 
## Otros comandos básicos
* Como poner banner / mensaje del día
* Examine la configuración actual del switch
* hostname S1
* Configurar reloj / protocolo NTP
* UNIDAD 4 – Administración, Detección Y mantenimiento de software IOS
# Protocolos de enrutamiento
## Enrutamiento estáticos VS dinámico
Configuración ip estáticas (unidad 2)
* Estático
  * Resumidas
  * Flotantes
* Dinámico
  * RIPv1
  * IGRP
  * RIPv2
  * EIGRP
  * OSPF
  * IS-IS
  * BGP
# Switches
* Comando básicos
* VLANs
* Trunk VS Access
* Port Security
* Syslog
* DHCP SNOOPING
* Routing-on-stick

| CIDR | SUBNET MASK     | WILDCARD MASK   | # OF IP ADDRESSES | # OF USABLE IP ADDRESSES |     |
| ---- | --------------- | --------------- | ----------------- | ------------------------ | --- |
| /32  | 255.255.255.255 | 0.0.0.0         | 1                 | 1                        |     |
| /31  | 255.255.255.254 | 0.0.0.1         | 2                 | 2*                       |     |
| /30  | 255.255.255.252 | 0.0.0.3         | 4                 | 2                        |     |
| /29  | 255.255.255.248 | 0.0.0.7         | 8                 | 6                        |     |
| /28  | 255.255.255.240 | 0.0.0.15        | 16                | 14                       |     |
| /27  | 255.255.255.224 | 0.0.0.31        | 32                | 30                       |     |
| /26  | 255.255.255.192 | 0.0.0.63        | 64                | 62                       |     |
| /25  | 255.255.255.128 | 0.0.0.127       | 128               | 126                      |     |
| /24  | 255.255.255.0   | 0.0.0.255       | 256               | 254                      |     |
| /23  | 255.255.254.0   | 0.0.1.255       | 512               | 510                      |     |
| /22  | 255.255.252.0   | 0.0.3.255       | 1,024             | 1,022                    |     |
| /21  | 255.255.248.0   | 0.0.7.255       | 2,048             | 2,046                    |     |
| /20  | 255.255.240.0   | 0.0.15.255      | 4,096             | 4,094                    |     |
| /19  | 255.255.224.0   | 0.0.31.255      | 8,192             | 8,190                    |     |
| /18  | 255.255.192.0   | 0.0.63.255      | 16,384            | 16,382                   |     |
| /17  | 255.255.128.0   | 0.0.127.255     | 32,768            | 32,766                   |     |
| /16  | 255.255.0.0     | 0.0.255.255     | 65,536            | 65,534                   |     |
| /15  | 255.254.0.0     | 0.1.255.255     | 131,072           | 131,070                  |     |
| /14  | 255.252.0.0     | 0.3.255.255     | 262,144           | 262,142                  |     |
| /13  | 255.248.0.0     | 0.7.255.255     | 524,288           | 524,286                  |     |
| /12  | 255.240.0.0     | 0.15.255.255    | 1,048,576         | 1,048,574                |     |
| /11  | 255.224.0.0     | 0.31.255.255    | 2,097,152         | 2,097,150                |     |
| /10  | 255.192.0.0     | 0.63.255.255    | 4,194,304         | 4,194,302                |     |
| /9   | 255.128.0.0     | 0.127.255.255   | 8,388,608         | 8,388,606                |     |
| /8   | 255.0.0.0       | 0.255.255.255   | 16,777,216        | 16,777,214               |     |
| /7   | 254.0.0.0       | 1.255.255.255   | 33,554,432        | 33,554,430               |     |
| /6   | 252.0.0.0       | 3.255.255.255   | 67,108,864        | 67,108,862               |     |
| /5   | 248.0.0.0       | 7.255.255.255   | 134,217,728       | 134,217,726              |     |
| /4   | 240.0.0.0       | 15.255.255.255  | 268,435,456       | 268,435,454              |     |
| /3   | 224.0.0.0       | 31.255.255.255  | 536,870,912       | 536,870,910              |     |
| /2   | 192.0.0.0       | 63.255.255.255  | 1,073,741,824     | 1,073,741,822            |     |
| /1   | 128.0.0.0       | 127.255.255.255 | 2,147,483,648     | 2,147,483,646            |     |
| /0   | 0.0.0.0         | 255.255.255.255 | 4,294,967,296     | 4,294,967,294            |     |
The IP address 192.168.1.0 is commonly used as a Class C private IP address in home and small office networks.

Let's explore why it's so prevalent:
- Private IP Address Range:

- The 192.168.0.0 to 192.168.255.255 address range is reserved for private networks.

- These addresses are not routable on the public internet and are meant for internal use within LANs.
- Home networks, relative to business networks, are typically small, making the smaller private address space of Class C suitable.
- Specifics of 192.168.1.0:

    - 192.168.1.0 is often chosen as the starting point for home networks.

    - It provides a convenient base address for subnetting and creating smaller subnetworks.

    - By using subnet masks, network administrators can divide this range into multiple subnets while maximizing the number of host addresses.


- Subnetting Example:

    -  Let's consider subnetting with a /26 subnet mask (255.255.255.192):
    - Four subnets can be created: 192.168.1.0, 192.168.1.64, 192.168.1.128, and 192.168.1.192.

    -  Each subnet can accommodate 62 hosts (2^6 - 2), where 6 bits are available for host addresses.

    - The broadcast addresses for these subnets are 192.168.1.63, 192.168.1.127, 192.168.1.191, and 192.168.1.255.

In summary, 192.168.1.0 is a common choice for home networks due to its simplicity, ease of subnetting, and ample host addresses.