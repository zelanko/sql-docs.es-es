---
title: Columnas sin nombre | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- names [SQL Server], columns without
ms.assetid: 440de44e-3a56-4531-b4e4-1533ca933cac
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e90ebc825e0da713149f02ae2b707f5e1611b3ad
ms.sourcegitcommit: d457bb828eb46ee83f8ff5bdecfff09b26d7b154
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/26/2018
ms.locfileid: "39259760"
---
# <a name="columns-without-a-name"></a>Columnas sin nombre
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Las columnas sin nombre se insertarán entre líneas. Por ejemplo, las columnas calculadas o las consultas escalares anidadas que no especifiquen alias de columna generarán columnas sin nombre. Si la columna es de tipo **xml** , se insertará el contenido de esa instancia de tipo de datos. De lo contrario, el contenido de la columna se insertará como un nodo de texto.  
  
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
  
```xml
<row>
  <ProductModelID>7</ProductModelID>
  <Name>HL Touring Frame</Name>
  <MI:Location ...LocationID="10" ...></MI:Location>
  <MI:Location ...LocationID="20" ...></MI:Location>
  ...
</row>
```

## <a name="see-also"></a>Ver también  
 [Usar el modo PATH con FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
