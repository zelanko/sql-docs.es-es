---
title: Columnas sin nombre | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns without
ms.assetid: 440de44e-3a56-4531-b4e4-1533ca933cac
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d36934be00b7d4be6b28a6ed1748f99ded2d310e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227005"
---
# <a name="columns-without-a-name"></a>Columnas sin nombre
  Las columnas sin nombre se insertarán entre líneas. Por ejemplo, las columnas calculadas o las consultas escalares anidadas que no especifiquen alias de columna generarán columnas sin nombre. Si la columna es de `xml` se inserta el tipo, el contenido de esa instancia del tipo de datos. De lo contrario, el contenido de la columna se insertará como un nodo de texto.  
  
```  
SELECT 2+2  
FOR XML PATH  
```  
  
 Cree este XML. De forma predeterminada, por cada fila del conjunto de filas, se genera un elemento <`row`> en el XML resultante. Ocurre lo mismo que en el modo RAW.  
  
 `<row>4</row>`  
  
 La consulta siguiente devuelve un conjunto de filas de tres columnas. La tercera columna sin nombre incluye los datos XML. El modo PATH inserta una instancia de tipo xml.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID,  
       Name,  
       Instructions.query('declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
                /MI:root/MI:Location   
              ')   
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH ;  
GO  
```  
  
 Éste es el resultado parcial:  
  
 `<row>`  
  
 `<ProductModelID>7</ProductModelID>`  
  
 `<Name>HL Touring Frame</Name>`  
  
 `<MI:Location ...LocationID="10" ...></MI:Location>`  
  
 `<MI:Location ...LocationID="20" ...></MI:Location>`  
  
 `...`  
  
 `</row>`  
  
## <a name="see-also"></a>Vea también  
 [Usar el modo PATH con FOR XML](use-path-mode-with-for-xml.md)  
  
  
