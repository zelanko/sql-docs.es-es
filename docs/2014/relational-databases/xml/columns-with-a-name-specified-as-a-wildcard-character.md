---
title: Columnas con un nombre especificado como carácter comodín | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- names [SQL Server], columns with
ms.assetid: d9551df1-5bb4-4c0b-880a-5bb049834884
caps.latest.revision: 10
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 6245d194882e680cfab4841ac5a4f307e58510f9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36107362"
---
# <a name="columns-with-a-name-specified-as-a-wildcard-character"></a>Columnas con un nombre especificado como carácter comodín
  Si el nombre de columna especificado es un carácter comodín (\*), su contenido se insertará como si no se hubiera especificado ningún nombre. Si esta columna no es`xml` tipo, el contenido de la columna se insertará como un nodo de texto, tal como se muestra en el ejemplo siguiente:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT E.BusinessEntityID "@EmpID",   
       FirstName "*",   
       MiddleName "*",   
       LastName "*"  
FROM   HumanResources.Employee AS E  
INNER JOIN Person.Person AS P  
    ON E.BusinessEntityID = P.BusinessEntityID  
WHERE E.BusinessEntityID=1  
FOR XML PATH;  
```  
  
 El resultado es el siguiente:  
  
 `<row EmpID="1">KenJSánchez</row>`  
  
 Si la columna es de tipo `xml`, se inserta el árbol XML correspondiente. Por ejemplo, la consulta siguiente especifica "*" para el nombre de columna que incluye el XML devuelto por XQuery con la columna Instructions.  
  
```  
SELECT   
       ProductModelID,  
       Name,  
       Instructions.query('declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
                /MI:root/MI:Location   
              ') as "*"  
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH;   
GO  
```  
  
 Éste es el resultado. El XML devuelto por XQuery se insertará sin un elemento de ajuste.  
  
 `<row>`  
  
 `<ProductModelID>7</ProductModelID>`  
  
 `<Name>HL Touring Frame</Name>`  
  
 `<MI:Location LocationID="10">...</MI:Location>`  
  
 `<MI:Location LocationID="20">...</MI:Location>`  
  
 `...`  
  
 `</row>`  
  
## <a name="see-also"></a>Vea también  
 [Usar el modo PATH con FOR XML](use-path-mode-with-for-xml.md)  
  
  