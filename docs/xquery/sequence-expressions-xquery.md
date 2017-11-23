---
title: Secuencia de expresiones (XQuery) | Documentos de Microsoft
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: XML
helpviewer_keywords:
- sequence [XQuery]
- expressions [XQuery], sequence
- filtering sequences [XQuery]
ms.assetid: 41e18b20-526b-45d2-9bd9-e3b7d7fbce4e
caps.latest.revision: "22"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fff2568f6793efe8c21d6d37dd92851fe9bece89
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="sequence-expressions-xquery"></a>Expresiones de secuencias (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] admite los operadores XQuery que se utilizan para generar, filtrar y combinar una secuencia de elementos. Un elemento puede ser un nodo o un valor atómico.  
  
## <a name="constructing-sequences"></a>Generar secuencias  
 El operador de comas se puede utilizar para generar una secuencia que concatene los elementos en una única secuencia.  
  
 Una secuencia puede contener valores duplicados. Las secuencias anidadas (una secuencia dentro de otra) se contraen. Por ejemplo, la secuencia (1, 2, (3, 4, (5))) pasa a ser (1, 2, 3, 4, 5). A continuación, se ofrecen ejemplos de cómo se generan secuencias.  
  
### <a name="example-a"></a>Ejemplo A  
 La consulta siguiente devuelve una secuencia de cinco valores atómicos:  
  
```  
declare @x xml  
set @x=''  
select @x.query('(1,2,3,4,5)')  
go  
-- result 1 2 3 4 5  
```  
  
 La consulta siguiente devuelve una secuencia de dos nodos:  
  
```  
-- sequence of 2 nodes  
declare @x xml  
set @x=''  
select @x.query('(<a/>, <b/>)')  
go  
-- result  
<a />  
<b />  
```  
  
 La consulta siguiente devuelve un error, porque se pretende generar una secuencia de valores atómicos y nodos. Esta es una secuencia heterogénea y no se admite.  
  
```  
declare @x xml  
set @x=''  
select @x.query('(1, 2, <a/>, <b/>)')  
go  
```  
  
### <a name="example-b"></a>Ejemplo B  
 La consulta siguiente genera una secuencia de valores atómicos mediante la combinación de cuatro secuencias de distinta longitud en una única secuencia.  
  
```  
declare @x xml  
set @x=''  
select @x.query('(1,2),10,(),(4, 5, 6)')  
go  
-- result = 1 2 10 4 5 6  
```  
  
 La secuencia se puede ordenar mediante FLOWR y ORDER BY:  
  
```  
declare @x xml  
set @x=''  
select @x.query('for $i in ((1,2),10,(),(4, 5, 6))  
                  order by $i  
                  return $i')  
go  
```  
  
 Se pueden contar los elementos de la secuencia mediante el **fn:Count()** función.  
  
```  
declare @x xml  
set @x=''  
select @x.query('count( (1,2,3,(),4) )')  
go  
-- result = 4  
```  
  
### <a name="example-c"></a>Ejemplo C  
 La siguiente consulta se especifica en la columna AdditionalContactInfo de la **xml** tipo en la tabla Contact. Esta columna almacena información de contacto adicional, como uno o más números de teléfono adicionales, números de buscapersonas y direcciones. El \<telephoneNumber >, \<buscapersonas >, y otros nodos pueden aparecer en cualquier lugar en el documento. La consulta genera una secuencia que contiene todos los \<telephoneNumber > elementos secundarios del nodo de contexto, seguido por el \<buscapersonas > elementos secundarios. Observe el uso del operador de comas de la secuencia en la expresión devuelta, `($a//act:telephoneNumber, $a//act:pager)`.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS act,  
 'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS aci)  
  
SELECT AdditionalContactInfo.query('  
   for $a in /aci:AdditionalContactInfo   
   return ($a//act:telephoneNumber, $a//act:pager)  
') As Result  
FROM Person.Contact  
WHERE ContactID=3  
```  
  
 El resultado es el siguiente:  
  
```  
<act:telephoneNumber xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3333</act:number>  
</act:telephoneNumber>  
<act:telephoneNumber xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>333-333-3334</act:number>  
</act:telephoneNumber>  
<act:pager xmlns:act="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes">  
  <act:number>999-555-1244</act:number>  
  <act:SpecialInstructions>  
Page only in case of emergencies.  
</act:SpecialInstructions>  
</act:pager>  
```  
  
## <a name="filtering-sequences"></a>Filtrar secuencias  
 Es posible filtrar la secuencia devuelta por una expresión si se agrega un predicado a la expresión. Para obtener más información, vea [expresiones de ruta de acceso &#40; XQuery &#41; ](../xquery/path-expressions-xquery.md). Por ejemplo, la consulta siguiente devuelve una secuencia de tres nodos de elemento <`a`>:  
  
```  
declare @x xml  
set @x = '<root>  
<a attrA="1">111</a>  
<a></a>  
<a></a>  
</root>'  
SELECT @x.query('/root/a')  
```  
  
 El resultado es el siguiente:  
  
```  
<a attrA="1">111</a>  
<a />  
<a />  
```  
  
 Para recuperar solo los elementos <`a`> que tengan el atributo attrA, se puede especificar un filtro en el predicado. La secuencia resultante tendrá un único elemento <`a`>.  
  
```  
declare @x xml  
set @x = '<root>  
<a attrA="1">111</a>  
<a></a>  
<a></a>  
</root>'  
SELECT @x.query('/root/a[@attrA]')  
```  
  
 El resultado es el siguiente:  
  
```  
<a attrA="1">111</a>  
```  
  
 Para obtener más información sobre cómo especificar predicados en una expresión de ruta de acceso, consulte [especificar predicados en un paso de expresión de ruta de acceso](../xquery/path-expressions-specifying-predicates.md).  
  
 En el ejemplo siguiente se genera una expresión de secuencia de subárboles y, después, se aplica un filtro al flujo.  
  
```  
declare @x xml  
set @x = '  
<a>  
  <c>C under a</c>  
</a>  
<b>    
   <c>C under b</c>  
</b>  
<c>top level c</c>  
<d></d>  
'  
```  
  
 La expresión de `(/a, /b)` genera una secuencia con los subárboles `/a` y `/b`, y, en la secuencia resultante, la expresión filtra el elemento `<c>`.  
  
```  
SELECT @x.query('  
  (/a, /b)/c  
')  
```  
  
 El resultado es el siguiente:  
  
```  
<c>C under a</c>  
<c>C under b</c>  
```  
  
 En el ejemplo siguiente se aplica un filtro de predicado. La expresión busca los elementos <`a`> y <`b`> que contienen el elemento <`c`>.  
  
```  
declare @x xml  
set @x = '  
<a>  
  <c>C under a</c>  
</a>  
<b>    
   <c>C under b</c>  
</b>  
  
<c>top level c</c>  
<d></d>  
'  
SELECT @x.query('  
  (/a, /b)[c]  
')  
```  
  
 El resultado es el siguiente:  
  
```  
<a>  
  <c>C under a</c>  
</a>  
<b>  
  <c>C under b</c>  
</b>  
```  
  
### <a name="implementation-limitations"></a>Limitaciones de la implementación  
 Éstas son las limitaciones:  
  
-   No se admiten las expresiones de rango XQuery.  
  
-   Las secuencias deben ser homogéneas. Concretamente, todos los elementos de una secuencia deben ser nodos o valores atómicos. Esto se comprueba de forma estática.  
  
-   No se admite la combinación de secuencias de nodos por medio del operador UNION, INTERSECT o EXCEPT.  
  
## <a name="see-also"></a>Vea también  
 [Expresiones XQuery](../xquery/xquery-expressions.md)  
  
  
