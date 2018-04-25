---
title: Leer datos de una tabla (Tutorial) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: t-sql
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- SQL Server 2016
helpviewer_keywords:
- reading data in a table
ms.assetid: 532232c9-3d41-45cd-9150-de67a1cbfcf5
caps.latest.revision: 14
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5fdea4946a0b4c311a631eb9569099a808cfe11b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="lesson-1-4---reading-the-data-in-a-table"></a>Lección 1-4: Leer los datos de una tabla
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]
Use la instrucción SELECT para leer los datos de una tabla. La instrucción SELECT es una de las instrucciones de [!INCLUDE[tsql](../includes/tsql-md.md)] más importantes y tiene muchas variaciones en la sintaxis. Para este tutorial, trabajará con cinco versiones sencillas.  
  
### <a name="to-read-the-data-in-a-table"></a>Para leer los datos de una tabla  
  
1.  Escriba y ejecute las siguientes instrucciones para leer los datos de la tabla `Products` .  
  
    ```  
    -- The basic syntax for reading data from a single table  
    SELECT ProductID, ProductName, Price, ProductDescription  
        FROM dbo.Products  
    GO  
  
    ```  
  
2.  Puede usar un asterisco para seleccionar todas las columnas de la tabla. Esto se suele usar en las consultas ad hoc. Debe proporcionar la lista de columnas en el código permanente de modo que la instrucción devuelva las columnas previstas, incluso si más tarde se agrega una columna nueva a la tabla.  
  
    ```  
    -- Returns all columns in the table  
    -- Does not use the optional schema, dbo  
    SELECT * FROM Products  
    GO  
  
    ```  
  
3.  Puede omitir columnas que ya no desea que se devuelvan. Las columnas se devolverán en el orden en que aparecen.  
  
    ```  
    -- Returns only two of the columns from the table  
    SELECT ProductName, Price  
        FROM dbo.Products  
    GO  
  
    ```  
  
4.  Use una cláusula `WHERE` para limitar las filas que se devuelven al usuario.  
  
    ```  
    -- Returns only two of the records in the table  
    SELECT ProductID, ProductName, Price, ProductDescription  
        FROM dbo.Products  
        WHERE ProductID < 60  
    GO  
  
    ```  
  
5.  Puede trabajar con los valores de las columnas según se devuelven. En el siguiente ejemplo se realiza una operación matemática en la columna `Price` . Las columnas que se han cambiado de esta manera no tendrán un nombre, a menos que proporcione uno mediante la palabra clave `AS` .  
  
    ```  
    -- Returns ProductName and the Price including a 7% tax  
    -- Provides the name CustomerPays for the calculated column  
    SELECT ProductName, Price * 1.07 AS CustomerPays  
        FROM dbo.Products  
    GO  
    ```  
  
## <a name="functions-that-are-useful-in-a-select-statement"></a>Funciones útiles en una instrucción SELECT  
Para obtener información sobre algunas de las funciones que puede usar para trabajar con datos en instrucciones SELECT, vea los siguientes temas:  
  
|||  
|-|-|  
|[Funciones de cadena &#40;Transact-SQL&#41;](../t-sql/functions/string-functions-transact-sql.md)|[Tipos de datos y funciones de fecha y hora &#40;Transact-SQL&#41;](../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)|  
|[Funciones matemáticas &#40;Transact-SQL&#41;](../t-sql/functions/mathematical-functions-transact-sql.md)|[Funciones de texto e imagen &#40;Transact-SQL&#41;](http://msdn.microsoft.com/library/b9c70488-1bf5-4068-a003-e548ccbc5199)|  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
[Resumen: Crear objetos de base de datos](../t-sql/lesson-1-5-summary-creating-database-objects.md)  
  
## <a name="see-also"></a>Ver también  
[SELECT &#40;Transact-SQL&#41;](../t-sql/queries/select-transact-sql.md)  
  
  
  
