---
title: Sys.dm_os_performance_counters (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- dm_os_performance_counters
- sys.dm_os_performance_counters_TSQL
- dm_os_performance_counters_TSQL
- sys.dm_os_performance_counters
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_performance_counters dynamic management view
ms.assetid: a1c3e892-cd48-40d4-b6be-2a9246e8fbff
caps.latest.revision: 34
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1bdbd9ea7029aaf8b18631a2303fdd1228ff0198
ms.sourcegitcommit: 7019ac41524bdf783ea2c129c17b54581951b515
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/23/2018
---
# <a name="sysdmosperformancecounters-transact-sql"></a>sys.dm_os_performance_counters (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-asdb-asdw-pdw-md.md)]

  Devuelve una fila por contador de rendimiento que se mantiene en el servidor. Para obtener información acerca de cada contador de rendimiento, consulte [usar objetos de SQL Server](../../relational-databases/performance-monitor/use-sql-server-objects.md).  
  
> [!NOTE]  
>  Para llamar a esta desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_os_performance_counters**.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**object_name**|**nchar(128)**|Categoría a la que pertenece este contador.|  
|**Nombre_contador**|**nchar(128)**|Nombre del contador. Para obtener más información acerca de un contador, este es el nombre del tema para seleccionar en la lista de contadores en [usar objetos de SQL Server](../../relational-databases/performance-monitor/use-sql-server-objects.md). |  
|**nombre_instancia**|**nchar(128)**|Nombre de la instancia específica del contador. A menudo contiene el nombre de la base de datos.|  
|**cntr_value**|**bigint**|Valor actual del contador.<br /><br /> **Nota:** contadores por segundo, este valor es acumulado. El valor de la tarifa se debe calcular probando el valor en intervalos de tiempo distintos. La diferencia entre dos valores de ejemplo sucesivos es igual a la tarifa del intervalo de tiempo usado.|  
|**cntr_type**|**int**|Tipo de contador definido en la arquitectura de rendimiento de Windows. Vea [WMI Performance Counter Types](http://msdn2.microsoft.com/library/aa394569.aspx) en MSDN o la documentación de Windows Server para obtener más información sobre los tipos de contador de rendimiento.|  
|**pdw_node_id**|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo que se encuentra en esta distribución.|  
  
## <a name="remarks"></a>Comentarios  
 Si la instancia de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no puede mostrar los contadores de rendimiento del sistema operativo Windows, utilice la consulta de [!INCLUDE[tsql](../../includes/tsql-md.md)] siguiente para confirmar que se han deshabilitado los contadores de rendimiento.  
  
```  
SELECT COUNT(*) FROM sys.dm_os_performance_counters;  
```  
  
 Si el valor devuelto es 0 filas, significa que se han deshabilitado los contadores de rendimiento. Debe examinar a continuación el registro de instalación y buscar el error 3409, "Vuelva a instalar sqlctr.ini para esta instancia y asegúrese de que la cuenta de inicio de sesión de la instancia tiene los permisos correctos para el Registro".  Esto denota que los contadores de rendimiento no estaban habilitados. Los errores inmediatamente anteriores al error 3409 deben indicar la causa principal del error en la habilitación del contador de rendimiento. Para obtener más información sobre los archivos de registro de instalación, consulte [ver y leer los archivos de registro de instalación de SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md).  
  
## <a name="permission"></a>Permiso

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requiere el `VIEW DATABASE STATE` permiso en la base de datos.   
 
## <a name="examples"></a>Ejemplos  
 El ejemplo siguiente devuelve valores de contador de rendimiento.  
  
```  
SELECT object_name, counter_name, instance_name, cntr_value, cntr_type  
FROM sys.dm_os_performance_counters;  
  
```  
  
## <a name="see-also"></a>Vea también  
  [Vistas de administración dinámica relacionadas con el sistema operativo SQL Server &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)   
 [sys.sysperfinfo &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysperfinfo-transact-sql.md)  
  
  


