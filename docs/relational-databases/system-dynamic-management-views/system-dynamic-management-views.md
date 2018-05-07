---
title: Vistas de administración dinámica (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: dmv's
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- database scoped dynamic management objects [SQL Server]
- dynamic management objects [SQL Server], about dynamic management objects
- server state information [SQL Server]
- dynamic management functions [SQL Server]
- metadata [SQL Server], dynamic management objects
- dynamic management views [SQL Server]
- DMVs [SQL Server]
- functions [SQL Server], dynamic management
- server scoped dynamic management objects [SQL Server]
- dynamic management objects [SQL Server]
ms.assetid: cf893ecb-0bf6-4cbf-ac00-8a1099e405b1
caps.latest.revision: 41
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: bdf9cf71081f756f9ab4bb399db9dc58ef6a1d5b
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="system-dynamic-management-views"></a>Vistas de administración dinámica del sistema
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Las funciones y vistas de administración dinámica devuelven información sobre el estado del servidor que se puede utilizar para controlar el estado de una instancia del servidor, para diagnosticar problemas y para optimizar el rendimiento.  
  
> [!IMPORTANT]  
>  Las funciones y vistas de administración dinámica devuelven datos sobre el estado interno de la implementación. Los esquemas y datos que ofrecen podrán variar en versiones futuras de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por lo tanto, es posible que las funciones y vistas de administración dinámica de las versiones futuras no sean compatibles con las funciones y vistas de administración dinámica en esta versión. Por ejemplo, en versiones futuras de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], Microsoft puede aumentar la definición de cualquier vista de administración dinámica y agregar columnas al final de la lista. Se recomienda no usar la sintaxis `SELECT * FROM dynamic_management_view_name` en código para producción, ya que el número de columnas devueltas podría cambiar y alterar la aplicación.  
  
 Hay dos tipos de funciones y vistas de administración dinámica:  
  
-   Funciones y vistas de administración dinámica con ámbito en el servidor. Se requiere el permiso VIEW SERVER STATE en el servidor.  
  
-   Funciones y vistas de administración dinámica con ámbito en la base de datos. Se requiere el permiso VIEW DATABASE STATE en la base de datos.  
  
## <a name="querying-dynamic-management-views"></a>Consultar las vistas de administración dinámica  
 Puede hacer referencia a las vistas de administración dinámica en instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] usando nombres formados por dos, tres o cuatro partes. Por otro lado, puede hacer referencia a las funciones de administración dinámica en instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] usando nombres formados por dos o tres partes. No se puede hacer referencia a funciones ni vistas de administración dinámica en instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] mediante nombres con una sola parte.  
  
 Todas las funciones y vistas de administración dinámica existen en el esquema sys y siguen la convención de nomenclatura siguiente: dm_*. Cuando utilice una función o vista de administración dinámica, debe agregar un prefijo al nombre de la función o vista mediante el esquema sys. Por ejemplo, para consultar la vista de administración dinámica dm_os_wait_stats, ejecute la consulta siguiente:  
  
 ```sql
SELECT wait_type, wait_time_ms  
FROM sys.dm_os_wait_stats;  
```  
  
### <a name="required-permissions"></a>Permisos necesarios  
 Para ejecutar una consulta en una función o vista de administración dinámica, es necesario el permiso SELECT sobre el objeto y el permiso VIEW SERVER STATE o VIEW DATABASE STATE. Así podrá restringir de forma selectiva el acceso de un usuario o inicio de sesión a las funciones y vistas de administración dinámica. Para ello, cree primero el usuario en la base de datos maestra y, a continuación, deniéguele el permiso SELECT sobre las funciones o vistas de administración dinámica a las que no desea que tenga acceso. Después de esto, el usuario no podrá seleccionar ninguna de estas funciones o vistas de administración dinámica, sin tener en cuenta el contexto de la base de datos del usuario.  
  
> [!NOTE]  
>  Dado que el permiso DENY tiene prioridad, si un usuario tiene concedido el permiso VIEW SERVER STATE, pero tiene denegado el permiso VIEW DATABASE STATE, el usuario podrá ver la información en el servidor, pero no en la base de datos.  
  
## <a name="in-this-section"></a>En esta sección  
 Las funciones y vistas de administración dinámica están organizadas en las categorías siguientes.  
  
|||  
|-|-|  
|[Siempre en vistas de administración dinámica de grupos de disponibilidad y funciones (Transact-SQL)](../../relational-databases/system-dynamic-management-views/always-on-availability-groups-dynamic-management-views-functions.md)|[Vistas de administración dinámica de tablas optimizadas en memoria &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)|  
|[Vistas de administración dinámica relacionadas con la captura de datos modificados &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/2a771d7d-693a-4f56-9227-02cd00e0e200)|[Funciones y vistas de administración dinámica, relacionadas con el objeto &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/object-related-dynamic-management-views-and-functions-transact-sql.md)|  
|[Vistas de administración dinámica relacionadas con el seguimiento de cambios](http://msdn.microsoft.com/library/dc8a0af9-fcd8-4c34-9453-5132717c9bdb)|[Vistas de administración dinámica relacionadas con notificaciones de consulta &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/92eb22d8-33f3-4c17-b32e-e23acdfbd8f4)|  
|[Vistas de administración dinámica relacionadas con el Common Language Runtime &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/common-language-runtime-related-dynamic-management-views-transact-sql.md)|[Vistas de administración dinámica relacionadas con la replicación &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/replication-related-dynamic-management-views-transact-sql.md)|  
|[Vistas de administración dinámica relacionadas con creación de reflejo de la base de datos &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/04fb21de-1b5e-4a8e-9ca6-1b78ad278db1)|[Vistas de administración dinámica relacionadas con el regulador de recursos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/resource-governor-related-dynamic-management-views-transact-sql.md)|  
|[Vistas de administración dinámica relacionadas con la base de datos &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)|[Funciones y vistas de administración dinámica relacionadas con la seguridad &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql.md)|  
|[Vistas de administración dinámica y funciones relacionadas con ejecuciones &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)|[Funciones y vistas de administración dinámica relacionadas con servidores &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/server-related-dynamic-management-views-and-functions-transact-sql.md)|  
|[Vistas de administración dinámica de eventos extendidos](../../relational-databases/system-dynamic-management-views/extended-events-dynamic-management-views.md)|[Service Broker relacionadas con vistas de administración dinámica & #40; Transact-SQL & #41;](../../relational-databases/system-dynamic-management-views/service-broker-related-dynamic-management-views-transact-sql.md)|  
|[FileStream y vistas de administración dinámica de FileTable &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)|[Datos espaciales relacionados con las funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/c542ac38-451f-43a5-bf8c-4edd38bb738e)|  
|[Funciones y vistas de administración dinámica de la búsqueda semántica y búsqueda de texto completo &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/full-text-and-semantic-search-dynamic-management-views-functions.md)|[Vistas de administración dinámica del almacenamiento de datos en paralelo y almacén de datos SQL &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-and-parallel-data-warehouse-dynamic-management-views.md)|  
|[Funciones y vistas de administración dinámica de replicación geográfica &#40;base de datos SQL Azure&#41;](../../relational-databases/system-dynamic-management-views/geo-replication-dynamic-management-views-and-functions-azure-sql-database.md)|[Vistas de administración dinámica relacionadas con el sistema operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)|  
|[Funciones y vistas de administración dinámica relacionadas con índices &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/index-related-dynamic-management-views-and-functions-transact-sql.md)|[Vistas de administración dinámica de la base de datos de Stretch &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/1193efce-a105-49a9-a8b8-26b063485567)|  
|[¿O relacionados con las funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/i-o-related-dynamic-management-views-and-functions-transact-sql.md)|[Funciones y vistas de administración dinámica relacionadas con transacciones &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/transaction-related-dynamic-management-views-and-functions-transact-sql.md)|  

  
## <a name="see-also"></a>Vea también  
 [CONCEDER permisos Server &#40;Transact-SQL&#41;](../../t-sql/statements/grant-server-permissions-transact-sql.md)   
 [GRANT &#40;permisos de base de datos de Transact-SQL&#41;](../../t-sql/statements/grant-database-permissions-transact-sql.md)   
 [Vistas del sistema &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)  
  
  
