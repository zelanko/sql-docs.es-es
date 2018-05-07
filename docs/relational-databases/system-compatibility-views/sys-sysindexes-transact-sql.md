---
title: Sys.sysindexes (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sysindexes
- sysindexes_TSQL
- sys.sysindexes
- sys.sysindexes_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sysindexes system table
- sys.sysindexes compatibility view
ms.assetid: f483d89c-35c4-4a08-8f8b-737fd80d13f5
caps.latest.revision: 57
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 276d2bfd5374fc24b31648250b5ffcd1eefb1ac7
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
---
# <a name="syssysindexes-transact-sql"></a>sys.sysindexes (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Contiene una fila por cada índice y tabla de la base de datos actual. Los índices XML no se admiten en esta vista. Índices y tablas con particiones no son totalmente compatibles en esta vista; Utilice la [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md) vista de catálogo en su lugar.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**id**|**int**|Id. de la tabla a la que pertenece el índice.|  
|**status**|**int**|Información de estado del sistema.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**first**|**binary(6)**|Puntero a la primera página o página raíz.<br /><br /> No usado cuando **indid** = 0.<br /><br /> NULL = índice tiene particiones cuando **indid** > 1.<br /><br /> NULL = la tabla tiene particiones cuando **indid** es 0 o 1.|  
|**indid**|**smallint**|Id. del índice:<br /><br /> 0 = Montón<br /><br /> 1 = Índice clúster<br /><br /> >1 = Índice no clúster|  
|**raíz**|**binary(6)**|Para **indid** > = 1, **raíz** es el puntero a la página raíz.<br /><br /> No usado cuando **indid** = 0.<br /><br /> NULL = índice tiene particiones cuando **indid** > 1.<br /><br /> NULL = la tabla tiene particiones cuando **indid** es 0 o 1.|  
|**minlen**|**smallint**|Tamaño mínimo de una fila.|  
|**keycnt**|**smallint**|Número de claves.|  
|**Id. de grupo**|**smallint**|Id. del grupo de archivos en el que se creó el objeto.<br /><br /> NULL = índice tiene particiones cuando **indid** > 1.<br /><br /> NULL = la tabla tiene particiones cuando **indid** es 0 o 1.|  
|**Dpages**|**int**|Para **indid** = 0 o **indid** = 1, **dpages** es el número de páginas de datos utilizadas.<br /><br /> Para **indid** > 1, **dpages** es el número de páginas de índice utilizadas.<br /><br /> 0 = índice tiene particiones cuando **indid** > 1.<br /><br /> 0 = la tabla tiene particiones cuando **indid** es 0 o 1.<br /><br /> No producen resultados precisos en caso de desbordamiento de fila.|  
|**Reservado**|**int**|Para **indid** = 0 o **indid** = 1, **reservada** es el número de páginas asignadas para todos los índices y datos de la tabla.<br /><br /> Para **indid** > 1, **reservada** es el número de páginas asignadas para el índice.<br /><br /> 0 = índice tiene particiones cuando **indid** > 1.<br /><br /> 0 = la tabla tiene particiones cuando **indid** es 0 o 1.<br /><br /> No producen resultados precisos en caso de desbordamiento de fila.|  
|**usar**|**int**|Para **indid** = 0 o **indid** = 1, **utiliza** es el número total de páginas utilizado para todos los datos de índice y tabla.<br /><br /> Para **indid** > 1, **utiliza** es el número de páginas utilizadas para el índice.<br /><br /> 0 = índice tiene particiones cuando **indid** > 1.<br /><br /> 0 = la tabla tiene particiones cuando **indid** es 0 o 1.<br /><br /> No producen resultados precisos en caso de desbordamiento de fila.|  
|**rowcnt**|**bigint**|Recuento de filas de datos se basa en **indid** = 0 y **indid** = 1.<br /><br /> 0 = índice tiene particiones cuando **indid** > 1.<br /><br /> 0 = la tabla tiene particiones cuando **indid** es 0 o 1.|  
|**rowmodctr**|**int**|Cuenta el número total de filas insertadas, eliminadas o actualizadas desde la última vez que se actualizaron las estadísticas de la tabla.<br /><br /> 0 = índice tiene particiones cuando **indid** > 1.<br /><br /> 0 = la tabla tiene particiones cuando **indid** es 0 o 1.<br /><br /> En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores, **rowmodctr** no es totalmente compatible con versiones anteriores. Para obtener más información, vea la sección Comentarios.|  
|**reserved3**|**int**|Devuelve 0.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**reserved4**|**int**|Devuelve 0.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**xmaxlen**|**smallint**|Tamaño máximo de una fila|  
|**maxirow**|**smallint**|Tamaño máximo de una fila de índice no hoja.<br /><br /> En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores, **maxirow** no es totalmente compatible con versiones anteriores.|  
|**OrigFillFactor**|**tinyint**|Valor de factor de relleno original empleado cuando se creó el índice. Este valor no se mantiene, aunque puede ser útil si necesita volver a crear un índice y no recuerda el valor del factor de relleno que se utilizó originalmente.|  
|**StatVersion**|**tinyint**|Devuelve 0.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**Reservado2**|**int**|Devuelve 0.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**FirstIAM**|**binary(6)**|NULL = Índice con particiones.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**impid**|**smallint**|Marca de implementación de índice.<br /><br /> Devuelve 0.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**LockFlags**|**smallint**|Se utiliza para restringir las granularidades de bloqueo que se tienen en cuenta para un índice. Por ejemplo, una tabla de búsqueda que es esencialmente de solo lectura se puede configurar de modo que solo imponga bloqueos en la tabla para minimizar el costo de bloqueo.|  
|**pgmodctr**|**int**|Devuelve 0.<br /><br /> [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**Claves**|**varbinary(816)**|Lista de los Id. de columna para las columnas que forman la clave de índice.<br /><br /> Devuelve NULL.<br /><br /> Para mostrar las columnas de clave de índice, use [sys.sysindexkeys](../../relational-databases/system-compatibility-views/sys-sysindexkeys-transact-sql.md).|  
|**Nombre**|**sysname**|Nombre del índice o estadística. Devuelve NULL cuando **indid** = 0. Modifique la aplicación para que busque un nombre de montón NULL.|  
|**statblob**|**imagen**|Objeto binario grande de estadística (BLOB).<br /><br /> Devuelve NULL.|  
|**MAXLEN**|**int**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**Filas**|**int**|Recuento de filas de datos se basa en **indid** = 0 y **indid** = 1, y el valor se repite para **indid** > 1.|  
  
## <a name="remarks"></a>Comentarios  
 Las columnas definidas como reservadas no deben utilizarse.  
  
 Las columnas **dpages**, **reservada**, y **utiliza** no devolverán resultados precisos si la tabla o índice contiene datos en la unidad de asignación row_overflow_data. Además, se realiza el seguimiento para el total de páginas de cada índice por separado y no se agregan para la tabla base. Para ver los recuentos de páginas, use el [sys.allocation_units](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md) o [sys.partitions](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md) vistas de catálogo, o la [sys.dm_db_partition_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md) vista de administración dinámica.  
  
 En SQL Server 2000 y versiones anteriores, [!INCLUDE[ssDE](../../includes/ssde-md.md)] mantenía contadores de modificaciones de filas. Este tipo de contadores se mantienen ahora en el nivel de columna. Por lo tanto, la **rowmodctr** columna se calcula y produce resultados que son similares a los resultados en versiones anteriores, pero no son exactos.  
  
 Si utiliza el valor en **rowmodctr** para determinar cuándo actualizar las estadísticas, tenga en cuenta las siguientes soluciones:  
  
-   No haga nada. El nuevo **rowmodctr** valor con frecuencia le ayudará a determinar cuándo actualizar las estadísticas porque el comportamiento es razonablemente parecido a los resultados de las versiones anteriores.  
  
-   Utilice AUTO_UPDATE_STATISTICS. Para obtener más información, vea [estadísticas](../../relational-databases/statistics/statistics.md).  
  
-   Utilice un límite de tiempo para determinar cuándo debe actualizar las estadísticas. Por ejemplo, cada hora, cada día o cada semana.  
  
-   Utilice la información de nivel de aplicación para determinar cuándo debe actualizar las estadísticas. Por ejemplo, cada vez el valor máximo de un **identidad** columna los cambios en más de 10.000, o se realiza cada vez que un masiva la operación de inserción.  
  
## <a name="see-also"></a>Vea también  
 [Vistas de catálogo &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [Asignar tablas del sistema a vistas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)  
  
  
