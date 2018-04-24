---
title: Configurar InfiniBand - sistema de la plataforma de análisis | Documentos de Microsoft
description: Describe cómo configurar los adaptadores de red InfiniBand en un servidor no sea de dispositivo cliente para conectarse al nodo de Control en el almacén de datos paralelos (PDW). Siga estas instrucciones para la conectividad básica y para lograr alta disponibilidad, para que los procesos de carga, la copia de seguridad y otros se conectan automáticamente a la red InfiniBand active.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 8e67d63e7bb4bded0bd19e5db4a0b7faddb80977
ms.sourcegitcommit: 056ce753c2d6b85cd78be4fc6a29c2b4daaaf26c
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/19/2018
---
# <a name="configure-infiniband-network-adapters-for-analytics-platform-system"></a>Configurar adaptadores de red InfiniBand para Analytics Platform System
Describe cómo configurar los adaptadores de red InfiniBand en un servidor no sea de dispositivo cliente para conectarse al nodo de Control en el almacén de datos paralelos (PDW). Siga estas instrucciones para la conectividad básica y para lograr alta disponibilidad, para que los procesos de carga, la copia de seguridad y otros se conectan automáticamente a la red InfiniBand active.  
  
## <a name="Basics"></a>Descripción  
Estas instrucciones muestran cómo encontrar y, a continuación, establecer la dirección IP correcta InfiniBand direcciones y máscaras de subred en el servidor conectado InfiniBand. Además, se explica cómo configurar el servidor para usar el dispositivo de APS DNS para que la conexión se resuelva en la red InfiniBand activa.  
  
Para lograr alta disponibilidad, puntos de acceso tiene dos redes InfiniBand, una activa y uno pasiva. Cada red InfiniBand tiene una dirección IP diferente para el nodo de Control. Si la red InfiniBand active deja de funcionar, la red InfiniBand pasiva se convierte en la red activa. Cuando esto sucede un script o un proceso se conecta automáticamente a la red InfiniBand active sin cambiar los parámetros de script.  
  
En concreto, en este artículo es:  
  
1.  Buscar servidores de las direcciones IP de InfiniBand del APS DNS (AD01 appliance_domain y appliance_domain *-AD02). Si desea iniciar sesión en los servidores AD01 y AD02 y obtener las direcciones IP para cada red InfiniBand. Las direcciones IP de InfiniBand en el nodo de AD son las direcciones IP de DNS.  
  
2.  Configure cada adaptador de red para usar una dirección IP disponible en las redes InfiniBand APS.  
  
    1.  Si tiene dos adaptadores de red InfiniBand, configurar un adaptador con una dirección IP disponible en la primera red InfiniBand que se denomina TeamIB1 y el otro adaptador con una dirección IP disponible en la red InfiniBand segundo que se denomina TeamIB2. Usar el TeamIB1 AD01 appliance_domain una dirección IP como el servidor DNS preferido y appliance_domain AD02 TeamIB1 dirección IP que el servidor DNS alternativo para el adaptador de red TeamIB1. Usar el TeamIB2 AD01 appliance_domain una dirección IP como el servidor DNS preferido y appliance_domain AD02 TeamIB2 dirección IP que el servidor DNS alternativo para el adaptador de red de TeamIB2.  
  
    2.  Si tiene un solo adaptador de red de InfiniBand, el adaptador se configura con una dirección IP disponible de una de las redes InfiniBand. A continuación, configurará el preferido y los servidores DNS alternativos en este adaptador mediante TeamIB1 appliance_domain AD01 y AD02 appliance_domain TeamIB1 o con TeamIB2 appliance_domain AD01 y AD02 appliance_domain TeamIB2 sea en el mismo red como el adaptador configurado como el preferido y los servidores DNS alternativos, respectivamente.  
  
3.  Configurar el adaptador de red InfiniBand para utilizar servidores de APS DNS para resolver la conexión a la red InfiniBand active.  
  
    1.  Para configurar esta opción que usar la configuración avanzada de TCP/IP para agregar el sufijo DNS del dominio de aplicación al principio de la lista de sufijos DNS en el servidor de cliente. Esto solo debe configurarse en uno de los adaptadores de red; la configuración se aplica a ambos adaptadores.  
  
Después de configurar los adaptadores de red InfiniBand, los procesos de cliente pueden conectarse al nodo de Control en la red InfiniBand mediante `PDW_region-SQLCTL01` para la dirección del servidor. El servidor agrega el sufijo DNS de sistema de plataforma de análisis, o bien puede escribir la dirección completa que es `PDW_region-SQLCTL01.appliance_domain.pdw.local`.  
  
Por ejemplo, si el nombre de la región PDW es MyPDW y el nombre del dispositivo es MyAPS, la especificación del servidor de dwloader para cargar los datos es uno de los siguientes:  
  
-   `dwloader –S MYPDW-SQLCTL01.MyAPS.pdw.local`  
  
-   `dwloader –S MYPDW-SQLCTL01`  
  
## <a name="BeforeBegin"></a>Antes de empezar  
  
### <a name="requirements"></a>Requisitos  
Necesita una cuenta de dominio de aplicación de APS para iniciar sesión en el nodo AD01. Por ejemplo, F12345 * \Administrator.  
  
Necesita una cuenta de Windows en el servidor de cliente que tiene permiso para configurar los adaptadores de red.  
  
### <a name="prerequisites"></a>Requisitos previos  
Estas instrucciones se supone el servidor de cliente ya está en rack y conectado a la red InfiniBand de dispositivo. Para la instalación en rack y cableado de instrucciones, consulte [adquirir y configurar un servidor de carga](acquire-and-configure-loading-server.md).  
  
### <a name="general-remarks"></a>Notas generales  
Mediante el uso de SQLCTL01, el sistema de plataforma de análisis de DNS se conecta el servidor de cliente al nodo de Control mediante el uso de la red InfiniBand active. Esto se aplica solo a va a conectar; Si la red InfiniBand deja de funcionar durante una carga o una copia de seguridad, debe reiniciar el proceso.  
  
Para satisfacer sus requisitos empresariales, también puede unir el servidor de cliente a su propio grupo de trabajo no sea de dispositivo o un dominio de Windows.  
  
## <a name="Sec1"></a>Paso 1: Obtener el dispositivo, configuración de red InfiniBand  
*Para obtener la aplicación configuración de red InfiniBand*  
  
1.  Inicie sesión en el dispositivo AD01 nodo mediante el uso de la cuenta appliance_domain\Administrator.  
  
2.  En el nodo de dispositivo AD01, abra el Panel de Control, seleccione red y Internet, seleccione red y recursos compartidos Center * y, a continuación, seleccione Cambiar configuración del adaptador.  
  
3.  En la ventana Conexiones de red, haga doble clic en el equipo IB1 y seleccione Propiedades.  
  
    ![Conexiones InfiniBand en el nodo Administración](media/network-teamib.png "conexiones InfiniBand en el nodo de administración")  
  
4.  En la ventana Propiedades de protocolo de Internet versión 4 (TCP/IPv4), anote los valores de la **dirección IP** y **máscara de subred**.  La dirección IP de la ***appliance_domain *-AD01** nodo es la dirección IP del servidor DNS de sistema de plataforma de análisis.  
  
5.  Repita los pasos 1 a 5 anteriores para el adaptador TeamIB1 en ***appliance_domain *-AD02** server.  
  
    ![Propiedades de InfiniBand 1 nodo de administración de PDW](media/network-ip1-properties.png "propiedades de InfiniBand 1 nodo de administración de PDW")  
  
6.  Haga clic en Cancelar para cerrar la ventana.  
  
7.  Buscar una dirección IP no utilizada en la red TeamIB1 y escribirlo.  
  
    Para buscar una dirección IP no utilizada, abra una ventana de comandos e intente hacer ping de direcciones IP dentro del intervalo de direcciones de su dispositivo. En este ejemplo, la dirección IP de la red TeamIB1 es 172.16.14.30. Buscar una dirección IP que empieza por 172.16.14 que no se utiliza. Por ejemplo, desde la línea de comandos escriba "hacer ping 172.16.14.254". Si la solicitud de ping se realiza correctamente, la dirección IP está disponible.  
  
8.  Haga lo mismo para TeamIB2. En el * ventana Conexiones de red, haga doble clic en el equipo IB2 y seleccione Propiedades.  
  
9. En la ventana Propiedades de protocolo de Internet versión 4 (TCP/IPv4), anote los valores de la dirección IP y máscara de subred de TeamIB2.  
  
10. Repita los pasos 8-9 anterior para el adaptador TeamIB2 appliance_domain AD02 servidor.  
  
    ![Propiedades de TeamIB2](media/network-ip2-properties.png "propiedades de TeamIB2")  
  
11. Buscar una dirección IP no utilizada en el **TeamIB2** de red y escribirlo.  
  
    Para buscar una dirección IP no utilizada, abra una ventana de comandos e intente hacer ping de direcciones IP dentro del intervalo de direcciones de su dispositivo. En este ejemplo, la dirección IP de la red de TeamIB2 es 172.16.18.30. Buscar una dirección IP que empieza por 172.16.18 que no se utiliza. Por ejemplo, desde la línea de comandos escriba "hacer ping 172.16.18.254". Si la solicitud de ping se realiza correctamente, la dirección IP está disponible.  
  
## <a name="Sec2"></a>Paso 2: Configurar la configuración del adaptador de red InfiniBand en el servidor de cliente  

### <a name="notes"></a>Notas  
  
-   Estos pasos muestran cómo registrar el servidor con los servidores DNS de APS.  
  
-   Para satisfacer sus propias necesidades de red, también puede unir el servidor de cliente a su propio grupo de trabajo no sea de dispositivo o un dominio de Windows.  
  
-   Las instrucciones paso a paso a través de la configuración de dos adaptadores de red en cada servidor.  Si sólo tiene un adaptador de red, elija una de las redes para configurar en el adaptador de red y, a continuación, agregar la segunda dirección IP de DNS como un servidor DNS alternativo.  
  
### <a name="to-configure-the-infiniband-network-adapter-settings-on-your-client-server"></a>Para configurar la configuración del adaptador de red InfiniBand en el servidor de cliente  
  
1.  Inicie sesión como administrador de Windows para la carga, copia de seguridad u otro servidor de cliente en el dispositivo de red InfiniBand.  
  
2.  Abra el panel de Control *, seleccione el centro de redes y recursos compartidos y, a continuación, seleccione Cambiar configuración del adaptador.  
  
### <a name="to-configure-the-first-network-adapter"></a>Para configurar el primer adaptador de red  
  
1.  En la ventana Conexiones de red, haga doble clic en una de las zonas de red no identificada para el adaptador Mellanox y seleccione Propiedades.  
  
    ![Seleccione las redes InfiniBand](media/network-connections.png "seleccione las redes InfiniBand")  
  
2.  En la ventana Propiedades  
  
    1.  En la ficha General, establezca la dirección IP a la dirección IP que comprobó como disponible en la prueba de ping para TeamIB1. Para los valores de ejemplo que se usan en este artículo, escribiría 172.16.14.254.  
  
    2.  Establecer la máscara de subred para la máscara de subred que escribió para TeamIB1.  
  
    3.  Establecer el servidor DNS preferido para la dirección IP de TeamIB1 que anotó anteriormente desde el appliance_domain *-nodo AD01.  
  
    4.  Establecer el servidor DNS alternativo a la dirección IP de TeamIB1 que anotó anteriormente desde el appliance_domain *-nodo AD02.  
  
        ![Propiedades del adaptador de red 1 InfiniBand](media/network-ib1-properties.png "SQL_Server_PDW_Network_IB1_properties")  
  
    5.  Haga clic en Aceptar para aplicar los cambios.  
  
### <a name="to-configure-the-second-network-adapter"></a>Para configurar el segundo adaptador de red  
  
1.  Omitir esta sección si solo tiene un adaptador de red.  
  
2.  En la ventana Conexiones de red, haga doble clic en la segunda ranura de red no identificada para el adaptador Mellanox y seleccione Propiedades.  
  
    ![Seleccione las redes InfiniBand](media/network-connections.png "seleccione las redes InfiniBand")  
  
3.  En la ventana Propiedades  
  
    1.  En la ficha General, establezca la dirección IP a la dirección IP que comprobó como disponible en la prueba de ping de TeamIB2. Para los valores de ejemplo que se usan en este artículo, escribiría 172.16.18.254.  
  
    2.  Establecer la máscara de subred para la máscara de subred que anotó de TeamIB2.  
  
    3.  Establecer el servidor DNS preferido para la dirección IP de TeamIB2 que anotó anteriormente desde el appliance_domain *-nodo AD01.  
  
    4.  Establecer el servidor DNS alternativo a la dirección IP de TeamIB2 que anotó anteriormente desde el appliance_domain *-nodo AD02.  
  
        > [!NOTE]  
        > Si sólo dispone de uno adaptador de red, configurar el preferido y los servidores DNS alternativos con el dispositivo AD01 TeamIB1 y el dispositivo AD02 TeamIB1 como el preferido y los servidores DNS alternativos, respectivamente o usar el dispositivo TeamIB2 AD01 y dispositivo TeamIB2 AD02 como el preferido y el servidor DNS alternativo dependiendo de si la máquina virtual de AD ha conmutado por error.  
  
        ![Propiedades del adaptador de red 1 InfiniBand](media/network-ib1-properties.png "InfiniBand propiedades del adaptador de red 1")  
  
    5.  Haga clic en Aceptar para aplicar los cambios.  
  
### <a name="to-configure-the-dns-suffix"></a>Para configurar el sufijo DNS  
  
1.  En la ventana Conexiones de red, haga doble clic en una de las zonas de red para el adaptador Mellanox y seleccione Propiedades.  
  
2.  Haga clic en Avanzadas... .  
  
3.  En la ventana de configuración avanzada de TCP/IP, si el anexado estas opciones de sufijos DNS (en orden) no está atenuada, llama a la casilla de verificación Anexar estos sufijos DNS (en orden):, seleccione el sufijo de dominio de aplicación y haga clic en Agregar... El sufijo de dominio de aplicación `appliance_domain.local`  
  
4.  Si la anexar estos sufijos DNS (en orden): opción está atenuada, puede agregar el dominio de puntos de acceso a este servidor mediante la modificación de la clave del registro HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\DNSClient.  
  
    ![Configuración de TCP/IP](media/network-tcpip.png "configuración TCP/IP")  
  
5.  Para agilizar la resolución de direcciones, se recomienda mover el sufijo de dispositivo a la parte superior de la lista.  
  
6.  Haga clic en Aceptar.  
  
7.  Ahora, puede conectarse a la red Infiniband de dispositivo mediante el uso de `PDW_region-SQLCTL01.appliance_domain.local`, o simplemente `appliance_domain-SQLCTL01`. Puede establecer la conexión con mayor rapidez si se conecta con el nombre completo y el sufijo DNS.  
  
    Ejemplos de un dispositivo denominado MyAPS con una región de MyPDW PDW:  
  
    -   MyPDW-SQLCTL01.MyAPS.local  
  
    -   MyPDW SQLCTL01  
  
## <a name="see-also"></a>Vea también  
[Adquirir y configurar un servidor de carga ](acquire-and-configure-loading-server.md)  
  
