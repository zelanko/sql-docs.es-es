---
title: "posición (función de XQuery) | Documentos de Microsoft"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: XML
helpviewer_keywords:
- position function
- fn:position function
ms.assetid: f1bab9e4-1715-4c06-9cb0-06c7e0c9c97f
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 287e178fb6b8c0a30ee8af9c014a46a7fa46883f
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="context-functions---position-xquery"></a>Funciones de contexto - posición (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Esta función devuelve un valor entero que indica la posición del elemento de contexto dentro de la secuencia de elementos que se está procesando.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn:position() as xs:integer  
```  
  
## <a name="remarks"></a>Comentarios  
 En [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], **fn:Position()** solo pueden usarse en el contexto de un predicado dependiente del contexto. Concretamente, solo se puede utilizar entre corchetes ([ ]). Las comparaciones con esta función no reducen la cardinalidad durante una inferencia de tipo estático.  
  
## <a name="examples"></a>Ejemplos  
 Este tema ofrecen ejemplos de XQuery con instancias XML almacenadas en varias **xml** escriba columnas en la [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] base de datos.  
  
### <a name="a-using-the-position-xquery-function-to-retrieve-the-first-two-product-features"></a>A. Usar la función position() de XQuery para recuperar las dos primeras características de producto  
 La consulta siguiente recupera las dos primeras características, es decir, los dos primeros elementos secundarios del elemento <`Features`>, a partir de la descripción del catálogo de modelos de productos. Si hay más características, se incorporará un elemento <`there-is-more/`> al resultado.  
  
```  
SELECT CatalogDescription.query('  
     declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     <Product>   
          { /pd:ProductDescription/@ProductModelID }  
          { /pd:ProductDescription/@ProductModelName }   
          {  
            for $f in /pd:ProductDescription/pd:Features/*[position()<=2]  
            return  
            $f   
          }  
          {  
            if (count(/pd:ProductDescription/pd:Features/*) > 2)  
            then <there-is-more/>  
            else ()  
          }   
     </Product>          
') as x  
FROM Production.ProductModel  
WHERE CatalogDescription is not null  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   El **espacio de nombres** palabra clave en el [prólogo de XQuery](../xquery/modules-and-prologs-xquery-prolog.md) define un prefijo de espacio de nombres que se usa en el cuerpo de la consulta.  
  
-   El cuerpo de la consulta genera XML que tiene un \<producto > elemento con **ProductModelID** y **ProductModelName** atributos y tiene características de producto que se devuelven como elementos secundarios.  
  
-   El **position()** función se utiliza en el predicado para determinar la posición de la \<características > elemento secundario de contexto. Si es la primera o segunda característica, se devuelve.  
  
-   La instrucción IF incorpora un \<allí-is-more / > elemento en el resultado si hay más de dos características en el catálogo de productos.  
  
-   Dado que no todos los modelos de producto tienen sus descripciones de catálogo almacenadas en la tabla, la cláusula WHERE descarta las filas para las que CatalogDescriptions es NULL.  
  
 Éste es un resultado parcial:  
  
```  
<Product ProductModelID="19" ProductModelName="Mountain 100">  
  <p1:Warranty xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 year</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
  </p1:Warranty>  
  <p2:Maintenance xmlns:p2="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p2:NoOfYears>10</p2:NoOfYears>  
    <p2:Description>maintenance contact available through your dealer or  
                    any AdventureWorks retail store.</p2:Description>  
  </p2:Maintenance>  
  <there-is-more/>  
</Product>   
…  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de XQuery con el tipo de datos xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
