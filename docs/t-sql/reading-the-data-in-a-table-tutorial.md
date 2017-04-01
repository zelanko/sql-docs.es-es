---
title: "Leer datos de una tabla (Tutorial) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
helpviewer_keywords: 
  - "leer datos de una tabla"
ms.assetid: 532232c9-3d41-45cd-9150-de67a1cbfcf5
caps.latest.revision: 14
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Leer datos de una tabla (Tutorial)
Use la instrucción SELECT para leer los datos de una tabla. La instrucción SELECT es una de las instrucciones de [!INCLUDE[tsql](../includes/tsql-md.md)] más importantes y tiene muchas variaciones en la sintaxis. Para este tutorial, trabajará con cinco versiones sencillas.  
  
### Para leer los datos de una tabla  
  
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
  
## Funciones útiles en una instrucción SELECT  
Para obtener información sobre algunas de las funciones que puede usar para trabajar con datos en instrucciones SELECT, vea los siguientes temas:  
  
|||  
|-|-|  
|[Funciones de cadena &#40;Transact-SQL&#41;](../t-sql/functions/string-functions-transact-sql.md)|[Tipos de datos y funciones de fecha y hora &#40;Transact-SQL&#41;](../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)|  
|[Funciones matemáticas &#40;Transact-SQL&#41;](../t-sql/functions/mathematical-functions-transact-sql.md)|[Funciones de texto e imagen &#40;Transact-SQL&#41;](../Topic/Text%20and%20Image%20Functions%20(Transact-SQL).md)|  
  
## Siguiente tarea de la lección  
[Resumen: Crear objetos de base de datos](../t-sql/summary-creating-database-objects.md)  
  
## Vea también  
[SELECT &#40;Transact-SQL&#41;](../t-sql/queries/select-transact-sql.md)  
  
  
  
