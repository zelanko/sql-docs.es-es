---
title: Crear una tabla (Tutorial) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- creating tables
ms.assetid: 653f2dd3-36a2-4bd5-8703-71a57d244661
author: VanMSFT
ms.author: vanto
ms.openlocfilehash: c772f2527bd5ddb8a6759cbaa72d8aed9277f5cb
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85048481"
---
# <a name="creating-a-table-tutorial"></a>Crear una tabla (Tutorial)
  Para crear una tabla, debe proporcionar un nombre para ésta además de los nombres y los tipos de datos de cada columna de la tabla. También es recomendable indicar si se permiten valores NULL en cada columna.  
  
 La mayoría de las tablas tienen una clave principal, que se compone de una o varias columnas de la tabla. Una clave principal siempre es única. [!INCLUDE[ssDE](../includes/ssde-md.md)] exigirá la restricción de que el valor de la clave principal no se puede repetir en la tabla.  
  
 Para obtener una lista de tipos de datos y vínculos para una descripción de cada uno, consulte [Tipos de datos &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql).  
  
> [!NOTE]  
>  [!INCLUDE[ssDE](../includes/ssde-md.md)] se puede instalar para distinguir mayúsculas de minúsculas o no distinguir mayúsculas de minúsculas. Si se instala [!INCLUDE[ssDE](../includes/ssde-md.md)] para distinguir mayúsculas de minúsculas, los nombres de objetos siempre deben tener las mismas mayúsculas y minúsculas. Por ejemplo, una tabla denominada OrderData es diferente de la denominada ORDERDATA. Si se instala [!INCLUDE[ssDE](../includes/ssde-md.md)] para no distinguir mayúsculas de minúsculas, esos dos nombres de tablas se consideran la misma tabla y ese nombre solo se puede utilizar una vez.  
  
### <a name="to-create-a-database-to-contain-the-new-table"></a>Para crear una base de datos que contenga la nueva tabla  
  
-   Escriba el código siguiente en una ventana del Editor de consultas.  
  
    ```  
    USE master;  
    GO  
  
    --Delete the TestData database if it exists.  
    IF EXISTS(SELECT * from sys.databases WHERE name='TestData')  
    BEGIN  
        DROP DATABASE TestData;  
    END  
  
    --Create a new database called TestData.  
    CREATE DATABASE TestData;  
    Press the F5 key to execute the code and create the database.  
    ```  
  
### <a name="switch-the-query-editor-connection-to-the-testdata-database"></a>Cambie la conexión del Editor de consultas a la base de datos TestData  
  
-   En una ventana del Editor de consultas, escriba y ejecute el siguiente código para cambiar la conexión a la base de datos `TestData` .  
  
    ```  
    USE TestData  
    GO  
    ```  
  
### <a name="to-create-a-table"></a>Para crear una tabla  
  
-   En una ventana del Editor de consultas, escriba y ejecute el siguiente código para crear una tabla sencilla denominada `Products`. Las columnas de la tabla son `ProductID`, `ProductName`, `Price`y `ProductDescription`. La columna `ProductID` es la clave principal de la tabla. `int`, `varchar(25)`, `money`y `text` son todos los tipos de datos. Solo las columnas `Price` y `ProductionDescription` pueden no tener datos cuando se inserta o cambia una fila. Esta instrucción contiene un elemento opcional (`dbo.`) denominado esquema. El esquema es el objeto de base de datos propietario de la tabla. Si es un administrador, `dbo` es el esquema predeterminado. `dbo` hace referencia al propietario de la base de datos.  
  
    ```  
    CREATE TABLE dbo.Products  
       (ProductID int PRIMARY KEY NOT NULL,  
        ProductName varchar(25) NOT NULL,  
        Price money NULL,  
        ProductDescription text NULL)  
    GO  
    ```  
  
## <a name="next-task-in-lesson"></a>Siguiente tarea de la lección  
 [Insertar y actualizar datos en una tabla &#40;Tutorial&#41;](../t-sql/lesson-1-3-inserting-and-updating-data-in-a-table.md)  
  
## <a name="see-also"></a>Consulte también  
 [CREATE TABLE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-table-transact-sql)  
  
  
