---
title: Conectarse a los nodos de dispositivo (Analytics Platform System)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/05/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: f975aa91-c816-4b29-89bf-923ab5b4abb4
caps.latest.revision: 19
ms.openlocfilehash: 9b95bc8285625170c9c9b4a91eeae99dcd3907a5
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/06/2018
---
# <a name="connect-to-appliance-nodes"></a>Conectarse a los nodos de dispositivo
En este tema se explica las diversas formas para conectarse a cada nodo en el dispositivo de sistema de la plataforma de análisis.  
  
## <a name="connecting-with-hadoop"></a>Conectar con Hadoop  
Antes de usar Hadoop con SQL Server PDW, pida al administrador de dispositivo para instalar el entorno de tiempo de ejecución de Java en PDW de SQL Server. Para obtener instrucciones, consulte [configurar PolyBase conectividad a datos externos &#40;Analytics Platform System&#41; ](configure-polybase-connectivity-to-external-data.md) en la Guía de operaciones de dispositivo.  
  
## <a name="ConnectingToIndividualNodes"></a>Conectarse a los nodos de dispositivo  
Cada uno de los nodos de dispositivo se acceda directa solo en escenarios de uso específicos y tipos de usuario específico. En la tabla siguiente se enumera los escenarios en los que los usuarios se conectarán directamente a ese nodo y cada nodo de dispositivo.  
  
<!-- MISSING LINKS For information on the purpose of each node, see [Understanding SQL Server PDW &#40;SQL Server PDW&#41;](../sqlpdw/understanding-sql-server-pdw-sql-server-pdw.md).  -->  
  
|||  
|-|-|  
|**Node**|**Escenarios de acceso**|  
|Nodo de control|Use un explorador web para tener acceso a la consola de administración, que se ejecuta en el nodo de Control. Para obtener más información, consulte [supervisar el dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md).<br /><br />Todas las herramientas y las aplicaciones cliente se conectan al nodo de Control, con independencia de si usa la conexión Ethernet o InfiniBand.<br /><br />Para configurar una conexión Ethernet al nodo de Control, use la dirección IP del clúster de nodo de Control y el puerto **17001**. Por ejemplo, "192.168.0.1,17001".<br /><br />Para configurar una conexión de InfiniBand al nodo de Control, use ***appliance_domain *-SQLCTL01** y el puerto **17001**. Mediante el uso de ***appliance_domain *-SQLCTL01**, el servidor DNS del dispositivo conectará el servidor a la red InfiniBand active. Para configurar el servidor no sea de dispositivo para poder usar este, consulte [configurar adaptadores de red InfiniBand](configure-infiniband-network-adapters.md).<br /><br />El Administrador de equipo se conecta al nodo de Control para realizar operaciones de administración. Por ejemplo, el administrador del equipo realiza las siguientes operaciones desde el nodo de Control:<br /><br />Configurar el sistema de la plataforma de análisis con la **dwconfig.exe** herramienta de configuración.|  
|Nodo de proceso|Calcular las conexiones de nodo se dirigen al nodo de Control. Las direcciones IP de los nodos de proceso nunca se introducen en comandos de la aplicación como parámetros.<br /><br />Para cargar, copia de seguridad, copia de la tabla remota y Hadoop, SQL Server PDW envíen o reciban datos directamente en paralelo entre los nodos de proceso y el dispositivo no son nodos o los servidores. Estas aplicaciones se conectan con PDW de SQL Server mediante la conexión al nodo de Control y, a continuación, el nodo de Control dirige PDW de SQL Server para establecer una comunicación entre los nodos de proceso y el servidor no sea de dispositivo.<br /><br />Por ejemplo, estas operaciones de transferencia de datos se producen en paralelo con conexiones directas a los nodos de proceso:<br /><br />Cargando desde el servidor de carga para PDW de SQL Server.<br /><br />Copias de seguridad de una base de datos de SQL Server PDW en el servidor de copia de seguridad.<br /><br />Restaurar una base de datos desde el servidor de copia de seguridad en SQL Server PDW.<br /><br />Consultar datos de Hadoop de PDW de SQL Server.<br /><br />Exportar datos de SQL Server PDW a una tabla externa de Hadoop.<br /><br />Si copia una tabla de SQL Server PDW una base de datos remota de SQL Server de SMP.|  
  
## <a name="connecting-to-the-ethernet-and-infiniband-networks"></a>Conectarse a la tarjeta Ethernet y redes InfiniBand  
Pueden conectarse a servidores remotos a través de la red de InfiniBand de dispositivo o a través de la red Ethernet. Por motivos de rendimiento, la carga de servidores, servidores de copia de seguridad y los servidores que reciben datos a través de **CREATE remoto TABLE AS SELECT** instrucciones, normalmente transferir datos a través de la red InfiniBand de dispositivo.  
  
Puede configurar los servidores no sea de dispositivo para que pertenezcan a su propio dominio o grupo de trabajo de cliente y, a continuación, usar su propia red de cliente para conectarse a los servidores y transferir datos a ellos. Además, los servidores no sea de dispositivo conectados al dispositivo InfiniBand tienen la opción para transferir datos entre sí a través de la red InfiniBand dispositivo; Tenga cuidado con esto porque puede reducir el rendimiento de SQL Server PDW.  
  
Por ejemplo, esta instrucción agrega credenciales de red para realizar copias de seguridad a través de InfiniBand a un servidor de copia de seguridad que tiene una dirección de InfiniBand IP 192.168.0.1. Es el dominio del equipo *mypdw*, y la instrucción se realiza desde el servidor de copia de seguridad. Antes de ejecutar esta instrucción, debe rellenar sus propios parámetros.  
  
```  
sqlcmd -S "mypdw-sqlctl01,17001" -U sa -P password -I -Q "exec sp_pdw_add_network_credentials '192.168.0.1', 'mypdw\Administrator', 'password'"  
```  
  
Por ejemplo, un comando de carga se iniciará con lo siguiente:  
  
```  
dwloader –S mypdw-SQLCTL01  
```  
  
<!-- MISSING LINKS ## See Also  
[Configure an External Windows System To Receive Remote Table Copies Using InfiniBand &#40;SQL Server PDW&#41;](../sqlpdw/configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
