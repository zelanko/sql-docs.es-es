---
title: 'Ejemplo: Especificar la directiva ELEMENT y la codificación de entidades | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- ELEMENT directive
- entity encoding [XML]
ms.assetid: 50cda5c1-7293-4080-93b3-872e3b8d484e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0e943e6dfb83d21d4a0e0beac0c6acd0d62881f1
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51667364"
---
# <a name="example-specifying-the-element-directive-and-entity-encoding"></a>Ejemplo: Especificar la directiva ELEMENT y la codificación de entidades
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
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
  
## <a name="see-also"></a>Ver también  
 [Usar el modo EXPLICIT con FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  
