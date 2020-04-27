---
title: Leer datos de una tabla (Tutorial) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- reading data in a table
ms.assetid: 532232c9-3d41-45cd-9150-de67a1cbfcf5
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: 0649e167ebaa90267422594ccd193ba468838e6f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "68187297"
---
# <a name="reading-the-data-in-a-table-tutorial"></a>Leer datos de una tabla (Tutorial)
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
|[Funciones de cadena &#40;Transact-SQL&#41;](/sql/t-sql/functions/string-functions-transact-sql)|[Tipos de datos y funciones de fecha y hora &#40;Transact-SQL&#41;](/sql/t-sql/functions/date-and-time-data-types-and-functions-transact-sql)|  
|[Funciones matemáticas &#40;Transact-SQL&#41;](/sql/t-sql/functions/mathematical-functions-transact-sql)|[Funciones de texto e imagen &#40;Transact-SQL&#41;](/sql/t-sql/functions/text-and-image-functions-textptr-transact-sql)|  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Resumen: Creación de objetos de base de datos](lesson-1-5-summary-creating-database-objects.md)  
  
## <a name="see-also"></a>Consulte también  
 [SELECT &#40;Transact-SQL&#41;](/sql/t-sql/queries/select-transact-sql)  
  
  
