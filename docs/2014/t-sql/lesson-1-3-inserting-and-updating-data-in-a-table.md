---
title: Inserción y actualización de datos en una tabla (Tutorial) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- inserting and updating data
ms.assetid: 514dc87a-b829-43b5-8fc8-1a400a260284
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: fbc9a3fb254e417b0d29a50a28e2897d5ecda3b9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198329"
---
# <a name="inserting-and-updating-data-in-a-table-tutorial"></a>Insertar y actualizar datos en una tabla (Tutorial)
  Ahora que ha creado la tabla **Products**, ya está listo para insertar datos en la tabla mediante la instrucción INSERT. Después de insertar los datos, cambiará el contenido de una fila con una instrucción UPDATE. Utilizará la cláusula WHERE de la instrucción UPDATE para restringir la actualización a una sola fila. Las cuatro instrucciones introducirán los siguientes datos.  
  
|ProductID|ProductName|Price|ProductDescription|  
|---------------|-----------------|-----------|------------------------|  
|1|Clamp|12,48|Workbench clamp|  
|50|Screwdriver|3,17|Flat head|  
|75|Tire Bar||Tool for changing tires.|  
|3000|3mm Bracket|,52||  
  
 La sintaxis básica es: INSERT, nombre de tabla, lista de columnas, VALUES y, a continuación, una lista de los valores que se van a insertar. Los dos guiones dobles antes de cada línea indican que la línea es un comentario y el compilador ignorará el texto. En este caso, el comentario describe una variación permitida de la sintaxis.  
  
### <a name="to-insert-data-into-a-table"></a>Para insertar datos en una tabla  
  
1.  Ejecute la instrucción siguiente para insertar una fila en la tabla `Products` que se ha creado en la tarea anterior. Ésta es la sintaxis básica.  
  
    ```  
    -- Standard syntax  
    INSERT dbo.Products (ProductID, ProductName, Price, ProductDescription)  
        VALUES (1, 'Clamp', 12.48, 'Workbench clamp')  
    GO  
  
    ```  
  
2.  La instrucción siguiente muestra cómo se puede cambiar el orden en que se proporcionan los parámetros modificando la situación de `ProductID` y `ProductName` en la lista de campos (entre paréntesis) y en la lista de valores.  
  
    ```  
    -- Changing the order of the columns  
    INSERT dbo.Products (ProductName, ProductID, Price, ProductDescription)  
        VALUES ('Screwdriver', 50, 3.17, 'Flat head')  
    GO  
  
    ```  
  
3.  La instrucción siguiente demuestra que los nombres de las columnas son opcionales, siempre y cuando los valores se enumeren en el orden correcto. Esta sintaxis es habitual, pero no se recomienda porque podría ser difícil para otros comprender su código. `NULL` se especifica para la columna `Price` porque el precio de este producto no se conoce todavía.  
  
    ```  
    -- Skipping the column list, but keeping the values in order  
    INSERT dbo.Products  
        VALUES (75, 'Tire Bar', NULL, 'Tool for changing tires.')  
    GO  
  
    ```  
  
4.  El nombre de esquema es opcional mientras tenga acceso a una tabla del esquema predeterminado y la modifique. Puesto que la columna `ProductDescription` permite valores NULL y no se ha proporcionado ningún valor, el nombre de columna y el valor de `ProductDescription` se pueden quitar por completo de la instrucción.  
  
    ```  
    -- Dropping the optional dbo and dropping the ProductDescription column  
    INSERT Products (ProductID, ProductName, Price)  
        VALUES (3000, '3mm Bracket', .52)  
    GO  
    ```  
  
### <a name="to-update-the-products-table"></a>Para actualizar la tabla de productos  
  
1.  Escriba y ejecute la siguiente instrucción `UPDATE` para cambiar el `ProductName` del segundo producto de `Screwdriver`a `Flat Head Screwdriver`.  
  
    ```  
    UPDATE dbo.Products  
        SET ProductName = 'Flat Head Screwdriver'  
        WHERE ProductID = 50  
    GO  
    ```  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Leer datos de una tabla &#40;Tutorial&#41;](lesson-1-4-reading-the-data-in-a-table.md)  
  
## <a name="see-also"></a>Vea también  
 [INSERT &#40;Transact-SQL&#41;](/sql/t-sql/statements/insert-transact-sql)   
 [UPDATE &#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql)  
  
  
