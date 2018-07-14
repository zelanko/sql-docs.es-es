---
title: 'Ejemplo: Especificar la directiva HIDE | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- HIDE directive
ms.assetid: 87504d87-1cbd-412a-9041-47884b6efcec
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 5069864e30f02d02fe7d3bf02324c013f6a69219
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37252057"
---
# <a name="example-specifying-the-hide-directive"></a>Ejemplo: Especificar la directiva HIDE
  En este ejemplo se muestra el uso de la directiva **HIDE** . Esta directiva es útil cuando se desea que la consulta devuelva un atributo para ordenar las filas de la tabla universal devuelta por la consulta, pero no se desea que ese atributo aparezca en el documento XML resultante.  
  
 Esta consulta genera este XML:  
  
```  
<ProductModel ProdModelID="19" Name="Mountain-100">  
  <Summary>  
    <SummaryDescription>  
           <Summary> element from XML stored in CatalogDescription column  
    </SummaryDescription>  
  </Summary>  
</ProductModel>  
```  
  
 Esta consulta genera el XML deseado. La consulta identifica dos grupos de columnas con valores 1 y 2 de Tag en los nombres de columna.  
  
 Esta consulta usa el [método query()](/sql/t-sql/xml/query-method-xml-data-type) del tipo de datos **xml** para consultar la columna CatalogDescription de tipo **xml** y recuperar la descripción resumida. Esta consulta también usa el [método value()](/sql/t-sql/xml/value-method-xml-data-type) del tipo de datos **xml** para recuperar el valor ProductModelID de la columna CatalogDescription. Este valor no se requiere en el XML resultante, pero sí es necesario para ordenar el conjunto de filas resultante. Por consiguiente, el nombre de columna, `[Summary!2!ProductModelID!HIDE]`, incluye la directiva **HIDE** . Si esta columna no se incluye en la instrucción SELECT, habrá que ordenar el conjunto de filas según `[ProductModel!1!ProdModelID]` y `[Summary!2!SummaryDescription]` , que es de tipo **xml** , y no se podrá usar la columna de tipo **xml** en ORDER BY. Por tanto, se agrega la columna adicional `[Summary!2!ProductModelID!HIDE]` y luego se especifica en la cláusula ORDER BY.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT  1 as Tag,  
        0 as Parent,  
        ProductModelID     as [ProductModel!1!ProdModelID],  
        Name               as [ProductModel!1!Name],  
        NULL               as [Summary!2!ProductModelID!hide],  
        NULL               as [Summary!2!SummaryDescription]  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not null  
UNION ALL  
SELECT  2 as Tag,  
        1 as Parent,  
        ProductModelID,  
        Name,  
        CatalogDescription.value('  
         declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
       (/PD:ProductDescription/@ProductModelID)[1]', 'int'),  
        CatalogDescription.query('  
         declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
         /pd:ProductDescription/pd:Summary')  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not null  
ORDER BY [ProductModel!1!ProdModelID],[Summary!2!ProductModelID!hide]  
FOR XML EXPLICIT  
go  
```  
  
 El resultado es el siguiente:  
  
```  
<ProductModel ProdModelID="19" Name="Mountain-100">  
  <Summary>  
    <SummaryDescription>  
      <pd:Summary xmlns:pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription" xmlns="">  
        <p1:p xmlns:p1="http://www.w3.org/1999/xhtml">Our top-of-the-line competition mountain bike. Performance-enhancing options include the innovative HL Frame, super-smooth front suspension, and traction for all terrain. </p1:p>  
      </pd:Summary>  
    </SummaryDescription>  
  </Summary>  
</ProductModel>  
```  
  
## <a name="see-also"></a>Vea también  
 [Usar el modo EXPLICIT con FOR XML](use-explicit-mode-with-for-xml.md)  
  
  
