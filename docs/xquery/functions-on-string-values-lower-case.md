---
title: "Función de letra minúscula (XQuery) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/09/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- lower-case Function (XQuery)
- lower-case
ms.assetid: 5222c4ff-890c-4d57-8506-c065a5ebfd3e
caps.latest.revision: "11"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 8503ca4813259e22a2d9f77b583d56b63fb67461
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="functions-on-string-values---lower-case"></a>Funciones en valores de cadena - minúsculas
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  La función de letra minúscula convierte cada carácter de *$arg* a su minúsculas equivalente. La conversión de grafía binaria de Microsoft Windows para los puntos de código Unicode especifica cómo se convierten los caracteres a letra minúscula. Esta norma no es idéntica a la asignación para la norma de punto de código Unicode.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn:lower-case($arg as xs:string?) as xs:string  
```  
  
## <a name="arguments"></a>Argumentos  
  
|||  
|-|-|  
|Término|Definición|  
|*$arg*|Valor de cadena que se va a convertir a letra minúscula.|  
  
## <a name="remarks"></a>Comentarios  
 Si el valor de *$arg* está vacía, se devuelve una cadena de longitud cero.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-changing-a-string-to-upper-case"></a>A. Cambiar una cadena a letra mayúscula  
 En el ejemplo siguiente se cambia la cadena de entrada ' abcDEF! @4' a minúsculas.  
  
```  
DECLARE @x xml = N'abcDEF!@4';  
SELECT @x.value('fn:lower-case(/text()[1])', 'nvarchar(10)');  
```  
  
 [!INCLUDE[ssResult](../includes/ssresult-md.md)]  
  
 `abcdef!@4`  
  
### <a name="b-search-for-a-specific-character-string"></a>B. Buscar una cadena de caracteres específica  
 En este ejemplo se muestra cómo utilizar la función de letra minúscula para realizar una búsqueda sin distinción entre mayúsculas y minúsculas.  
  
```  
USE AdventureWorks  
GO  
--WITH XMLNAMESPACES clause specifies the namespace prefix  
--to use.   
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
--The XQuery contains() function is used to determine whether  
--any of the text nodes below the <Summary> element contain  
--the word 'frame'. The lower-case() function makes the   
--case insensitive.  
  
SELECT ProductModelID, CatalogDescription.query('  
      <Prod>  
         { /pd:ProductDescription/@ProductModelID }  
         { /pd:ProductDescription/pd:Summary }  
      </Prod>  
 ') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
/pd:ProductDescription/pd:Summary//text()[  
          contains(lower-case(.), "FRAME")]')  = 1  
```  
  
 [!INCLUDE[ssResult](../includes/ssresult-md.md)]  
  
 `ProductModelID Result`  
  
 `-------------- ---------`  
  
 `19     <Prod ProductModelID="19">`  
  
 `<pd:Summary xmlns:pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">`  
  
 `<p1:p xmlns:p1="http://www.w3.org/1999/xhtml">Our top-of-the-line competition mountain bike.`  
  
 `Performance-enhancing options include the innovative HL Frame,`  
  
 `super-smooth front suspension, and traction for all terrain.`  
  
 `</p1:p>`  
  
 `</pd:Summary>`  
  
 `</Prod>`  
  
 `25     <Prod ProductModelID="25">`  
  
 `<pd:Summary xmlns:pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription">`  
  
 `<p1:p xmlns:p1="http://www.w3.org/1999/xhtml">This bike is ridden by race winners. Developed with the`  
  
 `Adventure Works Cycles professional race team, it has a extremely light`  
  
 `heat-treated aluminum frame, and steering that allows precision control.`  
  
 `</p1:p>`  
  
 `</pd:Summary>`  
  
 `</Prod>`  
  
## <a name="see-also"></a>Vea también  
 [Funciones de XQuery con el tipo de datos xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
