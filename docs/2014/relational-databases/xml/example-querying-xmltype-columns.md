---
title: 'Ejemplo: consultar columnas de tipo XML | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- RAW mode, querying XML example
ms.assetid: d9f3710d-7a2e-4abe-9c02-3e3c0df4d620
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 3ae1077d933d9872e3b5691e6233af4b82d61d58
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48218165"
---
# <a name="example-querying-xmltype-columns"></a>Ejemplo: Consultar columnas de tipo XML
  La consulta siguiente incluye columnas de `xml` tipo. La consulta recupera el identificador, nombre y pasos de fabricación del modelo de producto en la primera ubicación de la columna `Instructions` de tipo `xml`.  
  
## <a name="example"></a>Ejemplo  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name,  
   Instructions.query('  
declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
   /MI:root/MI:Location[1]/MI:step  
')   
FROM Production.ProductModel  
FOR XML RAW ('ProductModelData')  
GO  
```  
  
 A continuación se muestra el resultado. Tenga en cuenta que la tabla almacena las instrucciones de fabricación solo de algunos modelos de productos. Los pasos de fabricación se devuelven como subelementos del elemento <`ProductModelData`> en el resultado.  
  
```  
<ProductModelData ProductModelID="5" Name="HL Mountain Frame" />  
<ProductModelData ProductModelID="6" Name="HL Road Frame" />  
<ProductModelData ProductModelID="7" Name="HL Touring Frame">  
    <MI:step> ... </MI:step>  
    <MI:step> ... </MI:step>  
 </ProductModelData>  
```  
  
 Si la consulta especifica un nombre de columna para el XML devuelto por la consulta XQuery, como se especifica en la siguiente instrucción `SELECT`, los pasos de fabricación se incluyen en el elemento que tiene el nombre especificado.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name,  
   Instructions.query('  
declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
   /MI:root/MI:Location[1]/MI:step  
') as ManuSteps  
FROM Production.ProductModel  
FOR XML RAW ('ProductModelData')  
go  
```  
  
 El resultado es el siguiente:  
  
```  
<ProductModelData ProductModelID="5" Name="HL Mountain Frame" />  
<ProductModelData ProductModelID="6" Name="HL Road Frame" />  
<ProductModelData ProductModelID="7" Name="HL Touring Frame">  
  <ManuSteps>  
    <MI:step ... </MI:step>  
    <MI:step ... </MI:step>  
  </ManuSteps>  
</ProductModelData>  
```  
  
 En la consulta siguiente se especifica la directiva `ELEMENTS` . Por tanto, el resultado devuelto está centrado en elementos. La opción `XSINIL` especificada junto con la directiva `ELEMENTS` devuelve los elementos <`ManuSteps`>, aunque la columna correspondiente del conjunto de resultados sea NULL.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID, Name,  
   Instructions.query('  
declare namespace MI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"  
   /MI:root/MI:Location[1]/MI:step  
') as ManuSteps  
FROM Production.ProductModel  
FOR XML RAW ('ProductModelData'), root('MyRoot'), ELEMENTS XSINIL  
go  
```  
  
 El resultado es el siguiente:  
  
```  
<MyRoot xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">  
   ...  
  <ProductModelData>  
    <ProductModelID>6</ProductModelID>  
    <Name>HL Road Frame</Name>  
    <ManuSteps xsi:nil="true" />  
  </ProductModelData>  
  <ProductModelData>  
    <ProductModelID>7</ProductModelID>  
    <Name>HL Touring Frame</Name>  
    <ManuSteps>  
      <MI:step ... </MI:step>  
      <MI:step ...</MI:step>  
       ...  
    </ManuSteps>  
  </ProductModelData>  
</MyRoot>  
```  
  
## <a name="see-also"></a>Vea también  
 [Usar el modo RAW con FOR XML](use-raw-mode-with-for-xml.md)  
  
  
