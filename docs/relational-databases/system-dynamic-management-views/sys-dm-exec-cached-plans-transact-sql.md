---
title: sys.dm_exec_cached_plans (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_cached_plans
- dm_exec_cached_plans
- dm_exec_cached_plans_TSQL
- sys.dm_exec_cached_plans_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_cached_plans dynamic management view
ms.assetid: 95b707d3-3a93-407f-8e88-4515d4f2039d
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 8d23ba5a1fbb88bd430c1422019087a5df70c884
ms.sourcegitcommit: 671370ec2d49ed0159a418b9c9ac56acf43249ad
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/15/2019
ms.locfileid: "58072339"
---
# <a name="sysdmexeccachedplans-transact-sql"></a>sys.dm_exec_cached_plans (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve una fila para cada plan de consulta que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] almacena en caché para agilizar la ejecución. Puede usar esta vista de administración dinámica para ver los planes de consulta almacenados en caché, el texto de las consultas almacenadas en caché, la cantidad de memoria que ocupan los planes y el contador de reutilización de los planes almacenados en caché.  
  
 En [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], las vistas de administración dinámica no pueden exponer información que impactaría a la contención de la base de datos ni acerca de otras bases de datos a las que el usuario tenga acceso. Para evitar exponer esta información, cada fila que contiene datos que no pertenecen al inquilino conectado se filtra. Además, los valores de las columnas **memory_object_address** y **pool_id** se filtran; el valor de columna se establece en NULL.  
  
> [!NOTE]  
>  Al llamarlo desde [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] o [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], use el nombre **sys.dm_pdw_nodes_exec_cached_plans**.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|bucketid|**int**|Identificador del depósito de hash en el que se almacena en caché la entrada. El valor indica un intervalo comprendido entre 0 y el tamaño de la tabla hash para el tipo de caché.<br /><br /> En la memoria caché de planes SQL y planes de objetos, el tamaño de la tabla hash puede ser de hasta 10007 en sistemas de 32 bits y de hasta 40009 en sistemas de 64 bits. En la memoria caché de árboles enlazados, el tamaño de la tabla hash puede ser de hasta 1009 en sistemas de 32 bits y de hasta 4001 en sistemas de 64 bits. En la memoria caché de procedimientos almacenados extendidos, el tamaño de la tabla hash puede ser de hasta 127 en sistemas de 32 y de 64 bits.|  
|refcounts|**int**|Número de objetos de caché que hacen referencia a este objeto de caché. **RefCounts** debe ser al menos 1 para una entrada en la memoria caché.|  
|usecounts|**int**|Número de veces que se ha buscado el objeto de caché. Este número no se incrementa cuando las consultas con parámetros encuentran un plan en la memoria caché. Se puede incrementar varias veces cuando se utiliza un plan de representación.|  
|size_in_bytes|**int**|Número de bytes consumidos por el objeto de caché.|  
|memory_object_address|**varbinary(8)**|Dirección de memoria de la entrada de caché. Este valor se puede usar con [sys.dm_os_memory_objects](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md) para obtener el análisis de la memoria del plan almacenado en caché y con [sys.dm_os_memory_cache_entries](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-entries-transact-sql.md)para obtener el costo de almacenamiento en caché la entrada.|  
|cacheobjtype|**nvarchar(34)**|Tipo del objeto en la memoria caché. El valor puede ser uno de los siguientes:<br /><br /> Plan compilado<br /><br /> Código auxiliar del plan compilado<br /><br /> Árbol de análisis<br /><br /> Procedimiento extendido<br /><br /> Función compilada CLR<br /><br /> Procedimiento compilado CLR|  
|objtype|**nvarchar(16)**|Tipo de objeto. A continuación se muestran los valores posibles y sus correspondientes descripciones.<br /><br /> Procedimiento: Procedimiento almacenado<br />Preparado: Instrucción preparada<br />Ad hoc: Consulta ad hoc. Hace referencia a [!INCLUDE[tsql](../../includes/tsql-md.md)] enviada como eventos de lenguaje mediante **osql** o **sqlcmd** en lugar de como llamadas a procedimiento remoto.<br />ReplProc: Procedimiento de filtro de replicación<br />Desencadenador: Desencadenador<br />Vista: Ver<br />Predeterminado: Default<br />UsrTab: Tabla de usuario<br />SysTab: Tabla del sistema<br />Comprobar: Restricción CHECK<br />Regla: Regla|  
|plan_handle|**varbinary(64)**|Identificador del plan en memoria. Este identificador es transitorio y permanece constante solo mientras el plan permanece en la memoria caché. Este valor se puede usar con las siguientes funciones de administración dinámica:<br /><br /> [sys.dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)<br /><br /> [sys.dm_exec_query_plan](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)<br /><br /> [sys.dm_exec_plan_attributes](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)|  
|pool_id|**int**|El identificador del grupo de recursos de servidor considerado para este uso de memoria del plan.|  
|pdw_node_id|**int**|**Se aplica a**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> El identificador para el nodo en esta distribución.|  
  
 <sup>1</sup>  
  
## <a name="permissions"></a>Permisos

En [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], requiere `VIEW SERVER STATE` permiso.   
En [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], requiere el `VIEW DATABASE STATE` permiso en la base de datos.   

## <a name="examples"></a>Ejemplos  
  
### <a name="a-returning-the-batch-text-of-cached-entries-that-are-reused"></a>A. Devolver el texto del lote de las entradas en caché que se reutilizan  
 En el ejemplo siguiente se devuelve el texto SQL de todas las entradas en caché que se han usado más de una vez.  
  
```sql  
SELECT usecounts, cacheobjtype, objtype, text   
FROM sys.dm_exec_cached_plans   
CROSS APPLY sys.dm_exec_sql_text(plan_handle)   
WHERE usecounts > 1   
ORDER BY usecounts DESC;  
GO  
```  
  
### <a name="b-returning-query-plans-for-all-cached-triggers"></a>b. Devolver los planes de consulta de todos los desencadenadores almacenados en caché  
 En el ejemplo siguiente se devuelven los planes de consulta de todos los desencadenadores almacenados en caché.  
  
```sql  
SELECT plan_handle, query_plan, objtype   
FROM sys.dm_exec_cached_plans   
CROSS APPLY sys.dm_exec_query_plan(plan_handle)   
WHERE objtype ='Trigger';  
GO  
```  
  
### <a name="c-returning-the-set-options-with-which-the-plan-was-compiled"></a>C. Devolver las opciones SET con las que se compiló el plan  
 En el ejemplo siguiente se devuelven las opciones SET con las que se compiló el plan. El `sql_handle` de también se devuelve el plan. El operador PIVOT se usa al resultado de la `set_options` y `sql_handle` atributos como columnas en lugar de como filas. Para obtener más información sobre el valor devuelto en `set_options`, consulte [sys.dm_exec_plan_attributes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md).  
  
```sql  
SELECT plan_handle, pvt.set_options, pvt.sql_handle  
FROM (  
      SELECT plan_handle, epa.attribute, epa.value   
      FROM sys.dm_exec_cached_plans   
      OUTER APPLY sys.dm_exec_plan_attributes(plan_handle) AS epa  
      WHERE cacheobjtype = 'Compiled Plan'  
      ) AS ecpa   
PIVOT (MAX(ecpa.value) FOR ecpa.attribute IN ("set_options", "sql_handle")) AS pvt;  
GO  
```  
  
### <a name="d-returning-the-memory-breakdown-of-all-cached-compiled-plans"></a>D. Devolver el análisis de la memoria de todos los planes compilados almacenados en caché  
 En el ejemplo siguiente se devuelve un análisis de la memoria que usan todos los planes compilados de la memoria caché.  
  
```sql  
SELECT plan_handle, ecp.memory_object_address AS CompiledPlan_MemoryObject,   
    omo.memory_object_address, type, page_size_in_bytes   
FROM sys.dm_exec_cached_plans AS ecp   
JOIN sys.dm_os_memory_objects AS omo   
    ON ecp.memory_object_address = omo.memory_object_address   
    OR ecp.memory_object_address = omo.parent_address  
WHERE cacheobjtype = 'Compiled Plan';  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones y vistas de administración dinámica &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Vistas de administración dinámica y funciones relacionadas con ejecuciones &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_query_plan &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-query-plan-transact-sql.md)   
 [sys.dm_exec_plan_attributes &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-plan-attributes-transact-sql.md)   
 [sys.dm_exec_sql_text &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md)   
 [sys.dm_os_memory_objects &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-objects-transact-sql.md)   
 [sys.dm_os_memory_cache_entries &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-memory-cache-entries-transact-sql.md)   
 [FROM &#40;Transact-SQL&#41;](../../t-sql/queries/from-transact-sql.md)  
  
  


