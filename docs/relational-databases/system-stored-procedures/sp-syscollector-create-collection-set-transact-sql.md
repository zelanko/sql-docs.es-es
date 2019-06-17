---
title: sp_syscollector_create_collection_set (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_create_collection_set_TSQL
- sp_syscollector_create_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_create_collection_set
ms.assetid: 69e9ff0f-c409-43fc-89f6-40c3974e972c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: be818ed92a3c5a7f9522a6142f5acc815077bd10
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63004290"
---
# <a name="spsyscollectorcreatecollectionset-transact-sql"></a>sp_syscollector_create_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Crea un conjunto de recopilación nuevo. Puede utilizar este procedimiento almacenado para crear un conjunto de recopilación personalizado para la recopilación de datos.  
  
> [!WARNING]  
>  En los casos en que la cuenta de Windows configurada como proxy pertenezca a un usuario no interactivo o interactivo que aún no se ha conectado, el directorio del perfil no existirá y se producirá un error al crear el directorio de almacenamiento temporal. Por tanto, si utiliza una cuenta de proxy en un controlador de dominio, debe especificar una cuenta interactiva que se haya utilizado al menos una vez para asegurarse de que se ha creado el directorio del perfil.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_syscollector_create_collection_set   
      [ @name = ] 'name'  
    , [ [ @target = ] 'target' ]  
    , [ [ @collection_mode = ] collection_mode ]  
    , [ [ @days_until_expiration = ] days_until_expiration ]  
    , [ [ @proxy_id = ] proxy_id ]  
    , [ [ @proxy_name = ] 'proxy_name' ]  
    , [ [ @schedule_uid = ] 'schedule_uid' ]  
    , [ [ @schedule_name = ] 'schedule_name' ]  
    , [ [ @logging_level = ] logging_level ]  
    , [ [ @description = ] 'description' ]  
    , [ @collection_set_id = ] collection_set_id OUTPUT   
    , [ [ @collection_set_uid = ] 'collection_set_uid' OUTPUT ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @name = ] 'name'` Es el nombre del conjunto de recopilación. *nombre* es **sysname** y no puede ser una cadena vacía o NULL.  
  
 *nombre* deben ser únicos. Para obtener una lista de los nombres de conjuntos de recopilación actuales, consulte la vista del sistema syscollector_collection_sets.  
  
`[ @target = ] 'target'` Reservado para uso futuro. *nombre* es **nvarchar (128)** con un valor predeterminado es null.  
  
`[ @collection_mode = ] collection_mode` Especifica la manera en que se recopilan y almacenan los datos. *collection_mode* es **smallint** y puede tener uno de los siguientes valores:  
  
 0 - Modo de almacenamiento en caché. La recopilación y la carga de datos están en programaciones independientes. Especifique el modo de almacenamiento en caché para la recopilación continua.  
  
 1 - Modo sin almacenamiento en caché. Recopilación de datos y la carga se encuentra en la misma programación. Establezca el modo sin almacenamiento en caché para la recopilación ad hoc o la recopilación de instantáneas.  
  
 El valor predeterminado de *collection_mode* es 0. Cuando *collection_mode* es 0, *valor schedule_uid* o *schedule_name* debe especificarse.  
  
`[ @days_until_expiration = ] days_until_expiration` Es el número de días que los datos recopilados se guardan en el almacén de datos de administración. *days_until_expiration* es **smallint** con un valor predeterminado de 730 (dos años). *days_until_expiration* debe ser 0 o un entero positivo.  
  
`[ @proxy_id = ] proxy_id` Es el identificador único para un [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta de proxy del agente. *proxy_id* es **int** con un valor predeterminado es null. Si se especifica, *proxy_name* debe ser NULL. Para obtener *proxy_id*, consulta la tabla del sistema sysproxies. El rol fijo de base de datos dc_admin debe disponer de los permisos necesarios para obtener acceso al proxy. Para obtener más información, consulte [crear un Proxy del Agente SQL Server](../../ssms/agent/create-a-sql-server-agent-proxy.md).  
  
`[ @proxy_name = ] 'proxy_name'` Es el nombre de la cuenta de proxy. *proxy_name* es **sysname** con un valor predeterminado es null. Si se especifica, *proxy_id* debe ser NULL. Para obtener *proxy_name*, consulta la tabla del sistema sysproxies.  
  
`[ @schedule_uid = ] 'schedule_uid'` Es el GUID que apunta a una programación. *valor schedule_uid* es **uniqueidentifier** con un valor predeterminado es null. Si se especifica, *schedule_name* debe ser NULL. Para obtener *valor schedule_uid*, consulta la tabla del sistema sysschedules.  
  
 Cuando *collection_mode* se establece en 0, *valor schedule_uid* o *schedule_name* debe especificarse. Cuando *collection_mode* está establecido en 1, *valor schedule_uid* o *schedule_name* se omite si se especifica.  
  
`[ @schedule_name = ] 'schedule_name'` Es el nombre de la programación. *schedule_name* es **sysname** con un valor predeterminado es null. Si se especifica, *valor schedule_uid* debe ser NULL. Para obtener *schedule_name*, consulta la tabla del sistema sysschedules.  
  
`[ @logging_level = ] logging_level` Es el nivel de registro. *LOGGING_LEVEL* es **smallint** con uno de los siguientes valores:  
  
 0 - registrar la información de ejecución y los eventos [!INCLUDE[ssIS](../../includes/ssis-md.md)] que realizan el seguimiento:  
  
-   Iniciar/detener los conjuntos de recopilaciones  
  
-   Iniciar/detener los paquetes  
  
-   Información de error  
  
 1 - nivel de registro 0 y:  
  
-   Estadísticas de ejecución  
  
-   Progreso de recopilaciones que se ejecutan continuamente  
  
-   Eventos de advertencia de [!INCLUDE[ssIS](../../includes/ssis-md.md)]  
  
 2 - nivel de registro 1 e información detallada de eventos de [!INCLUDE[ssIS](../../includes/ssis-md.md)]  
  
 El valor predeterminado de *logging_level* es 1.  
  
`[ @description = ] 'description'` Es la descripción del conjunto de recopilación. *descripción* es **nvarchar (4000)** con un valor predeterminado es null.  
  
`[ @collection_set_id = ] collection_set_id` Es el identificador local único del conjunto de recopilación. *collection_set_id* es **int** con los resultados y es necesario.  
  
`[ @collection_set_uid = ] 'collection_set_uid'` Es el GUID del conjunto de recopilación. *collection_set_uid* es **uniqueidentifier** con OUTPUT y un valor predeterminado es NULL.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 sp_syscollector_create_collection_set se debe ejecutar en el contexto de la base de datos del sistema msdb.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol fijo de base de datos dc_admin (con permiso EXECUTE) para ejecutar este procedimiento.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-creating-a-collection-set-by-using-default-values"></a>A. Crear un conjunto de recopilación utilizando valores predeterminados  
 En el ejemplo siguiente se crea un conjunto de recopilación especificando solamente los parámetros necesarios. `@collection_mode` no se obligatorio, pero el modo de recopilación predeterminado (almacenamiento en caché) exige especificar un id. o un nombre de programación.  
  
```  
USE msdb;  
GO  
DECLARE @collection_set_id int;  
EXECUTE dbo.sp_syscollector_create_collection_set  
    @name = N'Simple collection set test 1',  
    @description = N'This is a test collection set that runs in non-cached mode.',  
    @collection_mode = 1,  
    @collection_set_id = @collection_set_id OUTPUT;  
GO  
```  
  
### <a name="b-creating-a-collection-set-by-using-specified-values"></a>b. Crear un conjunto de recopilación utilizando los valores especificados  
 En el ejemplo siguiente se crea un conjunto de recopilación con los valores especificados para muchos de los parámetros.  
  
```  
USE msdb;  
GO  
DECLARE @collection_set_id int;  
DECLARE @collection_set_uid uniqueidentifier;  
SET @collection_set_uid = NEWID();  
EXEC dbo.sp_syscollector_create_collection_set  
    @name = N'Simple collection set test 2',  
    @collection_mode = 0,  
    @days_until_expiration = 365,  
    @description = N'This is a test collection set that runs in cached mode.',  
    @logging_level = 2,  
    @schedule_name = N'CollectorSchedule_Every_30min',  
    @collection_set_id = @collection_set_id OUTPUT,  
    @collection_set_uid = @collection_set_uid OUTPUT;  
```  
  
## <a name="see-also"></a>Vea también  
 [Recopilación de datos](../../relational-databases/data-collection/data-collection.md)   
 [Crear un conjunto de recopilación personalizado que use el tipo de recopilador de consultas T-SQL genérico &#40;Transact-SQL&#41;](../../relational-databases/data-collection/create-custom-collection-set-generic-t-sql-query-collector-type.md)   
 [Procedimientos almacenados del recopilador de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [syscollector_collection_sets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)  
  
  
