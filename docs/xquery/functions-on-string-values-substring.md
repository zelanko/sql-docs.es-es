---
title: substring (función de XQuery) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- substring function [XQuery]
- fn:substring function
ms.assetid: 2b3b8651-de51-46dc-af82-c86c45eac871
author: rothja
ms.author: jroth
ms.openlocfilehash: 2188cff20411fe90d4858763f65cff7f6fe9c9d1
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68004645"
---
# <a name="functions-on-string-values---substring"></a>Funciones usadas en valores de cadena: substring
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve la parte del valor de *$sourceString*, empezando en la posición indicada por el valor de *$startingLoc,* y continúa durante el número de caracteres indicado por el valor de *$ longitud*.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn:substring($sourceString as xs:string?,  
                          $startingLoc as xs:decimal?) as xs:string?  
  
fn:substring($sourceString as xs:string?,  
                          $startingLoc as xs:decimal?,  
                          $length as xs:decimal?) as xs:string?  
```  
  
## <a name="arguments"></a>Argumentos  
 *$sourceString*  
 Cadena de origen.  
  
 *$startingLoc*  
 Punto inicial de la cadena de origen donde comienza la subcadena. Si este valor es negativo o es 0, solo se devuelven los caracteres en posiciones mayores que cero. Si es mayor que la longitud de la *$sourceString*, se devuelve la cadena de longitud cero.  
  
 *$length*  
 [opcional] Número de caracteres que se va a recuperar. Si no se especifica, devuelve todos los caracteres desde la ubicación especificada en *$startingLoc* hasta el final de cadena.  
  
## <a name="remarks"></a>Comentarios  
 La versión de la función con tres argumentos devuelve los caracteres de `$sourceString` cuya posición `$p` sea:  
  
 `fn:round($startingLoc) <= $p < fn:round($startingLoc) + fn:round($length)`  
  
 El valor de *$length* puede ser mayor que el número de caracteres en el valor de *$sourceString* la posición inicial. En este caso, la subcadena devuelve los caracteres hasta el final de *$sourceString*.  
  
 El primer carácter de una cadena se encuentra en la posición 1.  
  
 Si el valor de *$sourceString* es una secuencia vacía, se trata como la cadena de longitud cero. En caso contrario, si bien *$startingLoc* o *$length* es una secuencia vacía, se devuelve una secuencia vacía.  
  
## <a name="supplementary-characters-surrogate-pairs"></a>Caracteres adicionales (pares suplentes)  
 El comportamiento de pares suplentes en las funciones XQuery depende del nivel de compatibilidad de la base de datos y, en algunos casos, del URI del espacio de nombres predeterminado de las funciones. Para obtener más información, vea la sección "XQuery funciones detectan los caracteres suplentes" en el tema [cambios recientes en las características del motor de base de datos en SQL Server 2016](../database-engine/breaking-changes-to-database-engine-features-in-sql-server-2016.md). Consulte también [nivel de compatibilidad de ALTER DATABASE &#40;Transact-SQL&#41; ](../t-sql/statements/alter-database-transact-sql-compatibility-level.md) y [Collation and Unicode Support](../relational-databases/collations/collation-and-unicode-support.md).  
  
## <a name="implementation-limitations"></a>Limitaciones de la implementación  
 SQL Server requiere el *$startingLoc* y *$length parámetros* sea de tipo xs: decimal en lugar de xs: Double.  
  
 SQL Server permite *$startingLoc* y *$length* sean una secuencia vacía, porque la secuencia vacía es un valor posible debido a errores dinámicos se asignan a ().  
  
## <a name="examples"></a>Ejemplos  
 En este tema se proporciona ejemplos de XQuery con instancias XML almacenadas en varias **xml** escriba columnas en el [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] base de datos.  
  
### <a name="a-using-the-substring-xquery-function-to-retrieve-partial-summary-product-model-descriptions"></a>A. Utilizar la función substring() de XQuery para recuperar descripciones resumidas parciales de modelos de productos  
 La consulta recupera los 50 primeros caracteres del texto que describe el modelo de producto, el <`Summary`> elemento del documento.  
  
```  
WITH XMLNAMESPACES ('https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Prod>{ substring(string((/pd:ProductDescription/pd:Summary)[1]), 1, 50) }</Prod>  
 ') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('/pd:ProductDescription')  = 1;  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   El **string()** función devuelve el valor de cadena de la <`Summary`> elemento. Esta función se usa, porque el <`Summary`> elemento contiene el texto y los subelementos (elementos de formato html), y dado que se omitirán estos elementos y recuperar todo el texto.  
  
-   El **substring()** función recupera los 50 primeros caracteres del valor de cadena recuperado por el **string()** .  
  
 Éste es un resultado parcial:  
  
```  
ProductModelID Result  
-------------- ----------------------------------------------------  
19      <Prod>Our top-of-the-line competition mountain bike.</Prod>   
23      <Prod>Suitable for any type of riding, on or off-roa</Prod>  
...  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de XQuery con el tipo de datos xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
