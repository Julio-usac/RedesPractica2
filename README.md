# **MANUAL DE CONFIGURACION**
## Topología 1
## Topología 2
## Topología 3
Pasos para configurar la topologia 3.
### Configuración de la topología de red:
Componentes a utilizar:
- 5 VPC
- 2 Etherswitch
- 4 Etherswitch Router
- 1 Cloud

Conexiones de la topologia: 

<p align="center">
  <img src="img/topo2.png" width="600">
</p>

### Configuracion por dispositivos:
Configuracion de Etherswitch router 1:
1. Configuracion de enlaces truncales y vlans:
<p align="center">
  <img src="img/router1trunk.png" width="600">
</p>
2. Configuracion de port-channel:
<p align="center">
  <img src="img/router1channel.png" width="600">
</p>
Configuracion de Etherswitch router 2:
1. Configuracion de enlaces truncales y vlans:
<p align="center">
  <img src="img/router2trunk.png" width="600">
</p>
2. Configuracion de port-channel:
<p align="center">
  <img src="img/router2channel.png" width="600">
</p>
Configuracion de Etherswitch router 3:
1. Configuracion de enlaces truncales y vlans:
<p align="center">
  <img src="img/router3trunk.png" width="600">
</p>
2. Configuracion de port-channel:
<p align="center">
  <img src="img/router3channel.png" width="600">
</p>
Configuracion de Etherswitch router 4:
1. Configuracion de enlaces truncales y vlans:
<p align="center">
  <img src="img/router4trunk.png" width="600">
</p>
2. Configuracion de port-channel:
<p align="center">
  <img src="img/router4channel.png" width="600">
</p>
3. Configuracion de enlace de acceso:
<p align="center">
  <img src="img/router4access.png" width="600">
</p>

Configuracion de ip de VPC ventas1:

<p align="center">
  <img src="img/ventas1ip.png" width="600">
</p>

Configuracion de ip de VPC conta1:

<p align="center">
  <img src="img/conta1ip.png" width="600">
</p>

Configuracion de ip de VM ventas2:

<p align="center">
  <img src="img/Vmventas2.png" width="600">
</p>

Configuracion de switch 1:

<p align="center">
  <img src="img/switch1.png" width="600">
</p>

Configuracion de switch 2:

<p align="center">
  <img src="img/switch2.png" width="600">
</p>
### Comandos utilizados:

Se utilizaron los siguientes comandos para configurar los etherswitch router:

1. Se utilizaron los siguientes comandos para configurar los EtherChannel:
  ~~~
  int range f#/# - #  //Se especifca el rango de interfaces
  channel-group # mode on // Se especifica el grupo al que perteneceran
  end
  ~~~
2. Se utilizaron los siguientes comandos para configurar enlaces truncales entre los etherswitch router:
  ~~~
  int Po#   //Se especifica el puerto
  switchport mode trunk //Se cambia a modo truncal
  switchport trunk allowed vlan 1,10,20,30,1002-1005  //Se especifican las vlans
  end
  ~~~
3. Se utlizaron los siguientes comandos para configurar los enlaces truncales entre los etherswitch router y los etherswitch:
  ~~~
  int f#/#   //Se especifica la interfaz
  switchport mode trunk //Se cambia a modo truncal
  switchport trunk allowed vlan 1,10,20,30,1002-1005  //Se especifican las vlans
  end
  ~~~
4. Se utilizaron los siguientes comandos para configurar los enlaces de acceso entre los etherswitch router y las VPC:
  ~~~
  int f#/# //Se especifica la interfaz
  switchport mode access  //Se cambia a modo acceso
  switchport access vlan # //Se especifica la vlan
  End
  ~~~
5. Se utilizaron los siguientes comandos para configurar VTP:
  ~~~
  vtp domain "nombre" // Se configura el nombre del dominio
  vtp password "contraseña" // Se configura la contraseña
  vtp mode client //Se cambia a modo cliente
  end
  ~~~
6. Se utlizaron los siguientes comandos para guardar los cambios en el Etherswitch router:
  ~~~
  copy run start
  write memory
  ~~~

Se utilizaron los siguientes comandos para configurar las VPC:
1. Se utlizo el siguiente comando para configurar la ip:
  ~~~
  "ip 'tu ip'/'Tu mascara de red' 'tu gateway'"
  ~~~
2. Se utlizo el siguiente comando para guardar los cambios:
  ~~~
  save
  ~~~

