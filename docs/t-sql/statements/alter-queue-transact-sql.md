---
title: ALTER QUEUE (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 05/01/2016
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- ALTER_QUEUE_TSQL
- ALTER QUEUE
dev_langs:
- TSQL
helpviewer_keywords:
- number of queue readers
- modifying queues
- ALTER QUEUE statement
- queue readers [SQL Server]
- queues [Service Broker], modifying
- unavailable queues [SQL Server]
- activation stored procedures [Service Broker]
ms.assetid: d54aa325-8761-4cd4-8da7-acf33df12296
caps.latest.revision: 49
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9320e2f2af4bccd07ee8b255166b513c0b204a76
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="alter-queue-transact-sql"></a>ALTER QUEUE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia las propiedades de una cola.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
ALTER QUEUE <object>   
   queue_settings  
   | queue_action  
[ ; ]  
  
<object> : :=  
{  
    [ database_name. [ schema_name ] . | schema_name. ]  
        queue_name  
}   
  
<queue_settings> : :=  
WITH  
   [ STATUS = { ON | OFF } [ , ] ]  
   [ RETENTION = { ON | OFF } [ , ] ]  
   [ ACTIVATION (  
       { [ STATUS = { ON | OFF } [ , ] ]   
         [ PROCEDURE_NAME = <procedure> [ , ] ]  
         [ MAX_QUEUE_READERS = max_readers [ , ] ]  
         [ EXECUTE AS { SELF | 'user_name'  | OWNER } ]  
       |  DROP }  
          ) [ , ]]  
         [ POISON_MESSAGE_HANDLING (  
          STATUS = { ON | OFF } )  
         ]   
  
<queue_action> : :=  
   REBUILD [ WITH <query_rebuild_options> ]  
   | REORGANIZE [ WITH (LOB_COMPACTION = { ON | OFF } ) ]  
   | MOVE TO { file_group | "default" }  
  
<procedure> : :=  
{  
    [ database_name. [ schema_name ] . | schema_name. ]  
        stored_procedure_name  
}  
  
<queue_rebuild_options> : :=  
{  
   ( MAXDOP = max_degree_of_parallelism )  
}  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *database_name* (objeto)  
 Es el nombre de la base de datos que contiene la cola que se va a cambiar. Si no *database_name* es siempre el valor predeterminado es la base de datos actual.  
  
 *schema_name* (objeto)  
 Nombre del esquema al que pertenece la nueva cola. Si no *schema_name* es siempre el valor predeterminado es el esquema predeterminado para el usuario actual.  
  
 *nombre_de_cola*  
 Es el nombre de la cola que se va a cambiar.  
  
 STATUS (cola)  
 Especifica si la cola está disponible (ON) o no (OFF). Cuando la cola no está disponible, no pueden agregarse mensajes a ella ni tampoco quitarse.  
  
 RETENTION  
 Especifica la configuración de retención para la cola. Si RETENTION = ON, todos los mensajes enviados o recibidos relativos a conversaciones que utilizan esta cola se retendrán hasta que las conversaciones finalicen. Esto permite retener mensajes con fines de auditoría o realizar transacciones de compensación si un error se produce  
  
> [!NOTE]  
>  Si se establece RETENTION = ON puede reducir el rendimiento. Esta configuración solo debe utilizarse si es necesario satisfacer el acuerdo de nivel de servicio para la aplicación.  
  
 ACTIVATION  
 Especifica información acerca del procedimiento almacenado que se activa para procesar mensajes que llegan a esta cola.  
  
 STATUS (activación)   
 Especifica si una cola activa o no el procedimiento almacenado. Si STATUS = ON, la cola inicia el procedimiento almacenado especificado con PROCEDURE_NAME cuando el número de procedimientos que se ejecutan actualmente es menor que MAX_QUEUE_READERS y cuando los mensajes llegan a la cola antes de que los procedimientos almacenados reciban mensajes. Si STATUS = OFF, la cola no activa el procedimiento almacenado.  
  
 Volver a generar [WITH \<queue_rebuild_options >]  
 **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Vuelve a generar todos los índices de la tabla interna de la cola. Use esta función cuando están experimentando problemas de fragmentación debido a una carga elevada. MAXDOP es la cola compatible sola opción rebuild. Volver a generar siempre es una operación sin conexión.  
  
 REORGANIZAR [CON (LOB_COMPACTION = {ON | DESACTIVADO})]  
 **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Reorganizar todos los índices de la tabla interna de la cola.   
A diferencia de REORGANIZACIÓN en tablas de usuario, REORGANIZE en una cola siempre se realiza como una operación sin conexión porque los bloqueos de nivel de página se deshabilitarán explícitamente en las colas.  
  
> [!TIP]  
>  Para obtener instrucciones generales sobre la fragmentación del índice, una vez fragmentación entre 5 y 30%, reorganizar el índice. Cuando la fragmentación es superior al 30%, vuelva a generar el índice. Sin embargo, estos números son solo para obtener instrucciones generales como punto de partida para su entorno. Para determinar la cantidad de fragmentación del índice, use [sys.dm_db_index_physical_stats &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md) -vea el ejemplo G de ese artículo para obtener ejemplos.  
  
 Mover a { *file_group* | "default"}  
 **Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Mueve la tabla interna de cola (con sus índices) a un grupo de archivos especificado por el usuario.  El nuevo grupo de archivos no debe ser de solo lectura.  
  
 Procedure_name = \<procedimiento >  
 Especifica el nombre del procedimiento almacenado que se va a activar cuando la cola contiene mensajes para procesar. Este valor debe ser un identificador de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 *database_name* (procedimiento)  
 Nombre de la base de datos que contiene el procedimiento almacenado.  
  
 *schema_name* (procedimiento)  
 Nombre del esquema que tiene la propiedad del procedimiento almacenado.  
  
 *stored_procedure_name*  
 Es el nombre del procedimiento almacenado.  
  
 MAX_QUEUE_READERS =*max_reader*  
 Especifica el número máximo de instancias del procedimiento almacenado de activación que la cola inicia simultáneamente. El valor de *max_readers* debe ser un número entre 0 y 32767.  
  
 EXECUTE AS  
 Especifica la cuenta de usuario de base de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la que se ejecuta el procedimiento almacenado de activación. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe poder comprobar los permisos de este usuario en el momento en que la cola inicia el procedimiento almacenado. Para un usuario de dominio de Windows, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe estar conectado al dominio y debe poder validar los permisos del usuario especificado cuando se active el procedimiento o la activación genere un error. En usuarios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el servidor siempre puede comprobar los permisos.  
  
 SELF  
 Especifica que el procedimiento almacenado se ejecuta como el usuario actual. Es la entidad de seguridad de base de datos que ejecuta esta instrucción ALTER QUEUE.  
  
 '*nombre_usuario*'  
 Es el nombre de usuario con el que se ejecuta el procedimiento almacenado. *user_name* debe ser válido [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usuario especificado como un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identificador. El usuario actual debe tener el permiso IMPERSONATE para el *nombre_usuario* especificado.  
  
 OWNER  
 Especifica que el procedimiento almacenado se ejecuta como el propietario de la cola.  
  
 DROP  
 Elimina toda la información de activación asociada a la cola.  
  
 POISON_MESSAGE_HANDLING  
 Especifica si se ha habilitado controlar mensajes dudosos. El valor predeterminado es ON.  
  
 Una cola que tenga configurado en OFF el control de mensajes dudosos no se deshabilitará después de cinco reversiones de transacción consecutivas. Esto permite que el sistema de control de mensajes dudosos sea definido por la aplicación.  
  
## <a name="remarks"></a>Comentarios  
 Cuando una cola que tiene especificado un procedimiento almacenado de activación contiene mensajes, al cambiar el estado de activación de OFF a ON, se activa inmediatamente el procedimiento almacenado de activación. Cambiar el estado de activación de ON a OFF impide que el agente active instancias del procedimiento almacenado, pero las instancias que están en ejecución no se detienen.  
  
 Modificar una cola para agregar un procedimiento almacenado de activación no afecta al estado de activación de la cola. Modificar el procedimiento almacenado de activación de la cola no afecta a las instancias del procedimiento almacenado de activación que se estén ejecutando en el momento actual.  
  
 [!INCLUDE[ssSB](../../includes/sssb-md.md)] comprueba el número máximo de lectores de cola como parte del proceso de activación. Por tanto, si se modifica una cola para aumentar el número máximo de lectores de cola, [!INCLUDE[ssSB](../../includes/sssb-md.md)] iniciará inmediatamente más instancias del procedimiento almacenado de activación. Modificar una cola para reducir el número máximo de lectores de cola no afecta a las instancias del procedimiento almacenado de activación que se estén ejecutando en el momento actual. No obstante, [!INCLUDE[ssSB](../../includes/sssb-md.md)] no inicia ninguna nueva instancia del procedimiento almacenado hasta que el número de instancias del procedimiento almacenado de activación sea inferior al número máximo configurado.  
  
 Cuando una cola no está disponible, [!INCLUDE[ssSB](../../includes/sssb-md.md)] retiene los mensajes de los servicios que usan la cola en la cola de transmisión de la base de datos. El [sys.transmission_queue](../../relational-databases/system-catalog-views/sys-transmission-queue-transact-sql.md) vista de catálogo proporciona una vista de la cola de transmisión.  
  
 Si las instrucciones RECEIVE o GET CONVERSATION GROUP especifican una cola que no está disponible, generarán un error de [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
## <a name="permissions"></a>Permissions  
 De forma predeterminada, se concede permiso para modificar una cola al propietario de la cola, a los miembros de los roles fijos de base de datos db_ddladmin o db_owner y a los miembros del rol fijo de servidor sysadmin.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-making-a-queue-unavailable"></a>A. Hacer que una cola no esté disponible  
 En el ejemplo siguiente se hace que la cola de `ExpenseQueue` no esté disponible para recibir mensajes.  
  
```  
ALTER QUEUE ExpenseQueue WITH STATUS = OFF ;  
```  
  
### <a name="b-changing-the-activation-stored-procedure"></a>B. Cambiar el procedimiento almacenado de activación  
 En el siguiente ejemplo se muestra cómo cambiar el procedimiento almacenado iniciado por la cola. El procedimiento almacenado se ejecuta como el usuario que ejecutó la instrucción `ALTER QUEUE`.  
  
```  
ALTER QUEUE ExpenseQueue  
    WITH ACTIVATION (  
        PROCEDURE_NAME = new_stored_proc,  
        EXECUTE AS SELF) ;  
```  
  
### <a name="c-changing-the-number-of-queue-readers"></a>C. Cambiar el número de lectores de cola  
 En el ejemplo siguiente se establece en `7` el número máximo de instancias de procedimiento almacenado que inicia [!INCLUDE[ssSB](../../includes/sssb-md.md)] para esta cola.  
  
```  
ALTER QUEUE ExpenseQueue WITH ACTIVATION (MAX_QUEUE_READERS = 7) ;  
```  
  
### <a name="d-changing-the-activation-stored-procedure-and-the-execute-as-account"></a>D. Cambiar el procedimiento almacenado de activación y la cuenta EXECUTE AS  
 En el ejemplo siguiente se cambia el procedimiento almacenado iniciado por [!INCLUDE[ssSB](../../includes/sssb-md.md)]. El procedimiento almacenado se ejecuta como el usuario `SecurityAccount`.  
  
```  
ALTER QUEUE ExpenseQueue  
    WITH ACTIVATION (  
        PROCEDURE_NAME = AdventureWorks2012.dbo.new_stored_proc ,  
        EXECUTE AS 'SecurityAccount') ;  
```  
  
### <a name="e-setting-the-queue-to-retain-messages"></a>E. Configurar la cola para retener mensajes  
 En el siguiente ejemplo se muestra cómo configurar la cola para retener mensajes. La cola retiene todos los mensajes enviados a o desde los servicios que utilizan la cola hasta que la conversación que contiene el mensaje finaliza.  
  
```  
ALTER QUEUE ExpenseQueue WITH RETENTION = ON ;  
```  
  
### <a name="f-removing-activation-from-a-queue"></a>F. Quitar la activación de una cola  
 En el siguiente ejemplo se muestra cómo quitar toda la información de activación de la cola.  
  
```  
ALTER QUEUE ExpenseQueue WITH ACTIVATION (DROP) ;  
```  
  
### <a name="g-rebuilding-queue-indexes"></a>G. Volver a generar índices de cola  
  
**Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 En el ejemplo siguiente se vuelve a generar los índices de cola  
  
```  
ALTER QUEUE ExpenseQueue REBUILD WITH (MAXDOP = 2)   
```  
  
### <a name="h-reorganizing-queue-indexes"></a>H. La reorganización de índices de cola  
  
**Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 En el ejemplo siguiente se reorganiza los índices de cola  
  
```  
ALTER QUEUE ExpenseQueue REORGANIZE   
```  
  
### <a name="i-moving-queue-internal-table-to-another-filegroup"></a>I: Mover tabla interna de cola a otro grupo de archivos  
  
**Se aplica a**: desde [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
```  
ALTER QUEUE ExpenseQueue MOVE TO [NewFilegroup]   
```  
  
## <a name="see-also"></a>Vea también  
 [CREATE QUEUE &#40;Transact-SQL&#41;](../../t-sql/statements/create-queue-transact-sql.md)   
 [Eliminar cola &#40; Transact-SQL &#41;](../../t-sql/statements/drop-queue-transact-sql.md)   
 [EVENTDATA &#40;Transact-SQL&#41;](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
  
  

