---
title: 'Ejemplo: Especificar la directiva CDATA | Microsoft Docs'
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
- CDATA directive
ms.assetid: 949071e6-787f-480d-bb86-3ac16a027af1
caps.latest.revision: 9
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: d648d1762107125f679afdcbd4c9a1631fa02ccd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36109218"
---
# <a name="example-specifying-the-cdata-directive"></a>Ejemplo: Especificar la directiva CDATA
  Si se establece la directiva en **CDATA**, los datos contenidos no se codifican por entidad, pero se colocan en la sección CDATA. Los atributos **CDATA** no deben tener nombre.  
  
 La siguiente consulta engloba la descripción resumida de modelos de productos en una sección CDATA.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT  1 as Tag,  
        0 as Parent,  
        ProductModelID  as [ProductModel!1!ProdModelID],  
        Name            as [ProductModel!1!Name],  
        '<Summary>This is summary description</Summary>'     
            as [ProductModel!1!!CDATA] -- no attribute name so ELEMENT assumed  
FROM    Production.ProductModel  
WHERE   ProductModelID=19  
FOR XML EXPLICIT  
```  
  
 El resultado es el siguiente:  
  
```  
<ProductModel ProdModelID="19" Name="Mountain-100">  
   <![CDATA[<Summary>This is summary description</Summary>]]>  
</ProductModel>  
```  
  
## <a name="see-also"></a>Vea también  
 [Usar el modo EXPLICIT con FOR XML](use-explicit-mode-with-for-xml.md)  
  
  