---
title: Configurar InfiniBand - Analytics Platform System | Microsoft Docs
description: Describe cómo configurar los adaptadores de red InfiniBand en un servidor que no sea de dispositivo cliente para conectarse al nodo de Control en el almacenamiento de datos paralelos (PDW). Siga estas instrucciones para la conectividad básica y de alta disponibilidad, para que los procesos de copia de seguridad, la cargando y otros se conectan automáticamente a la red InfiniBand activa.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: e0e0ed3aea02ae8a79d89871f6849b1cbf40c9d0
ms.sourcegitcommit: fc6a6eedcea2d98c93e33d39c1cecd99fbc9a155
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/12/2018
ms.locfileid: "49169352"
---
# <a name="configure-infiniband-network-adapters-for-analytics-platform-system"></a>Configurar adaptadores de red InfiniBand para Analytics Platform System
Describe cómo configurar los adaptadores de red InfiniBand en un servidor que no sea de dispositivo cliente para conectarse al nodo de Control en el almacenamiento de datos paralelos (PDW). Siga estas instrucciones para la conectividad básica y de alta disponibilidad, para que los procesos de copia de seguridad, la cargando y otros se conectan automáticamente a la red InfiniBand activa.  
  
## <a name="Basics"></a>Descripción  
Estas instrucciones muestran cómo buscar y, a continuación, configurar las correcto InfiniBand IP direcciones y máscaras de subred en el servidor conectado con InfiniBand. También explica cómo configurar el servidor para usar el dispositivo APS DNS para que se resuelve como la conexión a la red InfiniBand activada.  
  
Para lograr alta disponibilidad, APS tiene dos redes InfiniBand, uno activo y uno pasivo. Cada red de InfiniBand tiene una dirección IP diferente para el nodo de Control. Si la red InfiniBand active deja de funcionar, la red InfiniBand pasiva se convierte en la red activa. Cuando esto sucede un script o un proceso se conecta automáticamente a la red InfiniBand activada sin cambiar los parámetros del script.  
  
En concreto, en este artículo es:  
  
1.  Buscar servidores de las direcciones IP de InfiniBand de APS DNS (appliance_domain AD01 y appliance_domain *-AD02). Para ello inicie sesión en los servidores AD01 y AD02 y obtener las direcciones IP para cada red InfiniBand. Las direcciones IP de InfiniBand en el nodo de AD son las direcciones IP de DNS.  
  
2.  Configurar cada adaptador de red para usar una dirección IP disponible en las redes InfiniBand APS.  
  
    1.  Si tiene dos adaptadores de red de InfiniBand, configurar un adaptador con una dirección IP disponible en la primera red InfiniBand que se denomina TeamIB1 y el otro adaptador con una dirección IP disponible en la segunda red InfiniBand que se denomina TeamIB2. Usar el TeamIB1 appliance_domain AD01 una dirección IP como el servidor DNS preferido y appliance_domain AD02 TeamIB1 dirección IP como servidor DNS alternativo para el adaptador de red TeamIB1. Usar el TeamIB2 appliance_domain AD01 una dirección IP como el servidor DNS preferido y appliance_domain AD02 TeamIB2 dirección IP como servidor DNS alternativo para el adaptador de red de TeamIB2.  
  
    2.  Si tiene un solo adaptador de red de InfiniBand, el adaptador se configura con una dirección IP disponible desde una de las redes InfiniBand. A continuación, configurará el preferido y los servidores DNS alternativos en este adaptador utilizar appliance_domain AD01 TeamIB1 y appliance_domain AD02 TeamIB1 o appliance_domain AD01 TeamIB2 y TeamIB2 appliance_domain AD02 sea en el mismo red como el adaptador configurado como el preferido y los servidores DNS alternativos, respectivamente.  
  
3.  Configurar el adaptador de red de InfiniBand para usar servidores DNS de APS para resolver la conexión a la red InfiniBand activada.  
  
    1.  Para configurar esto use la configuración avanzada de TCP/IP para agregar el sufijo DNS de dominio de aplicación al principio de la lista de sufijos DNS en el servidor de cliente. Esto solo debe configurarse en uno de los adaptadores de red; la configuración se aplica a ambos adaptadores.  
  
Después de configurar los adaptadores de red InfiniBand, procesos del cliente pueden conectarse al nodo de Control de la red InfiniBand mediante `PDW_region-SQLCTL01` para la dirección del servidor. El servidor anexa el sufijo DNS de Analytics Platform System, o puede escribir la dirección completa que es `PDW_region-SQLCTL01.appliance_domain.pdw.local`.  
  
Por ejemplo, si el nombre de la región PDW es MyPDW y el nombre del dispositivo es MyAPS, la especificación de servidor dwloader para cargar los datos es uno de los siguientes:  
  
-   `dwloader –S MYPDW-SQLCTL01.MyAPS.pdw.local`  
  
-   `dwloader –S MYPDW-SQLCTL01`  
  
## <a name="BeforeBegin"></a>Antes de empezar  
  
### <a name="requirements"></a>Requisitos  
Necesita una cuenta de dominio del dispositivo APS inicien sesión en el nodo AD01. Por ejemplo, F12345 * \Administrator.  
  
Se necesita una cuenta de Windows en el servidor de cliente que tiene permiso para configurar los adaptadores de red.  
  
### <a name="prerequisites"></a>Requisitos previos  
Estas instrucciones asumen que el servidor de cliente ya está de bastidor y cableado a la red InfiniBand de dispositivo. Para la instalación en bastidor y cableado de instrucciones, consulte [adquirir y configurar un servidor al cargar](acquire-and-configure-loading-server.md).  
  
### <a name="general-remarks"></a>Notas generales  
Mediante el uso de SQLCTL01, el sistema DNS de plataforma de análisis se conecta el servidor de cliente al nodo de Control mediante el uso de la red InfiniBand activa. Se aplica únicamente al establecimiento de conexiones; Si la red InfiniBand deja de funcionar durante una carga o copia de seguridad, deberá reiniciar el proceso.  
  
Para satisfacer sus requisitos empresariales, también puede unir el servidor de cliente a su propio grupo de trabajo que no sea de dispositivo o un dominio de Windows.  
  
## <a name="Sec1"></a>Paso 1: Obtener el dispositivo, configuración de red de InfiniBand  
*Para obtener el dispositivo la configuración de red de InfiniBand*  
  
1.  Inicie sesión en el dispositivo AD01 nodo mediante la cuenta appliance_domain\Administrator.  
  
2.  En el nodo AD01 del dispositivo, abra el Panel de Control, seleccione la red y Internet, seleccione la red y centro de recursos compartidos * y, a continuación, seleccione Cambiar configuración del adaptador.  
  
3.  En la ventana Conexiones de red, haga doble clic en el equipo IB1 y seleccione Propiedades.  
  
    ![Conexiones InfiniBand en el nodo Administración](media/network-teamib.png "conexiones InfiniBand en el nodo de administración")  
  
4.  En la ventana Propiedades de protocolo de Internet versión 4 (TCP/IPv4), anote los valores para el **dirección IP** y **máscara de subred**.  La dirección IP de la  **_dispositivo\_dominio_-AD01** nodo es la dirección IP del servidor DNS de sistema de plataforma de análisis.  
  
5.  Repita los pasos del 1 al 5 anteriores para el adaptador TeamIB1 en  **_dispositivo\_dominio_-AD02** server.  
  
    ![Propiedades de InfiniBand 1 nodo de administración de PDW](media/network-ip1-properties.png "propiedades de InfiniBand 1 nodo de administración de PDW")  
  
6.  Haga clic en Cancelar para cerrar la ventana.  
  
7.  Buscar una dirección IP no utilizada en la red de TeamIB1 y escribirlo.  
  
    Para buscar una dirección IP sin usar, abra una ventana de comandos e intente hacer ping las direcciones IP dentro del intervalo de direcciones de su dispositivo. En este ejemplo, la dirección IP de la red TeamIB1 es 172.16.14.30. Buscar una dirección IP que empieza por 172.16.14 que no se utiliza. Por ejemplo, desde la línea de comandos escriba "ping 172.16.14.254". Si la solicitud de ping se realiza correctamente, la dirección IP está disponible.  
  
8.  Lo mismo de TeamIB2. En la * ventana Conexiones de red, haga doble clic en el equipo IB2 y seleccione Propiedades.  
  
9. En la ventana Propiedades de protocolo de Internet versión 4 (TCP/IPv4), anote los valores de la dirección IP y máscara de subred de TeamIB2.  
  
10. Repita los pasos 8 y 9 anteriores para el adaptador TeamIB2 appliance_domain AD02 servidor.  
  
    ![Propiedades de TeamIB2](media/network-ip2-properties.png "propiedades de TeamIB2")  
  
11. Buscar una dirección IP no utilizada en el **TeamIB2** de red y escribirlo.  
  
    Para buscar una dirección IP sin usar, abra una ventana de comandos e intente hacer ping las direcciones IP dentro del intervalo de direcciones de su dispositivo. En este ejemplo, la dirección IP de la red de TeamIB2 es 172.16.18.30. Buscar una dirección IP que empieza por 172.16.18 que no se utiliza. Por ejemplo, desde la línea de comandos escriba "ping 172.16.18.254". Si la solicitud de ping se realiza correctamente, la dirección IP está disponible.  
  
## <a name="Sec2"></a>Paso 2: Configurar la configuración del adaptador de red InfiniBand en el servidor de cliente  

### <a name="notes"></a>Notas  
  
-   Estos pasos muestran cómo registrar el servidor con los servidores DNS de APS.  
  
-   Para satisfacer sus necesidades de la red, también puede unir el servidor de cliente a su propio grupo de trabajo que no sea de dispositivo o un dominio de Windows.  
  
-   Las instrucciones paso a través de la configuración de dos adaptadores de red en cada servidor.  Si solo tiene un adaptador de red, elija una de las redes para configurar el adaptador de red y, a continuación, agregar la segunda dirección IP de DNS como un servidor DNS alternativo.  
  
### <a name="to-configure-the-infiniband-network-adapter-settings-on-your-client-server"></a>Para configurar la configuración del adaptador de red InfiniBand en el servidor de cliente  
  
1.  Inicie sesión como administrador de Windows en la carga, copia de seguridad u otro servidor de cliente en el dispositivo de red InfiniBand.  
  
2.  Abra el panel de Control *, seleccione el centro de redes y recursos compartidos y, a continuación, seleccione Cambiar configuración del adaptador.  
  
### <a name="to-configure-the-first-network-adapter"></a>Para configurar el primer adaptador de red  
  
1.  En la ventana Conexiones de red, haga doble clic en una de las ranuras de la red no identificada para el adaptador Mellanox y seleccione Propiedades.  
  
    ![Seleccione las redes InfiniBand](media/network-connections.png "seleccione las redes InfiniBand")  
  
2.  En la ventana Propiedades  
  
    1.  En la ficha General, establezca la dirección IP a la dirección IP que ha comprobado como disponible en la prueba de ping para TeamIB1. Para los valores de ejemplo utilizados en este artículo, escribiría 172.16.14.254.  
  
    2.  Establece la máscara de subred en la máscara de subred que anotó para TeamIB1.  
  
    3.  Establecer el servidor DNS preferido para la dirección IP de TeamIB1 que anotó anteriormente desde appliance_domain *-nodo AD01.  
  
    4.  Establecer el servidor DNS alternativo a la dirección IP de TeamIB1 que anotó anteriormente desde appliance_domain *-nodo AD02.  
  
        ![Propiedades del adaptador de InfiniBand 1 red](media/network-ib1-properties.png "SQL_Server_PDW_Network_IB1_properties")  
  
    5.  Haga clic en Aceptar para aplicar los cambios.  
  
### <a name="to-configure-the-second-network-adapter"></a>Para configurar el segundo adaptador de red  
  
1.  Omitir esta sección si solo tiene un adaptador de red.  
  
2.  En la ventana Conexiones de red, haga doble clic en la segunda ranura de red no identificada para el adaptador Mellanox y seleccione Propiedades.  
  
    ![Seleccione las redes InfiniBand](media/network-connections.png "seleccione las redes InfiniBand")  
  
3.  En la ventana Propiedades  
  
    1.  En la ficha General, establezca la dirección IP en la dirección IP que ha comprobado como disponible en la prueba de ping de TeamIB2. Para los valores de ejemplo utilizados en este artículo, escribiría 172.16.18.254.  
  
    2.  Establece la máscara de subred en la máscara de subred que anotó de TeamIB2.  
  
    3.  Establecer el servidor DNS preferido para la dirección IP de TeamIB2 que anotó anteriormente desde appliance_domain *-nodo AD01.  
  
    4.  Establecer el servidor DNS alternativo a la dirección IP de TeamIB2 que anotó anteriormente desde appliance_domain *-nodo AD02.  
  
        > [!NOTE]  
        > Si solo tiene una adaptador de red, configurar el preferido y los servidores DNS alternativos con el dispositivo AD01 TeamIB1 y el dispositivo AD02 TeamIB1 como el preferido y los servidores DNS alternativos, respectivamente o usar el dispositivo TeamIB2 AD01 y dispositivo AD02 TeamIB2 como el preferido y los servidores DNS alternativos dependiendo de si la máquina virtual de AD ha conmutado.  
  
        ![Propiedades del adaptador de InfiniBand 1 red](media/network-ib1-properties.png "InfiniBand propiedades del adaptador de red 1")  
  
    5.  Haga clic en Aceptar para aplicar los cambios.  
  
### <a name="to-configure-the-dns-suffix"></a>Para configurar el sufijo DNS  
  
1.  En la ventana Conexiones de red, haga doble clic en una de las ranuras de la red para el adaptador Mellanox y seleccione Propiedades.  
  
2.  Haga clic en el avanzado... botón Examinar (...).  
  
3.  En la ventana de configuración avanzada de TCP/IP, si la anexar estos sufijos DNS (en orden) opción no es atenuada, llama la casilla de verificación Anexar estos sufijos DNS (en orden): seleccione el sufijo de dominio de aplicación y haga clic en Agregar... El sufijo de dominio de aplicación `appliance_domain.local`  
  
4.  Si la anexar estos sufijos DNS (en orden): opción está atenuada, puede agregar el dominio de puntos de acceso a este servidor mediante la modificación de la clave del registro HKEY_LOCAL_MACHINE\SOFTWARE\Policies\Microsoft\Windows NT\DNSClient.  
  
    ![Configuración de TCP/IP](media/network-tcpip.png "configuración TCP/IP")  
  
5.  Para agilizar la resolución de direcciones, se recomienda mover el sufijo del dispositivo a la parte superior de la lista.  
  
6.  Haga clic en Aceptar.  
  
7.  Ahora, puede conectarse a la red Infiniband de dispositivo mediante el uso de `PDW_region-SQLCTL01.appliance_domain.local`, o simplemente `appliance_domain-SQLCTL01`. Puede establecer la conexión con mayor rapidez si se conecta con el nombre completo y el sufijo DNS.  
  
    Ejemplos de un dispositivo denominado MyAPS con una región de PDW MyPDW:  
  
    -   MyPDW-SQLCTL01.MyAPS.local  
  
    -   MyPDW SQLCTL01  
  
## <a name="see-also"></a>Vea también  
[Adquirir y configurar un servidor de carga ](acquire-and-configure-loading-server.md)  
  
