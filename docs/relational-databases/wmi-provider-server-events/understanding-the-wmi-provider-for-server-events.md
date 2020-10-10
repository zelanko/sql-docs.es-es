---
title: Descripción del proveedor WMI para eventos de servidor
description: Obtenga información acerca de cómo el proveedor WMI para eventos de servidor utiliza Instrumental de administración de Windows para supervisar eventos mediante la activación de SQL Server en un objeto WMI administrado.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- architecture [WMI]
- SQL Server Agent [WMI]
- WMI Provider for Server Events, about WMI Provider for Server Events
ms.assetid: 8fd7bd18-76d0-4b28-8fee-8ad861441ab2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 6187c97f246a8c4eb445fb0afe224922b2c57f03
ms.sourcegitcommit: 783b35f6478006d654491cb52f6edf108acf2482
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/09/2020
ms.locfileid: "91891965"
---
# <a name="understanding-the-wmi-provider-for-server-events"></a>Descripción del proveedor WMI para eventos de servidor
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  El proveedor WMI para eventos de servidor le permite utilizar el Instrumental de administración de Windows (WMI) para supervisar eventos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El proveedor trabaja convirtiendo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un objeto WMI administrado. Todos los eventos que puedan generar una notificación de eventos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se aprovechan en el WMI que utiliza el proveedor. Además, como una aplicación de administración que interactúa con el WMI, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede responder a estos eventos aumentando el ámbito de los eventos cubiertos por el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en versiones anteriores.  
  
 Las aplicaciones de administración como el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden utilizar el proveedor WMI para eventos de servidor para obtener acceso a los eventos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] emitiendo instrucciones WQL (Lenguaje de consulta de WMI). WQL es un subconjunto simplificado de lenguaje de consulta estructurado (SQL) con algunas extensiones específicas de WMI. Al utilizar WQL, una aplicación recupera un tipo de evento en una base de datos u objeto de base de datos específicos. El proveedor WMI para eventos de servidor convierte la consulta en una notificación de eventos, creando eficazmente una notificación de eventos en la base de datos de destino. Para obtener más información sobre cómo funcionan las notificaciones de eventos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vea [conceptos del proveedor WMI para eventos de servidor](./wmi-provider-for-server-events-concepts.md). Los eventos que se pueden consultar se enumeran en el [proveedor WMI para las clases y propiedades de eventos de servidor](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-classes-and-properties.md).  
  
 Cuando se produce un evento que desencadena la notificación de eventos para enviar un mensaje, el mensaje se dirige a un servicio de destino predefinido en **msdb** que se denomina **SQL/Notifications/ProcessWMIEventProviderNotification/v 1.0**. El servicio coloca el evento en una cola predefinida en **msdb** que se denomina **WMIEventProviderNotificationQueue**. El proveedor crea dinámicamente el servicio y la cola cuando se conecta por primera vez a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A continuación, el proveedor Lee los datos de evento de esta cola y los transforma en Managed Object Format (MOF) antes de devolverlos a la aplicación. En la siguiente ilustración se muestra este proceso.  
  
 ![Diagrama de flujo del proveedor WMI para eventos del servidor](../../relational-databases/wmi-provider-server-events/media/wmi-provider-functional-spec.gif "Diagrama de flujo del proveedor WMI para eventos del servidor")  
  
 Por ejemplo, considere la siguiente consulta WQL:  
  
```  
SELECT * FROM DDL_DATABASE_LEVEL_EVENTS  
WHERE DatabaseName = 'AdventureWorks'  
```  
  
 En respuesta a esta consulta, el proveedor WMI de eventos de servidor crea la notificación de eventos equivalente en la base de datos de destino:  
  
```  
USE AdventureWorks ;  
GO  
CREATE EVENT NOTIFICATION SQLWEP_76CF38C1_18BB_42DD_A7DC_C8820155B0E9  
    ON DATABASE  
    WITH FAN_IN  
    FOR DDL_DATABASE_LEVEL_EVENTS  
    TO SERVICE  
        'SQL/Notifications/ProcessWMIEventProviderNotification/v1.0',   
        'A7E5521A-1CA6-4741-865D-826F804E5135';  
GO  
```  
  
 En este ejemplo, `SQLWEP_76CF38C1_18BB_42DD_A7DC_C8820155B0E9` es un identificador de [!INCLUDE[tsql](../../includes/tsql-md.md)] compuesto por el prefijo `SQLWEP_` y un GUID. `SQLWEP` crea un nuevo GUID para cada identificador. El valor `A7E5521A-1CA6-4741-865D-826F804E5135` de la `TO SERVICE` cláusula es el GUID que identifica la instancia del agente en la base de datos **msdb** .  
  
 Para obtener más información sobre cómo trabajar con WQL, vea [usar WQL con el proveedor WMI para eventos de servidor](https://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx).  
  
 Las aplicaciones de administración dirigen el proveedor WMI de eventos de servidor a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conectándose a un espacio de nombres WMI definido por el proveedor. El servicio WMI de Windows asigna este espacio de nombres al archivo DLL del proveedor, Sqlwep.dll, y lo carga en memoria. El proveedor administra un espacio de nombres WMI para eventos de servidor para cada instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el formato es: \\ \\ . \\ *raíz*\Microsoft\SqlServer\ServerEvents \\ *instance_name*, donde *instance_name* tiene como valor predeterminado MSSQLSERVER. Para obtener más información sobre cómo conectarse a un espacio de nombres WMI para una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vea [usar WQL con el proveedor WMI para eventos de servidor](https://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx).  
  
 La DLL del proveedor, Sqlwep.dll, solo se carga una vez en el servicio de host de WMI del sistema operativo del servidor, con independencia del número de instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que haya en el servidor.  
  
 Para obtener un ejemplo de una [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplicación de administración de agentes que usa el proveedor WMI para eventos de servidor, vea [ejemplo: crear una alerta de Agente SQL Server mediante el proveedor WMI para eventos de servidor](./sample-creating-a-sql-server-agent-alert-with-the-wmi-provider.md). Para obtener un ejemplo de una aplicación de administración que utiliza el proveedor WMI para eventos de servidor en código administrado, vea [ejemplo: usar el proveedor de eventos WMI en código administrado](./sample-using-the-wmi-event-provider-with-the-net-framework.md). También hay más información disponible sobre WMI en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK de.  
  
## <a name="see-also"></a>Consulte también  
 [Conceptos del proveedor WMI para eventos de servidor](./wmi-provider-for-server-events-concepts.md)  
  
