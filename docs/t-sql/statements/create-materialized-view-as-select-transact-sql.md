---
title: CREATE MATERIALIZED VIEW AS SELECT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2020
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: data-warehouse
ms.topic: language-reference
f1_keywords:
- CREATE VIEW
- VIEW_TSQL
- VIEW
- CREATE_VIEW_TSQL
- SCHEMABINDING_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- table creation [SQL Server], CREATE VIEW
- views [SQL Server], creating
- CREATE VIEW statement
- updatable partitioned views
- tables [SQL Server], virtual
- updatable views
- modifying partitioned views
- virtual tables [SQL Server]
- number of columns per view
- partitioned views [SQL Server], creating
- WITH ENCRYPTION clause
- WITH CHECK OPTION clause
- partitioned views [SQL Server], modifying
- partitioned views [SQL Server], replication
- distributed partitioned views [SQL Server]
- views [SQL Server], indexed views
- maximum number of columns per view
ms.assetid: aecc2f73-2ab5-4db9-b1e6-2f9e3c601fb9
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest||=sqlallproducts-allversions
ms.openlocfilehash: 73fcf068c55b28448d87245b380281b461ef36b0
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/17/2020
ms.locfileid: "81633615"
---
# <a name="create-materialized-view-as-select-transact-sql"></a>CREATE MATERIALIZED VIEW AS SELECT (Transact-SQL)  

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

En este artículo se explica la instrucción CREATE MATERIALIZED VIEW AS SELECT de T-SQL en Azure SQL Data Warehouse para soluciones en desarrollo. En el artículo también se proporcionan ejemplos de código.

Una vista materializada conserva los datos que ha devuelto la consulta de visualización de definición y se actualiza automáticamente a medida que cambian los datos en las tablas subyacentes.   Mejora el rendimiento de las consultas complejas (por lo general, consultas con combinaciones y agregaciones), a la vez que ofrece operaciones de mantenimiento simples.   Con su función de correspondencia automática del plan de ejecución, no es necesario que se haga referencia a una vista materializada en la consulta para que el optimizador tenga en cuenta la vista con fines de sustitución.  Esta capacidad permite a los ingenieros de datos implementar vistas materializadas como mecanismo para mejorar el tiempo de respuesta de las consultas, sin necesidad de cambiarlas.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```syntaxsql
CREATE MATERIALIZED VIEW [ schema_name. ] materialized_view_name
    WITH (  
      <distribution_option>
    )
    AS <select_statement>
[;]

<distribution_option> ::=
    {  
        DISTRIBUTION = HASH ( distribution_column_name )  
      | DISTRIBUTION = ROUND_ROBIN  
    }

<select_statement> ::=
    SELECT select_criteria
```  
  
## <a name="arguments"></a>Argumentos

*schema_name*     
 Es el nombre del esquema al que pertenece la vista.  
  
*materialized_view_name*   
Es el nombre de la vista. Los nombres de las vistas deben cumplir las reglas de los identificadores. La especificación del nombre del propietario de la vista es opcional.  

*opción de distribución*     
Solo se admiten distribuciones HASH y ROUND_ROBIN.

*select_statement*   
La lista SELECT de la definición de la vista materializada debe cumplir al menos uno de estos dos criterios:
- La lista SELECT contiene una función de agregado.
- Se usa GROUP BY en la definición de la vista materializada y todas las columnas de GROUP BY se incluyen en la lista SELECT.  En la cláusula GROUP BY se pueden usar hasta 32 columnas.

Las funciones de agregado son necesarias en la lista SELECT de la definición de la vista materializada.  Entre las agregaciones admitidas figuran MAX, MIN, AVG, COUNT, COUNT_BIG, SUM, VAR, STDEV.

Cuando se usan los agregados MIN/MAX en la lista SELECT de la definición de la vista materializada, es necesario cumplir estos requisitos:
 
- FOR_APPEND es necesario.  Por ejemplo:
  ```sql 
  CREATE MATERIALIZED VIEW mv_test2  
  WITH (distribution = hash(i_category_id), FOR_APPEND)  
  AS
  SELECT MAX(i.i_rec_start_date) as max_i_rec_start_date, MIN(i.i_rec_end_date) as min_i_rec_end_date, i.i_item_sk, i.i_item_id, i.i_category_id
  FROM syntheticworkload.item i  
  GROUP BY i.i_item_sk, i.i_item_id, i.i_category_id
  ```

- La vista materializada se deshabilitará cuando tenga lugar una operación UPDATE o DELETE en las tablas base de referencia.  Esta restricción no se aplica a las operaciones INSERT.  Para volver a habilitar la vista materializada, ejecute ALTER MATERIALIZED VIEW con REBUILD.
  
## <a name="remarks"></a>Observaciones

Las vistas materializadas en el almacenamiento de datos de Azure son similares a las vistas indexadas de SQL Server.  Comparte casi las mismas restricciones que la vista indizada (consulte [Crear vistas indizadas](/sql/relational-databases/views/create-indexed-views) para obtener más información), salvo que una vista materializada admite las funciones de agregado.   

La vista materializada solo admite CLUSTERED COLUMNSTORE INDEX. 

Una vista materializada no puede hacer referencia a otras vistas.  

No se puede crear una vista materializada en una tabla con enmascaramiento de datos dinámicos (DDM), aunque la columna DDM no forme parte de la vista materializada.  Si una columna de tabla forma parte de una vista materializada activa o una vista materializada deshabilitada, DDM no se puede agregar a esta columna.  

No se puede crear una vista materializada en una tabla con seguridad de nivel de fila habilitada.

Las vistas materializadas se pueden crear en tablas con particiones.  La partición SPLIT/MERGE se admite en las tablas base de las vistas materializadas, mientras que la partición SWITCH, no.  
 
ALTER TABLE SWITCH no se admite en las tablas a las que se hace referencia en las vistas materializadas. Deshabilite o quite las vistas materializadas antes de usar ALTER TABLE SWITCH. En los siguientes escenarios, la creación de una vista materializada requiere la adición de nuevas columnas a la vista materializada:

|Escenario|Nuevas columnas para agregar a la vista materializada|Comentario|  
|-----------------|---------------|-----------------|
|Falta COUNT_BIG() en la lista SELECT de la definición de una vista materializada.| COUNT_BIG (*) |Se agrega automáticamente al crear una vista materializada.  No se requiere ninguna acción del usuario.|
|SUM(a) lo especifican los usuarios en la lista SELECT de la definición de una vista materializada Y "a" es una expresión que admite un valor NULL. |COUNT_BIG (a) |Los usuarios deben agregar la expresión "a" manualmente en la definición de la vista materializada.|
|AVG(a) lo especifican los usuarios en la lista SELECT de la definición de una vista materializada en la que "a" es una expresión.|SUM(a), COUNT_BIG(a)|Se agrega automáticamente al crear una vista materializada.  No se requiere ninguna acción del usuario.|
|STDEV(a) lo especifican los usuarios en la lista SELECT de la definición de una vista materializada en la que "a" es una expresión.|SUM(a), COUNT_BIG(a), SUM(square(a))|Se agrega automáticamente al crear una vista materializada.  No se requiere ninguna acción del usuario. |
| | | |

Las vistas materializadas, una vez creadas, son visibles dentro de SQL Server Management Studio en la carpeta de vistas de la instancia de Azure SQL Data Warehouse.

Los usuarios pueden ejecutar [SP_SPACEUSED](/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql?view=azure-sqldw-latest) y [DBCC PDW_SHOWSPACEUSED](/sql/t-sql/database-console-commands/dbcc-pdw-showspaceused-transact-sql?view=azure-sqldw-latest) para determinar el espacio que consume una vista materializada.  

Una vista materializada se puede quitar mediante DROP VIEW.  Puede usar ALTER MATERIALIZED VIEW para deshabilitar o volver a generar una vista materializada.   

El plan de EXPLAIN y el plan de ejecución estimado gráfico en SQL Server Management Studio pueden mostrar si una vista materializada se tiene en cuenta por el optimizador de consultas para la ejecución de las consultas. y el plan de ejecución estimado gráfico en SQL Server Management Studio pueden mostrar si una vista materializada se tiene en cuenta por el optimizador de consultas para la ejecución de las consultas.

Para averiguar si una instrucción SQL puede beneficiarse de una nueva vista materializada, ejecute el comando `EXPLAIN` con `WITH_RECOMMENDATIONS`.  Para obtener más información, consulte [EXPLAIN (Transact-SQL)](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest).

## <a name="permissions"></a>Permisos

Se necesita el permiso CREATE VIEW en la base de datos y el permiso ALTER en el esquema en que se crea la vista. 
  
## <a name="see-also"></a>Consulte también

[Optimización del rendimiento con vista materializada](/azure/sql-data-warehouse/performance-tuning-materialized-views)   
[ALTER MATERIALIZED VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-materialized-view-transact-sql?view=azure-sqldw-latest)      
[DROP VIEW](/sql/t-sql/statements/drop-view-transact-sql?view=azure-sqldw-latest)  
[EXPLAIN &#40;Transact-SQL&#41;](/sql/t-sql/queries/explain-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_column_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-column-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_distribution_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-distribution-properties-transact-sql?view=azure-sqldw-latest)   
[sys.pdw_materialized_view_mappings &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-pdw-materialized-view-mappings-transact-sql?view=azure-sqldw-latest)   
[DBCC PDW_SHOWMATERIALIZEDVIEWOVERHEAD &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-pdw-showmaterializedviewoverhead-transact-sql?view=azure-sqldw-latest)   
[Vistas de catálogo de SQL Data Warehouse y Almacenamiento de datos paralelos](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)   
[Vistas de sistema admitidas en Azure SQL Data Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-system-views)   
[Instrucciones de T-SQL compatibles con Azure SQL Data Warehouse](/azure/sql-data-warehouse/sql-data-warehouse-reference-tsql-statements)
