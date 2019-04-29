---
title: Función local-name (XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- fn:local-name function
- local-name function
ms.assetid: c901ef5d-89c5-482a-bf64-3eefbcf3098d
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 93f289ed165742ae8fdf8d49732186161a4a8b5d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62936542"
---
# <a name="functions-on-nodes---local-name"></a>Funciones usadas en nodos: local-name
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve la parte local del nombre de *$arg* como xs: String que será la cadena de longitud cero o tendrá la forma léxica de un xs: NCName. Si no se proporciona el argumento, el valor predeterminado será el nodo de contexto.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
fn:local-name() as xs:string  
fn:local-name($arg as node()?) as xs:string  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Nombre del nodo cuya parte de nombre local se recuperará.  
  
## <a name="remarks"></a>Comentarios  
  
-   En SQL Server, **fn:local-name()** sin un argumento solo se puede utilizar en el contexto de un predicado dependiente del contexto. En concreto, solo se puede utilizar entre corchetes (`[ ]`).  
  
-   Si se proporciona el argumento y es la secuencia vacía, la función devolverá la cadena de longitud cero.  
  
-   Si el nodo de destino no tiene nombre porque es un nodo de documento, un comentario o un nodo de texto, la función devolverá la cadena de longitud cero.  
  
## <a name="examples"></a>Ejemplos  
 En este tema se proporciona ejemplos de XQuery con instancias XML almacenadas en varias **xml** columnas de tipo en la base de datos AdventureWorks.  
  
### <a name="a-retrieve-local-name-of-a-specific-node"></a>A. Recuperar el nombre local de un nodo específico  
 La consulta siguiente se especifica en una instancia XML sin tipo. La expresión de consulta, `local-name(/ROOT[1])`, recupera la parte de nombre local del nodo especificado.  
  
```  
declare @x xml  
set @x='<ROOT><a>111</a></ROOT>'  
SELECT @x.query('local-name(/ROOT[1])')  
-- result = ROOT  
```  
  
 La consulta siguiente se especifica en la columna Instructions, una columna xml con tipo, de la tabla ProductModel. La expresión, `local-name(/AWMI:root[1]/AWMI:Location[1])`, devuelve el nombre local, `Location`, del nodo especificado.  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
     local-name(/AWMI:root[1]/AWMI:Location[1])') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
-- result = Location  
```  
  
### <a name="b-using-local-name-without-argument-in-a-predicate"></a>b. Usar local-name sin argumento en un predicado  
 La siguiente consulta se especifica en la columna Instructions, escribió **xml** columna de la tabla ProductModel. La expresión devuelve todos los elementos secundarios de la <`root`> cuya parte del nombre local de QName es "Location" del elemento. El **local-name()** función se especifica en el predicado y no tiene ningún argumento de la función usa el nodo de contexto.  
  
```  
SELECT Instructions.query('  
declare namespace AWMI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" ;  
  /AWMI:root//*[local-name() = "Location"]') as Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 La consulta devuelve todos los <`Location`> elementos secundarios de la <`root`> elemento.  
  
## <a name="see-also"></a>Vea también  
 [Funciones usadas en nodos](https://msdn.microsoft.com/library/09a8affa-3341-4f50-aebc-fdf529e00c08)   
 [Función namespace-uri &#40;XQuery&#41;](../xquery/functions-on-nodes-namespace-uri.md)  
  
  
