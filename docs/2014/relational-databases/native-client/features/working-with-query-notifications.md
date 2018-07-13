---
title: Trabajar con las notificaciones de consulta | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client  - "database-engine" - "docset-sql-devref"
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], query notifications
- rowsets [SQL Server], notifications
- SQL Server Native Client, query notifications
- notifications [SQL Server Native Client]
- query notifications [SQL Server], SQL Server Native Client
- canceling rowset changes
- IRowsetNotify interface
- SQLNCLI, query notifications
- SQL Server Native Client OLE DB provider, query notifications
- consumer notification for rowset changes [SQL Server Native Client]
ms.assetid: 2f906fff-5ed9-4527-9fd3-9c0d27c3dff7
caps.latest.revision: 40
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a0f71aec8196f4815d8bc39ec9dd9dc0be443a01
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37417934"
---
# <a name="working-with-query-notifications"></a>Trabajar con notificaciones de consulta
  Las notificaciones de consulta se introdujeron con [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Las notificaciones de consulta, creadas a partir de la infraestructura de Service Broker introducida en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], permiten notificar a las aplicaciones si los datos han cambiado. Esta característica resulta especialmente útil para las aplicaciones que proporcionan una caché de información de una base de datos, como una aplicación web, y necesitan recibir notificaciones si se modifican los datos de origen.  
  
 Las notificaciones de consulta permiten al usuario solicitar notificaciones dentro de un período de tiempo de espera especificado si se modifican los datos subyacentes de una consulta. La solicitud de notificación especifica las opciones de notificación, entre las que se incluyen el nombre de servicio, el texto del mensaje y el valor de tiempo de espera para el servidor. Las notificaciones se entregan a través de una cola de Service Broker que las aplicaciones pueden sondear de cara a las notificaciones disponibles.  
  
 La sintaxis de la cadena de opciones de notificación de consulta es la siguiente:  
  
 `service=<service-name>[;(local database=<database> | broker instance=<broker instance>)]`  
  
 Por ejemplo:  
  
 `service=mySSBService;local database=mydb`  
  
 Las suscripciones de notificación duran más que el proceso que las inicia, de modo que una aplicación puede crear una suscripción de notificación y, a continuación, terminar. La suscripción seguirá siendo válida y la notificación se producirá si los datos cambian dentro del período de tiempo de espera especificado al crear la suscripción. Una notificación se identifica mediante la consulta ejecutada, las opciones de notificación y el texto del mensaje, y puede cancelarse estableciendo su valor de tiempo de espera en cero.  
  
 Las notificaciones se envían una sola vez. Para obtener notificaciones continuas de cambios de datos, debe crearse una nueva suscripción ejecutando de nuevo la consulta después de procesar cada notificación.  
  
 [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Las aplicaciones cliente nativas suelen reciben las notificaciones mediante el uso de la [!INCLUDE[tsql](../../../includes/tsql-md.md)] [recepción](/sql/t-sql/statements/receive-transact-sql) comando para leer las notificaciones de la cola asociada con el servicio especificado en las opciones de notificación.  
  
> [!NOTE]  
>  Los nombres de tabla deben calificarse en las consultas para las que se requiere notificación como, por ejemplo, `dbo.myTable`. Las tablas deben calificarse con nombres de dos partes. La suscripción no será válida si se usan nombres de tres o cuatro partes.  
  
 La infraestructura de notificación se crea a partir una característica de colas introducida en [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. Normalmente, las notificaciones generadas en el servidor se envían a través de estas colas para procesarse más adelante.  
  
 Para poder usar notificaciones de consulta, debe haber una cola y un servicio en el servidor. Pueden crearse utilizando código [!INCLUDE[tsql](../../../includes/tsql-md.md)] similar al siguiente:  
  
```  
CREATE QUEUE myQueue  
CREATE SERVICE myService ON QUEUE myQueue   
  
([http://schemas.microsoft.com/SQL/Notifications/PostQueryNotification])  
```  
  
> [!NOTE]  
>  El servicio debe usar el contrato predefinido `http://schemas.microsoft.com/SQL/Notifications/PostQueryNotification`, tal y como se indicó anteriormente.  
  
## <a name="sql-server-native-client-ole-db-provider"></a>Proveedor OLE DB de SQL Server Native Client  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor OLE DB de Native Client admite notificaciones al consumidor a la modificación del conjunto de filas. El consumidor recibe notificaciones en cada fase de modificación del conjunto de filas y ante cualquiera intento de modificación.  
  
> [!NOTE]  
>  Pasar una consulta de notificación al servidor con **ICommand:: Execute** es la única forma válida para suscribirse a notificaciones de consulta con el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] proveedor Native Client OLE DB.  
  
### <a name="the-dbpropsetsqlserverrowset-property-set"></a>Conjunto de propiedades DBPROPSET_SQLSERVERROWSET  
 Para admitir las notificaciones de consulta a través de OLE DB, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client agrega las siguientes propiedades nuevas al conjunto de propiedades DBPROPSET_SQLSERVERROWSET.  
  
|Nombre|Tipo|Descripción|  
|----------|----------|-----------------|  
|SSPROP_QP_NOTIFICATION_TIMEOUT|VT_UI4|Número de segundos que la notificación de consulta va a permanecer activa.<br /><br /> El valor predeterminado es 432000 segundos (5 días). El valor mínimo es 1 segundo y el valor máximo es 2^31-1 segundos.|  
|SSPROP_QP_NOTIFICATION_MSGTEXT|VT_BSTR|Texto del mensaje de la notificación. Lo define el usuario y no tiene ningún formato predefinido.<br /><br /> De forma predeterminada, la cadena está vacía. Puede especificarse un mensaje usando de 1 a 2000 caracteres.|  
|SSPROP_QP_NOTIFICATION_OPTIONS|VT_BSTR|Opciones de notificación de consulta. Se especifican en una cadena con *nombre*=*valor* sintaxis. El usuario es responsable de la creación del servicio y de la lectura de las notificaciones fuera de la cola.<br /><br /> El valor predeterminado es una cadena vacía.|  
  
 La suscripción de notificación se confirma siempre, independientemente de que la instrucción se haya ejecutado en una transacción de usuario o en una confirmación automática o de que la transacción en la que se haya ejecutado la instrucción se haya confirmado o revertido. La notificación del servidor se activa ante cualquiera de las siguientes condiciones de notificación no válida: cambio de esquema o datos subyacentes o cuando se alcanza el período de tiempo de espera, lo que ocurra antes. Los registros de notificación se eliminan en cuanto se activan. Por lo tanto, al recibir las notificaciones, la aplicación debe suscribirse de nuevo en caso de que deseen obtenerse actualizaciones posteriores.  
  
 Otra conexión o subproceso puede comprobar las notificaciones en la cola de destino. Por ejemplo:  
  
```  
WAITFOR (RECEIVE * FROM MyQueue);   // Where MyQueue is the queue name.   
```  
  
 Tenga en cuenta que seleccione * no eliminar la entrada de la cola, sin embargo recibir \* FROM sí. Esto detiene un subproceso del servidor si la cola está vacía. Si hay entradas en la cola en el momento de la llamada, se devuelven inmediatamente; de lo contrario, la llamada espera a que se realice una entrada en la cola.  
  
```  
RECEIVE * FROM MyQueue  
```  
  
 Si la cola está vacía, esta instrucción devuelve inmediatamente un conjunto de resultados vacío; de lo contrario, devuelve todas las notificaciones en cola.  
  
 Si los valores SSPROP_QP_NOTIFICATION_MSGTEXT y SSPROP_QP_NOTIFICATION_OPTIONS son distintos de NULL y no están vacíos, el encabezado TDS de notificación de consulta que contiene las tres propiedades definidas anteriormente se envía al servidor cada vez que se ejecuta el comando. Si alguno de estos valores es NULL (o está vacío), el encabezado no se envía y se produce un error DB_E_ERRORSOCCURRED (o DB_S_ERRORSOCCURRED si ambas propiedades están marcadas como opcionales) y el valor de estado se establece en DBPROPSTATUS_BADVALUE. La validación se produce durante la ejecución y preparación. De forma similar, se produce un error DB_S_ERRORSOCCURED cuando se establecen las propiedades de notificación de consulta para las conexiones a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] las versiones anteriores a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]. En este caso, el valor de estado es DBPROPSTATUS_NOTSUPPORTED.  
  
 Iniciar una suscripción no garantiza que los mensajes posteriores se entregarán correctamente. Además, no se realiza ninguna comprobación de validez del nombre de servicio especificado.  
  
> [!NOTE]  
>  La preparación de instrucciones no hará nunca que se inicie una suscripción; esta acción solo se consigue mediante la ejecución de instrucciones, y las notificaciones de consulta no se verán afectadas por el uso de los servicios principales de OLE DB.  
  
 Para obtener más información sobre el conjunto de propiedades DBPROPSET_SQLSERVERROWSET, vea [las propiedades del conjunto de filas y comportamientos](../../native-client-ole-db-rowsets/rowset-properties-and-behaviors.md).  
  
## <a name="sql-server-native-client-odbc-driver"></a>Controlador ODBC de SQL Server Native Client  
 El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client admite notificaciones de consulta a través de la adición de tres nuevos atributos a la [SQLGetStmtAttr](../../native-client-odbc-api/sqlgetstmtattr.md) y [SQLSetStmtAttr](../../native-client-odbc-api/sqlsetstmtattr.md) funciones:  
  
-   SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT  
  
-   SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS  
  
-   SQL_SOPT_SS_QUERYNOTIFICATION_TIMEOUT  
  
 Si los valores de SQL_SOPT_SS_QUERYNOTIFICATION_MSGTEXT y SQL_SOPT_SS_QUERYNOTIFICATION_OPTIONS son distintos de NULL, el encabezado TDS de notificación de consulta que contiene los tres atributos definidos anteriormente se enviará al servidor cada vez que se ejecute el comando. Si alguno de estos valores es NULL, el encabezado no se envía y se devuelve SQL_SUCCESS_WITH_INFO. La validación se produce en [SQLPrepare Function](http://go.microsoft.com/fwlink/?LinkId=59360), **SqlExecDirect**, y **SqlExecute**, todo se producirán errores si los atributos no son válidos. Del mismo modo, cuando estos atributos de notificación de consulta se establecen para versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)], se produce un error de ejecución con SQL_SUCCESS_WITH_INFO.  
  
> [!NOTE]  
>  La preparación de instrucciones no hará que se inicie nunca la suscripción; la ejecución de la instrucción sí que puede iniciar la suscripción.  
  
## <a name="special-cases-and-restrictions"></a>Restricciones y casos especiales  
 Las notificaciones no admiten los siguientes tipos de datos:  
  
-   `text`  
  
-   `ntext`  
  
-   `image`  
  
 Si se realiza una solicitud de notificación para una consulta que devuelve cualquiera de estos tipos, la notificación se activa inmediatamente, especificando que no fue posible la suscripción de notificación.  
  
 Cuando se realiza una solicitud de suscripción para un lote o procedimiento almacenado, se realiza una solicitud de suscripción independiente para cada instrucción del lote o procedimiento almacenado. Las instrucciones EXECUTE no registrarán ninguna notificación, pero enviarán la solicitud de notificación al comando ejecutado. Si se trata de un lote, el contexto se aplicará a las instrucciones ejecutadas y se aplicarán las mismas reglas descritas anteriormente.  
  
 El envío de una consulta de notificación enviada por el mismo usuario bajo el mismo contexto de base de datos y con la misma plantilla, los mismos valores de parámetro, el mismo identificador de notificación y la misma ubicación de entrega de una suscripción activa existente, renovará la suscripción existente, restableciendo el nuevo tiempo de espera especificado. Esto significa que si se solicita una notificación para consultas idénticas, solo se enviará una notificación. Esto se aplicaría a una consulta duplicada de un lote o si se llamó varias veces a una consulta de un procedimiento almacenado.  
  
## <a name="see-also"></a>Vea también  
 [Características de SQL Server Native Client](sql-server-native-client-features.md)  
  
  
