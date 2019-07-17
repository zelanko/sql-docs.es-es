---
title: Descripción del proveedor WMI para eventos de servidor | Microsoft Docs
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 56cacefdcc0afd1ff2b17986658b27d7f4eddb07
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68139221"
---
# <a name="understanding-the-wmi-provider-for-server-events"></a>Descripción del proveedor WMI para eventos de servidor
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  El proveedor WMI para eventos de servidor le permite utilizar el Instrumental de administración de Windows (WMI) para supervisar eventos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El proveedor trabaja convirtiendo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un objeto WMI administrado. Todos los eventos que puedan generar una notificación de eventos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se aprovechan en el WMI que utiliza el proveedor. Además, como una aplicación de administración que interactúa con el WMI, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede responder a estos eventos aumentando el ámbito de los eventos cubiertos por el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en versiones anteriores.  
  
 Las aplicaciones de administración como el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pueden utilizar el proveedor WMI para eventos de servidor para obtener acceso a los eventos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] emitiendo instrucciones WQL (Lenguaje de consulta de WMI). WQL es un subconjunto simplificado de lenguaje de consulta estructurado (SQL) con algunas extensiones específicas de WMI. Al utilizar WQL, una aplicación recupera un tipo de evento en una base de datos u objeto de base de datos específicos. El proveedor WMI para eventos de servidor convierte la consulta en una notificación de eventos, creando eficazmente una notificación de eventos en la base de datos de destino. Para obtener más información sobre cómo funcionan las notificaciones de eventos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [proveedor WMI para eventos de conceptos del servidor](https://technet.microsoft.com/library/ms180560.aspx). Se muestran los eventos que se pueden consultar en [proveedor WMI de clases de eventos de servidor y las propiedades](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-classes-and-properties.md).  
  
 Cuando se produce un evento que desencadena la notificación de eventos para enviar un mensaje, el mensaje pasa a un servicio de destino predefinidas en **msdb** que se denomina **SQL/Notifications/ProcessWMIEventProviderNotification/v1.0**. El servicio coloca el evento en una cola predefinida de **msdb** que se denomina **WMIEventProviderNotificationQueue**. (El servicio y la cola son creados dinámicamente por el proveedor cuando se conecta primero al [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].) El proveedor, a continuación, lee los datos del evento de la cola y lo transforma managed object Format (MOF) antes de devolverlo a la aplicación. En la siguiente ilustración se muestra este proceso.  
  
 ![Diagrama de flujo del proveedor WMI para eventos de servidor](../../relational-databases/wmi-provider-server-events/media/wmi-provider-functional-spec.gif "diagrama de flujo del proveedor WMI para eventos de servidor")  
  
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
  
 En este ejemplo, `SQLWEP_76CF38C1_18BB_42DD_A7DC_C8820155B0E9` es un identificador de [!INCLUDE[tsql](../../includes/tsql-md.md)] compuesto por el prefijo `SQLWEP_` y un GUID. `SQLWEP` crea un nuevo GUID para cada identificador. El valor `A7E5521A-1CA6-4741-865D-826F804E5135` en el `TO SERVICE` cláusula es el GUID que identifica la instancia de broker en la **msdb** base de datos.  
  
 Para obtener más información sobre cómo trabajar con WQL, vea [usar WQL con el proveedor WMI para eventos de servidor](https://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx).  
  
 Las aplicaciones de administración dirigen el proveedor WMI de eventos de servidor a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conectándose a un espacio de nombres WMI definido por el proveedor. El servicio WMI de Windows asigna este espacio de nombres al archivo DLL del proveedor, Sqlwep.dll, y lo carga en memoria. El proveedor administra un espacio de nombres WMI para eventos de servidor para cada instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], y el formato es: \\ \\.\\ *raíz*\Microsoft\SqlServer\ServerEvents\\*instance_name*, donde *instance_name* el valor predeterminado es MSSQLSERVER. Para obtener más información acerca de cómo conectarse a un espacio de nombres WMI para una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [usar WQL con el proveedor WMI para eventos de servidor](https://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx).  
  
 La DLL del proveedor, Sqlwep.dll, solo se carga una vez en el servicio de host de WMI del sistema operativo del servidor, con independencia del número de instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que haya en el servidor.  
  
 Para obtener un ejemplo de un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplicación de administración de agente que usa el proveedor WMI para eventos de servidor, consulte [ejemplo: Creación de una alerta del Agente SQL Server mediante el proveedor WMI para eventos de servidor](https://technet.microsoft.com/library/ms186385.aspx). Para obtener un ejemplo de una aplicación de administración que utiliza el proveedor WMI para eventos de servidor en código administrado, consulte [ejemplo: Usar el proveedor de eventos WMI en código administrado](https://technet.microsoft.com/library/ms179315.aspx). También hay información más acerca de WMI en el [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
## <a name="see-also"></a>Vea también  
 [Conceptos del proveedor WMI para eventos de servidor](https://technet.microsoft.com/library/ms180560.aspx)  
  
  
