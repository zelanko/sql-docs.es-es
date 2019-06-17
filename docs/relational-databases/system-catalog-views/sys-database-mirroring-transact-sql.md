---
title: sys.database_mirroring (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.database_mirroring
- database_mirroring
- sys.database_mirroring_TSQL
- database_mirroring_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.database_mirroring catalog view
ms.assetid: 480de2b0-2c16-497d-a6a3-bf7f52a7c9a0
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: bea7712fd4efa1934117937a5168843d727d0dc6
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62693912"
---
# <a name="sysdatabasemirroring-transact-sql"></a>sys.database_mirroring (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada base de datos de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Si la base de datos no está en línea o no está habilitada la creación de reflejo de base de datos, los valores de todas las columnas excepto database_id será NULL.  
  
 Para ver la fila de una base de datos que no sea master o tempdb, debe ser el propietario de la base de datos o tener al menos permiso de nivel de servidor ALTER ANY DATABASE o VIEW ANY DATABASE o el permiso CREATE DATABASE en la base de datos maestra. Para ver los valores no NULL en una base de datos reflejada, debe ser miembro de la **sysadmin** rol fijo de servidor.  
  
> [!NOTE]  
>  Si una base de datos no participa en la creación de reflejo, todas las columnas con el prefijo "mirroring_" son NULL.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|Identificador de la base de datos. Es único en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**mirroring_guid**|**uniqueidentifier**|Id. de la creación de reflejo de la asociación.<br /><br /> NULL = la base de datos es inaccesible o no está reflejada.<br /><br /> Nota: Si la base de datos no participa en la creación de reflejo, todas las columnas con el prefijo "mirroring_" son NULL.|  
|**mirroring_state**|**tinyint**|Estado de la base de datos reflejada y de la sesión de creación de reflejo de la base de datos.<br /><br /> 0 = suspensión<br /><br /> 1 = Desconectada del otro asociado<br /><br /> 2 = En proceso de sincronización<br /><br /> 3 = Pendiente de conmutación por error<br /><br /> 4 = Sincronizada<br /><br /> 5 = Los asociados no están sincronizados. La conmutación por error no es posible.<br /><br /> 6 = Los socios están sincronizados. La conmutación por error es potencialmente posible. Para obtener información sobre los requisitos para la conmutación por error, vea [Database Mirroring Operating Modes](../../database-engine/database-mirroring/database-mirroring-operating-modes.md).<br /><br /> NULL= No se puede tener acceso a la base de datos o no está reflejada.|  
|**mirroring_state_desc**|**nvarchar(60)**|Descripción del estado de la base de datos reflejada y de la sesión de creación de reflejo de base de datos, uno de los siguientes:<br /><br /> DISCONNECTED<br /><br /> SYNCHRONIZED<br /><br /> SYNCHRONIZING<br /><br /> PENDING_FAILOVER<br /><br /> SUSPENDED<br /><br /> UNSYNCHRONIZED<br /><br /> SYNCHRONIZED<br /><br /> NULL<br /><br /> Para obtener más información, vea [Estados de creación de reflejo &#40;SQL Server&#41;](../../database-engine/database-mirroring/mirroring-states-sql-server.md).|  
|**mirroring_role**|**tinyint**|Rol que representa la base de datos local en la sesión de creación de reflejo de la base de datos.<br /><br /> 1 = Entidad de seguridad<br /><br /> 2 = Reflejo<br /><br /> NULL= No se puede tener acceso a la base de datos o no está reflejada.|  
|**mirroring_role_desc**|**nvarchar(60)**|Descripción del rol que desempeña la base de datos local en la creación de reflejo, una de las siguientes:<br /><br /> PRINCIPAL<br /><br /> MIRROR|  
|**mirroring_role_sequence**|**int**|Número de veces que los asociados de creación de reflejo han cambiado entre los roles de principal y reflejo debido a una conmutación por error o a un servicio forzado.<br /><br /> NULL= No se puede tener acceso a la base de datos o no está reflejada.|  
|**mirroring_safety_level**|**tinyint**|Configuración de seguridad para las actualizaciones en la base de datos reflejada:<br /><br /> 0 = Estado desconocido<br /><br /> 1 = Desactivada [asincrónica]<br /><br /> 2 = Completa [sincrónica]<br /><br /> NULL= No se puede tener acceso a la base de datos o no está reflejada.|  
|**mirroring_safety_level_desc**|**nvarchar(60)**|Configuración de seguridad de las transacciones para realizar actualizaciones en la base de datos reflejada, uno de los valores siguientes:<br /><br /> UNKNOWN<br /><br /> OFF<br /><br /> FULL<br /><br /> NULL|  
|**mirroring_safety_sequence**|**int**|Número de secuencia de actualización para los cambios de nivel de seguridad de transacciones.<br /><br /> NULL= No se puede tener acceso a la base de datos o no está reflejada.|  
|**mirroring_partner_name**|**nvarchar(128)**|Nombre de servidor del asociado de creación de reflejo de la base de datos.<br /><br /> NULL= No se puede tener acceso a la base de datos o no está reflejada.|  
|**mirroring_partner_instance**|**nvarchar(128)**|Nombre de instancia y nombre de equipo del otro asociado. Los clientes necesitan esta información para conectarse al asociado si se convierte en el servidor principal.<br /><br /> NULL= No se puede tener acceso a la base de datos o no está reflejada.|  
|**mirroring_witness_name**|**nvarchar(128)**|Nombre de servidor del testigo de creación de reflejo de la base de datos.<br /><br /> NULL = No existe ningún testigo.|  
|mirroring_witness_state|**tinyint**|Estado del testigo en la sesión de creación de reflejo de la base de datos, uno de los siguientes:<br /><br /> 0 = Desconocido<br /><br /> 1 = Conectado<br /><br /> 2 = Desconectado<br /><br /> NULL = No existe ningún testigo, la base de datos no está en línea o la base de datos no está reflejada.|  
|**mirroring_witness_state_desc**|**nvarchar(60)**|Descripción del estado, que puede ser uno de los siguientes:<br /><br /> UNKNOWN<br /><br /> CONNECTED<br /><br /> DISCONNECTED<br /><br /> NULL|  
|**mirroring_failover_lsn**|**numeric(25,0)**|Número de secuencia de registro (LSN) de la última entrada del registro de transacciones para la que se garantiza que será reforzada en el disco de ambos asociados. Después de una conmutación por error, el **mirroring_failover_lsn** los socios comerciales sirve como punto de reconciliación en el que el nuevo servidor reflejado comienza a sincronizar la base de datos reflejada con la nueva base de datos principal.|  
|**mirroring_connection_timeout**|**int**|Tiempo de espera de la conexión de creación de reflejo, en segundos. Es el número de segundos durante los cuales se espera una respuesta de un asociado o testigo antes de considerarlos no disponibles. El valor predeterminado del tiempo de espera es de 10 segundos.<br /><br /> NULL= No se puede tener acceso a la base de datos o no está reflejada.|  
|**mirroring_redo_queue**|**int**|Cantidad máxima de registro que debe rehacerse en el reflejo. Si mirroring_redo_queue_type se establece en UNLIMITED, que es la configuración predeterminada, esta columna es NULL. Si la base de datos no está en línea, esta columna también es NULL.<br /><br /> En caso contrario, esta columna contiene la cantidad máxima de registro, en megabytes. Cuando se alcanza el valor máximo, el registro se detiene temporalmente en el servidor principal mientras el servidor reflejado se pone al mismo nivel. Esta característica limita el tiempo de conmutación por error.<br /><br /> Para obtener más información, vea [Calcular la interrupción del servicio durante la conmutación de roles &#40;creación de reflejo de la base de datos&#41;](../../database-engine/database-mirroring/estimate-the-interruption-of-service-during-role-switching-database-mirroring.md).|  
|**mirroring_redo_queue_type**|**nvarchar(60)**|UNLIMITED indica que la creación de reflejo no impedirá la cola de rehacer. Esta es la configuración predeterminada.<br /><br /> MB indica el tamaño máximo de la cola de rehacer, en megabytes. Tenga en cuenta que, si el tamaño de la cola se especificó en kilobytes o gigabytes, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] convertirá el valor a megabytes.<br /><br /> Si la base de datos no está en línea, esta columna es NULL.|  
|**mirroring_end_of_log_lsn**|**numeric(25,0)**|El final de registro local se ha volcado en el disco. Esto es comparable al LSN protegido del servidor reflejado (vea la **mirroring_failover_lsn** columna).|  
|**mirroring_replication_lsn**|**numeric(25,0)**|El LSN máximo que la replicación puede enviar.|  
  
## <a name="permissions"></a>Permisos  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [ALTER DATABASE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)   
 [sys.database_mirroring_witnesses &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/database-mirroring-witness-catalog-views-sys-database-mirroring-witnesses.md)   
 [sys.database_mirroring_endpoints &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-database-mirroring-endpoints-transact-sql.md)   
 [Vistas de catálogo de archivos y bases de datos &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/databases-and-files-catalog-views-transact-sql.md)   
 [Preguntas frecuentes sobre consultas del catálogo de sistema de SQL Server](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
