---
title: Creación de vistas sobre columnas XML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- views [XML in SQL Server]
ms.assetid: eb5f0439-1f69-49c2-8759-e59bda1633b7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 767844d7b195ece286b8f19cc34855bf50185a0c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48049835"
---
# <a name="create-views-over-xml-columns"></a>Crear vistas sobre columnas XML
  Puede usar un `xml` columna de tipo para crear vistas. El ejemplo siguiente crea una vista en la que el valor de un `xml` columna de tipo se recupera utilizando la `value()` método de la `xml` tipo de datos.  
  
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
  
 Tenga en cuenta los siguientes puntos acerca de cómo utilizar el `xml` tipo de datos para crear vistas:  
  
-   El tipo de datos xml se puede crear en una vista materializada. La vista materializada no puede basarse en un método de tipo de datos xml. Sin embargo, puede convertirse en una colección de esquemas XML distinta del tipo de columna xml de la tabla base.  
  
-   El `xml` no se puede utilizar el tipo de datos en vistas con particiones distribuidas.  
  
-   Los predicados de SQL que se ejecutan con la vista no se insertarán en la expresión XQuery de la definición de vista.  
  
-   Los métodos del tipo de datos XML de una vista no son actualizables.  
  
  
