---
title: Usar WQL con el proveedor WMI para eventos de servidor
description: Obtenga información sobre cómo las aplicaciones de administración tienen acceso a SQL Server eventos mediante el proveedor WMI para eventos de servidor mediante la emisión de instrucciones de lenguaje de consulta de WMI.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
helpviewer_keywords:
- queries [WMI]
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Server Events, WQL
ms.assetid: 58b67426-1e66-4445-8e2c-03182e94c4be
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 076c91605c245ad49f6c51a2a656d48c7dba2109
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545181"
---
# <a name="using-wql-with-the-wmi-provider-for-server-events"></a>Usar WQL con el proveedor WMI para eventos de servidor
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Las aplicaciones de administración tienen acceso a los eventos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que utilizan el proveedor WMI de eventos de servidor emitiendo instrucciones WQL (Lenguaje de consulta de WMI). WQL es un subconjunto simplificado de lenguaje de consulta estructurado (SQL) con algunas extensiones específicas de WMI. Al utilizar WQL, una aplicación recupera un tipo de evento con una instancia concreta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], una base de datos o un objeto de base de datos (el único objeto actualmente admitido es la cola). El proveedor WMI de eventos de servidor convierte la consulta en una notificación de eventos que se crea en la base de datos de destino para las notificaciones de eventos de ámbito de base de datos o de ámbito de objeto, o en la base de datos **maestra** para las notificaciones de eventos de ámbito de servidor.  
  
 Por ejemplo, considere la siguiente consulta WQL:  
  
```  
SELECT * FROM DDL_DATABASE_LEVEL_EVENTS WHERE DatabaseName = 'AdventureWorks'  
```  
  
 En esta consulta, el proveedor WMI intenta generar el equivalente de esta notificación de eventos en el servidor de destino:  
  
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
  
 El argumento de la cláusula `FROM` de la consulta WQL (`DDL_DATABASE_LEVEL_EVENTS`) puede ser cualquier evento válido en el que se pueda crear una notificación de eventos. Los argumentos de las cláusulas `SELECT` y `WHERE` pueden especificar cualquier propiedad de evento asociada a un evento o a su evento principal. Para obtener una lista de eventos y propiedades de evento válidos, vea [notificaciones de eventos (motor de base de datos)](https://technet.microsoft.com/library/ms182602.aspx).  
  
 El proveedor WMI de eventos de servidor admite explícitamente la sintaxis WQL siguiente. Se puede especificar sintaxis WQL adicional, pero no es específica de este proveedor y es analizada en su lugar por el servicio de host de WMI. Para obtener más información acerca del Lenguaje de consulta de WMI, vea la documentación de WQL en Microsoft Developer Network (MSDN).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SELECT { event_property [ ,...n ] | * }  
FROM event_type   
WHERE where_condition   
```  
  
## <a name="arguments"></a>Argumentos  
 *event_property*  
 Es una propiedad de un evento. Entre los ejemplos se incluyen **posttime**, **SPID**y **LoginName**. Busque todos los eventos enumerados en el [proveedor WMI para las clases y propiedades de eventos de servidor](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-classes-and-properties.md) para determinar qué propiedades contiene. Por ejemplo, el evento DDL_DATABASE_LEVEL_EVENTS contiene las propiedades **DatabaseName** y **username** . También hereda las propiedades **SQLInstance**, **LoginName**, **posttime**, **SPID**y **ComputerName** de sus eventos primarios.  
  
 **,** *... n*  
 Indica que *event_property* se pueden consultar varias veces, separadas por comas.  
  
 \*  
 Especifica que se consultan todas las propiedades asociadas a un evento.  
  
 *event_type*  
 Es cualquier evento sobre el que se puede crear una notificación de eventos. Para obtener una lista de eventos disponibles, vea [proveedor WMI para las clases y propiedades de eventos de servidor](https://technet.microsoft.com/library/ms186449.aspx). Tenga en cuenta que los nombres de *tipo de evento* corresponden al mismo *event_type*  |  *event_group* que se pueden especificar al crear manualmente una notificación de eventos mediante la creación de una notificación de eventos. Entre los ejemplos de *tipos de evento* se incluyen CREATE_TABLE, LOCK_DEADLOCK, DDL_USER_EVENTS y TRC_DATABASE.  
  
> [!NOTE]  
>  Determinados procedimientos almacenados del sistema que realizan operaciones similares a DDL también pueden activar notificaciones de eventos. Pruebe las notificaciones de eventos para determinar su respuesta a los procedimientos almacenados del sistema que se ejecutan. Por ejemplo, la instrucción CREATE TYPE y **sp_addtype** procedimiento almacenado activarán una notificación de eventos que se crea en un evento de CREATE_TYPE. Sin embargo, el **sp_rename** procedimiento almacenado no activa ninguna notificación de eventos. Para obtener más información, vea[eventos DDL](../../relational-databases/triggers/ddl-events.md).  
  
 *where_condition*  
 Es un predicado de consulta de la cláusula WHERE formado por nombres de *event_property* y operadores lógicos y de comparación. El *where_condition* determina el ámbito en el que se registra la notificación de eventos correspondiente en la base de datos de destino. También puede actuar como un filtro para tener como destino un esquema o un objeto determinado desde el que consultar *event_type.* Para obtener más información, vea la sección Comentarios más adelante en este tema.  
  
 Solo `=` se puede usar el operando junto con **DatabaseName**, **SchemaName**y **objectname**. Otras expresiones no se pueden utilizar con estas propiedades de evento.  
  
## <a name="remarks"></a>Observaciones  
 La *where_condition* de la sintaxis del proveedor WMI para eventos de servidor determina lo siguiente:  
  
-   El ámbito por el que el proveedor intenta recuperar el *event_type*especificado: el nivel de servidor, el nivel de base de datos o el nivel de objeto (el único objeto actualmente admitido es la cola). Finalmente, este ámbito determina el tipo de notificación de eventos creado en la base de datos de destino. Este proceso efectuó una llamada al registro de notificación de eventos.  
  
-   La base de datos, el esquema y el objeto, según corresponda, en que registrarse.  
  
 El proveedor WMI de eventos de servidor usa un algoritmo ascendente de tipo "el primero que sea válido" para generar un ámbito lo más restringido posible para la EVENT NOTIFICATION subyacente. El algoritmo intenta minimizar la actividad interna en el tráfico del servidor y de la red entre la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el proceso de host de WMI. El proveedor examina el *event_type* especificado en la cláusula FROM y las condiciones de la cláusula WHERE e intenta registrar la notificación de eventos subyacente con el ámbito más restringido posible. Si el proveedor no se puede registrar en el ámbito más restringido, intenta registrarse en ámbitos superiores consecutivamente hasta que el registro resulta satisfactorio finalmente. Si llega al ámbito superior en el nivel de servidor y se produce un error, devuelve un error al consumidor.  
  
 Por ejemplo, si se especifica DatabaseName =**'** AdventureWorks **'** en la cláusula WHERE, el proveedor intenta registrar una notificación de eventos en la [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] base de datos. Si la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] existe y el cliente que realiza la llamada tiene los permisos necesarios para crear una notificación de eventos en [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], el registro es satisfactorio. De lo contrario, se intenta registrar la notificación de eventos en el nivel de servidor. El registro es satisfactorio si el cliente de WMI tiene los permisos necesarios. Sin embargo, en esta situación, los eventos no se devuelven al cliente hasta que no se haya creado la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
 El *where_condition* también puede actuar como filtro para limitar además la consulta a una base de datos, un esquema o un objeto específicos. Por ejemplo, considere la siguiente consulta WQL:  
  
```  
SELECT * FROM ALTER_TABLE   
WHERE DatabaseName = 'AdventureWorks' AND SchemaName = 'Sales'   
    AND ObjectType='Table' AND ObjectName = 'SalesOrderDetail'  
```  
  
 Dependiendo del resultado del proceso de registro, esta consulta WQL se puede registrar en el nivel de base de datos o de servidor. Sin embargo, aunque se registre en el nivel del servidor, el proveedor filtra finalmente los eventos `ALTER_TABLE` que no se aplican a la tabla `AdventureWorks.Sales.SalesOrderDetail`. En otras palabras, el proveedor devuelve solamente las propiedades de los eventos `ALTER_TABLE` que se producen en esa tabla concreta.  
  
 Si se especifica una expresión compuesta como `DatabaseName='AW1'` OR `DatabaseName='AW2'`, se intenta registrar una notificación de eventos única en el ámbito de servidor en lugar de dos notificaciones de eventos independientes. El registro es satisfactorio si el cliente que realiza la llamada tiene permisos.  
  
 Si `SchemaName='X' AND ObjectType='Y' AND ObjectName='Z'` se especifican todos en la `WHERE` cláusula, se intenta registrar la notificación de eventos directamente en el objeto `Z` en el esquema `X` . El registro es satisfactorio si el cliente que realiza la llamada tiene permisos. Tenga en cuenta que, actualmente, los eventos de nivel de objeto solo se admiten en las colas y solo en el *event_type*de QUEUE_ACTIVATION.  
  
 Observe que no todos los eventos se pueden consultar en cualquier ámbito determinado. Por ejemplo, una consulta WQL en un evento de seguimiento como Lock_Deadlock o un grupo de eventos de seguimiento como TRC_LOCKS, solo se puede registrar en el nivel de servidor. De forma similar, el evento CREATE_ENDPOINT y el grupo de eventos DDL_ENDPOINT_EVENTS también se pueden registrar solo en el nivel de servidor. Para obtener más información acerca del ámbito adecuado para registrar eventos, consulte [diseño de notificaciones de eventos](https://technet.microsoft.com/library/ms175854\(v=sql.105\).aspx). Un intento de registrar una consulta WQL cuyo *event_type* solo se puede registrar en el nivel de servidor siempre se realiza en el nivel de servidor. El registro es satisfactorio si el cliente de WMI tiene permisos. De lo contrario, se devuelve un error al cliente. En algunos casos, sin embargo, puede utilizar todavía la cláusula WHERE como filtro para los eventos en el nivel de servidor basados en las propiedades que corresponden al evento. Por ejemplo, muchos eventos de seguimiento tienen una propiedad **DatabaseName** que se puede usar en la cláusula WHERE como filtro.  
  
 Las notificaciones de eventos de ámbito de servidor se crean en la base de datos **maestra** y se pueden consultar los metadatos mediante la vista de catálogo [Sys. server_event_notifications](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md) .  
  
 Las notificaciones de eventos de ámbito de base de datos o de ámbito de objeto se crean en la base de datos especificada y se pueden consultar para los metadatos mediante la vista de catálogo [Sys. event_notifications](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md) . (Debe anteponer a la vista de catálogo el nombre de la base de datos correspondiente).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-querying-for-events-at-the-server-scope"></a>A. Consultar eventos en el ámbito de servidor  
 La consulta WQL siguiente recupera todas las propiedades de evento de los eventos de seguimiento `SERVER_MEMORY_CHANGE` que se produzcan en la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
SELECT * FROM SERVER_MEMORY_CHANGE  
```  
  
### <a name="b-querying-for-events-at-the-database-scope"></a>B. Consultar eventos en el ámbito de base de datos  
 La consulta WQL siguiente recupera propiedades de evento concretas de los eventos que se produzcan en la base de datos `AdventureWorks` y existan bajo el grupo de eventos `DDL_DATABASE_LEVEL_EVENTS`.  
  
```  
SELECT SPID, SQLInstance, DatabaseName FROM DDL_DATABASE_LEVEL_EVENTS   
WHERE DatabaseName = 'AdventureWorks'   
```  
  
### <a name="c-querying-for-events-at-the-database-scope-filtering-by-schema-and-object"></a>C. Consultar eventos en el ámbito de base de datos, filtrar por esquema y objeto  
 La consulta siguiente recupera todas las propiedades de evento de los eventos `ALTER_TABLE` que se produzcan en la tabla `AdventureWorks.Sales.SalesOrderDetail`.  
  
```  
SELECT * FROM ALTER_TABLE   
WHERE DatabaseName = 'AdventureWorks' AND SchemaName = 'Sales'   
    AND ObjectType='Table' AND ObjectName = 'SalesOrderDetail'  
```  
  
## <a name="see-also"></a>Consulte también  
 [Conceptos del proveedor WMI para eventos de servidor](https://technet.microsoft.com/library/ms180560.aspx)   
 [Notificaciones de eventos (motor de base de datos)](https://technet.microsoft.com/library/ms182602.aspx)  
  
  
