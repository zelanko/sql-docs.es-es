---
title: "Creación de vistas sobre columnas XML | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-xml
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- views [XML in SQL Server]
ms.assetid: eb5f0439-1f69-49c2-8759-e59bda1633b7
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: e5f71a5ebacb8af3a58c6eada233c16b955b6ae5
ms.contentlocale: es-es
ms.lasthandoff: 04/11/2017

---
# <a name="create-views-over-xml-columns"></a>Crear vistas sobre columnas XML
  Puede utilizar una columna de tipo **xml** para crear vistas. En el siguiente ejemplo se crea una vista en la que se recupera el valor de una columna de tipo `xml` por medio del método **value()** del tipo de datos **xml** .  
  
```  
-- Create the table.  
CREATE TABLE T (  
    ProductID          int primary key,   
    CatalogDescription xml)  
GO  
-- Insert sample data.  
INSERT INTO T values(1,'<ProductDescription ProductID="1" ProductName="SomeName" />')  
GO  
-- Create view (note the value() method used to retrieve ProductName   
-- attribute value from the XML).  
CREATE VIEW MyView AS   
  SELECT ProductID,  
         CatalogDescription.value('(/ProductDescription/@ProductName)[1]', 'varchar(40)') AS PName  
  FROM T  
GO   
```  
  
 Ejecute la consulta siguiente con la vista:  
  
```  
SELECT *   
FROM   MyView  
```  
  
 El resultado es el siguiente:  
  
```  
ProductID   PName        
----------- ------------  
1           SomeName   
```  
  
 Tenga en cuenta los puntos siguientes sobre cómo utilizar el tipo de datos **xml** para crear las vistas:  
  
-   El tipo de datos xml se puede crear en una vista materializada. La vista materializada no puede basarse en un método de tipo de datos xml. Sin embargo, puede convertirse en una colección de esquemas XML distinta del tipo de columna xml de la tabla base.  
  
-   El tipo de datos **xml** no se puede utilizar en vistas distribuidas con particiones.  
  
-   Los predicados de SQL que se ejecutan con la vista no se insertarán en la expresión XQuery de la definición de vista.  
  
-   Los métodos del tipo de datos XML de una vista no son actualizables.  
  
  
