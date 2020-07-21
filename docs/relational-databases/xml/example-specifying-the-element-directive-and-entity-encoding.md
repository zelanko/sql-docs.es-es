---
title: Especificación de la directiva ELEMENT y la codificación de entidades | Microsoft Docs
description: Obtenga información sobre cómo especificar la directiva ELEMENT en una consulta SQL para que el resultado de la consulta sea la entidad codificada.
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
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
ms.openlocfilehash: 176cbbd92b55ada81a845018826cbf0b899b3475
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85632660"
---
# <a name="example-specifying-the-element-directive-and-entity-encoding"></a>Ejemplo: Especificación de la directiva ELEMENT y la codificación de entidades
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Este ejemplo muestra la diferencia entre las directivas **ELEMENT** y **XML** . La directiva **ELEMENT** crea entidades para los datos, pero la directiva **XML** no lo hace. Al elemento \<Summary> se le asigna el XML, `<Summary>This is summary description</Summary>`, en la consulta.  
  
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
  
## <a name="see-also"></a>Consulte también  
 [Usar el modo EXPLICIT con FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
  
  
