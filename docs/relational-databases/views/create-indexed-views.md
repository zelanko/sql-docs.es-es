---
title: "Creación de vistas indexadas | Microsoft Docs"
ms.custom: 
ms.date: 01/22/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: views
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-views
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- indexed views [SQL Server], creating
- clustered indexes, views
- CREATE INDEX statement
- large_value_types_out_of_row option
- indexed views [SQL Server]
- views [SQL Server], indexed views
ms.assetid: f86dd29f-52dd-44a9-91ac-1eb305c1ca8d
caps.latest.revision: 
author: sstein
manager: craigg
ms.workload: Active
ms.openlocfilehash: dc562d47b04c20a3878bc0e1b8c63bf5d1151e09
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="create-indexed-views"></a>Crear vistas indizadas
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
En este tema se describe cómo crear índices en una vista. El primer índice creado en una vista debe ser un índice clúster único. Después de haber creado el índice clúster único, puede crear más índices no clúster. La creación de un índice clúster único en una vista mejora el rendimiento de la consulta porque la vista se almacena en la base de datos de la misma manera que se almacena una tabla con un índice clúster. El optimizador de consultas puede utilizar vistas indizadas para acelerar la ejecución de las consultas. No es necesario hacer referencia a la vista en la consulta para que el optimizador tenga en cuenta esa vista al hacer una sustitución.  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
 Para crear una vista indizada, es necesario seguir los pasos descritos a continuación, que son fundamentales para la correcta implementación de la vista indizada:  
  
1.  Compruebe que las opciones SET sean correctas para todas las tablas existentes a las que se hará referencia en la vista.    
2.  Compruebe que las opciones SET de la sesión estén establecidas correctamente antes de crear cualquier tabla y la vista.   
3.  Compruebe que la definición de vista sea determinista.   
4.  Cree la vista con la opción `WITH SCHEMABINDING`.   
5.  Cree el índice clúster único en la vista.   

> [!IMPORTANT]
> Al ejecutar DML<sup>1</sup> en una tabla a la que hace referencia un gran número de vistas indexadas, o bien menos vistas indexadas pero muy complejas, dichas vistas indexadas a las que se hace referencia deberán actualizarse igualmente. Como resultado, el rendimiento de la consulta DML se puede degradar notablemente o, en algunos casos, puede que tampoco se genere un plan de consulta.   
> En estos casos, pruebe las consultas DML antes de usarlas en entornos de producción, analice el plan de consulta y ajuste o simplifique la instrucción DML.   
>   
> <sup>1</sup> Como las operaciones UPDATE, DELETE o INSERT.   
  
###  <a name="Restrictions"></a> Opciones SET requeridas para vistas indizadas  
La evaluación de la misma expresión puede producir resultados diferentes en el [!INCLUDE[ssDE](../../includes/ssde-md.md)] cuando hay diferentes opciones SET activas cuando se ejecuta la consulta. Por ejemplo, después de establecer la opción SET `CONCAT_NULL_YIELDS_NULL` en ON, la expresión `'abc' + NULL` devuelve el valor NULL `NULL`, aunque al establecer `CONCAT_NULL_YIEDS_NULL` en OFF, la misma expresión genera `'abc'`.  
  
Para asegurar el correcto mantenimiento de las vistas y la generación de resultados coherentes, las vistas indizadas requieren valores fijos para varias opciones SET. Las opciones SET de la tabla siguiente se deben establecer en los valores que se muestran en la columna **Valor requerido** siempre que se den las siguientes condiciones:  
  
-   Se crean la vista y los índices siguientes en la vista.    
  
-   Las tablas base a las que se hace referencia en la vista cuando se crea la tabla.    
  
-   Se realiza una operación de inserción, actualización o eliminación en cualquier tabla que participa en la vista indizada. Este requisito incluye operaciones como copia masiva, replicación y consultas distribuidas.    
  
-   El optimizador de consultas utiliza la vista indizada para producir el plan de consulta.   
  
|Opciones SET|Valor requerido|Valor de servidor predeterminado|Valor predeterminado<br /><br /> Valor de OLE DB y ODBC|Valor predeterminado<br /><br /> predeterminado|  
|-----------------|--------------------|--------------------------|---------------------------------------|-----------------------------------|  
|ANSI_NULLS|ON|ON|ON|OFF|  
|ANSI_PADDING|ON|ON|ON|OFF|  
|ANSI_WARNINGS<sup>1</sup>|ON|ON|ON|OFF|  
|ARITHABORT|ON|ON|OFF|OFF|  
|CONCAT_NULL_YIELDS_NULL|ON|ON|ON|OFF|  
|NUMERIC_ROUNDABORT|OFF|OFF|OFF|OFF|  
|QUOTED_IDENTIFIER|ON|ON|ON|OFF|  
  
<sup>1</sup> Si se establece `ANSI_WARNINGS` en ON, `ARITHABORT` se establece implícitamente en ON.  
  
Si usa una conexión de servidor OLE DB u ODBC, el único valor que se debe modificar es la configuración de `ARITHABORT`. Todos los valores de DB-Library se deben establecer correctamente en el nivel de servidor mediante **sp_configure** o desde la aplicación a través del comando SET.  
  
> [!IMPORTANT]  
> Se recomienda encarecidamente que establezca la opción de usuario `ARITHABORT` en ON en todo el servidor en cuanto se cree la primera vista indizada o el primer índice en una columna calculada en cualquier base de datos del servidor.  
  
### <a name="deterministic-views"></a>Vistas deterministas  
La definición de una vista indizada debe ser determinista. Una vista es determinista si todas las expresiones de la lista de selección y las cláusulas `WHERE` y `GROUP BY` son deterministas. Las expresiones deterministas siempre devuelven el mismo resultado cada vez que son evaluadas con un conjunto específico de valores de entrada. Solo las funciones deterministas pueden participar en expresiones deterministas. Por ejemplo, la función `DATEADD` es determinista porque siempre devuelve el mismo resultado para cualquier conjunto dado de valores de argumento para sus tres parámetros. `GETDATE` no es determinista porque siempre se invoca con el mismo argumento, pero el valor que devuelve varía cada vez que se ejecuta.  
  
Para determinar si una columna de la vista es determinista, use la propiedad **IsDeterministic** de la función [COLUMNPROPERTY](../../t-sql/functions/columnproperty-transact-sql.md) . Para determinar si una columna determinista de una vista con enlaces de esquema es precisa, use la propiedad **IsPrecise** de la función `COLUMNPROPERTY`. `COLUMNPROPERTY` devuelve 1 si el valor es TRUE, 0 si es FALSE y NULL en entradas no válidas. Esto significa que la columna no es determinista ni precisa.  
  
Aun cuando una expresión sea determinista, si contiene expresiones de tipo float, es posible que un resultado exacto dependa de la arquitectura de procesador o de la versión de microcódigo. Para asegurar la integridad de los datos, estas expresiones solo pueden participar como columnas que no son de clave de vistas indizadas. Las expresiones deterministas que no contienen expresiones flotantes se denominan expresiones precisas. Solo las expresiones deterministas precisas pueden participar en columnas de clave y en cláusulas `WHERE` o `GROUP BY` de vistas indizadas.  

### <a name="additional-requirements"></a>Requisitos adicionales  
Además de las opciones SET y los requisitos de funciones deterministas, se deben cumplir los requisitos siguientes:  
  
-   El usuario que ejecuta `CREATE INDEX` debe ser el propietario de la vista.    
  
-   Cuando crea el índice, la opción `IGNORE_DUP_KEY` debe establecerse en OFF (configuración predeterminada).    
  
-   En la definición de vista, se debe hacer referencia a las tablas mediante nombres de dos partes, *esquema***.***nombredetabla*.    
  
-   Las funciones definidas por el usuario a las que se hace referencia en la vista se deben crear con la opción `WITH SCHEMABINDING`.    
  
-   Para hacer referencia a las funciones definidas por el usuario a las que se hace referencia en la vista, se deben usar nombres de dos partes, *\<schema>***.***\<function>*.   
  
-   La propiedad de acceso a datos de una función definida por el usuario debe ser `NO SQL` y la propiedad de acceso externo debe ser `NO`.   
  
-   Las funciones de Common Language Runtime (CLR) pueden aparecer en la lista de selección de la vista, pero no pueden formar parte de la definición de la clave de índice clúster. Las funciones CLR no pueden aparecer en la cláusula WHERE de la vista ni en la cláusula ON de una operación JOIN en la vista.   
  
-   Los métodos y las funciones CLR de tipos definidos por el usuario CLR utilizados en la definición de la vista deben establecer las propiedades según se indica en la tabla siguiente.   
  
    |Propiedad|Nota|  
    |--------------|----------|  
    |DETERMINISTIC = TRUE|Debe declararse de forma explícita como un atributo del método de Microsoft .NET Framework.|  
    |PRECISE = TRUE|Debe declararse de forma explícita como un atributo del método de .NET Framework.|  
    |DATA ACCESS = NO SQL|Se determina mediante la definición del atributo DataAccess como DataAccessKind.None y del atributo SystemDataAccess como SystemDataAccessKind.None.|  
    |EXTERNAL ACCESS = NO|Esta propiedad tiene el valor predeterminado NO en rutinas CLR.|  
  
-   La vista se debe crear mediante la opción `WITH SCHEMABINDING`.  
  
-   La vista solo debe hacer referencia a tablas base que estén en la misma base de datos que la vista. La vista no puede hacer referencia a otras vistas.  
  
-   La instrucción SELECT de la definición de vista no debe contener los siguientes elementos de Transact-SQL:  
  
    ||||  
    |-|-|-|  
    |`COUNT`|Funciones de ROWSET (`OPENDATASOURCE`, `OPENQUERY`, `OPENROWSET` y `OPENXML`)|Combinaciones `OUTER` (`LEFT`, `RIGHT` o `FULL`)|  
    |Tabla derivada (definida mediante una instrucción `SELECT` en la cláusula `FROM`)|Autocombinaciones|Especificación de columnas mediante `SELECT *` o `SELECT <table_name>.*`|  
    |`DISTINCT`|`STDEV`, `STDEVP`, `VAR`, `VARP` o `AVG`|Expresión de tabla común (CTE)|  
    |Columnas **float**<sup>1</sup>, **text**, **ntext**, **image**, **XML** o **filestream**|Subconsulta|Cláusula `OVER`, que incluye funciones de categoría o de agregado|  
    |Predicados de texto completo (`CONTAINS`, `FREETEXT`)|Función `SUM` que hace referencia a una expresión que acepta valores NULL|`ORDER BY`|  
    |Función de agregado definida por el usuario CLR|`TOP`|Operadores `CUBE`, `ROLLUP` o `GROUPING SETS`|  
    |`MIN`, `MAX`|Operadores `UNION`, `EXCEPT` o `INTERSECT`|`TABLESAMPLE`|  
    |Variables de tabla|`OUTER APPLY` o `CROSS APPLY`|`PIVOT`, `UNPIVOT`|  
    |Conjuntos de columnas dispersas|Funciones insertadas (TVF) o con valores de tabla de múltiples instrucciones (MSTVF)|`OFFSET`|  
    |`CHECKSUM_AGG`|||  
  
     <sup>1</sup> La vista indexada puede contener columnas **float**, aunque no se pueden incluir en la clave de índice agrupado.  
  
-   Si `GROUP BY` está presente, la definición de VIEW debe contener `COUNT_BIG(*)`, pero no `HAVING`. Estas restricciones `GROUP BY` solo se pueden aplicar a la definición de vista indizada. Una consulta puede usar una vista indizada en su plan de ejecución aun cuando no satisfaga estas restricciones `GROUP BY`.  
  
-   Si la definición de vista contiene una cláusula `GROUP BY`, la clave del índice clúster único solo puede hacer referencia a las columnas especificadas en la cláusula `GROUP BY`.  
  
> [!IMPORTANT]  
> No se admiten vistas indexadas con consultas temporales (las consultas que usan la cláusula `FOR SYSTEM_TIME`).  

###  <a name="Recommendations"></a> Recomendaciones  
 Cuando haga referencia a los literales de cadena **datetime** y **smalldatetime** de las vistas indizadas, se recomienda convertir explícitamente el literal al tipo de datos deseado mediante un estilo de formato de fecha determinista. Para obtener una lista de los estilos de formato de fecha deterministas, vea [CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md). Para obtener más información sobre las expresiones deterministas y no deterministas, consulte la sección [Consideraciones](#nondeterministic) de esta página.

Al ejecutar DML (como `UPDATE`, `DELETE` or `INSERT`) en una tabla a la que hace referencia un gran número de vistas indexadas, o menos vistas indexadas pero muy complejas, dichas vistas indexadas deberán actualizarse igualmente durante la ejecución de DML. Como resultado, el rendimiento de la consulta DML se puede degradar notablemente o, en algunos casos, puede que tampoco se genere un plan de consulta. En estos casos, pruebe las consultas DML antes de usarlas en entornos de producción, analice el plan de consulta y ajuste o simplifique la instrucción DML.
  
###  <a name="Considerations"></a> Consideraciones  
 La configuración de la opción **large_value_types_out_of_row** de las columnas de una vista indexada se hereda de la configuración de la columna correspondiente de la tabla base. Este valor se establece mediante [sp_tableoption](../../relational-databases/system-stored-procedures/sp-tableoption-transact-sql.md). La configuración predeterminada de las columnas formadas a partir de expresiones es 0. Esto significa que los tipos de valores grandes se almacenan de forma consecutiva.  
  
 En una tabla con particiones se pueden crear vistas indizadas, en las que a su vez se pueden crear particiones.  
  
 Para evitar que [!INCLUDE[ssDE](../../includes/ssde-md.md)] use vistas indexadas, incluya la sugerencia `OPTION (EXPAND VIEWS)` en la consulta. Además, si alguna de las opciones enumeradas no está establecida correctamente, el optimizador no utilizará los índices en las vistas. Para obtener más información sobre la sugerencia `OPTION (EXPAND VIEWS)`, vea [SELECT &#40;Transact-SQL&#41;](../../t-sql/queries/select-transact-sql.md).  
  
 Si se quita la vista, todos sus índices se quitan. Todos los índices no clúster y las estadísticas creadas automáticamente de una vista se quitan si se quita el índice clúster. Las estadísticas creadas por el usuario de la vista se conservan. Los índices no clúster se pueden quitar individualmente. Quitar el índice clúster de la vista quita el conjunto de resultados almacenado; el optimizador vuelve a procesar la vista como una vista estándar.  
  
 Los índices de las tablas y las vistas se pueden deshabilitar. Cuando se deshabilita un índice clúster de una tabla, también se deshabilitan los índices de las vistas asociadas a la tabla.  
 
<a name="nondeterministic"></a> Las expresiones que implican la conversión implícita de cadenas de caracteres a **datetime** o **smalldatetime** se consideran no deterministas. Esto se debe a que los resultados dependen de los valores LANGUAGE y DATEFORMAT de la sesión de servidor. Por ejemplo, los resultados de la expresión `CONVERT (datetime, '30 listopad 1996', 113)` dependen del valor de LANGUAGE porque la cadena '`listopad`' significa distintos meses en distintos idiomas. De forma similar, en la expresión `DATEADD(mm,3,'2000-12-01')`, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpretará la cadena `'2000-12-01'` en función del valor de DATEFORMAT. La conversión implícita de los datos de caracteres no Unicode entre intercalaciones también se considera no determinista.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Se necesita el permiso **CREATE VIEW** en la base de datos y el permiso **ALTER** en el esquema en que se crea la vista.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-create-an-indexed-view"></a>Para crear una vista indizada  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. El ejemplo crea una vista y un índice en esa vista. Se incluyen dos consultas que utilizan la vista indizada.  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    --Set the options to support indexed views.  
    SET NUMERIC_ROUNDABORT OFF;  
    SET ANSI_PADDING, ANSI_WARNINGS, CONCAT_NULL_YIELDS_NULL, ARITHABORT,  
        QUOTED_IDENTIFIER, ANSI_NULLS ON;  
    GO  
    --Create view with schemabinding.  
    IF OBJECT_ID ('Sales.vOrders', 'view') IS NOT NULL  
    DROP VIEW Sales.vOrders ;  
    GO  
    CREATE VIEW Sales.vOrders  
    WITH SCHEMABINDING  
    AS  
        SELECT SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Revenue,  
            OrderDate, ProductID, COUNT_BIG(*) AS COUNT  
        FROM Sales.SalesOrderDetail AS od, Sales.SalesOrderHeader AS o  
        WHERE od.SalesOrderID = o.SalesOrderID  
        GROUP BY OrderDate, ProductID;  
    GO  
    --Create an index on the view.  
    CREATE UNIQUE CLUSTERED INDEX IDX_V1   
        ON Sales.vOrders (OrderDate, ProductID);  
    GO  
    --This query can use the indexed view even though the view is   
    --not specified in the FROM clause.  
    SELECT SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Rev,   
        OrderDate, ProductID  
    FROM Sales.SalesOrderDetail AS od  
        JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID=o.SalesOrderID  
            AND ProductID BETWEEN 700 and 800  
            AND OrderDate >= CONVERT(datetime,'05/01/2002',101)  
    GROUP BY OrderDate, ProductID  
    ORDER BY Rev DESC;  
    GO  
    --This query can use the above indexed view.  
    SELECT  OrderDate, SUM(UnitPrice*OrderQty*(1.00-UnitPriceDiscount)) AS Rev  
    FROM Sales.SalesOrderDetail AS od  
        JOIN Sales.SalesOrderHeader AS o ON od.SalesOrderID=o.SalesOrderID  
            AND DATEPART(mm,OrderDate)= 3  
            AND DATEPART(yy,OrderDate) = 2002  
    GROUP BY OrderDate  
    ORDER BY OrderDate ASC;  
    GO  
    ```  
  
Para obtener más información, vea [CREATE VIEW &#40;Transact-SQL&#41;](../../t-sql/statements/create-view-transact-sql.md).  
  
## <a name="see-also"></a>Ver también  
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)   
 [SET ARITHABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-arithabort-transact-sql.md)   
 [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)   
 [SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](../../t-sql/statements/set-numeric-roundabort-transact-sql.md)   
 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](../../t-sql/statements/set-quoted-identifier-transact-sql.md)  
  
  
