# **MANUAL DE CONFIGURACION**
## Topología 1
## Topología 2
La topología 2 es la encargada de distribuir y repartir las VLANS hacia las demás topologías, es el Cuarto de telecomunciaciones
### Configuración de la topología de red:
Componentes a utilizar:
- 4 Etherswitch Router
- 2 Cloud
Conexiones de la topologia: 

<p align="center">
  <img src="img/Topo2_1.png" width="600">
</p>

Podemos ver que los portchannels están configurados y la interface que se conecta a la nube en el ESW1 con el comando sh int trunk

<p align="center">
  <img src="img/Topo2_2.png" width="600">
</p>

Además el ESW1 es el que se configura en modo servidor y por lo tanto el encargado de suministrarle las VLANS creadas en este hacia los demas switchs, miramos esto con el comando sh vtp status

<p align="center">
  <img src="img/Topo2_3.png" width="600">
</p>

Para todos los demás switchs son configurados en modo cliente y las VLANs automáticamente son asignadas, como podemos ver el caso del ESW3 con el comando sh vlan-switch

<p align="center">
  <img src="img/Topo2_4.png" width="600">
</p>

Además de esto se le aplicó el Spanning Tree Protocol, esto nos ayuda a que no se enciclen los paquetes y pueda todo llegar a su destino, este fue configurado en el ESW1, lo cual genera un bloqueo de puertos en este caso en el  ESW2 y esto verifica que todo esté configurado correctamente

<p align="center">
  <img src="img/Topo2_5.png" width="600">
</p>


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

### pruebas de ping:

Ping entre la VCP's de contabilidad:
<p align="center">
  <img src="img/ventas1ping.png" width="600">
</p>
<p align="center">
  <img src="img/ventas2ping.png" width="600">
</p>
Ping entre las VPC's de ventas:
<p align="center">
  <img src="img/conta1ping.png" width="600">
</p>
<p align="center">
  <img src="img/conta2ping.png" width="600">
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

