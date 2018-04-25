---
title: Inserción y actualización de datos en una tabla (Tutorial) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
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
- inserting and updating data
ms.assetid: 514dc87a-b829-43b5-8fc8-1a400a260284
caps.latest.revision: 13
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 407b1c470f691de3c6165cddfe1252afc6e44da9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="lesson-1-3---inserting-and-updating-data-in-a-table"></a>Lección 1-3: Inserción y actualización de datos en una tabla
[!INCLUDE[tsql-appliesto-ss2008-all-md](../includes/tsql-appliesto-ss2008-all-md.md)]
Ahora que ha creado la tabla **Products** , ya está listo para insertar datos en la tabla mediante la instrucción INSERT. Después de insertar los datos, cambiará el contenido de una fila con una instrucción UPDATE. Utilizará la cláusula WHERE de la instrucción UPDATE para restringir la actualización a una sola fila. Las cuatro instrucciones introducirán los siguientes datos.  
  
|ProductID|ProductName|Price|ProductDescription|  
|-------------|---------------|---------|----------------------|  
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
[Leer datos de una tabla &#40;Tutorial&#41;](../t-sql/lesson-1-4-reading-the-data-in-a-table.md)  
  
## <a name="see-also"></a>Ver también  
[INSERT &#40;Transact-SQL&#41;](../t-sql/statements/insert-transact-sql.md)  
[UPDATE &#40;Transact-SQL&#41;](../t-sql/queries/update-transact-sql.md)  
  
  
  
