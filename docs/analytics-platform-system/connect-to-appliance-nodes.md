---
title: Conectarse a los nodos del dispositivo
description: En este artículo se explican las distintas formas de conectarse a cada nodo en el dispositivo de sistema de plataforma de análisis.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: e1182d174e3281fda944c0b6490b114d4b6f2244
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401244"
---
# <a name="connect-to-appliance-nodes-in-analytics-platform-system"></a>Conexión a los nodos del dispositivo en Analytics Platform System
En este artículo se explican las distintas formas de conectarse a cada nodo en el dispositivo de sistema de plataforma de análisis.  
  
## <a name="connecting-with-hadoop"></a>Conexión con Hadoop  
Antes de usar Hadoop con PDW de SQL Server, pida al administrador de la aplicación que instale el Java Runtime Environment en PDW de SQL Server. Para obtener instrucciones, consulte Configuración de la [conectividad de polybase con datos externos &#40;Analytics Platform System&#41;](configure-polybase-connectivity-to-external-data.md) en la guía de operaciones del dispositivo.  
  
## <a name="connecting-to-appliance-nodes"></a><a name="ConnectingToIndividualNodes"></a>Conexión a nodos del dispositivo  
Solo se tiene acceso a cada uno de los nodos del dispositivo directamente en escenarios de uso específicos y por tipos de usuario específicos. En la tabla siguiente se enumeran los nodos de cada dispositivo y los escenarios en los que los usuarios se conectarán directamente a ese nodo.  
  
<!-- MISSING LINKS For information on the purpose of each node, see [Understanding SQL Server PDW &#40;SQL Server PDW&#41;](../sqlpdw/understanding-sql-server-pdw-sql-server-pdw.md).  -->  

> [!WARNING]  
> Cambiar la configuración de la base de datos o de la tabla en los nodos de control o de proceso sin el consentimiento explícito del equipo de producto o del equipo de soporte técnico al cliente de APS puede dejar el dispositivo APS fuera del soporte técnico.
  
|||  
|-|-|  
|**Nodo**|**Escenarios de acceso**|  
|Nodo de control|Use un explorador Web para tener acceso a la consola de administración de, que se ejecuta en el nodo de control. Para más información, consulte [supervisión del dispositivo mediante la consola de administración &#40;Analytics Platform System&#41;](monitor-the-appliance-by-using-the-admin-console.md).<br /><br />Todas las herramientas y aplicaciones cliente se conectan al nodo de control, independientemente de si la conexión usa Ethernet o InfiniBand.<br /><br />Para configurar una conexión Ethernet al nodo de control, use la dirección IP del clúster del nodo de control y el puerto **17001**. Por ejemplo, "192.168.0.1, 17001".<br /><br />Para configurar una conexión de InfiniBand al nodo de control, use <strong> *appliance_domain*-SQLCTL01</strong> y el puerto **17001**. Mediante el uso <strong>de *appliance_domain*-SQLCTL01</strong>, el servidor DNS del dispositivo conectará el servidor a la red InfiniBand activa. Para configurar el servidor que no es de dispositivo para usarlo, consulte [configuración de adaptadores de red InfiniBand](configure-infiniband-network-adapters.md).<br /><br />El administrador del dispositivo se conecta al nodo de control para realizar las operaciones de administración. Por ejemplo, el administrador del dispositivo realiza las siguientes operaciones desde el nodo de control:<br /><br />Configure Analytics Platform System con la herramienta de configuración **dwconfig. exe** .|  
|Nodo de ejecución|El nodo de control dirige las conexiones del nodo de proceso. Las direcciones IP de los nodos de proceso nunca se escriben en los comandos de la aplicación como parámetros.<br /><br />En el caso de carga, copia de seguridad, copia de tabla remota y Hadoop, PDW de SQL Server envía o recibe datos directamente en paralelo entre los nodos de proceso y los nodos o servidores que no son del dispositivo. Estas aplicaciones se conectan con PDW de SQL Server mediante la conexión al nodo de control y, a continuación, el nodo de control dirige PDW de SQL Server para establecer la comunicación entre los nodos de proceso y el servidor que no es de la aplicación.<br /><br />Por ejemplo, estas operaciones de transferencia de datos se producen en paralelo con conexiones directas a los nodos de proceso:<br /><br />Cargando del servidor de carga a PDW de SQL Server.<br /><br />Realizar una copia de seguridad de una base de datos de PDW de SQL Server en el servidor de copia de seguridad.<br /><br />Restaurar una base de datos del servidor de copia de seguridad en PDW de SQL Server.<br /><br />Consultar datos de Hadoop desde PDW de SQL Server.<br /><br />Exportar datos de PDW de SQL Server a una tabla de Hadoop externa.<br /><br />Copiar una tabla de PDW de SQL Server en una base de datos de SQL Server SMP remota.|  
  
## <a name="connecting-to-the-ethernet-and-infiniband-networks"></a>Conexión a las redes Ethernet e InfiniBand  
Los servidores remotos se pueden conectar a través de la red InfiniBand del dispositivo o a través de la red Ethernet. Por motivos de rendimiento, la carga de servidores, servidores de copia de seguridad y servidores que reciben datos a través de **Create REMOTE Table como instrucciones SELECT** , normalmente transfieren datos a través de la red InfiniBand del dispositivo.  
  
Puede configurar servidores que no son de aplicación para que pertenezcan a su propio grupo de trabajo de cliente o dominio y, a continuación, usar su propia red de cliente para conectarse a esos servidores y transferir datos a ellos. Además, los servidores que no son dispositivos conectados al dispositivo InfiniBand tienen la opción de transferir datos entre sí a través de la red InfiniBand de la aplicación. Tenga cuidado con esto, ya que puede ralentizar el rendimiento de PDW de SQL Server.  
  
Por ejemplo, esta instrucción agrega credenciales de red para realizar copias de seguridad a través de InfiniBand a un servidor de copia de seguridad que tiene una dirección IP InfiniBand 192.168.0.1. El dominio del dispositivo es *mypdw*y la instrucción se realiza desde el servidor de copia de seguridad. Antes de ejecutar esta instrucción, debe rellenar sus propios parámetros.  
  
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
  
