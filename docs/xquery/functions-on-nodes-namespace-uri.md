---
title: Función namespace-uri (XQuery) | Documentos de Microsoft
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- fn:namespace-uri function
- namespace-uri function
ms.assetid: 9b48d216-26c8-431d-9ab4-20ab187917f4
caps.latest.revision: 14
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 0107819414ce52418b369401feecff73441b63bd
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="functions-on-nodes---namespace-uri"></a>Funciones en nodos - uri de espacio de nombres
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el espacio de nombres URI del QName especificado en *$arg* como xs: String.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
fn:namespace-uri() as xs:string  
fn:namespace-uri($arg as node()?) as xs:string  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Nombre del nodo cuya parte del URI del espacio de nombres se va a recuperar.  
  
## <a name="remarks"></a>Comentarios  
  
-   Si se omite este argumento, el valor predeterminado es el nodo del contexto.  
  
-   En SQL Server, **fn:namespace-URI()** sin un argumento solo se puede utilizar en el contexto de un predicado dependiente del contexto. En concreto, solo se puede utilizar entre corchetes ([ ]).  
  
-   Si *$arg* es una secuencia vacía, se devuelve la cadena de longitud cero.  
  
-   Si *$arg* es un elemento o nodo de atributo cuyo QName expandido no está en un espacio de nombres, la función devuelve la cadena de longitud cero  
  
## <a name="examples"></a>Ejemplos  
 En este tema se ofrece ejemplos de XQuery con instancias XML almacenadas en varias **xml** columnas de tipo en la base de datos de AdventureWorks.  
  
### <a name="a-retrieve-namespace-uri-of-a-specific-node"></a>A. Recuperar el URI de espacio de nombres de un nodo específico  
 La consulta siguiente se especifica en una instancia XML sin tipo. La expresión de la consulta, `namespace-uri(/ROOT[1])`, recupera la parte del URI del espacio de nombres del nodo especificado.  
  
```  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('namespace-uri(/ROOT[1])')  
```  
  
 Dado que el QName especificado no tiene la parte del URI del espacio de nombres sino únicamente la parte del nombre local, el resultado es una cadena de longitud cero.  
  
 La siguiente consulta se especifica en las instrucciones que se ha escrito **xml** columna. La expresión `namespace-uri(/AWMI:root[1]/AWMI:Location[1])` devuelve el URI del espacio de nombres del primer elemento secundario <`Location`> del elemento <`root`>.  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     namespace-uri(/AWMI:root[1]/AWMI:Location[1])') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 El resultado es el siguiente:  
  
```  
http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions  
```  
  
### <a name="b-using-namespace-uri-without-argument-in-a-predicate"></a>B. Usar namespace-uri() sin argumento en un predicado  
 La siguiente consulta se especifica para la columna xml con tipo CatalogDescription. La expresión devuelve todos los nodos de elementos cuyo URI del espacio de nombres es `http://www.adventure-works.com/schemas/OtherFeatures`. El espacio de nombres -**uri()** se especifica sin un argumento de función y usa el nodo de contexto.  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
   /p1:ProductDescription//*[namespace-uri() = "http://www.adventure-works.com/schemas/OtherFeatures"]  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Éste es el resultado parcial:  
  
```  
<p1:wheel xmlns:p1="http://www.adventure-works.com/schemas/OtherFeatures">High performance wheels.</p1:wheel>  
<p2:saddle xmlns:p2="http://www.adventure-works.com/schemas/OtherFeatures">  
  <p3:i xmlns:p3="http://www.w3.org/1999/xhtml">Anatomic design</p3:i> and made from durable leather for a full-day of riding in comfort.</p2:saddle>  
…  
```  
  
 Puede cambiar el URI del espacio de nombres de la consulta anterior por `http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain`. En este caso, recibirá todos los elementos secundarios del nodo del elemento <`ProductDescription`> cuya parte del URI del espacio de nombres del QName expandido es `http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain`.  
  
### <a name="implementation-limitations"></a>Limitaciones de la implementación  
 Éstas son las limitaciones:  
  
-   El **espacio** función devuelve instancias de tipo xs: String en lugar de xs: anyURI.  
  
## <a name="see-also"></a>Vea también  
 [Funciones en nodos](http://msdn.microsoft.com/library/09a8affa-3341-4f50-aebc-fdf529e00c08)   
 [Función local-name &#40;XQuery&#41;](../xquery/functions-on-nodes-local-name.md)  
  
  
