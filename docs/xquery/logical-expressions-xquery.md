---
title: "Expresiones lógicas (XQuery) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- logical operators [SQL Server], XQuery
- effective Boolean value [XQuery]
- logical expressions [XQuery]
- EBV
- expressions [XQuery], logical
ms.assetid: de94cd2e-2d48-49fb-9ebd-a2d90c79bf62
caps.latest.revision: "26"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d19a9e384b8a4e0f1ac1a20d101c37343eff4369
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="logical-expressions-xquery"></a>Expresiones lógicas (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery admite la operación lógica **y** y **o** operadores.  
  
```  
expression1 and expression2  
expression1 or expression2  
```  
  
 Las expresiones de prueba, `expression1,``expression2`, en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] puede dar lugar a una secuencia vacía, una secuencia de uno o más nodos o un solo valor booleano. En función del resultado, se determinará su valor booleano efectivo de la forma siguiente:    
  
-   Si la expresión de prueba da como resultado una secuencia vacía, el resultado será False.  
  
-   Si la expresión de prueba da como resultado un solo valor booleano, este valor será el resultado de la expresión.  
  
-   Si la expresión de prueba da como resultado una secuencia de uno o varios nodos, el resultado de la expresión será True.  
  
-   De lo contrario, se generará un error estático.  
  
 La operación lógica **y** y **o** operador, a continuación, se aplica a los valores booleanos resultantes de las expresiones con la semántica lógica estándar.  
  
 La consulta siguiente recupera del catálogo de productos las imágenes pequeñas de ángulo frontal, el elemento <`Picture`>, de un modelo de producto determinado. Tenga en cuenta que para cada documento de descripción de productos, se pueden almacenar en el catálogo una o varias imágenes de producto con distintos atributos, como el tamaño y el ángulo.  
  
```  
SELECT CatalogDescription.query('  
     declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     for $F in /PD:ProductDescription/PD:Picture[PD:Size="small"   
                                                 and PD:Angle="front"]  
     return   
         $F   
    ') as Result  
FROM  Production.ProductModel  
where ProductModelID=19  
```  
  
 El resultado es el siguiente:  
  
```  
<PD:Picture   
  xmlns:PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
  <PD:Angle>front</PD:Angle>  
  <PD:Size>small</PD:Size>  
  <PD:ProductPhotoID>31</PD:ProductPhotoID>  
</PD:Picture>  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Expresiones XQuery](../xquery/xquery-expressions.md)  
  
  
