---
title: Usar WQL con el proveedor WMI para eventos de servidor | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- queries [WMI]
- query language [WMI]
- WMI Query Language [WMI]
- WQL [WMI]
- WMI Provider for Server Events, WQL
ms.assetid: 58b67426-1e66-4445-8e2c-03182e94c4be
caps.latest.revision: 36
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 05731087009d1f1ab444c7f740889ee441bb99a6
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="using-wql-with-the-wmi-provider-for-server-events"></a>Usar WQL con el proveedor WMI para eventos de servidor
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Las aplicaciones de administración tienen acceso a los eventos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que utilizan el proveedor WMI de eventos de servidor emitiendo instrucciones WQL (Lenguaje de consulta de WMI). WQL es un subconjunto simplificado de lenguaje de consulta estructurado (SQL) con algunas extensiones específicas de WMI. Al utilizar WQL, una aplicación recupera un tipo de evento con una instancia concreta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], una base de datos o un objeto de base de datos (el único objeto actualmente admitido es la cola). El proveedor WMI para eventos de servidor convierte la consulta en una notificación de eventos que se crea en la base de datos de destino para las notificaciones de eventos de ámbito de base de datos o del ámbito del objeto, o en la **maestro** base de datos de evento con ámbito de servidor notificaciones.  
  
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
  
 El argumento de la cláusula `FROM` de la consulta WQL (`DDL_DATABASE_LEVEL_EVENTS`) puede ser cualquier evento válido en el que se pueda crear una notificación de eventos. Los argumentos de las cláusulas `SELECT` y `WHERE` pueden especificar cualquier propiedad de evento asociada a un evento o a su evento principal. Para obtener una lista de eventos y propiedades de eventos válidos, consulte [notificaciones de eventos (motor de base de datos)](http://technet.microsoft.com/library/ms182602.aspx).  
  
 El proveedor WMI de eventos de servidor admite explícitamente la sintaxis WQL siguiente. Se puede especificar sintaxis WQL adicional, pero no es específica de este proveedor y es analizada en su lugar por el servicio de host de WMI. Para obtener más información acerca del Lenguaje de consulta de WMI, vea la documentación de WQL en Microsoft Developer Network (MSDN).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SELECT { event_property [ ,...n ] | * }  
FROM event_type   
WHERE where_condition   
```  
  
## <a name="arguments"></a>Argumentos  
 *event_property*  
 Es una propiedad de un evento. Algunos ejemplos son **PostTime**, **SPID**, y **LoginName**. Buscar todos los eventos enumerados en [proveedor WMI de clases de eventos de servidor y propiedades](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-classes-and-properties.md) para determinar qué propiedades contienen. Por ejemplo, el evento DDL_DATABASE_LEVEL_EVENTS contiene el **DatabaseName** y **nombre de usuario** propiedades. También hereda la **SQLInstance**, **LoginName**, **PostTime**, **SPID**, y **NombreDeEquipo** propiedades de sus eventos principales.  
  
 **,** *.. .n*  
 Indica que *event_property* se pueden consultar varias veces, separados por comas.  
  
 \*  
 Especifica que se consultan todas las propiedades asociadas a un evento.  
  
 *event_type*  
 Es cualquier evento sobre el que se puede crear una notificación de eventos. Para obtener una lista de los eventos disponibles, vea [proveedor WMI de clases de eventos de servidor y propiedades](http://technet.microsoft.com/library/ms186449.aspx). Tenga en cuenta que *tipo de evento* nombres corresponden al mismo *event_type* | *event_group* que se puede especificar al crear manualmente una notificación de eventos mediante el uso de CREATE EVENT NOTIFICATION. Ejemplos de *tipo de evento* incluye CREATE_TABLE, LOCK_DEADLOCK, DDL_USER_EVENTS y TRC_DATABASE.  
  
> [!NOTE]  
>  Determinados procedimientos almacenados del sistema que realizan operaciones similares a DDL también pueden activar notificaciones de eventos. Pruebe las notificaciones de eventos para determinar su respuesta a los procedimientos almacenados del sistema que se ejecutan. Por ejemplo, la instrucción CREATE TYPE y **sp_addtype** procedimiento almacenado activarán una notificación de eventos que se crea en un evento CREATE_TYPE. Sin embargo, el **sp_rename** procedimiento almacenado no activa ninguna notificación de eventos. Para obtener más información, consulte[eventos DDL](../../relational-databases/triggers/ddl-events.md).  
  
 *where_condition*  
 Es un predicado de consulta de cláusula WHERE compuesto por *event_property* nombres y lógicos y operadores de comparación. El *where_condition* determina el ámbito en el que se registra la notificación de eventos correspondiente en la base de datos de destino. También pueden actuar como un filtro para identificar un esquema u objeto determinado desde el que consulta *event_type.* Para obtener más información, vea la sección Comentarios más adelante en este tema.  
  
 Solo el `=` operando puede usarse junto con **DatabaseName**, **SchemaName**, y **ObjectName**. Otras expresiones no se pueden utilizar con estas propiedades de evento.  
  
## <a name="remarks"></a>Comentarios  
 El *where_condition* del proveedor WMI para eventos de servidor sintaxis determina lo siguiente:  
  
-   El ámbito mediante el cual el proveedor intenta recuperar especificado *event_type*: el nivel de servidor, el nivel de base de datos o el nivel de objeto (el único objeto actualmente admitido es la cola). Finalmente, este ámbito determina el tipo de notificación de eventos creado en la base de datos de destino. Este proceso efectuó una llamada al registro de notificación de eventos.  
  
-   La base de datos, el esquema y el objeto, según corresponda, en que registrarse.  
  
 El proveedor WMI de eventos de servidor usa un algoritmo ascendente de tipo "el primero que sea válido" para generar un ámbito lo más restringido posible para la EVENT NOTIFICATION subyacente. El algoritmo intenta minimizar la actividad interna en el tráfico del servidor y de la red entre la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el proceso de host de WMI. El proveedor examina el *event_type* especificados en la cláusula FROM y las condiciones de la cláusula WHERE e intenta registrar la EVENT NOTIFICATION subyacente con el ámbito más restringido posible. Si el proveedor no se puede registrar en el ámbito más restringido, intenta registrarse en ámbitos superiores consecutivamente hasta que el registro resulta satisfactorio finalmente. Si llega al ámbito superior en el nivel de servidor y se produce un error, devuelve un error al consumidor.  
  
 Por ejemplo, si DatabaseName =**'**AdventureWorks**'**se especifica en la cláusula WHERE, el proveedor intenta registrar una notificación de eventos en el [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] base de datos. Si la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] existe y el cliente que realiza la llamada tiene los permisos necesarios para crear una notificación de eventos en [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)], el registro es satisfactorio. De lo contrario, se intenta registrar la notificación de eventos en el nivel de servidor. El registro es satisfactorio si el cliente de WMI tiene los permisos necesarios. Sin embargo, en esta situación, los eventos no se devuelven al cliente hasta que no se haya creado la base de datos [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].  
  
 El *where_condition* también pueden actuar como un filtro para limitar la consulta a un objeto, esquema o base de datos específica. Por ejemplo, considere la siguiente consulta WQL:  
  
```  
SELECT * FROM ALTER_TABLE   
WHERE DatabaseName = 'AdventureWorks' AND SchemaName = 'Sales'   
    AND ObjectType='Table' AND ObjectName = 'SalesOrderDetail'  
```  
  
 Dependiendo del resultado del proceso de registro, esta consulta WQL se puede registrar en el nivel de base de datos o de servidor. Sin embargo, aunque se registre en el nivel del servidor, el proveedor filtra finalmente los eventos `ALTER_TABLE` que no se aplican a la tabla `AdventureWorks.Sales.SalesOrderDetail`. En otras palabras, el proveedor devuelve solamente las propiedades de los eventos `ALTER_TABLE` que se producen en esa tabla concreta.  
  
 Si se especifica una expresión compuesta como `DatabaseName='AW1'` OR `DatabaseName='AW2'`, se intenta registrar una notificación de eventos única en el ámbito de servidor en lugar de dos notificaciones de eventos independientes. El registro es satisfactorio si el cliente que realiza la llamada tiene permisos.  
  
 Si `SchemaName='X' AND ObjectType='Y' AND ObjectName='Z'` se especifica en el `WHERE` cláusula, se realiza un intento para registrar la notificación de eventos directamente en el objeto `Z` en esquema `X`. El registro es satisfactorio si el cliente que realiza la llamada tiene permisos. Tenga en cuenta que actualmente, se admiten los eventos de nivel de objeto solo en las colas y solo para el QUEUE_ACTIVATION *event_type*.  
  
 Observe que no todos los eventos se pueden consultar en cualquier ámbito determinado. Por ejemplo, una consulta WQL en un evento de seguimiento como Lock_Deadlock o un grupo de eventos de seguimiento como TRC_LOCKS, solo se puede registrar en el nivel de servidor. De forma similar, el evento CREATE_ENDPOINT y el grupo de eventos DDL_ENDPOINT_EVENTS también se pueden registrar solo en el nivel de servidor. Para obtener más información acerca del ámbito adecuado para registrar los eventos, vea [diseñar notificaciones de eventos](http://technet.microsoft.com/library/ms175854\(v=sql.105\).aspx). Un intento de registrar un WQL consulta cuya *event_type* solo se pueden registrar en el servidor de nivel siempre se realiza en el nivel de servidor. El registro es satisfactorio si el cliente de WMI tiene permisos. De lo contrario, se devuelve un error al cliente. En algunos casos, sin embargo, puede utilizar todavía la cláusula WHERE como filtro para los eventos en el nivel de servidor basados en las propiedades que corresponden al evento. Por ejemplo, muchos eventos de seguimiento tienen un **DatabaseName** propiedad que puede usarse en la cláusula WHERE como filtro.  
  
 Las notificaciones de eventos con ámbito de servidor se crean en el **maestro** la base de datos y se puede consultar para los metadatos mediante el uso de la [sys.server_event_notifications](../../relational-databases/system-catalog-views/sys-server-event-notifications-transact-sql.md) vista de catálogo.  
  
 Ámbito de base de datos o las notificaciones de eventos de ámbito de objeto se crean en la base de datos especificada y se pueden consultar para los metadatos mediante el uso de la [sys.event_notifications](../../relational-databases/system-catalog-views/sys-event-notifications-transact-sql.md) vista de catálogo. (Debe anteponer a la vista de catálogo el nombre de la base de datos correspondiente).  
  
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
  
## <a name="see-also"></a>Vea también  
 [Proveedor WMI para eventos conceptos del servidor](http://technet.microsoft.com/library/ms180560.aspx)   
 [Notificaciones de eventos (motor de base de datos)](http://technet.microsoft.com/library/ms182602.aspx)  
  
  
