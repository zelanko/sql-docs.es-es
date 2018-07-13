---
title: Creación de vistas indexadas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: table-view-index
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- indexed views [SQL Server], creating
- clustered indexes, views
- CREATE INDEX statement
- large_value_types_out_of_row option
- indexed views [SQL Server]
- views [SQL Server], indexed views
ms.assetid: f86dd29f-52dd-44a9-91ac-1eb305c1ca8d
caps.latest.revision: 77
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d56783347d9c5aaf59a1b45b24e2003a35df96df
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37150426"
---
# <a name="create-indexed-views"></a>Crear vistas indizadas
  En este tema se describe cómo crear una vista indizada en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[tsql](../../includes/tsql-md.md)]. El primer índice creado en una vista debe ser un índice clúster único. Después de haber creado el índice clúster único, puede crear más índices no clúster. La creación de un índice clúster único en una vista mejora el rendimiento de la consulta porque la vista se almacena en la base de datos de la misma manera que se almacena una tabla con un índice clúster. El optimizador de consultas puede utilizar vistas indizadas para acelerar la ejecución de las consultas. No es necesario hacer referencia a la vista en la consulta para que el optimizador tenga en cuenta esa vista al hacer una sustitución.  
  
  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
 Para crear una vista indizada, es necesario seguir los pasos descritos a continuación, que son fundamentales para la correcta implementación de la vista indizada:  
  
1.  Compruebe que las opciones SET sean correctas para todas las tablas existentes a las que se hará referencia en la vista.  
  
2.  Compruebe que las opciones SET de la sesión estén establecidas correctamente antes de crear cualquier tabla y la vista.  
  
3.  Compruebe que la definición de vista sea determinista.  
  
4.  Cree la vista mediante la opción WITH SCHEMABINDING.  
  
5.  Cree el índice clúster único en la vista.  
  
###  <a name="Restrictions"></a> Opciones SET requeridas para vistas indizadas  
 La evaluación de la misma expresión puede producir resultados diferentes en el [!INCLUDE[ssDE](../../includes/ssde-md.md)] cuando hay diferentes opciones SET activas cuando se ejecuta la consulta. Por ejemplo, después de establecer la opción SET CONCAT_NULL_YIELDS_NULL en ON, la expresión **'** abc **'** + NULL devuelve el valor NULL, aunque al establecer CONCAT_NULL_YIEDS_NULL en OFF, la misma expresión genera **'** abc **'**.  
  
 Para asegurar el correcto mantenimiento de las vistas y la generación de resultados coherentes, las vistas indizadas requieren valores fijos para varias opciones SET. Se deben establecer las opciones SET de la tabla siguiente para los valores mostrados en la **RequiredValue** columna cada vez que se producen las condiciones siguientes:  
  
-   Se crean la vista y los índices siguientes en la vista.  
  
-   Las tablas base a las que se hace referencia en la vista cuando se crea la tabla.  
  
-   Se realiza una operación de inserción, actualización o eliminación en cualquier tabla que participa en la vista indizada. Este requisito incluye operaciones como copia masiva, replicación y consultas distribuidas.  
  
-   El optimizador de consultas utiliza la vista indizada para producir el plan de consulta.  
  
    |Opciones SET|Valor requerido|Valor de servidor predeterminado|Valor predeterminado<br /><br /> Valor de OLE DB y ODBC|Valor predeterminado<br /><br /> predeterminado|  
    |-----------------|--------------------|--------------------------|---------------------------------------|-----------------------------------|  
    |ANSI_NULLS|ON|ON|ON|OFF|  
    |ANSI_PADDING|ON|ON|ON|OFF|  
    |ANSI_WARNINGS*|ON|ON|ON|OFF|  
    |ARITHABORT|ON|ON|OFF|OFF|  
    |CONCAT_NULL_YIELDS_NULL|ON|ON|ON|OFF|  
    |NUMERIC_ROUNDABORT|OFF|OFF|OFF|OFF|  
    |QUOTED_IDENTIFIER|ON|ON|ON|OFF|  
  
     *Setting ANSI_WARNINGS to ON implicitly sets ARITHABORT to ON.  
  
 Si utiliza una conexión de servidor OLE DB u ODBC, el único valor que se debe modificar es la configuración de ARITHABORT. Todos los valores de DB-Library se deben establecer correctamente en el nivel de servidor mediante **sp_configure** o desde la aplicación a través del comando SET.  
  
> [!IMPORTANT]  
>  Se recomienda encarecidamente que establezca la opción de usuario ARITHABORT en ON en todo el servidor en cuanto se cree la primera vista indizada o el primer índice en una columna calculada en cualquier base de datos del servidor.  
  
### <a name="deterministic-views"></a>Vistas deterministas  
 La definición de una vista indizada debe ser determinista. Una vista es determinista si todas las expresiones de la lista de selección y las cláusulas WHERE y GROUP BY son deterministas. Las expresiones deterministas siempre devuelven el mismo resultado cada vez que son evaluadas con un conjunto específico de valores de entrada. Solo las funciones deterministas pueden participar en expresiones deterministas. Por ejemplo, la función DATEADD es determinista porque siempre devuelve el mismo resultado para cualquier conjunto dado de valores de argumento para sus tres parámetros. GETDATE no es determinista porque siempre se invoca con el mismo argumento, pero el valor que devuelve varía cada vez que se ejecuta.  
  
 Para determinar si una columna de la vista es determinista, use la propiedad **IsDeterministic** de la función [COLUMNPROPERTY](/sql/t-sql/functions/columnproperty-transact-sql) . Para determinar si una columna determinista de una vista con enlaces de esquema es precisa, use la propiedad **IsPrecise** de la función COLUMNPROPERTY. COLUMNPROPERTY devuelve 1 si el valor es TRUE, 0 si es FALSE y NULL en entradas no válidas. Esto significa que la columna no es determinista ni precisa.  
  
 Aun cuando una expresión sea determinista, si contiene expresiones de tipo float, es posible que un resultado exacto dependa de la arquitectura de procesador o de la versión de microcódigo. Para asegurar la integridad de los datos, estas expresiones solo pueden participar como columnas que no son de clave de vistas indizadas. Las expresiones deterministas que no contienen expresiones flotantes se denominan expresiones precisas. Solo las expresiones deterministas precisas pueden participar en columnas de clave y en cláusulas WHERE o GROUP BY de vistas indizadas.  
  
### <a name="additional-requirements"></a>Requisitos adicionales  
 Además de las opciones SET y los requisitos de funciones deterministas, se deben cumplir los requisitos siguientes:  
  
-   El usuario que ejecuta CREATE INDEX debe ser el propietario de la vista.  
  
-   Cuando crea el índice, la opción IGNORE_DUP_KEY debe establecerse en OFF (configuración predeterminada).  
  
-   En la definición de vista, se debe hacer referencia a las tablas mediante nombres de dos partes, *esquema ***.*** nombredetabla*.  
  
-   Las funciones definidas por el usuario a las que se hace referencia en la vista se deben crear con la opción WITH SCHEMABINDING.  
  
-   Para hacer referencia a las funciones definidas por el usuario a las que se hace referencia en la vista, se deben usar nombres de dos partes, *esquema ***.*** función*.  
  
-   La propiedad de acceso a datos de una función definida por el usuario debe ser NO SQL y la propiedad de acceso externo debe ser NO.  
  
-   Las funciones de Common Language Runtime (CLR) pueden aparecer en la lista de selección de la vista, pero no pueden formar parte de la definición de la clave de índice clúster. Las funciones CLR no pueden aparecer en la cláusula WHERE de la vista ni en la cláusula ON de una operación JOIN en la vista.  
  
-   Los métodos y las funciones CLR de tipos definidos por el usuario CLR utilizados en la definición de la vista deben establecer las propiedades según se indica en la tabla siguiente.  
  
    |Property|Nota|  
    |--------------|----------|  
    |DETERMINISTIC = TRUE|Debe declararse de forma explícita como un atributo del método de Microsoft .NET Framework.|  
    |PRECISE = TRUE|Debe declararse de forma explícita como un atributo del método de .NET Framework.|  
    |DATA ACCESS = NO SQL|Se determina mediante la definición del atributo DataAccess como DataAccessKind.None y del atributo SystemDataAccess como SystemDataAccessKind.None.|  
    |EXTERNAL ACCESS = NO|Esta propiedad tiene el valor predeterminado NO en rutinas CLR.|  
  
-   Esta vista se debe crear utilizando la opción WITH SCHEMABINDING.  
  
-   La vista solo debe hacer referencia a tablas base que estén en la misma base de datos que la vista. La vista no puede hacer referencia a otras vistas.  
  
-   La instrucción SELECT de la definición de vista no debe contener los siguientes elementos de Transact-SQL:  
  
    ||||  
    |-|-|-|  
    |COUNT|Funciones ROWSET (OPENDATASOURCE, OPENQUERY, OPENROWSET y OPENXML)|Combinaciones externas (LEFT, RIGHT o FULL)|  
    |Tabla derivada (definida mediante una instrucción SELECT en la cláusula FROM)|Autocombinaciones|Especificar columnas mediante SELECT \* o SELECT *nombre_tabla*.*|  
    |DISTINCT|STDEV, STDEVP, VAR, VARP o AVG|Expresión de tabla común (CTE)|  
    |`float`\*, `text`, `ntext`, `image`, `XML`, o `filestream` columnas|Subconsulta|Cláusula OVER, que incluye funciones de categoría o de agregado|  
    |Predicados de texto completo (CONTAIN, FREETEXT)|Función SUM que hace referencia a una expresión que acepta valores NULL|ORDER BY|  
    |Función de agregado definida por el usuario CLR|ARRIBA|Operadores CUBE, ROLLUP o GROUPING SETS|  
    |MIN, MAX|Operadores UNION, EXCEPT o INTERSECT|TABLESAMPLE|  
    |Variables de tabla|OUTER APPLY o CROSS APPLY|PIVOT, UNPIVOT|  
    |Conjuntos de columnas dispersas|Funciones insertadas o con valores de tabla de múltiples instrucciones|OFFSET|  
    |CHECKSUM_AGG|||  
  
     \*La vista indizada puede contener `float` columnas; sin embargo, estas columnas no pueden incluirse en la clave de índice agrupado.  
  
-   Si GROUP BY está presente, la definición de VIEW debe contener COUNT_BIG(*) y no debe contener HAVING. Estas restricciones GROUP BY solo se pueden aplicar a la definición de vista indizada. Una consulta puede utilizar una vista indizada en su plan de ejecución aun cuando no satisfaga estas restricciones GROUP BY.  
  
-   Si la definición de vista contiene una cláusula GROUP BY, la clave del índice clúster único solo puede hacer referencia a las columnas especificadas en esta cláusula.  
  
###  <a name="Recommendations"></a> Recomendaciones  
 Cuando haga referencia a los literales de cadena `datetime` y `smalldatetime` de las vistas indizadas, se recomienda convertir explícitamente el literal al tipo de datos deseado mediante un estilo de formato de fecha determinista. Para obtener una lista de los estilos de formato de fecha deterministas, vea [CAST y CONVERT &#40;Transact-SQL&#41;](/sql/t-sql/functions/cast-and-convert-transact-sql). Las expresiones que implican la conversión implícita de cadenas de caracteres a `datetime` o `smalldatetime` se consideran no deterministas. Esto se debe a que los resultados dependen de los valores LANGUAGE y DATEFORMAT de la sesión de servidor. Por ejemplo, los resultados de la expresión `CONVERT (datetime, '30 listopad 1996', 113)` dependen del valor de LANGUAGE porque la cadena '`listopad`' significa distintos meses en distintos idiomas. De forma similar, en la expresión `DATEADD(mm,3,'2000-12-01')`, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interpretará la cadena `'2000-12-01'` en función del valor de DATEFORMAT.  
  
 La conversión implícita de los datos de caracteres no Unicode entre intercalaciones también se considera no determinista.  
  
###  <a name="Considerations"></a> Consideraciones  
 La configuración de la opción **large_value_types_out_of_row** de las columnas de una vista indexada se hereda de la configuración de la columna correspondiente de la tabla base. Este valor se establece mediante [sp_tableoption](/sql/relational-databases/system-stored-procedures/sp-tableoption-transact-sql). La configuración predeterminada de las columnas formadas a partir de expresiones es 0. Esto significa que los tipos de valores grandes se almacenan de forma consecutiva.  
  
 En una tabla con particiones se pueden crear vistas indizadas, en las que a su vez se pueden crear particiones.  
  
 Para evitar que el [!INCLUDE[ssDE](../../includes/ssde-md.md)] use vistas indizadas, incluya la sugerencia OPTION (EXPAND VIEWS) en la consulta. Además, si alguna de las opciones enumeradas no está establecida correctamente, el optimizador no utilizará los índices en las vistas. Para obtener más información sobre la sugerencia OPTION (EXPAND VIEWS), vea [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql).  
  
 Si se quita la vista, todos sus índices se quitan. Todos los índices no clúster y las estadísticas creadas automáticamente de una vista se quitan si se quita el índice clúster. Las estadísticas creadas por el usuario de la vista se conservan. Los índices no clúster se pueden quitar individualmente. Quitar el índice clúster de la vista quita el conjunto de resultados almacenado; el optimizador vuelve a procesar la vista como una vista estándar.  
  
 Los índices de las tablas y las vistas se pueden deshabilitar. Cuando se deshabilita un índice clúster de una tabla, también se deshabilitan los índices de las vistas asociadas a la tabla.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Se necesita el permiso CREATE VIEW en la base de datos y el permiso ALTER en el esquema en que se crea la vista.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-create-an-indexed-view"></a>Para crear una vista indizada  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. El ejemplo crea una vista y un índice en esa vista. Se incluyen dos consultas que utilizan la vista indizada.  
  
    ```  
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
  
 Para obtener más información, vea [CREATE VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-view-transact-sql).  
  
## <a name="see-also"></a>Vea también  
 [CREATE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-index-transact-sql)   
 [SET ANSI_NULLS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-nulls-transact-sql)   
 [SET ANSI_PADDING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-padding-transact-sql)   
 [SET ANSI_WARNINGS &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-ansi-warnings-transact-sql)   
 [SET ARITHABORT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-arithabort-transact-sql)   
 [SET CONCAT_NULL_YIELDS_NULL &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-concat-null-yields-null-transact-sql)   
 [SET NUMERIC_ROUNDABORT &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-numeric-roundabort-transact-sql)   
 [SET QUOTED_IDENTIFIER &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-quoted-identifier-transact-sql)  
  
  
