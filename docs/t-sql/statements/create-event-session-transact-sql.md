---
title: "Crear sesión de eventos (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- CREATE EVENT SESSION
- SESSION
- EVENT SESSION
- SESSION_TSQL
- EVENT_SESSION_TSQL
- CREATE_EVENT_SESSION_TSQL
dev_langs: TSQL
helpviewer_keywords:
- event sessions [SQL Server]
- CREATE EVENT SESSION statement
ms.assetid: 67683027-2b0f-47aa-b223-604731af8b4d
caps.latest.revision: "65"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: ede0fb6715067bba3bafb1e77863483590d5f6a7
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="create-event-session-transact-sql"></a>CREATE EVENT SESSION (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Crea una sesión de eventos extendidos que identifica el origen de los eventos, los destinos de la sesión de eventos y las opciones de la sesión de eventos.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "icono de vínculo de tema") [convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CREATE EVENT SESSION event_session_name  
ON SERVER  
{  
    <event_definition> [ ,...n]  
    [ <event_target_definition> [ ,...n] ]  
    [ WITH ( <event_session_options> [ ,...n] ) ]  
}  
;  
  
<event_definition>::=  
{  
    ADD EVENT [event_module_guid].event_package_name.event_name   
         [ ( {   
                 [ SET { event_customizable_attribute = <value> [ ,...n] } ]  
                 [ ACTION ( { [event_module_guid].event_package_name.action_name [ ,...n] } ) ]  
                 [ WHERE <predicate_expression> ]  
        } ) ]  
}  
  
<predicate_expression> ::=   
{  
    [ NOT ] <predicate_factor> | {( <predicate_expression> ) }   
    [ { AND | OR } [ NOT ] { <predicate_factor> | ( <predicate_expression> ) } ]   
    [ ,...n ]  
}  
  
<predicate_factor>::=   
{  
    <predicate_leaf> | ( <predicate_expression> )  
}  
  
<predicate_leaf>::=  
{  
      <predicate_source_declaration> { = | < > | ! = | > | > = | < | < = } <value>   
    | [event_module_guid].event_package_name.predicate_compare_name ( <predicate_source_declaration>, <value> )   
}  
  
<predicate_source_declaration>::=   
{  
    event_field_name | ( [event_module_guid].event_package_name.predicate_source_name )  
}  
  
<value>::=   
{  
    number | 'string'  
}  
  
<event_target_definition>::=  
{  
    ADD TARGET [event_module_guid].event_package_name.target_name  
        [ ( SET { target_parameter_name = <value> [ ,...n] } ) ]  
}  
  
<event_session_options>::=  
{  
    [    MAX_MEMORY = size [ KB | MB ] ]  
    [ [,] EVENT_RETENTION_MODE = { ALLOW_SINGLE_EVENT_LOSS | ALLOW_MULTIPLE_EVENT_LOSS | NO_EVENT_LOSS } ]  
    [ [,] MAX_DISPATCH_LATENCY = { seconds SECONDS | INFINITE } ]  
    [ [,] MAX_EVENT_SIZE = size [ KB | MB ] ]  
    [ [,] MEMORY_PARTITION_MODE = { NONE | PER_NODE | PER_CPU } ]  
    [ [,] TRACK_CAUSALITY = { ON | OFF } ]  
    [ [,] STARTUP_STATE = { ON | OFF } ]  
}  
```  
  
## <a name="arguments"></a>Argumentos  
 *event_session_name*  
 Es el nombre definido por el usuario para identificar la sesión de eventos. *event_session_name* es alfanumérico, puede tener hasta 128 caracteres, deben ser únicos dentro de una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]y debe cumplir las reglas de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 Agregar eventos [ *event_module_guid* ]. *event_package_name*. *event_name*  
 Es el evento que se va a asociar con la sesión de eventos, donde:  
  
-   *event_module_guid* es el GUID para el módulo que contiene el evento.  
  
-   *event_package_name* es el paquete que contiene el objeto de acción.  
  
-   *event_name* es el objeto de evento.  
  
 Los eventos aparecen en la vista sys.dm_xe_objects como object_type "event".  
  
 Establezca { *event_customizable_attribute*= \<valor > [,...*n*] }  
 Permite establecer los atributos personalizables del evento. Atributos personalizables aparecen en la vista sys.dm_xe_object_columns como column_type 'customizable' y object_name = *event_name*.  
  
 ACCIÓN ({[*event_module_guid*]. *event_package_name*. *NombreDeAcción* [ **,**... *n*] })  
 Es la acción que se va a asociar a la sesión de eventos, donde:  
  
-   *event_module_guid* es el GUID para el módulo que contiene el evento.  
  
-   *event_package_name* es el paquete que contiene el objeto de acción.  
  
-   *NombreDeAcción* es el objeto de acción.  
  
 Las acciones aparecen en la vista sys.dm_xe_objects como object_type 'action'.  
  
 DONDE \<predicate_expression > especifica la expresión de predicado que se usa para determinar si debe procesarse un evento. Si \<predicate_expression > es true, se procesa el evento más acciones y los destinos de la sesión. Si \<predicate_expression > es false, el evento se quita la sesión antes de ser procesados por las acciones y los destinos de la sesión. Las expresiones de predicado se limitan a 3.000 caracteres, lo que limita los argumentos de cadena. 
  
 *event_field_name*  
 Es el nombre del campo de evento que identifica el origen del predicado.  
  
 [*event_module_guid*]. *event_package_name*. *predicate_source_name*  
 Es el nombre del origen del predicado global, donde:  
  
-   *event_module_guid* es el GUID para el módulo que contiene el evento.  
  
-   *event_package_name* es el paquete que contiene el objeto de predicado.  
  
-   *predicate_source_name* se define en la vista sys.dm_xe_objects como object_type "pred_source".  
  
 [*event_module_guid*]. *event_package_name*. *predicate_compare_name*  
 Es el nombre del objeto de predicado que se va a asociar al evento, donde:  
  
-   *event_module_guid* es el GUID para el módulo que contiene el evento.  
  
-   *event_package_name* es el paquete que contiene el objeto de predicado.  
  
-   *predicate_compare_name* es un origen global definido en la vista sys.dm_xe_objects como object_type 'pred_compare'.  
  
 *number*  
 Es cualquier tipo numérico, incluido **decimal**. Las limitaciones son la falta de memoria física disponible o un número demasiado grande para ser representado como un entero de 64 bits.  
  
 '*cadena*'  
 Una cadena ANSI o Unicode según lo requerido por la comparación de predicado. No se realiza ninguna conversión implícita de tipos de cadena para las funciones de comparación de predicado. Si se pasa el tipo incorrecto se producirá un error.  
  
 Agregar destino [*event_module_guid*]. *event_package_name*. *target_name*  
 Es el destino que se va a asociar con la sesión de eventos, donde:  
  
-   *event_module_guid* es el GUID para el módulo que contiene el evento.  
  
-   *event_package_name* es el paquete que contiene el objeto de acción.  
  
-   *target_name* es el destino. Los destinos aparecen en la vista sys.dm_xe_objects como object_type 'target'.  
  
 Establezca { *target_parameter_name*= \<valor > [, ...*n*] }  
 Establece un parámetro de destino. Parámetros de destino aparecen en la vista sys.dm_xe_object_columns como column_type 'customizable' y object_name = *target_name*.  
  
> [!IMPORTANT]  
>  Si usa el destino de búfer en anillo, le recomendamos que establezca el parámetro de destino max_memory en 2048 kilobytes (KB) para intentar evitar el truncamiento de los datos en la salida XML. Para obtener más información sobre cuándo utilizar los diferentes tipos de destino, vea [SQL Server Extended Events Targets](http://msdn.microsoft.com/library/e281684c-40d1-4cf9-a0d4-7ea1ecffa384).  
  
 CON ( \<event_session_options > [ ,... *n* ]) Especifica opciones que se va a usar con la sesión de eventos.  
  
 MAX_MEMORY =*tamaño* [KB | **MB** ]  
 Especifica la cantidad máxima de memoria que se asigna a la sesión para el almacenamiento en búfer de los eventos. El valor predeterminado es 4 MB. *tamaño* es un número entero y puede tener un valor de megabytes (MB) o kilobytes (KB).  
  
 EVENT_RETENTION_MODE = { **ALLOW_SINGLE_EVENT_LOSS** | ALLOW_MULTIPLE_EVENT_LOSS | NO_EVENT_LOSS}  
 Especifica el modo de retención de eventos usado para controlar las pérdidas de eventos.  
  
 **ALLOW_SINGLE_EVENT_LOSS**  
 Puede perderse un evento de la sesión. Se elimina un único evento solo cuando todos los búferes de eventos están llenos. La pérdida de un único evento cuando los búferes de eventos están llenos permite un rendimiento de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aceptable, al mismo tiempo que minimiza las pérdidas de datos en el flujo de eventos procesado.  
  
 ALLOW_MULTIPLE_EVENT_LOSS  
 En la sesión pueden perderse búferes completos de eventos que contienen varios eventos. El número de eventos perdidos depende del tamaño de memoria asignada a la sesión, el particionamiento de la memoria y el tamaño de los eventos en el búfer. Esta opción minimiza el impacto en el rendimiento del servidor si los búferes de eventos se llenan rápidamente, pero se puede perder un gran número de eventos de la sesión.  
  
 NO_EVENT_LOSS  
 No se permite ninguna pérdida de eventos. Esta opción asegura que se van a retener todos los eventos que aparezcan. Al utilizar esta opción, se obliga a todas las tareas que activan eventos a esperar hasta que haya espacio disponible en un búfer de eventos. Esto puede producir problemas detectables de rendimiento mientras la sesión de eventos está activa. Las conexiones de usuario pueden detenerse a la espera de que se quiten eventos del búfer.  
  
 MAX_DISPATCH_LATENCY = { *segundos* segundos | **Infinito** }  
 Especifica el tiempo que los eventos se almacenarán en memoria antes de enviarse a los destinos de la sesión de eventos. De forma predeterminada, este valor está establecido en 30 segundos.  
  
 *segundos* segundos  
 Tiempo, en segundos, que hay que esperar antes de que empiecen a vaciarse los búferes en los destinos. *segundos* es un número entero. El valor de latencia mínimo es de 1 segundo. Sin embargo, puede usarse el valor 0 para especificar la latencia INFINITE.  
  
 **INFINITO**  
 Los búferes se vacían en los destinos solo si están llenos o cuando se cierra la sesión de eventos.  
  
> [!NOTE]  
>  MAX_DISPATCH_LATENCY = 0 SECONDS es equivalente a MAX_DISPATCH_LATENCY = INFINITE.  
  
 MAX_EVENT_SIZE =*tamaño* [KB | **MB** ]  
 Especifica el tamaño máximo permitido para los eventos. MAX_EVENT_SIZE solo se debe establecer para permitir los eventos únicos mayores que MAX_MEMORY; al establecerlo en un valor menor que MAX_MEMORY, se producirá un error. *tamaño* es un número entero y puede tener un valor de megabytes (MB) o kilobytes (KB). Si *tamaño* se especifica en kilobytes, el tamaño mínimo permitido es 64 KB. Cuando se establece MAX_EVENT_SIZE, dos búferes de *tamaño* se crean además de MAX_MEMORY. Esto significa que la memoria total utilizada en búferes de eventos es MAX_MEMORY + 2 * MAX_EVENT_SIZE.  
  
 MEMORY_PARTITION_MODE = { **NONE** | PER_NODE | PER_CPU}  
 Especifica la ubicación en la que se van a crear los búferes de eventos.  
  
 **NONE**  
 Se crea un conjunto único de búferes dentro de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 PER_NODE  
 Se crea un único conjunto de búferes por cada nodo NUMA.  
  
 PER_CPU  
 Se crea un conjunto de búferes para cada CPU.  
  
 TRACK_CAUSALITY = {ON | **OFF** }  
 Especifica si se va a realizar el seguimiento de la causalidad. Si está habilitado, la causalidad permite correlacionar eventos relacionados en las diferentes conexiones con el servidor.  
  
 STARTUP_STATE = {ON | **OFF** }  
 Especifica si esta sesión de eventos se inicia automáticamente cuando se inicie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Si STARTUP_STATE = ON, la sesión de eventos se iniciará solo si se detiene SQL Server y se reinicia a continuación.  
  
 ON  
 La sesión de eventos se inicia en el inicio.  
  
 **OFF**  
 La sesión de eventos no se inicia en el inicio.  
  
## <a name="remarks"></a>Comentarios  
 El orden de prioridad de los operadores lógicos es NOT (el más alto), seguido de AND y OR.  
  
## <a name="permissions"></a>Permissions  
 Necesita el permiso ALTER ANY EVENT SESSION.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra cómo crear una sesión de eventos denominada `test_session`. En este ejemplo se agregan dos eventos y utiliza el Seguimiento de eventos para Windows.  
  
```  
IF EXISTS(SELECT * FROM sys.server_event_sessions WHERE name='test_session')  
    DROP EVENT session test_session ON SERVER;  
GO  
CREATE EVENT SESSION test_session  
ON SERVER  
    ADD EVENT sqlos.async_io_requested,  
    ADD EVENT sqlserver.lock_acquired  
    ADD TARGET package0.etw_classic_sync_target   
        (SET default_etw_session_logfile_path = N'C:\demo\traces\sqletw.etl' )  
    WITH (MAX_MEMORY=4MB, MAX_EVENT_SIZE=4MB);  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/alter-event-session-transact-sql.md)   
 [DROP EVENT SESSION &#40;Transact-SQL&#41;](../../t-sql/statements/drop-event-session-transact-sql.md)   
 [Sys.server_event_sessions &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-server-event-sessions-transact-sql.md)   
 [Sys.dm_xe_objects &#40; Transact-SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-objects-transact-sql.md)   
 [sys.dm_xe_object_columns &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-xe-object-columns-transact-sql.md)  
  
  

