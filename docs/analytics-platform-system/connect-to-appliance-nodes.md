---
title: 'Conectarse al dispositivo nodos: Analytics Platform System | Microsoft Docs'
description: En este artículo se explica las diversas maneras de conectarse a cada nodo en el dispositivo de Analytics Platform System.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 873ce3cf5ad2707979d66068b3930d6f59f7057c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66186798"
---
# <a name="connect-to-appliance-nodes-in-analytics-platform-system"></a>Conectarse a los nodos del dispositivo en Analytics Platform System
En este artículo se explica las diversas maneras de conectarse a cada nodo en el dispositivo de Analytics Platform System.  
  
## <a name="connecting-with-hadoop"></a>Conectando con Hadoop  
Antes de usar Hadoop con PDW de SQL Server, pida al administrador de dispositivo para instalar el Java Runtime Environment en PDW de SQL Server. Para obtener instrucciones, consulte [configurar la conectividad de PolyBase a datos externos &#40;Analytics Platform System&#41; ](configure-polybase-connectivity-to-external-data.md) en la Guía de operaciones de dispositivo.  
  
## <a name="ConnectingToIndividualNodes"></a>Conectarse a los nodos del dispositivo  
Cada uno de los nodos del dispositivo se acceda directa solo en escenarios de uso específicos y los tipos de usuario específico. En la tabla siguiente se enumera cada nodo de dispositivo y los escenarios en que los usuarios se conectarán directamente a ese nodo.  
  
<!-- MISSING LINKS For information on the purpose of each node, see [Understanding SQL Server PDW &#40;SQL Server PDW&#41;](../sqlpdw/understanding-sql-server-pdw-sql-server-pdw.md).  -->  

> [!WARNING]  
> Cambiar la configuración de base de datos o una tabla en nodos de proceso o de Control sin consentimiento explícito del equipo del producto o el equipo de soporte técnico de cliente de puntos de acceso puede provocar que el dispositivo APS fuera del soporte técnico.
  
|||  
|-|-|  
|**Node**|**Escenarios de acceso**|  
|Nodo de control|Use un explorador web para tener acceso a la consola de administración, que se ejecuta en el nodo de Control. Para obtener más información, consulte [supervisar el dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md).<br /><br />Todas las herramientas y aplicaciones cliente conectan al nodo de Control, independientemente de si usa la conexión Ethernet o InfiniBand.<br /><br />Para configurar una conexión Ethernet en el nodo de Control, use la dirección IP del clúster de nodo de Control y el puerto **17001**. Por ejemplo, "192.168.0.1,17001".<br /><br />Para configurar una conexión de InfiniBand para el nodo de Control, use  <strong>*appliance_domain*-SQLCTL01</strong> y el puerto **17001**. Mediante el uso de  <strong>*appliance_domain*-SQLCTL01</strong>, el servidor DNS del dispositivo conectará el servidor a la red InfiniBand activada. Para configurar el servidor que no sea de dispositivo para poder usar este, consulte [configurar adaptadores de red de InfiniBand](configure-infiniband-network-adapters.md).<br /><br />El administrador del dispositivo se conecta al nodo de Control para realizar operaciones de administración. Por ejemplo, el administrador del dispositivo realiza las siguientes operaciones desde el nodo de Control:<br /><br />Configuración de Analytics Platform System con el **dwconfig.exe** herramienta de configuración.|  
|Nodo de proceso|Las conexiones de nodo se dirigen al nodo de Control de proceso. Las direcciones IP de los nodos de proceso nunca se introducen en comandos de la aplicación como parámetros.<br /><br />Para la carga, copia de seguridad, copia de la tabla remota y Hadoop, SQL Server PDW envíen o reciban datos directamente en paralelo entre los nodos de proceso y los nodos que no sea de dispositivo o los servidores. Estas aplicaciones se conectarán con PDW de SQL Server mediante la conexión al nodo de Control y, a continuación, el nodo de Control dirige PDW de SQL Server para establecer la comunicación entre los nodos de proceso y el servidor que no sea de dispositivo.<br /><br />Por ejemplo, estas operaciones de transferencia de datos tienen lugar en paralelo con conexiones directas a los nodos de proceso:<br /><br />Carga desde el servidor de carga para PDW de SQL Server.<br /><br />Copia de seguridad de una base de datos de PDW de SQL Server en el servidor de copia de seguridad.<br /><br />Restaurar una base de datos desde el servidor de copia de seguridad en PDW de SQL Server.<br /><br />Consultar datos de Hadoop de PDW de SQL Server.<br /><br />Exportar datos de PDW de SQL Server a una tabla externa de Hadoop.<br /><br />Copiar una tabla de PDW de SQL Server a una base de datos de SQL Server de SMP remoto.|  
  
## <a name="connecting-to-the-ethernet-and-infiniband-networks"></a>Conectarse a la tarjeta Ethernet y redes InfiniBand  
Pueden conectarse a servidores remotos a través de la red de InfiniBand de dispositivo o a través de la red Ethernet. Por motivos de rendimiento, la carga de los servidores, servidores de copia de seguridad y recibir datos a través de los servidores **crear REMOTE TABLE AS SELECT** instrucciones, normalmente transferir datos a través de la red InfiniBand de dispositivo.  
  
Puede configurar los servidores que no sea de dispositivo para que pertenezcan a su propio dominio o grupo de trabajo de cliente y, a continuación, usar su propia red de cliente para conectarse a esos servidores y transferir datos a ellos. Además, los servidores que no sea de dispositivo conectados al equipo InfiniBand, tienen la opción para transferir datos entre sí a través de la red InfiniBand de dispositivo; Tenga cuidado con esto puesto que puede ralentizar el rendimiento de SQL Server PDW.  
  
Por ejemplo, esta instrucción agrega credenciales de red para realizar copias de seguridad a través de InfiniBand a un servidor de copia de seguridad que tiene una dirección de InfiniBand IP 192.168.0.1. Es el dominio del equipo *mypdw*, y la instrucción se realiza desde el servidor de copia de seguridad. Antes de ejecutar esta instrucción, debe rellenar en sus propios parámetros.  
  
```  
sqlcmd -S "mypdw-sqlctl01,17001" -U sa -P password -I -Q "exec sp_pdw_add_network_credentials '192.168.0.1', 'mypdw\Administrator', 'password'"  
```  
  
Por ejemplo, un comando de carga se iniciará con lo siguiente:  
  
```  
dwloader -S mypdw-SQLCTL01  
```  
  
<!-- MISSING LINKS ## See Also  
[Configure an External Windows System To Receive Remote Table Copies Using InfiniBand &#40;SQL Server PDW&#41;](../sqlpdw/configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband-sql-server-pdw.md)  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  -->  
  
