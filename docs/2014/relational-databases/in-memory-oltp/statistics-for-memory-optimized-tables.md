---
title: Estadísticas para las tablas con optimización para memoria | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: e644766d-1d1c-43d7-83ff-8ccfe4f3af9f
author: rothja
ms.author: jroth
ms.openlocfilehash: 0ae09d76c2642e23c56afcdd5ae4e1e468ef5883
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85025772"
---
# <a name="statistics-for-memory-optimized-tables"></a>Estadísticas para las tablas con optimización para memoria
  El optimizador de consultas utiliza las estadísticas de las columnas para crear planes de consulta que mejoren el rendimiento de las consultas. Las estadísticas se recopilan de las tablas de la base de datos y se almacenan en los metadatos de la base de datos.  
  
 Las estadísticas se crean automáticamente, pero también se pueden crear manualmente. Por ejemplo, para las columnas de clave de índice, las estadísticas se crean automáticamente cuando se crea el índice. Para obtener más información acerca de cómo crear estadísticas, vea [Statistics](../statistics/statistics.md).  
  
 Normalmente, los datos de tabla cambian a medida que se insertan, se actualizan y se eliminan filas. Esto significa que las estadísticas deben actualizarse periódicamente. De forma predeterminada, las estadísticas basadas en disco se actualizan automáticamente cuando el optimizador determina que podrían estar obsoletas.  
  
 Las estadísticas de tablas optimizadas para memoria no se actualizan de forma predeterminada. En su lugar, debe actualizarlas manualmente. Use [Update statistics &#40;Transact-SQL&#41;](/sql/t-sql/statements/update-statistics-transact-sql) para columnas, índices o tablas individuales. Use [sp_updatestats &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql) para actualizar las estadísticas de todas las tablas de usuario e internas de la base de datos.  
  
 Al usar [Create statistics &#40;Transact-sql&#41;](/sql/t-sql/statements/create-statistics-transact-sql) o [UPDATE STATISTICS &#40;transact-SQL&#41;](/sql/t-sql/statements/update-statistics-transact-sql), debe especificar `NORECOMPUTE` para deshabilitar la actualización automática de las estadísticas de las tablas optimizadas para memoria. En el caso de las tablas basadas en disco, [sp_updatestats &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql) solo actualiza las estadísticas si la tabla se ha modificado desde el último [sp_updatestats &#40;Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql)&#41;. En el caso de las tablas optimizadas para memoria, [sp_updatestats &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql) siempre genera estadísticas actualizadas. [sp_updatestats &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql) es una buena opción para las tablas optimizadas para memoria; en caso contrario, debe saber qué tablas tienen cambios significativos para que pueda actualizar las estadísticas de forma individual.  
  
 Se pueden generar estadísticas mediante el muestreo de los datos o realizando un examen completo. Las estadísticas muestreadas solo usan un ejemplo de los datos de la tabla para estimar la distribución de los datos. Las estadísticas completas examinan toda la tabla para determinar la distribución de los datos. Las estadísticas completas suelen ser más precisas pero tardan más tiempo en calcularse. Las estadísticas muestreadas se pueden recopilar más rápidamente.  
  
 Las tablas basadas en disco usan las estadísticas muestreadas de forma predeterminada. Las tablas con optimización para memoria solo admiten las estadísticas completas. Al usar [Create statistics &#40;Transact-sql&#41;](/sql/t-sql/statements/create-statistics-transact-sql) o [UPDATE STATISTICS &#40;transact-SQL&#41;](/sql/t-sql/statements/update-statistics-transact-sql), debe especificar la `FULLSCAN` opción para las tablas optimizadas para memoria.  
  
 Consideraciones adicionales sobre las estadísticas de tablas optimizadas para memoria:  
  
-   Los índices de las tablas optimizadas para memoria se crean con la tabla. Las estadísticas de las columnas de clave de índice se crean cuando la tabla está vacía. Por lo tanto, estas estadísticas deberán actualizarse después de que los datos se hayan cargado en la tabla.  
  
-   Para los procedimientos almacenados compilados de forma nativa, los planes de ejecución de las consultas del procedimiento se optimizan cuando se compila el procedimiento. Esto solo ocurre cuando se crea el procedimiento y se reinicia el servidor, no cuando se actualizan las estadísticas. Por tanto, las tablas deben contener un conjunto de datos representativo, y las estadísticas deben actualizarse antes de que se creen los procedimientos. (Los procedimientos almacenados compilados de forma nativa se vuelven a compilar si la base de datos se deja sin conexión y se vuelve a poner en línea o si se ha reiniciado el servidor).  
  
## <a name="guidelines-for-statistics-when-deploying-memory-optimized-tables"></a>Directrices para las estadísticas cuando se implementan tablas con optimización para memoria  
 Para asegurarse de que el optimizador de consultas dispone de estadísticas actualizadas al crear los planes de consulta, implemente las tablas optimizadas para memoria siguiendo estos cinco pasos:  
  
1.  Cree tablas e índices. Los índices se especifican insertados en instrucciones `CREATE TABLE`.  
  
2.  Cargue datos en las tablas.  
  
3.  Actualice las estadísticas de las tablas.  
  
4.  Cree procedimientos almacenados que tengan acceso a las tablas.  
  
5.  Ejecute la carga de trabajo, que puede contener una combinación de procedimientos almacenados de [!INCLUDE[tsql](../../../includes/tsql-md.md)] compilados de forma nativa e interpretados, así como lotes ad hoc.  
  
 El hecho de crear procedimientos almacenados compilados de forma nativa después de cargar los datos y actualizar las estadísticas asegura que el optimizador dispondrá de estadísticas para las tablas optimizadas para memoria. Esto garantizará planes de consulta eficaces cuando se compile el procedimiento.  
  
## <a name="guidelines-for-maintaining-statistics-on-memory-optimized-tables"></a>Directrices para el mantenimiento de estadísticas en las tablas con optimización para memoria  
 Para mantener las estadísticas actualizadas, actualice periódicamente las estadísticas de las tablas optimizadas para memoria.  
  
 Si los datos cambian con frecuencia, deberá actualizar las estadísticas a menudo. Por ejemplo, actualice las estadísticas de las tablas después de cada actualización por lotes. Después de actualizar las estadísticas, quite y vuelva a crear los procedimientos almacenados compilados de forma nativa para que puedan beneficiarse de las estadísticas actualizadas.  
  
 .  
  
 No actualice las estadísticas durante un período de carga de trabajo máxima.  
  
 Para actualizar las estadísticas:  
  
-   Use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para [Create a Maintenance Plan](../maintenance-plans/create-a-maintenance-plan.md) con una [Tarea Actualizar estadísticas](../maintenance-plans/update-statistics-task-maintenance-plan.md)  
  
-   O bien, actualice las estadísticas mediante un script [!INCLUDE[tsql](../../../includes/tsql-md.md)] , tal como se describe a continuación.  
  
 Para actualizar las estadísticas de una sola tabla optimizada para memoria (*myschema*. *Mytable*), ejecute el script siguiente:  
  
```  
UPDATE STATISTICS myschema.Mytable WITH FULLSCAN, NORECOMPUTE  
```  
  
 Para actualizar las estadísticas de todas las tablas optimizadas para memoria de la base de datos actual, ejecute el script siguiente:  
  
```sql  
DECLARE @sql NVARCHAR(MAX) = N''  
  
SELECT @sql += N'  
   UPDATE STATISTICS ' + quotename(schema_name(schema_id)) + N'.' + quotename(name) + N' WITH FULLSCAN, NORECOMPUTE'  
FROM sys.tables WHERE is_memory_optimized=1  
  
EXEC sp_executesql @sql  
```  
  
 Para actualizar las estadísticas de todas las tablas de la base de datos, ejecute [sp_updatestats &#40;&#41;de Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-updatestats-transact-sql).  
  
 En el ejemplo siguiente se informa de cuándo se han actualizado por última vez las estadísticas de las tablas optimizadas para memoria. Esta información puede ayudarle a determinar si necesita actualizar las estadísticas.  
  
```sql  
select t.object_id, t.name, sp.last_updated as 'stats_last_updated'  
from sys.tables t join sys.stats s on t.object_id=s.object_id cross apply sys.dm_db_stats_properties(t.object_id, s.stats_id) sp  
where t.is_memory_optimized=1  
```  
  
## <a name="see-also"></a>Consulte también  
 [Tablas optimizadas para la memoria](memory-optimized-tables.md)  
  
  
