---
title: MSSQLSERVER_207 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 207 (Database Engine error)
ms.assetid: d1ab00c7-0331-437a-84fe-bae53b82feec
caps.latest.revision: 17
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ba320288a06dd8498d9699712a6e53e34ae93c09
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver207"></a>MSSQLSERVER_207
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Nombre del producto|SQL Server|  
|Identificador del evento|207|  
|Origen del evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nombre simbólico|SQ_BADCOL|  
|Texto del mensaje|El nombre de columna '%.*ls' no es válido.|  
  
## <a name="explanation"></a>Explicación  
Este error de consulta puede deberse a uno de los siguientes problemas:  
  
-   El nombre de la columna no se ha escrito correctamente o la columna no existe en ninguna de las tablas especificadas.  
  
-   La intercalación de la base de datos distingue entre mayúsculas y minúsculas, y la grafía del nombre de columna especificado en la consulta no coincide con el de la columna definida en la tabla. Por ejemplo, cuando una columna se define en una tabla como **LastName** y la base de datos usa una intercalación con distinción entre mayúsculas y minúsculas, las consultas que hacen referencia a la columna como **Lastname** o como **lastname** harán que se devuelva el error 207 porque el nombre de columna no coincide.  
  
-   Otras cláusulas como WHERE o GROUP BY hacen referencia a un alias de columna, definido en la cláusula SELECT. Por ejemplo, la siguiente consulta define el alias de columna `Year` en la cláusula SELECT y hace referencia a él en la cláusula GROUP BY.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT DATEPART(yyyy,OrderDate) AS Year, SUM(TotalDue) AS Total  
    FROM Sales.SalesOrderHeader  
    GROUP BY Year;  
    ```  
  
    Debido al orden en el que las cláusulas de consulta se procesan de manera lógica, el ejemplo devuelve el error 207. El orden de procesamiento es el siguiente:  
  
    1.  FROM  
  
    2.  ON  
  
    3.  JOIN  
  
    4.  WHERE  
  
    5.  GROUP BY  
  
    6.  WITH CUBE o WITH ROLLUP  
  
    7.  HAVING  
  
    8.  SELECT  
  
    9. DISTINCT  
  
    10. ORDER BY  
  
    11. ARRIBA  
  
    Puesto que un alias de columna no se define hasta que se procesa la cláusula SELECT, no se conoce el nombre de alias cuando se procesa la cláusula GROUP BY.  
  
-   La instrucción MERGE genera este error cuando la cláusula *<merge_matched>* hace referencia a las columnas de la tabla de origen, pero la tabla de origen de la cláusula WHEN NOT MATCHED BY SOURCE no devuelve ninguna fila. El error ocurre porque no se puede obtener acceso a las columnas de la tabla de origen cuando no se devuelven filas a la consulta. Por ejemplo, la cláusula `WHEN NOT MATCHED BY SOURCE THEN UPDATE SET TargetTable.Col1 = SourceTable.Col1` puede hacer que la instrucción genere un error si `Col1` en la tabla de origen es inaccesible.  
  
## <a name="user-action"></a>Acción del usuario  
Compruebe la información siguiente y corrija la instrucción según corresponda.  
  
-   El nombre de columna existe en la tabla y está correctamente escrito. En el siguiente ejemplo, se consulta a la vista de catálogo **sys.columns** para que devuelva todos los nombres de columna para una tabla determinada.  
  
    ```  
    SELECT name FROM sys.columns WHERE object_id = OBJECT_ID('schema_name.table_name');  
    ```  
  
-   La distinción entre mayúsculas y minúsculas de la intercalación de bases de datos. La siguiente instrucción devuelve la intercalación de la base de datos especificada.  
  
    ```  
    SELECT collation_name FROM sys.databases WHERE name = 'database_name';  
    ```  
  
    La abreviatura CS en el nombre de la intercalación indica que distingue entre mayúsculas y minúsculas. Por ejemplo, Latin1_General_CS_AS es una intercalación que distingue mayúsculas de minúsculas que distingue acentos. Modifique el nombre de columna para que la grafía coincida con el nombre de columna definido en la tabla.  
  
-   La referencia a un alias de columna no es correcta. Modifique la instrucción repitiendo la expresión que define el alias en la cláusula apropiada o usando una tabla derivada. El siguiente ejemplo repite las expresiones que define el alias `Year` en la cláusula GROUP BY.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT DATEPART(yyyy,OrderDate) AS Year ,SUM(TotalDue) AS Total  
    FROM Sales.SalesOrderHeader  
    GROUP BY DATEPART(yyyy,OrderDate);  
    ```  
  
    El siguiente ejemplo usa una tabla derivada para que otras cláusulas de la consulta puedan disponer del nombre de alias. Tenga en cuenta que el alias `Year` se define en la cláusula FROM, que se procesa en primer lugar, y por lo tanto otras cláusulas de la consulta pueden disponer de él.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT d.Year, SUM(TotalDue) AS Total  
    FROM (SELECT DATEPART(yyyy,OrderDate) AS Year, TotalDue  
          FROM Sales.SalesOrderHeader)AS d  
    GROUP BY Year;  
    ```  
  
-   La cláusula WHEN NOT MATCHED BY SOURCE de la instrucción MERGE hace referencia a un valor al que se puede tener acceso. Modifique la instrucción MERGE para que la tabla de origen devuelva al menos una fila en la cláusula WHEN NOT MATCHED BY SOURCE. Por ejemplo, puede que tenga que agregar o revisar la condición de búsqueda especificada para la cláusula. De manera alternativa, puede modificar la cláusula para que especifique un valor que no haga referencia a la tabla de origen. Por ejemplo, `WHEN NOT MATCHED BY SOURCE THEN UPDATE SET TargetTable.Col1 = <expression, or other available value>`.  
  
## <a name="see-also"></a>Vea también  
[MERGE &#40;Transact-SQL&#41;](~/t-sql/statements/merge-transact-sql.md)  
[FROM &#40;Transact-SQL&#41;](~/t-sql/queries/from-transact-sql.md)  
[SELECT &#40;Transact-SQL&#41;](~/t-sql/queries/select-transact-sql.md)  
[UPDATE &#40;Transact-SQL&#41;](~/t-sql/queries/update-transact-sql.md)  
  

