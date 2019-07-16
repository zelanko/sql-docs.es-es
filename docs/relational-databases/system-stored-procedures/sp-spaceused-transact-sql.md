---
title: sp_spaceused (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_spaceused_TSQL
- sp_spaceused
dev_langs:
- TSQL
helpviewer_keywords:
- sp_spaceused
ms.assetid: c6253b48-29f5-4371-bfcd-3ef404060621
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1dc80f17fc88fa665b41a130bb69ebe0d4f1f26c
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68032868"
---
# <a name="spspaceused-transact-sql"></a>sp_spaceused (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Muestra el número de filas, el espacio de disco reservado y el espacio de disco utilizado por una tabla, vista indizada o cola de [!INCLUDE[ssSB](../../includes/sssb-md.md)] de la base de datos actual, o bien muestra el espacio de disco reservado y el que utiliza la base de datos completa.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sp_spaceused [[ @objname = ] 'objname' ]   
[, [ @updateusage = ] 'updateusage' ]  
[, [ @mode = ] 'mode' ]  
[, [ @oneresultset = ] oneresultset ]  
[, [ @include_total_xtp_storage = ] include_total_xtp_storage ]
```  
  
## <a name="arguments"></a>Argumentos  

Para [!INCLUDE[sssdw-md](../../includes/sssdw-md.md)] y [!INCLUDE[sspdw-md](../../includes/sspdw-md.md)], `sp_spaceused` debe especificar los parámetros con nombre (por ejemplo `sp_spaceused (@objname= N'Table1');` en lugar de confiar en la posición ordinal de parámetros. 

`[ @objname = ] 'objname'`
   
 Se trata del nombre completo o incompleto de la tabla, vista indizada o cola para la que se solicita información de uso del espacio. Las comillas solo son necesarias si se especifica un nombre de objeto completo. Si se proporciona un nombre de objeto completo, incluido el nombre de una base de datos, el nombre de la base de datos debe ser el nombre de la base de datos actual.  
Si *objname* no se especifica, se devuelven resultados para toda la base de datos.  
*objname* es **nvarchar(776)** , su valor predeterminado es null.  
> [!NOTE]  
> [!INCLUDE[sssdw-md](../../includes/sssdw-md.md)] y [!INCLUDE[sspdw-md](../../includes/sspdw-md.md)] sólo admite objetos de base de datos y tabla.
  
`[ @updateusage = ] 'updateusage'` Indica que se debe ejecutar DBCC UPDATEUSAGE para actualizar la información de uso de espacio. Cuando *objname* no es se especifica, la instrucción se ejecuta en la base de datos completa; en caso contrario, la instrucción se ejecuta en *objname*. Los valores pueden ser **true** o **false**. *UPDATEUSAGE* es **varchar (5)** , su valor predeterminado es **false**.  
  
`[ @mode = ] 'mode'` Indica el ámbito de los resultados. Para una tabla ajustada o la base de datos, el *modo* parámetro le permite incluir o excluir de la parte del objeto remota. Para obtener más información, vea [Stretch Database](../../sql-server/stretch-database/stretch-database.md).  
  
 El *modo* argumento puede tener los siguientes valores:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|ALL|Devuelve las estadísticas de almacenamiento del objeto o la base de datos incluidos en la parte local y la parte remota.|  
|LOCAL_ONLY|Devuelve las estadísticas de almacenamiento sólo una parte local del objeto o la base de datos. Si el objeto o la base de datos no está habilitada para Stretch, devuelve las estadísticas de la mismas que cuando @mode = ALL.|  
|REMOTE_ONLY|Devuelve las estadísticas de almacenamiento sólo una parte remota de la base de datos u objeto. Esta opción genera un error cuando se cumple una de las condiciones siguientes:<br /><br /> La tabla no está habilitada para Stretch.<br /><br /> La tabla está habilitada para Stretch, pero nunca se ha habilitado la migración de datos. En este caso, la tabla remota no tiene todavía un esquema.<br /><br /> El usuario ha soltado manualmente la tabla remota.<br /><br /> El aprovisionamiento del archivo de datos remoto ha devuelto un estado de éxito, pero en realidad se produjo un error.|  
  
 *modo* es **varchar (11)** , su valor predeterminado es **n '** .  
  
`[ @oneresultset = ] oneresultset` Indica si se debe devolver un conjunto de resultados único. El *oneresultset* argumento puede tener los siguientes valores:  
  
|Valor|Descripción|  
|-----------|-----------------|  
|0|Cuando *@objname* es null o no se especifica, se devuelven dos conjuntos de resultados. Dos conjuntos de resultados es el comportamiento predeterminado.|  
|1|Cuando *@objname* = null o no es se especifica, se devuelve un conjunto de resultados único.|  
  
 *oneresultset* es **bit**, su valor predeterminado es **0**.  

`[ @include_total_xtp_storage] 'include_total_xtp_storage'`
**Se aplica a:** [!INCLUDE[sssql17-md](../../includes/sssql17-md.md)], [!INCLUDE[sssds-md](../../includes/sssds-md.md)].  
  
 Cuando @oneresultset= 1, el parámetro @include_total_xtp_storage determina si el conjunto de resultados solo incluye las columnas para el almacenamiento MEMORY_OPTIMIZED_DATA. El valor predeterminado es decir, 0, de forma predeterminada (si se omite el parámetro) no se incluyen las columnas XTP en el conjunto de resultados.  

## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Si *objname* se omite y el valor de *oneresultset* es 0, se devuelven los siguientes conjuntos de resultados para proporcionar información de tamaño de base de datos actual.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|Nombre de la base de datos actual.|  
|**database_size**|**varchar(18)**|Tamaño de la base de datos actual en megabytes. **database_size** incluye archivos de registro y de datos.|  
|**espacio sin asignar**|**varchar(18)**|Espacio de la base de datos que no se ha reservado para objetos de base de datos.|  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**reserved**|**varchar(18)**|Espacio total asignado por los objetos de la base de datos.|  
|**data**|**varchar(18)**|Cantidad total de espacio utilizado por los datos.|  
|**index_size**|**varchar(18)**|Cantidad total de espacio utilizado por índices.|  
|**sin usar**|**varchar(18)**|Espacio total reservado para los objetos de la base de datos, pero no utilizado todavía.|  
  
 Si *objname* se omite y el valor de *oneresultset* es 1, se devuelve el siguiente conjunto de resultados único para proporcionar información de tamaño de base de datos actual.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|Nombre de la base de datos actual.|  
|**database_size**|**varchar(18)**|Tamaño de la base de datos actual en megabytes. **database_size** incluye archivos de registro y de datos.|  
|**espacio sin asignar**|**varchar(18)**|Espacio de la base de datos que no se ha reservado para objetos de base de datos.|  
|**reserved**|**varchar(18)**|Espacio total asignado por los objetos de la base de datos.|  
|**data**|**varchar(18)**|Cantidad total de espacio utilizado por los datos.|  
|**index_size**|**varchar(18)**|Cantidad total de espacio utilizado por índices.|  
|**sin usar**|**varchar(18)**|Espacio total reservado para los objetos de la base de datos, pero no utilizado todavía.|  
  
 Si *objname* se especifica, se devuelve el siguiente conjunto de resultados para el objeto especificado.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**name**|**nvarchar(128)**|Nombre del objeto del que se solicitó la información de utilización de espacio.<br /><br /> El nombre del esquema del objeto no se devuelve. Si se requiere el nombre del esquema, use el [sys.dm_db_partition_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md) o [sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md) vistas de administración dinámica para obtener información de tamaño equivalente.|  
|**rows**|**char(20)**|Número de filas de la tabla. Si el objeto especificado es una cola de [!INCLUDE[ssSB](../../includes/sssb-md.md)], esta columna indica el número de mensajes de la misma.|  
|**reserved**|**varchar(18)**|Cantidad total de espacio reservado para *objname*.|  
|**data**|**varchar(18)**|Cantidad total de espacio utilizado por los datos en *objname*.|  
|**index_size**|**varchar(18)**|Cantidad total de espacio utilizado por los índices en *objname*.|  
|**sin usar**|**varchar(18)**|Cantidad total de espacio reservado para *objname* pero aún no se ha usado.|  
 
Este es el modo predeterminado, cuando se especifica ningún parámetro. Los siguientes conjuntos de resultados se devuelven información de tamaño de base de datos en disco que se detallan. 

|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|Nombre de la base de datos actual.|  
|**database_size**|**varchar(18)**|Tamaño de la base de datos actual en megabytes. **database_size** incluye archivos de registro y de datos. Si la base de datos tiene un grupo de archivos MEMORY_OPTIMIZED_DATA, esto incluye el tamaño en disco total de todos los archivos de punto de control en el grupo de archivos.|  
|**espacio sin asignar**|**varchar(18)**|Espacio de la base de datos que no se ha reservado para objetos de base de datos. Si la base de datos tiene un grupo de archivos MEMORY_OPTIMIZED_DATA, esto incluye el tamaño en disco total de los archivos de punto de control con estado PRECREATED en el grupo de archivos.|  

Espacio usado por las tablas en la base de datos: (este conjunto de resultados no refleja las tablas optimizadas para memoria, ya que no hay ninguna contabilidad por tabla de uso de disco) 

|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**reserved**|**varchar(18)**|Espacio total asignado por los objetos de la base de datos.|  
|**data**|**varchar(18)**|Cantidad total de espacio utilizado por los datos.|  
|**index_size**|**varchar(18)**|Cantidad total de espacio utilizado por índices.|  
|**sin usar**|**varchar(18)**|Espacio total reservado para los objetos de la base de datos, pero no utilizado todavía.|

Se devuelve el conjunto de resultados siguiente **sólo si** la base de datos tiene un grupo de archivos MEMORY_OPTIMIZED_DATA con al menos un contenedor: 

|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**xtp_precreated**|**varchar(18)**|Tamaño total de archivos de punto de control con estado PRECREATED, en KB. Cuenta para el espacio sin asignar en la base de datos como un todo. [Por ejemplo, si hay 600.000 KB de archivos de punto de comprobación creados previamente, esta columna contiene ' 600000 KB']|  
|**xtp_used**|**varchar(18)**|Tamaño total de archivos de punto de comprobación con Estados UNDER CONSTRUCTION, ACTIVE y MERGE TARGET, en KB. Este es el espacio en disco usado activamente para los datos en tablas optimizadas para memoria.|  
|**xtp_pending_truncation**|**varchar(18)**|Tamaño total de archivos de punto de control con estado WAITING_FOR_LOG_TRUNCATION, en KB. Este es el espacio en disco usado para los archivos de punto de control que están en espera de limpieza, una vez que se produce el truncamiento del registro.|

Si *objname* es se omite, el valor de oneresultset es 1, y *include_total_xtp_storage* es 1, se devuelve el siguiente conjunto de resultados único para proporcionar información de tamaño de base de datos actual. Si `include_total_xtp_storage` es 0 (valor predeterminado), se omiten las últimas tres columnas. 

|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**database_name**|**nvarchar(128)**|Nombre de la base de datos actual.|  
|**database_size**|**varchar(18)**|Tamaño de la base de datos actual en megabytes. **database_size** incluye archivos de registro y de datos. Si la base de datos tiene un grupo de archivos MEMORY_OPTIMIZED_DATA, esto incluye el tamaño en disco total de todos los archivos de punto de control en el grupo de archivos.|
|**espacio sin asignar**|**varchar(18)**|Espacio de la base de datos que no se ha reservado para objetos de base de datos. Si la base de datos tiene un grupo de archivos MEMORY_OPTIMIZED_DATA, esto incluye el tamaño en disco total de los archivos de punto de control con estado PRECREATED en el grupo de archivos.|  
|**reserved**|**varchar(18)**|Espacio total asignado por los objetos de la base de datos.|  
|**data**|**varchar(18)**|Cantidad total de espacio utilizado por los datos.|  
|**index_size**|**varchar(18)**|Cantidad total de espacio utilizado por índices.|  
|**sin usar**|**varchar(18)**|Espacio total reservado para los objetos de la base de datos, pero no utilizado todavía.|
|**xtp_precreated**|**varchar(18)**|Tamaño total de archivos de punto de control con estado PRECREATED, en KB. Esta cuenta para el espacio sin asignar en la base de datos como un todo. Devuelve NULL si la base de datos no tiene un grupo de archivos memory_optimized_data con al menos un contenedor. *Esta columna solo está incluido si @include_total_xtp_storage= 1*.| 
|**xtp_used**|**varchar(18)**|Tamaño total de archivos de punto de comprobación con Estados UNDER CONSTRUCTION, ACTIVE y MERGE TARGET, en KB. Este es el espacio en disco usado activamente para los datos en tablas optimizadas para memoria. Devuelve NULL si la base de datos no tiene un grupo de archivos memory_optimized_data con al menos un contenedor. *Esta columna solo está incluido si @include_total_xtp_storage= 1*.| 
|**xtp_pending_truncation**|**varchar(18)**|Tamaño total de archivos de punto de control con estado WAITING_FOR_LOG_TRUNCATION, en KB. Este es el espacio en disco usado para los archivos de punto de control que están en espera de limpieza, una vez que se produce el truncamiento del registro. Devuelve NULL si la base de datos no tiene un grupo de archivos memory_optimized_data con al menos un contenedor. Esta columna solo está incluido si `@include_total_xtp_storage=1`.|

## <a name="remarks"></a>Comentarios  
 **database_size** sea siempre mayor que la suma de **reservada** + **espacio sin asignar** porque incluye el tamaño de los archivos de registro, pero **reservado**y **unallocated_space** considere solo las páginas de datos.  
  
 Las páginas que usan los índices XML e índices de texto completo se incluyen en **index_size** para ambos conjuntos de resultados. Cuando *objname* se especifica, también se cuentan las páginas de los índices XML e índices de texto completo para el objeto en el total **reservada** y **index_size** resultados.  
  
 Si se calcula el uso de espacio para una base de datos o un objeto que tiene un índice espacial, las columnas de tamaño de espacio, como **database_size**, **reservada**, y **index_size**, incluir el tamaño del índice espacial.  
  
 Cuando *updateusage* se especifica, el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] examina los datos de las páginas de la base de datos y las realiza correcciones necesarias la **sys.allocation_units** y **sys.partitions** vistas relacionados con el espacio de almacenamiento usado por cada tabla de catálogo. Existen algunas situaciones, como por ejemplo después de quitar un índice, en las que la información de espacio para la tabla podría no estar actualizada. *UPDATEUSAGE* puede tardar algún tiempo en ejecutarse en tablas grandes o bases de datos. Use *updateusage* solo cuando sospeche que están devolviéndose valores incorrectos y cuando el proceso no tendrá un efecto adverso en otros usuarios o procesos en la base de datos. Si se prefiere, DBCC UPDATEUSAGE puede ejecutarse por separado.  
  
> [!NOTE]  
>  Al quitar o volver a generar índices grandes, o al quitar o truncar tablas grandes, el [!INCLUDE[ssDE](../../includes/ssde-md.md)] difiere las cancelaciones de asignación de páginas, así como sus bloqueos asociados, hasta que se confirma la transacción. Las operaciones de eliminación diferidas no liberan inmediatamente el espacio asignado. Por lo tanto, los valores devueltos por **sp_spaceused** inmediatamente después de quitar o truncar un objeto grande puede no reflejar el espacio en disco real disponible.  
  
## <a name="permissions"></a>Permisos  
 El permiso para ejecutar **sp_spaceused** se otorga al rol **public** . Solo los miembros del rol fijo de base de datos **db_owner** pueden especificar el parámetro **@updateusage** .  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-displaying-disk-space-information-about-a-table"></a>A. Mostrar información de espacio en disco acerca de una tabla  
 El siguiente ejemplo muestra información de espacio en disco para la tabla `Vendor` y sus índices.  
  
```sql  
USE AdventureWorks2012;  
GO  
EXEC sp_spaceused N'Purchasing.Vendor';  
GO  
```  
  
### <a name="b-displaying-updated-space-information-about-a-database"></a>b. Mostrar información de espacio actualizada acerca de una base de datos  
 En este ejemplo se resume el espacio utilizado en la base de datos actual y se utiliza el parámetro opcional `@updateusage` para garantizar que se devuelvan los valores actuales.  
  
```sql  
USE AdventureWorks008R2;  
GO  
EXEC sp_spaceused @updateusage = N'TRUE';  
GO  
```  
  
### <a name="c-displaying-space-usage-information-about-the-remote-table-associated-with-a-stretch-enabled-table"></a>C. Mostrar información de uso de espacio acerca de la tabla remota asociada con una tabla habilitada para Stretch  
 En el ejemplo siguiente se resume el espacio utilizado por la tabla remota asociada con una tabla habilitada para Stretch mediante el uso de la **@mode** argumento para especificar el destino remoto. Para obtener más información, vea [Stretch Database](../../sql-server/stretch-database/stretch-database.md).  
  
```sql  
USE StretchedAdventureWorks2016  
GO  
EXEC sp_spaceused N'Purchasing.Vendor', @mode = 'REMOTE_ONLY'  
```  
  
### <a name="d-displaying-space-usage-information-for-a-database-in-a-single-result-set"></a>D. Mostrar información de uso de espacio para una base de datos en un único resultado conjunto  
 El ejemplo siguiente resume el uso del espacio de la base de datos actual en un único conjunto de resultados.  
  
```sql  
USE AdventureWorks2016  
GO  
EXEC sp_spaceused @oneresultset = 1  
```  

### <a name="e-displaying-space-usage-information-for-a-database-with-at-least-one-memoryoptimized-file-group-in-a-single-result-set"></a>E. Mostrar la información de uso de espacio para una base de datos con al menos un grupo de archivos MEMORY_OPTIMIZED en un único conjunto de resultados 
 El ejemplo siguiente resume el uso del espacio de la base de datos actual con al menos un grupo de archivos MEMORY_OPTIMIZED en un único conjunto de resultados.
 
```sql
USE WideWorldImporters
GO
EXEC sp_spaceused @updateusage = 'FALSE', @mode = 'ALL', @oneresultset = '1', @include_total_xtp_storage = '1';
GO
``` 

### <a name="f-displaying-space-usage-information-for-a-memoryoptimized-table-object-in-a-database"></a>F. Mostrar información de uso de espacio para un objeto de tabla MEMORY_OPTIMIZED en una base de datos.
 El ejemplo siguiente resume el uso del espacio de un objeto de tabla MEMORY_OPTIMIZED en la base de datos actual con al menos un grupo de archivos MEMORY_OPTIMIZED.
 
```sql
USE WideWorldImporters
GO
EXEC sp_spaceused
@objname = N'VehicleTemparatures',
@updateusage = 'FALSE',
@mode = 'ALL',
@oneresultset = '0',
@include_total_xtp_storage = '1';
GO
```  

## <a name="see-also"></a>Vea también  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)   
 [DBCC UPDATEUSAGE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-updateusage-transact-sql.md)   
 [SQL Server Service Broker](../../database-engine/configure-windows/sql-server-service-broker.md)   
 [sys.allocation_units &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-allocation-units-transact-sql.md)   
 [sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)   
 [sys.index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-index-columns-transact-sql.md)   
 [sys.objects &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)   
 [sys.partitions &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-partitions-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
