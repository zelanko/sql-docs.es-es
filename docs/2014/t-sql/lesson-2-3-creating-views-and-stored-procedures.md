---
title: Crear vistas y procedimientos almacenados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- creating views and stored procedures
ms.assetid: 53a0426d-07d8-4b7c-aa21-22632753bad8
author: VanMSFT
ms.author: vanto
manager: craigg
ms.openlocfilehash: ee4ba8c35accc6a7d81732ee3d9f9fe5ad1cd01c
ms.sourcegitcommit: 182b8f68bfb345e9e69547b6d507840ec8ddfd8b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/27/2018
ms.locfileid: "43025734"
---
# <a name="creating-views-and-stored-procedures"></a>Crear vistas y procedimientos almacenados
  Ahora que Mary puede tener acceso a la base de datos **TestData** , puede que desee crear algunos objetos de base de datos, como una vista o un procedimiento almacenado y concederle a Mary acceso a los mismos. Una vista es una instrucción SELECT almacenada y un procedimiento almacenado es una o varias instrucciones [!INCLUDE[tsql](../includes/tsql-md.md)] que se ejecutan como un lote.  
  
 Las vistas se consultan como las tablas y no aceptan parámetros. Los procedimientos almacenados son más complejos que las vistas. Los procedimientos almacenados pueden tener parámetros de entrada y salida y pueden contener instrucciones para controlar el flujo del código, como instrucciones IF y WHILE. Una práctica recomendable de programación es usar procedimientos almacenados para realizar todas las tareas repetitivas en la base de datos.  
  
 Para este ejemplo, usará CREATE VIEW para crear una vista que seleccione solo dos de las columnas de la tabla **Products** . A continuación, usará CREATE PROCEDURE para crear un procedimiento almacenado que acepta un parámetro de precio y devuelve solo los productos cuyo costo es menor que el valor del parámetro especificado.  
  
### <a name="to-create-a-view"></a>Para crear una vista  
  
1.  Ejecute la instrucción siguiente para crear una vista muy sencilla que ejecuta una instrucción SELECT y devuelve los nombres y los precios de nuestros productos al usuario.  
  
    ```  
    CREATE VIEW vw_Names  
       AS  
       SELECT ProductName, Price FROM Products;  
    GO  
  
    ```  
  
### <a name="test-the-view"></a>Pruebe la vista  
  
1.  Las vistas se tratan como tablas. Use una instrucción `SELECT` para tener acceso a la vista.  
  
    ```  
    SELECT * FROM vw_Names;  
    GO  
  
    ```  
  
### <a name="to-create-a-stored-procedure"></a>Para crear un procedimiento almacenado  
  
1.  La siguiente instrucción crea un procedimiento almacenado denominado `pr_Names`, acepta un parámetro de entrada denominado `@VarPrice` del tipo de datos `money`. El procedimiento almacenado imprime la instrucción `Products less than` concatenada con el parámetro de entrada que cambia del tipo de datos `money` a un tipo de datos de carácter `varchar(10)` . A continuación, el procedimiento ejecuta una instrucción `SELECT` en la vista y le pasa el parámetro de entrada como parte de la cláusula `WHERE` . Esto devuelve todos los productos cuyo costo es menor que el valor del parámetro de entrada.  
  
    ```  
    CREATE PROCEDURE pr_Names @VarPrice money  
       AS  
       BEGIN  
          -- The print statement returns text to the user  
          PRINT 'Products less than ' + CAST(@VarPrice AS varchar(10));  
          -- A second statement starts here  
          SELECT ProductName, Price FROM vw_Names  
                WHERE Price < @varPrice;  
       END  
    GO  
  
    ```  
  
### <a name="test-the-stored-procedure"></a>Probar el procedimiento almacenado  
  
1.  Para probar el procedimiento almacenado, escriba y ejecute la instrucción siguiente. El procedimiento debe devolver los nombres de dos productos introducidos en la tabla `Products` en la lección 1 con un precio menor que `10.00`.  
  
    ```  
    EXECUTE pr_Names 10.00;  
    GO  
  
    ```  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Conceder acceso a un objeto de base de datos](lesson-2-4-granting-access-to-a-database-object.md)  
  
## <a name="see-also"></a>Vea también  
 [CREATE VIEW &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-view-transact-sql)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-procedure-transact-sql)  
  
  
