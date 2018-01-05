---
title: "CREAR estadísticas (Transact-SQL) | Documentos de Microsoft"
ms.custom: 
ms.date: 01/04/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- STATISTICS
- STATISTICS_TSQL
- CREATE STATISTICS
- CREATE_STATISTICS_TSQL
dev_langs: TSQL
helpviewer_keywords:
- query optimization statistics [SQL Server], creating
- indexed views [SQL Server], statistics
- FULLSCAN option
- CREATE STATISTICS statement
- filtered statistics [SQL Server]
- creating statistics [SQL Server]
- NORECOMPUTE clause
ms.assetid: b23e2f6b-076c-4e6d-9281-764bdb616ad2
caps.latest.revision: "105"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 088b79e73be6258afc5c664aaf14ba3cad9d2f5f
ms.sourcegitcommit: 4aeedbb88c60a4b035a49754eff48128714ad290
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/05/2018
---
# <a name="create-statistics-transact-sql"></a>CREATE STATISTICS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Crea las estadísticas de optimización de consulta en una o más columnas de una tabla, una vista indizada o una tabla externa. Para la mayoría de las consultas, el optimizador de consultas genera ya las estadísticas necesarias para un plan de consulta de alta calidad; en algunos casos, para mejorar el rendimiento de la consulta necesita crear estadísticas adicionales con CREATE STATISTICS modificar el diseño de la consulta.  
  
 Para obtener más información, consulte [estadísticas](../../relational-databases/statistics/statistics.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
-- Syntax for SQL Server and Azure SQL Database  
  
-- Create statistics on an external table  
CREATE STATISTICS statistics_name   
ON { table_or_indexed_view_name } ( column [ ,...n ] )   
    [ WITH FULLSCAN ] ;  
  
-- Create statistics on a regular table or indexed view  
CREATE STATISTICS statistics_name   
ON { table_or_indexed_view_name } ( column [ ,...n ] )   
    [ WHERE <filter_predicate> ]  
    [ WITH   
        [ [ FULLSCAN   
            [ [ , ] PERSIST_SAMPLE_PERCENT = { ON | OFF } ]    
          | SAMPLE number { PERCENT | ROWS }   
            [ [ , ] PERSIST_SAMPLE_PERCENT = { ON | OFF } ]    
          | <update_stats_stream_option> [ ,...n ]    
        [ [ , ] NORECOMPUTE ]   
        [ [ , ] INCREMENTAL = { ON | OFF } ] 
        [ [ , ] MAXDOP = max_degree_of_parallelism ]
    ] ;  
  
<filter_predicate> ::=   
    <conjunct> [AND <conjunct>]  
  
<conjunct> ::=  
    <disjunct> | <comparison>  
  
<disjunct> ::=  
        column_name IN (constant ,…)  
  
<comparison> ::=  
        column_name <comparison_op> constant  
  
<comparison_op> ::=  
    IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !<  
    
<update_stats_stream_option> ::=  
    [ STATS_STREAM = stats_stream ]  
    [ ROWCOUNT = numeric_constant ]  
    [ PAGECOUNT = numeric_contant ] 
```  
  
```  
-- Syntax for Azure SQL Data Warehouse and Parallel Data Warehouse  
  
CREATE STATISTICS statistics_name   
    ON [ database_name . [schema_name ] . | schema_name. ] table_name   
    ( column_name  [ ,...n ] )   
    [ WHERE <filter_predicate> ]  
    [ WITH {  
           FULLSCAN   
           | SAMPLE number PERCENT   
      }  
    ]  
[;]  
  
<filter_predicate> ::=   
    <conjunct> [AND <conjunct>]  
  
<conjunct> ::=  
    <disjunct> | <comparison>  
  
<disjunct> ::=  
        column_name IN (constant ,…)  
  
<comparison> ::=  
        column_name <comparison_op> constant  
  
<comparison_op> ::=  
    IS | IS NOT | = | <> | != | > | >= | !> | < | <= | !<  
```  
  
## <a name="arguments"></a>Argumentos  
 *statistics_name*  
 Es el nombre de las estadísticas que se van a crear.  
  
 *table_or_indexed_view_name*  
 Es el nombre de la tabla, una vista indizada o una tabla externa en la que se va a crear las estadísticas. Para crear estadísticas en otra base de datos, especifique un nombre de tabla completo.  
  
 *columna [,... n]*  
 Una o varias columnas que se incluirán en las estadísticas. Las columnas deben ser en orden de prioridad, de izquierda a derecha. Sólo la primera columna se usa para crear el histograma. Todas las columnas se usan para las estadísticas de correlación entre las columnas que se llama densidades.  
  
 Se puede especificar cualquier columna que pueda ser especificada como columna de clave de índice con las siguientes excepciones:  
  
-   **XML**, búsqueda de texto completo, y no se pueden especificar columnas FILESTREAM.  
  
-   Solamente se pueden especificar columnas calculadas si las opciones de base de datos ARITHABORT y QUOTED_IDENTIFIER están establecidas en ON.  
  
-   Se pueden especificar columnas de tipo CLR definido por el usuario si el tipo admite el orden binario. Es posible especificar columnas calculadas definidas como llamadas a métodos de una columna de un tipo definido por el usuario si los métodos están marcados como deterministas.  
  
 DONDE \<filter_predicate > especifica una expresión para seleccionar un subconjunto de filas que se va a incluir al crear el objeto de estadísticas. Las estadísticas que se crean con un predicado de filtro se llaman estadísticas filtradas. El predicado de filtro utiliza la lógica de comparación simple y no se puede hacer referencia a una columna calculada, una columna UDT, una columna de tipo de datos espaciales, o un **hierarchyID** columna tipo de datos. Las comparaciones que utilizan literales NULL no se admiten con los operadores de comparación. En su lugar, use los operadores IS NULL e IS NOT NULL.  
  
 Los siguientes son algunos ejemplos de predicados de filtro para la tabla Production.BillOfMaterials:  
  
 * `WHERE StartDate > '20000101' AND EndDate <= '20000630'`  
  
 * `WHERE ComponentID IN (533, 324, 753)`  
  
 * `WHERE StartDate IN ('20000404', '20000905') AND EndDate IS NOT NULL`  
  
 Para obtener más información acerca de los predicados de filtro, vea [Create Filtered Indexes](../../relational-databases/indexes/create-filtered-indexes.md).  
  
 FULLSCAN  
 Calcular las estadísticas, examine todas las filas. FULLSCAN y SAMPLE 100 PERCENT tienen los mismos resultados. FULLSCAN no se puede utilizar con la opción SAMPLE.  
  
 Cuando se omite, SQL Server utiliza el muestreo a crear las estadísticas y determina el tamaño de muestra que se requiere para crear un plan de consulta de alta calidad  
  
 EJEMPLO *número* {% | FILAS}  
 Especifica el porcentaje o número de filas aproximado de la tabla o vista indizada que usa el optimizador de consultas al crear las estadísticas. En PERCENT, *número* puede estar comprendido entre 0 y 100 y para las filas, *número* puede oscilar entre 0 y el número total de filas. El porcentaje o número de filas real de los ejemplos del optimizador de consultas podría no coincidir con el porcentaje o el número especificado. Por ejemplo, el optimizador de consultas examina todas las filas en una página de datos.  
  
 SAMPLE es útil para casos especiales en el que el plan de consulta, basado en el muestreo predeterminado, no es óptimo. En la mayoría de las situaciones, no es necesario especificar SAMPLE porque el optimizador de consultas ya utiliza el muestreo y determina el tamaño de muestra estadísticamente significativo de forma predeterminada, tal y como se exige para crear planes de consulta de alta calidad.  
  
 SAMPLE no se puede utilizar con la opción FULLSCAN. Cuando no se especifica SAMPLE ni FULLSCAN, el optimizador de consultas utiliza los datos muestreados y calcula el tamaño de la muestra de forma predeterminada.  
  
 Recomendamos no especificar 0 PERCENT ni 0 ROWS. Cuando se especifican 0 PERCENT o ROWS, el objeto de estadísticas se crea pero no contiene datos de estadísticas.  
 
 PERSIST_SAMPLE_PERCENT = {ON | {OFF}  
 Cuando **ON**, las estadísticas conservará el porcentaje de muestreo de creación para las actualizaciones posteriores que no especifican explícitamente un porcentaje de muestreo. Cuando **OFF**, porcentaje de muestreo de las estadísticas se restablecería a muestreo predeterminado en actualizaciones posteriores que no especifican explícitamente un porcentaje de muestreo. El valor predeterminado es **OFF**. 
 
 **Se aplica a**: [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] (a partir de [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU4) a través de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] (a partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU1).    
  
 STATS_STREAM  **=**  *stats_stream*  
 [!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  
  
 NORECOMPUTE  
 Deshabilitar las estadísticas automáticas opción de actualización, AUTO_UPDATE_STATISTICS, para *statistics_name*. Si se especifica esta opción, el optimizador de consultas finalizará cualquier actualización de estadísticas en curso para *statistics_name* y deshabilitará las actualizaciones futuras.  
  
 Para volver a habilitar las actualizaciones de estadísticas, quite las estadísticas con [DROP STATISTICS](../../t-sql/statements/drop-statistics-transact-sql.md) y, a continuación, ejecutar CREATE STATISTICS sin la opción NORECOMPUTE.  
  
> [!WARNING]  
>  Utilizar esta opción puede producir planes de consulta poco óptimos. Se recomienda usar esta opción con moderación y que lo haga únicamente un administrador de sistemas cualificado.  
  
 Para obtener más información acerca de la opción AUTO_UPDATE_STATISTICS, consulte [ALTER DATABASE SET Options &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-database-transact-sql-set-options.md). Para obtener más información acerca de cómo deshabilitar y volver a habilitar las actualizaciones de estadísticas, vea [estadísticas](../../relational-databases/statistics/statistics.md).  
  
 INCREMENTAL = { ON | OFF }  
 Cuando **ON**, son las estadísticas creadas por cada partición. Cuando **OFF**, se combinan las estadísticas de todas las particiones. El valor predeterminado es **OFF**.  
  
 Si no se admiten las estadísticas por partición, se genera un error. Las estadísticas incrementales no se admiten para los siguientes tipos de estadísticas:  
  
-   Estadísticas creadas con índices que no están alineados por partición con la tabla base.  
-   Estadísticas creadas sobre bases de datos secundarias legibles AlwaysOn.  
-   Estadísticas creadas sobre bases de datos de solo lectura.  
-   Estadísticas creadas sobre índices filtrados.  
-   Estadísticas creadas sobre vistas.  
-   Estadísticas creadas sobre tablas internas.  
-   Estadísticas creadas con índices espaciales o índices XML.  
  
**Se aplica a**: desde [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] hasta [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
MAXDOP = *max_degree_of_parallelism*  
**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (a partir de [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)] CU3).  
  
 Invalida el **grado máximo de paralelismo** opción de configuración para la duración de la operación de estadística. Para obtener más información, vea [Establecer la opción de configuración del servidor Grado máximo de paralelismo](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md). Utilice MAXDOP para establecer un límite para el número de procesadores utilizados en la ejecución de un plan paralelo. El máximo es 64 procesadores.  
  
 *max_degree_of_parallelism* puede ser:  
  
 1  
 Suprime la generación de planes paralelos.  
  
 \>1  
 Restringe el número máximo de procesadores utilizados en una operación estadística paralelo al número especificado o al menos, según la carga de trabajo del sistema actual.  
  
 0 (predeterminado)  
 Usa el número real de procesadores o menos, según la carga de trabajo actual del sistema.  
  
 \<update_stats_stream_option >[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]  

## <a name="permissions"></a>Permissions  
 Requiere uno de estos permisos:  
  
-   ALTER TABLE  
-   Usuario es propietario de la tabla  
-   Pertenencia en el **db_ddladmin** rol fijo de base de datos  
  
## <a name="general-remarks"></a>Notas generales  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Puede usar tempdb para ordenar las filas buscadas antes de crear las estadísticas.  
  
### <a name="statistics-for-external-tables"></a>Estadísticas para tablas externas  
 Al crear las estadísticas de tabla externa, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] importa la tabla externa en un archivo temporal [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de tabla y, a continuación, crea las estadísticas. Para las estadísticas de ejemplos, se importan solo las filas muestreadas. Si tiene una tabla externa grande, será mucho más rápido que utiliza el muestreo predeterminado en lugar de la opción de examen completo.  
  
### <a name="statistics-with-a-filtered-condition"></a>Estadísticas con una condición de filtrado  
 Las estadísticas filtradas pueden mejorar el rendimiento de las consultas que se seleccionan desde subconjuntos de datos bien definidos. Las estadísticas filtradas utilizan un predicado de filtro de la cláusula WHERE para seleccionar el subconjunto de datos que se incluye en las estadísticas.  
  
### <a name="when-to-use-create-statistics"></a>Cuándo utilizar CREATE STATISTICS  
 Para obtener más información sobre cuándo utilizar CREATE STATISTICS, vea [estadísticas](../../relational-databases/statistics/statistics.md).  
  
### <a name="referencing-dependencies-for-filtered-statistics"></a>Hacer referencia a las dependencias para las estadísticas filtradas  
 El [sys.sql_expression_dependencies](../../relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql.md) vista de catálogo realiza el seguimiento de cada columna en el predicado de estadísticas filtradas como una dependencia de referencia. Tenga en cuenta las operaciones que realiza en las columnas de la tabla antes de crear estadísticas filtradas, porque no puede quitar, modificar, cambiar el nombre de la definición de una columna de tabla definida en un predicado de estadísticas filtradas.  
  
## <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
* No se admite la actualización de las estadísticas en tablas externas. Para actualizar las estadísticas en una tabla externa, quite y vuelva a crear las estadísticas.  
* Puede mostrar hasta 64 columnas por objeto de estadísticas.
* La opción MAXDOP no es compatible con opciones STATS_STREAM, recuento de filas y PAGECOUNT.
  
## <a name="examples"></a>Ejemplos  

### <a name="examples-use-the-adventureworks-database"></a>Ejemplos utilizan la base de datos de AdventureWorks.  

### <a name="a-using-create-statistics-with-sample-number-percent"></a>A. Utilizar CREATE STATISTICS con SAMPLE number PERCENT  
 En el ejemplo siguiente, se crean las estadísticas `ContactMail1` a partir de una muestra aleatoria del 5 por ciento de las columnas `BusinessEntityID` y `EmailPromotion` de la tabla `Contact` de la base de datos [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)].  
  
```sql  
CREATE STATISTICS ContactMail1  
    ON Person.Person (BusinessEntityID, EmailPromotion)  
    WITH SAMPLE 5 PERCENT;  
```  
  
### <a name="b-using-create-statistics-with-fullscan-and-norecompute"></a>B. Utilizar CREATE STATISTICS con FULLSCAN y NORECOMPUTE  
 En el ejemplo siguiente se crean las estadísticas `ContactMail2` para todas las filas de las columnas `BusinessEntityID` y `EmailPromotion` de la tabla `Contact` y se deshabilita la posibilidad de volver a calcular las estadísticas automáticamente.  
  
```sql  
CREATE STATISTICS NamePurchase  
    ON AdventureWorks2012.Person.Person (BusinessEntityID, EmailPromotion)  
    WITH FULLSCAN, NORECOMPUTE;  
```  
  
### <a name="c-using-create-statistics-to-create-filtered-statistics"></a>C. Utilizar CREATE STATISTICS para crear estadísticas filtradas  
 En el ejemplo siguiente se crean las estadísticas filtradas `ContactPromotion1`. El [!INCLUDE[ssDE](../../includes/ssde-md.md)] muestrea el 50 por ciento de los datos y, a continuación, selecciona las filas cuyo valor `EmailPromotion` es igual a 2.  
  
```sql  
CREATE STATISTICS ContactPromotion1  
    ON Person.Person (BusinessEntityID, LastName, EmailPromotion)  
WHERE EmailPromotion = 2  
WITH SAMPLE 50 PERCENT;  
GO  
```  
  
### <a name="d-create-statistics-on-an-external-table"></a>D. Crear estadísticas en una tabla externa  
 La única decisión que debe tomar al crear las estadísticas en una tabla externa, además de proporcionar la lista de columnas, es si desea crear las estadísticas mediante el muestreo de las filas o examinando todas las filas.  
  
 Puesto que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] importa datos de la tabla externa en una tabla temporal para crear estadísticas, la opción de examen completo tardará mucho más tiempo. Para una tabla grande, el método de muestreo predeterminado es generalmente es suficiente.  
  
```sql  
--Create statistics on an external table and use default sampling.  
CREATE STATISTICS CustomerStats1 ON DimCustomer (CustomerKey, EmailAddress);  
  
--Create statistics on an external table and scan all the rows  
CREATE STATISTICS CustomerStats1 ON DimCustomer (CustomerKey, EmailAddress) WITH FULLSCAN;  
```  

### <a name="e-using-create-statistics-with-fullscan-and-persistsamplepercent"></a>E. Utilizar CREATE STATISTICS con FULLSCAN y PERSIST_SAMPLE_PERCENT  
 En el ejemplo siguiente se crea el `ContactMail2` estadísticas para todas las filas de la `BusinessEntityID` y `EmailPromotion` columnas de la `Contact` de tabla y establece un porcentaje de muestreo del 100 por ciento de todas las actualizaciones subsiguientes que realice explícitamente no especifican un muestreo porcentaje.  
  
```sql  
CREATE STATISTICS NamePurchase  
    ON AdventureWorks2012.Person.Person (BusinessEntityID, EmailPromotion)  
    WITH FULLSCAN, PERSIST_SAMPLE_PERCENT = ON;  
```  
  
### <a name="examples-using-adventureworksdw-database"></a>Ver ejemplos de uso de la base de datos AdventureWorksDW. 
  
### <a name="f-create-statistics-on-two-columns"></a>F. Crear estadísticas en dos columnas  
 En el ejemplo siguiente se crea el `CustomerStats1` estadísticas, tomando como base la `CustomerKey` y `EmailAddress` columnas de la `DimCustomer` tabla. Las estadísticas se crean en función de un muestreo estadísticamente significativo de las filas de la `Customer` tabla.  
  
```sql  
CREATE STATISTICS CustomerStats1 ON DimCustomer (CustomerKey, EmailAddress);  
```  
  
### <a name="g-create-statistics-by-using-a-full-scan"></a>G. Crear estadísticas mediante un examen completo  
 En el ejemplo siguiente se crea el `CustomerStatsFullScan` estadísticas, en función de examen de todas las filas en el `DimCustomer` tabla.  
  
```sql  
CREATE STATISTICS CustomerStatsFullScan 
ON DimCustomer (CustomerKey, EmailAddress) WITH FULLSCAN;  
```  
  
### <a name="h-create-statistics-by-specifying-the-sample-percentage"></a>H. Especifica el porcentaje de ejemplo para crear estadísticas  
 En el ejemplo siguiente se crea el `CustomerStatsSampleScan` estadísticas, en función de examen el 50 por ciento de las filas de la `DimCustomer` tabla.  
  
```sql  
CREATE STATISTICS CustomerStatsSampleScan 
ON DimCustomer (CustomerKey, EmailAddress) WITH SAMPLE 50 PERCENT;  
```  
  
## <a name="see-also"></a>Vea también  
 [Estadísticas](../../relational-databases/statistics/statistics.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [sys.stats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)   
 [Sys.stats_columns &#40; Transact-SQL &#41;](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)  
  
  

