---
title: 'Ejemplo: Especificación de la directiva ELEMENT y la codificación de entidades | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- ELEMENT directive
- entity encoding [XML]
ms.assetid: 50cda5c1-7293-4080-93b3-872e3b8d484e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 28e0e9f808820acc1959ccc11266174e5610600c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63287238"
---
# <a name="example-specifying-the-element-directive-and-entity-encoding"></a>Ejemplo: Especificación de la directiva ELEMENT y la codificación de entidades
  Este ejemplo muestra la diferencia entre las directivas **ELEMENT** y **XML** . La directiva **ELEMENT** crea entidades para los datos, pero la directiva **XML** no lo hace. Al elemento \<Summary> se le asigna XML, `<Summary>This is summary description</Summary>`, en la consulta.  
  
 Considere esta consulta:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT  1 as Tag,  
        0 as Parent,  
        ProductModelID  as [ProductModel!1!ProdModelID],  
        Name            as [ProductModel!1!Name],  
        NULL            as [Summary!2!SummaryDescription!ELEMENT]  
FROM    Production.ProductModel  
WHERE   ProductModelID=19  
UNION ALL  
SELECT  2 as Tag,  
        1 as Parent,  
        ProductModelID,  
        NULL,  
       '<Summary>This is summary description</Summary>'  
FROM   Production.ProductModel  
WHERE  ProductModelID=19  
FOR XML EXPLICIT  
```  
  
 Éste es el resultado. Se crea una entidad en el resultado para la descripción resumida.  
  
```  
<ProductModel ProdModelID="19" Name="Mountain-100">  
  <Summary>  
    <SummaryDescription><Summary>This is summary description</Summary></SummaryDescription>  
  </Summary>  
</ProductModel>  
```  
  
 Ahora, si se especifica la directiva **XML** en el nombre de columna `Summary!2!SummaryDescription!XML`, en lugar de la directiva **ELEMENT** , se recibirá la descripción resumida sin la creación de entidades.  
  
```  
<ProductModel ProdModelID="19" Name="Mountain-100">  
  <Summary>  
    <SummaryDescription>  
      <Summary>This is summary description</Summary>  
    </SummaryDescription>  
  </Summary>  
</ProductModel>  
```  
  
 En lugar de asignar un valor XML estático, la consulta siguiente usa el método **query()** del tipo **xml** para recuperar la descripción resumida del modelo de productos de la columna CatalogDescription de tipo **xml** . Como se sabe que el resultado es de tipo **xml** , no se aplica la creación de entidades.  
  
```  
SELECT  1 as Tag,  
        0 as Parent,  
        ProductModelID  as [ProductModel!1!ProdModelID],  
        Name            as [ProductModel!1!Name],  
        NULL            as [Summary!2!SummaryDescription]  
FROM    Production.ProductModel  
WHERE   CatalogDescription is not null  
UNION ALL  
SELECT  2 as Tag,  
        1 as Parent,  
        ProductModelID,  
        Name,  
       (SELECT CatalogDescription.query('  
            declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
          /pd:ProductDescription/pd:Summary'))  
FROM     Production.ProductModel  
WHERE    CatalogDescription is not null  
ORDER BY [ProductModel!1!ProdModelID],Tag  
FOR XML EXPLICIT  
```  
  
## <a name="see-also"></a>Vea también  
 [Usar el modo EXPLICIT con FOR XML](use-explicit-mode-with-for-xml.md)  
  
  
