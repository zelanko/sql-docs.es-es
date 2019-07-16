---
title: Función namespace-uri (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:namespace-uri function
- namespace-uri function
ms.assetid: 9b48d216-26c8-431d-9ab4-20ab187917f4
author: rothja
ms.author: jroth
ms.openlocfilehash: 05412c69aa121b9de14f2bab16555db2a8a4fdb4
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67929943"
---
# <a name="functions-on-nodes---namespace-uri"></a>Funciones usadas en nodos: namespace-uri
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el URI del QName especificado en el espacio de nombres *$arg* como xs: String.  
  
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
 En este tema se proporciona ejemplos de XQuery con instancias XML almacenadas en varias **xml** columnas de tipo en la base de datos AdventureWorks.  
  
### <a name="a-retrieve-namespace-uri-of-a-specific-node"></a>A. Recuperar el URI de espacio de nombres de un nodo específico  
 La consulta siguiente se especifica en una instancia XML sin tipo. La expresión de la consulta, `namespace-uri(/ROOT[1])`, recupera la parte del URI del espacio de nombres del nodo especificado.  
  
```  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('namespace-uri(/ROOT[1])')  
```  
  
 Dado que el QName especificado no tiene la parte del URI del espacio de nombres sino únicamente la parte del nombre local, el resultado es una cadena de longitud cero.  
  
 La siguiente consulta se especifica en las instrucciones que se ha escrito **xml** columna. La expresión, `namespace-uri(/AWMI:root[1]/AWMI:Location[1])`, devuelve el espacio de nombres URI de los primeros <`Location`> elemento secundario de la <`root`> elemento.  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     namespace-uri(/AWMI:root[1]/AWMI:Location[1])') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Éste es el resultado:  
  
```  
https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions  
```  
  
### <a name="b-using-namespace-uri-without-argument-in-a-predicate"></a>b. Usar namespace-uri() sin argumento en un predicado  
 La siguiente consulta se especifica para la columna xml con tipo CatalogDescription. La expresión devuelve todos los nodos de elementos cuyo URI del espacio de nombres es `https://www.adventure-works.com/schemas/OtherFeatures`. El espacio de nombres -**uri()** se especifica sin un argumento de función y usa el nodo de contexto.  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
   /p1:ProductDescription//*[namespace-uri() = "https://www.adventure-works.com/schemas/OtherFeatures"]  
') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Éste es el resultado parcial:  
  
```  
<p1:wheel xmlns:p1="https://www.adventure-works.com/schemas/OtherFeatures">High performance wheels.</p1:wheel>  
<p2:saddle xmlns:p2="https://www.adventure-works.com/schemas/OtherFeatures">  
  <p3:i xmlns:p3="http://www.w3.org/1999/xhtml">Anatomic design</p3:i> and made from durable leather for a full-day of riding in comfort.</p2:saddle>  
...  
```  
  
 Puede cambiar el URI del espacio de nombres de la consulta anterior por `https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain`. A continuación, recibirá todos los secundarios del nodo de elemento de la <`ProductDescription`> cuya parte URI de espacio de nombres de QName expandido es el elemento `https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain`.  
  
### <a name="implementation-limitations"></a>Limitaciones de la implementación  
 Éstas son las limitaciones:  
  
-   El **espacio** función devuelve instancias de tipo xs: String en lugar de xs: anyURI.  
  
## <a name="see-also"></a>Vea también  
 [Funciones usadas en nodos](https://msdn.microsoft.com/library/09a8affa-3341-4f50-aebc-fdf529e00c08)   
 [Función local-name &#40;XQuery&#41;](../xquery/functions-on-nodes-local-name.md)  
  
  
