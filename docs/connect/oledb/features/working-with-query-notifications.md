---
title: Trabajar con notificaciones de consulta | Microsoft Docs
description: Trabajar con notificaciones de consulta en el controlador de OLE DB para SQL Server
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], query notifications
- rowsets [SQL Server], notifications
- OLE DB Driver for SQL Server, query notifications
- notifications [OLE DB Driver for SQL Server]
- query notifications [SQL Server], OLE DB Driver for SQL Server
- canceling rowset changes
- IRowsetNotify interface
- MSOLEDBSQL, query notifications
- OLE DB Driver for SQL Server, query notifications
- consumer notification for rowset changes [OLE DB Driver for SQL Server]
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 29aaab523b3a754c65b1b7a0312ceb5ea122f2d3
ms.sourcegitcommit: 1f222ef903e6aa0bd1b14d3df031eb04ce775154
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419318"
---
# <a name="working-with-query-notifications"></a>Trabajar con notificaciones de consulta

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

Las notificaciones de consulta se [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] introdujeron en y OLE DB controlador para SQL Server. Las notificaciones de consulta, creadas en la infraestructura de SQL Service Broker introducida en SQL Server 2005 (9.x), permiten notificar a las aplicaciones si los datos han cambiado. Esta característica resulta especialmente útil para las aplicaciones que proporcionan una caché de información de una base de datos, como una aplicación web, y necesitan recibir notificaciones si se modifican los datos de origen.

Mediante el uso de notificaciones de consulta, puede solicitar notificaciones dentro de un período de tiempo de espera especificado cuando cambien los datos subyacentes de una consulta. La solicitud especifica las opciones de notificación, entre las que se incluyen el nombre del servicio, el texto del mensaje y el valor de tiempo de espera para el servidor. Las notificaciones se entregan a través de una cola de Service Broker que las aplicaciones pueden sondear de cara a las notificaciones disponibles.

La sintaxis de la cadena de opciones de notificación de consulta es la siguiente:

`service=<service-name>[;(local database=<database> | broker instance=<broker instance>)]`

 Por ejemplo:

`service=mySSBService;local database=mydb`

Las suscripciones de notificación durar más el proceso que las inicia. Esto se debe a que una aplicación puede crear una suscripción de notificación y después finalizar. La suscripción sigue siendo válida y la notificación se produce si los datos cambian dentro del período de tiempo de espera especificado al crear la suscripción. Una notificación se identifica mediante la consulta ejecutada, las opciones de notificación y el texto del mensaje. Puede cancelarla estableciendo su valor de tiempo de espera en cero.

Las notificaciones se envían una sola vez. Para que se le notifiquen continuamente los cambios en los datos, cree una nueva suscripción volviendo a ejecutar la consulta después de procesar cada notificación.

OLE DB controlador para las aplicaciones de SQL Server normalmente recibe notificaciones mediante [!INCLUDE[tsql](../../../includes/tsql-md.md)] el comando [Receive](../../../t-sql/statements/receive-transact-sql.md) . Este comando se usa para leer las notificaciones de la cola asociada al servicio especificado en las opciones de notificación.

> [!NOTE]
> Los nombres de tabla deben calificarse en las consultas para las que se requiere notificación. Por ejemplo, `dbo.myTable`. Las tablas deben calificarse con nombres de dos partes. La suscripción no será válida si se usan nombres de tres o cuatro partes.

La infraestructura de notificación se crea a partir una característica de colas introducida en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Normalmente, las notificaciones generadas en el servidor se envían a través de estas colas para procesarse más adelante.

Para poder usar notificaciones de consulta, debe haber una cola y un servicio en el servidor. Se pueden crear mediante el [!INCLUDE[tsql](../../../includes/tsql-md.md)] comando, similar al siguiente:

```sql
CREATE QUEUE myQueue
CREATE SERVICE myService ON QUEUE myQueue
([https://schemas.microsoft.com/SQL/Notifications/PostQueryNotification])
```

> [!NOTE]
> El servicio debe usar el contrato predefinido, tal y como se indicó anteriormente.

## <a name="ole-db-driver-for-sql-server"></a>Controlador OLE DB para SQL Server

El controlador de OLE DB para SQL Server admite notificaciones de consumidor al modificar conjuntos de filas. El consumidor recibe una notificación en cada fase de modificación del conjunto de filas y ante cualquiera intento de cambio.

> [!NOTE]
> Pasar una consulta de notificación al servidor con **ICommand::Execute** es la única forma válida de suscribirse a notificaciones de consulta con el controlador OLE DB para SQL Server.

### <a name="dbpropsetsqlserverrowset-property-set"></a>Conjunto de propiedades DBPROPSET_SQLSERVERROWSET

Para admitir notificaciones de consulta a través de OLE DB, el controlador OLE DB for SQL Server agrega las siguientes propiedades nuevas al conjunto de propiedades `DBPROPSET_SQLSERVERROWSET`.

|Nombre|Tipo|Descripción|
|----------|----------|-----------------|
|SSPROP_QP_NOTIFICATION_TIMEOUT|VT_UI4|Número de segundos que la notificación de consulta va a permanecer activa.<br /><br /> El valor predeterminado es 432 000 segundos (5 días). El valor mínimo es 1 segundo y el valor máximo es 2^31-1 segundos.|
|SSPROP_QP_NOTIFICATION_MSGTEXT|VT_BSTR|Texto del mensaje de la notificación. Es un texto definido por el usuario y no tiene ningún formato predefinido.<br /><br /> De forma predeterminada, la cadena está vacía. Especifique un mensaje con entre 1 y 2000 caracteres.|
|SSPROP_QP_NOTIFICATION_OPTIONS|VT_BSTR|Opciones de notificación de consulta. Se especifican en una cadena con la sintaxis *nombre*=*valor*. El usuario es responsable de la creación del servicio y de la lectura de las notificaciones fuera de la cola.<br /><br /> El valor predeterminado es una cadena vacía.|

La suscripción de notificación siempre se confirma. Esto sucede independientemente de si la instrucción se ejecutó en una transacción de usuario o en autocommit o si la transacción en la que se ejecutó o revirtió la instrucción. La notificación del servidor se activa ante cualquiera de las siguientes condiciones de notificación no válida: cambio de esquema o datos subyacentes o cuando se alcanza el período de tiempo de espera, lo que ocurra antes. 

Los registros de notificación se eliminan en cuanto se activan. Por lo tanto, al recibir las notificaciones, la aplicación debe suscribirse de nuevo en caso de que deseen obtenerse actualizaciones posteriores.

Otra conexión o subproceso puede comprobar las notificaciones en la cola de destino. Por ejemplo:

```sql
WAITFOR (RECEIVE * FROM MyQueue); -- Where MyQueue is the queue name.
```

> [!NOTE]
> `SELECT *`no elimina la entrada de la cola. Sin embargo `RECEIVE * FROM` , sí lo hace. Esto detiene un subproceso del servidor si la cola está vacía. Si hay entradas en la cola en el momento de la llamada, se devuelven inmediatamente. De lo contrario, la llamada espera hasta que se realiza una entrada en la cola.

```sql
RECEIVE * FROM MyQueue
```

Esta instrucción devuelve inmediatamente un conjunto de resultados vacío si la cola está vacía. De lo contrario, devuelve todas las notificaciones de cola.

Si `SSPROP_QP_NOTIFICATION_MSGTEXT` y`SSPROP_QP_NOTIFICATION_OPTIONS` no son NULL y no están vacíos, el encabezado TDS de las notificaciones de consulta que contiene las tres propiedades definidas anteriormente se envían al servidor. Esto sucede cuando se ejecuta el comando. Si uno de ellos es null (o está vacío), no se envía el `DB_E_ERRORSOCCURRED` encabezado y se genera `DB_S_ERRORSOCCURRED` (o se genera, si las propiedades se marcan como opcionales). El valor de estado se establece en `DBPROPSTATUS_BADVALUE`. La validación se produce tras la ejecución y preparación. Del mismo modo, `DB_S_ERRORSOCCURED` se genera cuando las propiedades de la notificación de consulta se han configurado para conexiones a versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. En este caso, el valor de `DBPROPSTATUS_NOTSUPPORTED`estado es.

Iniciar una suscripción no garantiza que los mensajes posteriores se entregarán correctamente. Además, no se realiza ninguna comprobación de validez del nombre de servicio especificado.

> [!NOTE]
> La preparación de instrucciones nunca hará que se inicie la suscripción. Solo la ejecución de instrucciones permitirá la iniciación. Las notificaciones de consulta no se ven afectadas por el uso de OLE DB Core Services.

Para obtener más información sobre `DBPROPSET_SQLSERVERROWSET` el conjunto de propiedades, vea [propiedades y comportamientos de conjuntos de filas](../../oledb/ole-db-rowsets/rowset-properties-and-behaviors.md).

## <a name="see-also"></a>Vea también

[Controlador OLE DB para las características de SQL Server](../../oledb/features/oledb-driver-for-sql-server-features.md)
