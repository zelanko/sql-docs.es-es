---
title: "número de función (XQuery) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- number function
- fn:number function
ms.assetid: dff6d19b-765c-4df9-afff-9a0e7be9b91b
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 85882cd83303223917300175059f0905a2d6ad2d
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="functions-on-nodes---number"></a>Funciones en nodos - número
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve el valor numérico del nodo indicado por *$arg*.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn:number() as xs:double?   
fn:number($arg as node()?) as xs:double?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Nodo cuyo valor se devolverá como un número.  
  
## <a name="remarks"></a>Comentarios  
 Si *$arg* no es se especifica, se devuelve el valor numérico del nodo de contexto, convertido en un doble. En SQL Server, **fn:Number()** sin un argumento solo se puede utilizar en el contexto de un predicado dependiente del contexto. En concreto, solo se puede utilizar entre corchetes ([ ]). Por ejemplo, la expresión siguiente devuelve el elemento <`ROOT`>.  
  
```  
declare @x xml  
set @x='<ROOT>111</ROOT>'  
select @x.query('/ROOT[number()=111]')  
```  
  
 Si el valor del nodo no es una representación léxica válida de un tipo simple numérico, tal como se define en **XML Schema Part 2: Datatypes, W3C Recommendation**, la función devuelve una secuencia vacía. No se admiten los valores NaN.  
  
## <a name="examples"></a>Ejemplos  
 En este tema se ofrece ejemplos de XQuery con instancias XML almacenadas en varias **xml** columnas de tipo en la base de datos de AdventureWorks.  
  
### <a name="a-using-the-number-xquery-function-to-retrieve-the-numeric-value-of-an-attribute"></a>A. Usar la función number() de XQuery para recuperar el valor numérico de un atributo  
 La consulta siguiente recupera el valor numérico del atributo de tamaño de lote de la primera ubicación de centro de trabajo del proceso de fabricación del modelo de producto 7.  
  
```  
SELECT ProductModelID, Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     for $i in (//AWMI:root//AWMI:Location)[1]  
     return   
       <Location LocationID="{ ($i/@LocationID) }"   
                   LotSizeA="{  $i/@LotSize }"  
                   LotSizeB="{  number($i/@LotSize) }"  
                   LotSizeC="{ number($i/@LotSize) + 1 }" >  
  
       </Location>  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   El **number()** función no es necesaria, como se muestra en la consulta para la **LotSizeA** atributo. Se trata de una función de XPath 1.0 incluida sobre todo para mantener la compatibilidad con versiones anteriores.  
  
-   La expresión XQuery para **LotSizeB** especifica la función de número y es redundante.  
  
-   La consulta para **LotSizeD** muestra el uso de un valor numérico en una operación aritmética.  
  
 El resultado es el siguiente:  
  
```  
ProductModelID   Result  
----------------------------------------------  
7              <Location LocationID="10"   
                         LotSizeA="100"   
                         LotSizeB="100"   
                         LotSizeC="101" />  
```  
  
### <a name="implementation-limitations"></a>Limitaciones de la implementación  
 Éstas son las limitaciones:  
  
-   El **number()** función solo acepta nodos. No acepta valores atómicos.  
  
-   Cuando no se puede devolver valores como un número, el **number()** función devuelve una secuencia vacía en lugar de NaN.  
  
## <a name="see-also"></a>Vea también  
 [Funciones de XQuery con el tipo de datos xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
