---
title: Sys.Servers (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- servers_TSQL
- sys.servers_TSQL
- servers
- sys.servers
dev_langs:
- TSQL
helpviewer_keywords:
- sys.servers catalog view
ms.assetid: 4e774ed9-4e83-4726-9f1d-8efde8f9feff
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 858fe45f817572eea387ce3971a52e72cc23f045
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="sysservers-transact-sql"></a>sys.servers (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada servidor vinculado o remoto registrado y una fila para el servidor local que tenga **server_id** = 0.  
  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**server_id**|**int**|Id. local del servidor vinculado.|  
|**Nombre**|**sysname**|Cuando **server_id** = 0, este es el nombre de servidor.<br /><br /> Cuando **server_id** > 0, éste es el nombre local del servidor vinculado.|  
|**product**|**sysname**|Nombre de producto del servidor vinculado. "SQL Server" indica que ésta es otra instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**proveedor**|**sysname**|Nombre del proveedor OLE DB para la conexión con el servidor vinculado.|  
|**data_source**|**nvarchar(4000)**|Propiedad de conexión del origen de datos OLE DB.|  
|**ubicación**|**nvarchar(4000)**|Propiedad de conexión de la ubicación OLE DB. Es NULL si no hay ninguna.|  
|**provider_string**|**nvarchar(4000)**|Propiedad de conexión de la cadena del proveedor OLE DB.<br /><br /> Es NULL a menos que el autor de la llamada tenga permiso ALTER ANY LINKED SERVER.|  
|**catálogo**|**sysname**|Propiedad de conexión del catálogo OLE DB. Es NULL si no hay ninguna.|  
|**connect_timeout**|**int**|Tiempo de espera de conexión, en segundos. Es 0 si no hay ninguno.|  
|**query_timeout**|**int**|Tiempo de espera de la consulta, en segundos. Es 0 si no hay ninguno.|  
|**is_linked**|**bit**|0 = es un servidor antiguo agregado mediante **sp_addserver**, con diferentes RPC y el comportamiento de las transacciones distribuidas.<br /><br /> 1 = Servidor vinculado estándar.|  
|**is_remote_login_enabled**|**bit**|Se establece la opción de RPC para habilitar los inicios de sesión remotos entrantes en este servidor.|  
|**is_rpc_out_enabled**|**bit**|Se habilitan las RPC salientes (desde este servidor).|  
|**is_data_access_enabled**|**bit**|El servidor está habilitado para las consultas distribuidas.|  
|**is_collation_compatible**|**bit**|Si no se dispone de información sobre la intercalación, se da por supuesto que la intercalación de datos remotos es compatible con los datos locales.|  
|**uses_remote_collation**|**bit**|Si es 1, se utiliza la intercalación notificada por el servidor remoto; en caso contrario, se utiliza la intercalación especificada en la columna siguiente.|  
|**collation_name**|**sysname**|Nombre de la intercalación que se va a utilizar, o NULL si solo se usa la local.|  
|**lazy_schema_validation**|**bit**|Si es 1, no se comprueba la validación del esquema al iniciar la consulta.|  
|**is_system**|**bit**|Únicamente el sistema interno puede tener acceso a este servidor.|  
|**is_publisher**|**bit**|El servidor es un publicador de replicación.|  
|**is_subscriber**|**bit**|El servidor es un suscriptor de replicación.|  
|**is_distributor**|**bit**|El servidor es un distribuidor de replicación.|  
|**is_nonsql_subscriber**|**bit**|El servidor es un suscriptor de replicación que no es de SQL Server.|  
|**is_remote_proc_transaction_promotion_enabled**|**bit**|Si es 1, al llamar a un procedimiento remoto almacenado se inicia una transacción distribuida y se da de alta en MS DTC. Para obtener más información, vea [sp_serveroption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-serveroption-transact-sql.md).|  
|**modify_date**|**datetime**|Fecha en que cambió por última vez la información del servidor.|  
  
## <a name="permissions"></a>Permissions  
 El valor de **provider_string** siempre es NULL, a menos que el llamador tiene el permiso ALTER ANY LINKED SERVER.  
  
 No se requieren permisos para ver el servidor local (**server_id** = 0).  
  
 Cuando se crea un servidor vinculado o remoto, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] crea una asignación de inicio de sesión predeterminada para el **público** rol de servidor. Esto significa que, de forma predeterminada, todos los inicios de sesión pueden ver todos los servidores vinculados y remotos. Para restringir la visibilidad de estos servidores, quite la asignación de inicio de sesión predeterminada ejecutando [sp_droplinkedsrvlogin](../../relational-databases/system-stored-procedures/sp-droplinkedsrvlogin-transact-sql.md) y especificar el valor NULL para la *locallogin* parámetro.  
  
 Si se elimina la asignación de inicio de sesión predeterminada, solo los usuarios que se hayan agregado de forma explícita como un inicio de sesión vinculado o remoto podrán ver los servidores vinculados o remotos para los que tienen un inicio de sesión. Para ver todos los servidores vinculados y remotos después de eliminar la asignación de inicio de sesión predeterminada se requieren los permisos siguientes:  
  
-   ALTER ANY LINKED SERVER o ALTER ANY LOGIN ON SERVER  
  
-   Pertenencia en el **setupadmin** o **sysadmin** roles fijos de servidor  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Vistas de catálogo de los servidores vinculados &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/linked-servers-catalog-views-transact-sql.md)   
 [sp_addlinkedsrvlogin &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql.md)   
 [sp_addremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)  
  
  
