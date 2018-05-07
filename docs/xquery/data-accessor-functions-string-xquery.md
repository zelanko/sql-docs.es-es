---
title: cadena (función de XQuery) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/09/2017
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
- string function
- fn:string function
ms.assetid: 7baa2959-9340-429b-ad53-3df03d8e13fc
caps.latest.revision: 27
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c20973cdaa3b3d80124a9713a104d7294d6c20f2
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="data-accessor-functions---string-xquery"></a>Funciones de descriptor de acceso de datos: cadena (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve el valor de *$arg* representado como una cadena.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn:string() as xs:string  
fn:string($arg as item()?) as xs:string  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Es un nodo o un valor atómico.  
  
## <a name="remarks"></a>Comentarios  
  
-   Si *$arg* es una secuencia vacía, se devuelve la cadena de longitud cero.  
  
-   Si *$arg* es un nodo, la función devuelve el valor de cadena del nodo que se obtiene con el descriptor de acceso de valor de cadena. Esto está definido en la especificación del modelo de datos de W3C XQuery 1.0 y XPath 2.0.  
  
-   Si *$arg* es un valor atómico, la función devuelve la misma cadena que se devuelve la expresión asignada como **xs: String**, *$arg*, excepto cuando se indique lo contrario.  
  
-   Si el tipo de *$arg* es **xs: anyURI**, el URI se convierte en una cadena sin escape de caracteres especiales.  
  
-   En esta implementación, **fn:String()** sin un argumento solo se puede utilizar en el contexto de un predicado dependiente del contexto. En concreto, solo se puede utilizar entre corchetes ([ ]).  
  
## <a name="examples"></a>Ejemplos  
 Este tema ofrecen ejemplos de XQuery con instancias XML almacenadas en varias **xml** columnas de tipo en la base de datos de AdventureWorks.  
  
### <a name="a-using-the-string-function"></a>A. Usar la función string  
 La consulta siguiente recupera el nodo de elemento secundario <`Features`> del elemento <`ProductDescription`>.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
 /PD:ProductDescription/PD:Features  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 Éste es el resultado parcial:  
  
```  
<PD:Features xmlns:PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">  
   These are the product highlights.   
   <p1:Warranty xmlns:p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain">  
    <p1:WarrantyPeriod>3 years</p1:WarrantyPeriod>  
    <p1:Description>parts and labor</p1:Description>  
   </p1:Warranty>  
       ...  
</PD:Features>  
```  
  
 Si especifica la **string()** función, recibirá el valor de cadena del nodo especificado.  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
 string(/PD:ProductDescription[1]/PD:Features[1])  
')  
FROM Production.ProductModel  
WHERE ProductModelID=19  
```  
  
 El resultado parcial es el siguiente.  
  
```  
These are the product highlights.   
3 yearsparts and labor...    
```  
  
### <a name="b-using-the-string-function-on-various-nodes"></a>B. Usar la función string en varios nodos  
 En el ejemplo siguiente, se asigna una instancia XML a una variable de tipo xml. Las consultas se especifican para mostrar el resultado de aplicar **string()** a varios nodos.  
  
```  
declare @x xml  
set @x = '<?xml version="1.0" encoding="UTF-8" ?>  
<!--  This is a comment -->  
<root>  
  <a>10</a>  
just text  
  <b attr="x">20</b>  
</root>  
'  
```  
  
 La consulta siguiente recupera el valor de cadena del nodo de documento. Este valor se forma concatenando el valor de cadena de todos sus nodos de texto descendientes.  
  
```  
select @x.query('string(/)')  
```  
  
 El resultado es el siguiente:  
  
```  
This is a comment 10  
just text  
 20  
```  
  
 La consulta siguiente intenta recuperar el valor de cadena de un nodo de instrucción de procesamiento. El resultado es una secuencia vacía, porque no contiene un nodo de texto.  
  
```  
select @x.query('string(/processing-instruction()[1])')  
```  
  
 La consulta siguiente recupera el valor de cadena del nodo de comentario y devuelve el nodo de texto.  
  
```  
select @x.query('string(/comment()[1])')  
```  
  
 El resultado es el siguiente:  
  
```  
This is a comment   
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de XQuery con el tipo de datos xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
