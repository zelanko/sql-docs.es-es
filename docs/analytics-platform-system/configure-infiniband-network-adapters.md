---
title: Configuración de InfiniBand
description: Describe cómo configurar los adaptadores de red InfiniBand en un servidor cliente que no es de dispositivo para conectarse al nodo de control en el almacenamiento de datos paralelo (PDW). Siga estas instrucciones para la conectividad básica y para lograr alta disponibilidad, de modo que la carga, la copia de seguridad y otros procesos se conecten automáticamente a la red InfiniBand activa.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 583d7617c0620d5d1ec24d60fbf10435a547616d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401294"
---
# <a name="configure-infiniband-network-adapters-for-analytics-platform-system"></a>Configuración de adaptadores de red InfiniBand para el sistema de plataforma de análisis
Describe cómo configurar los adaptadores de red InfiniBand en un servidor cliente que no es de dispositivo para conectarse al nodo de control en el almacenamiento de datos paralelo (PDW). Siga estas instrucciones para la conectividad básica y para lograr alta disponibilidad, de modo que la carga, la copia de seguridad y otros procesos se conecten automáticamente a la red InfiniBand activa.  
  
## <a name="description"></a><a name="Basics"></a>Descripción  
Estas instrucciones muestran cómo encontrar y, a continuación, establecer las direcciones IP de InfiniBand y las máscaras de subred correctas en el servidor conectado a InfiniBand. También se explica cómo configurar el servidor para que use el DNS del dispositivo APS para que la conexión se resuelva en la red InfiniBand activa.  
  
Para lograr una alta disponibilidad, APS tiene dos redes InfiniBand, una activa y otra pasiva. Cada red InfiniBand tiene una dirección IP diferente para el nodo de control. Si la red de InfiniBand activa deja de funcionar, la red InfiniBand pasiva se convierte en la red activa. Cuando esto sucede, un script o un proceso se conecta automáticamente a la red InfiniBand activa sin cambiar los parámetros del script.  
  
En concreto, en este artículo:  
  
1.  Busque las direcciones IP de InfiniBand de los servidores DNS de APS (appliance_domain-AD01 y appliance_domain *-AD02). Para ello, inicie sesión en los servidores AD01 y AD02 y obtenga las direcciones IP de cada red InfiniBand. Las direcciones IP de InfiniBand del nodo AD son las direcciones IP de DNS.  
  
2.  Configure cada adaptador de red para que use una dirección IP disponible en las redes de APS InfiniBand.  
  
    1.  Si tiene dos adaptadores de red InfiniBand, configure un adaptador con una dirección IP disponible en la primera red InfiniBand denominada TeamIB1 y el otro adaptador con una dirección IP disponible en la segunda red InfiniBand denominada TeamIB2. Use la dirección IP appliance_domain-AD01 TeamIB1 como el servidor DNS preferido y la dirección IP appliance_domain-AD02 TeamIB1 como servidor DNS alternativo para el adaptador de red de TeamIB1. Use la dirección IP appliance_domain-AD01 TeamIB2 como el servidor DNS preferido y la dirección IP appliance_domain-AD02 TeamIB2 como servidor DNS alternativo para el adaptador de red de TeamIB2.  
  
    2.  Si solo tiene un adaptador de red InfiniBand, configure el adaptador con una dirección IP disponible desde una de las redes InfiniBand. A continuación, configure los servidores DNS preferidos y alternativos en este adaptador mediante appliance_domain-AD01 TeamIB1 y appliance_domain-AD02 TeamIB1 o usando appliance_domain-AD01 TeamIB2 y appliance_domain-AD02 TeamIB2, lo que esté en la misma red que el adaptador configurado como los servidores DNS preferidos y alternativos respectivamente.  
  
3.  Configure el adaptador de red de InfiniBand para usar servidores DNS de APS para resolver la conexión a la red InfiniBand activa.  
  
    1.  Para configurar esto, use la configuración avanzada de TCP/IP para agregar el sufijo DNS del dominio del dispositivo al principio de la lista de sufijos DNS en el servidor cliente. Solo debe configurarse en uno de los adaptadores de red. la configuración se aplica a ambos adaptadores.  
  
Después `PDW_region-SQLCTL01` de configurar los adaptadores de red de InfiniBand, los procesos de cliente pueden conectarse al nodo de control de la red InfiniBand mediante para la dirección del servidor. El servidor anexa el sufijo DNS del sistema de plataforma de análisis, o bien puede escribir la dirección completa, `PDW_region-SQLCTL01.appliance_domain.pdw.local`que es.  
  
Por ejemplo, si el nombre de la región de PDW es MyPDW y el nombre del dispositivo es MyAPS, la especificación del servidor dwloader para cargar datos es una de las siguientes:  
  
-   `dwloader -S MYPDW-SQLCTL01.MyAPS.pdw.local`  
  
-   `dwloader -S MYPDW-SQLCTL01`  
  
## <a name="before-you-begin"></a><a name="BeforeBegin"></a>Antes de empezar  
  
### <a name="requirements"></a>Requisitos  
Necesita una cuenta de dominio de aplicación APS para iniciar sesión en el nodo AD01. Por ejemplo, F12345 * \Administrator.  
  
Necesita una cuenta de Windows en el servidor cliente que tenga permiso para configurar los adaptadores de red.  
  
### <a name="prerequisites"></a>Prerrequisitos  
En estas instrucciones se da por supuesto que el servidor cliente ya está en bastidor y está conectado a la red InfiniBand. Para obtener instrucciones sobre el montaje en bastidor y el cableado, consulte [adquirir y configurar un servidor de carga](acquire-and-configure-loading-server.md).  
  
### <a name="general-remarks"></a>Notas generales  
Mediante el uso de SQLCTL01, el DNS del sistema de plataforma de análisis conecta el servidor cliente al nodo de control mediante la red InfiniBand activa. Esto solo se aplica a la conexión; Si la red InfiniBand deja de funcionar durante una carga o una copia de seguridad, deberá reiniciar el proceso.  
  
Para satisfacer sus propios requisitos empresariales, también puede unir el servidor cliente a su propio grupo de trabajo o dominio de Windows que no sea de dispositivo.  
  
## <a name="step-1-obtain-the-appliance-infiniband-network-settings"></a><a name="Sec1"></a>Paso 1: obtener la configuración de red de la aplicación InfiniBand  
*Para obtener la configuración de red de la aplicación InfiniBand*  
  
1.  Inicie sesión en el nodo AD01 del dispositivo con la cuenta appliance_domain \Administrador.  
  
2.  En el nodo AD01 del dispositivo, abra el panel de control, seleccione red e Internet, seleccione Centro de redes y recursos compartidos * y, a continuación, seleccione cambiar la configuración del adaptador.  
  
3.  En la ventana conexiones de red, haga clic con el botón derecho en Team IB1 y seleccione Propiedades.  
  
    ![Conexiones de InfiniBand en el nodo de administración](media/network-teamib.png "Conexiones de InfiniBand en el nodo de administración")  
  
4.  En el ventana Propiedades del Protocolo de Internet versión 4 (TCP/IPv4), anote los valores para la **dirección IP** y la **máscara de subred**.  La dirección IP del nodo ** _domain\__-AD01 del dispositivo** es la dirección IP del servidor DNS del sistema de plataforma de análisis.  
  
5.  Repita los pasos 1-5 anteriores para el adaptador de TeamIB1 en el servidor ** _dominio\__-AD02 del dispositivo** .  
  
    ![Propiedades de InfiniBand 1 del nodo de administración de PDW](media/network-ip1-properties.png "Propiedades de InfiniBand 1 del nodo de administración de PDW")  
  
6.  Haga clic en Cancelar para cerrar la ventana.  
  
7.  Busque una dirección IP sin usar en la red TeamIB1 y escríbala.  
  
    Para buscar una dirección IP no utilizada, abra una ventana de comandos e intente hacer ping en las direcciones IP dentro del intervalo de direcciones del dispositivo. En este ejemplo, la dirección IP de la red TeamIB1 es 172.16.14.30. Busque una dirección IP que empiece por 172.16.14 que no se use. Por ejemplo, desde la línea de comandos, escriba "ping 172.16.14.254". Si la solicitud de ping no se realiza correctamente, la dirección IP está disponible.  
  
8.  Haga lo mismo para TeamIB2. En la ventana * conexiones de red, haga clic con el botón derecho en Team IB2 y seleccione Propiedades.  
  
9. En el ventana Propiedades del Protocolo de Internet versión 4 (TCP/IPv4), anote los valores para la dirección IP y la máscara de subred para TeamIB2.  
  
10. Repita los pasos 8-9 anteriores para el adaptador de TeamIB2 en el servidor appliance_domain-AD02.  
  
    ![Propiedades de TeamIB2](media/network-ip2-properties.png "Propiedades de TeamIB2")  
  
11. Busque una dirección IP sin usar en la red **TeamIB2** y escríbala.  
  
    Para buscar una dirección IP no utilizada, abra una ventana de comandos e intente hacer ping en las direcciones IP dentro del intervalo de direcciones del dispositivo. En este ejemplo, la dirección IP de la red TeamIB2 es 172.16.18.30. Busque una dirección IP que empiece por 172.16.18 que no se use. Por ejemplo, desde la línea de comandos, escriba "ping 172.16.18.254". Si la solicitud de ping no se realiza correctamente, la dirección IP está disponible.  
  
## <a name="step-2-configure-the-infiniband-network-adapter-settings-on-your-client-server"></a><a name="Sec2"></a>Paso 2: configurar la configuración del adaptador de red InfiniBand en el servidor cliente  

### <a name="notes"></a>Notas  
  
-   En estos pasos se muestra cómo registrar el servidor con los servidores DNS APS.  
  
-   Para satisfacer sus propias necesidades de red, también puede unir el servidor cliente a su propio grupo de trabajo o dominio de Windows que no sea de dispositivo.  
  
-   En las instrucciones se detallan los pasos para configurar dos adaptadores de red en cada servidor.  Si solo tiene un adaptador de red, seleccione una de las redes para configurar en el adaptador de red y, a continuación, agregue la segunda dirección IP de DNS como un servidor DNS alternativo.  
  
### <a name="to-configure-the-infiniband-network-adapter-settings-on-your-client-server"></a>Para configurar las opciones del adaptador de red InfiniBand en el servidor cliente  
  
1.  Inicie sesión como administrador de Windows para la carga, la copia de seguridad u otro servidor cliente en la red InfiniBand de la aplicación.  
  
2.  Abra el panel de control *, seleccione Centro de redes y recursos compartidos y, a continuación, seleccione cambiar la configuración del adaptador.  
  
### <a name="to-configure-the-first-network-adapter"></a>Para configurar el primer adaptador de red  
  
1.  En la ventana conexiones de red, haga clic con el botón secundario en una de las ranuras de red no identificadas para el adaptador Mellanox y seleccione Propiedades.  
  
    ![Seleccione las redes InfiniBand](media/network-connections.png "Seleccione las redes InfiniBand")  
  
2.  En el ventana Propiedades  
  
    1.  En la pestaña general, establezca la dirección IP en la dirección IP que comprobó como disponible en la prueba de ping para TeamIB1. Para los valores de ejemplo que se usan en este artículo, debe escribir 172.16.14.254.  
  
    2.  Establezca la máscara de subred en la máscara de subred que anotó para TeamIB1.  
  
    3.  Establezca el servidor DNS preferido en la dirección IP de TeamIB1 que anotó anteriormente en el nodo appliance_domain *-AD01.  
  
    4.  Establezca el servidor DNS alternativo en la dirección IP de TeamIB1 que anotó anteriormente en el nodo appliance_domain *-AD02.  
  
        ![Propiedades del adaptador de red InfiniBand 1](media/network-ib1-properties.png "SQL_Server_PDW_Network_IB1_properties")  
  
    5.  Haga clic en Aceptar para aplicar los cambios.  
  
### <a name="to-configure-the-second-network-adapter"></a>Para configurar el segundo adaptador de red  
  
1.  Omita esta sección si solo tiene un adaptador de red.  
  
2.  En la ventana conexiones de red, haga clic con el botón secundario en la segunda ranura de red no identificada para el adaptador Mellanox y seleccione Propiedades.  
  
    ![Seleccione las redes InfiniBand](media/network-connections.png "Seleccione las redes InfiniBand")  
  
3.  En el ventana Propiedades  
  
    1.  En la pestaña general, establezca la dirección IP en la dirección IP que comprobó como disponible en la prueba de ping para TeamIB2. Para los valores de ejemplo que se usan en este artículo, debe escribir 172.16.18.254.  
  
    2.  Establezca la máscara de subred en la máscara de subred que anotó para TeamIB2.  
  
    3.  Establezca el servidor DNS preferido en la dirección IP de TeamIB2 que anotó anteriormente en el nodo appliance_domain *-AD01.  
  
    4.  Establezca el servidor DNS alternativo en la dirección IP de TeamIB2 que anotó anteriormente en el nodo appliance_domain *-AD02.  
  
        > [!NOTE]  
        > Si solo tiene un adaptador de red, configure los servidores DNS preferidos y alternativos mediante el dispositivo AD01 TeamIB1 y el dispositivo AD02 TeamIB1 como los servidores DNS preferidos y alternativos, o use el dispositivo AD01 TeamIB2 y el dispositivo AD02 TeamIB2 como los servidores DNS preferidos y alternativos, en función de si la máquina virtual de AD ha conmutado por error.  
  
        ![Propiedades del adaptador de red InfiniBand 1](media/network-ib1-properties.png "Propiedades del adaptador de red InfiniBand 1")  
  
    5.  Haga clic en Aceptar para aplicar los cambios.  
  
### <a name="to-configure-the-dns-suffix"></a>Para configurar el sufijo DNS  
  
1.  En la ventana conexiones de red, haga clic con el botón secundario en una de las ranuras de red del adaptador Mellanox y seleccione Propiedades.  
  
2.  Haga clic en la configuración avanzada... botón.  
  
3.  En la ventana Configuración avanzada de TCP/IP, si la opción anexar estos sufijos DNS (en orden) no está atenuada, active la casilla denominada anexar estos sufijos DNS (en orden):, seleccione el sufijo de dominio del dispositivo y haga clic en Agregar.... El sufijo del dominio del dispositivo es`appliance_domain.local`  
  
4.  Si la opción anexar estos sufijos DNS (en orden): está atenuada, puede Agregar el dominio APS a este servidor mediante la modificación de la clave del registro HKEY_LOCAL_MACHINE \SOFTWARE\Policies\Microsoft\Windows NT\DNSClient.  
  
    ![Configuración de TCP/IP](media/network-tcpip.png "Configuración de TCP/IP")  
  
5.  Para una resolución más rápida de direcciones, se recomienda mover el sufijo del dispositivo a la parte superior de la lista.  
  
6.  Haga clic en Aceptar.  
  
7.  Ahora puede conectarse a la red InfiniBand de la aplicación mediante `PDW_region-SQLCTL01.appliance_domain.local`, o simplemente. `appliance_domain-SQLCTL01` La conexión se puede establecer más rápido si se conecta con el nombre completo y el sufijo DNS.  
  
    Ejemplos para un dispositivo denominado MyAPS con una región PDW de MyPDW:  
  
    -   MyPDW-SQLCTL01. MyAPS. local  
  
    -   MyPDW-SQLCTL01  
  
## <a name="see-also"></a>Consulte también  
[Adquisición y configuración de un servidor de carga](acquire-and-configure-loading-server.md)  
  
