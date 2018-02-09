---
title: "datos (función de XQuery) | Documentos de Microsoft"
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
- fn:data function
- data function [XQuery]
ms.assetid: 511b5d7d-c679-4cb2-a3dd-170cc126f49d
caps.latest.revision: 
author: rothja
ms.author: jroth
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: bc544e5f0c1f735f0a4b174a67416e52efae1da1
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="data-accessor-functions---data-xquery"></a>Funciones de descriptor de acceso de datos - datos (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Devuelve el valor con tipo para cada elemento especificado por *$arg*.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
fn:data ($arg as item()*) as xdt:untypedAtomic*  
```  
  
## <a name="arguments"></a>Argumentos  
 *$arg*  
 Secuencia de elementos cuyos valores con tipo van a devolverse.  
  
## <a name="remarks"></a>Comentarios  
 La siguiente información se aplica a los valores con tipo:  
  
-   El valor con tipo de un valor atómico es el propio valor atómico.  
  
-   El valor con tipo de un nodo de texto es el valor de cadena del nodo de texto.  
  
-   El valor con tipo de un comentario es el valor de cadena del comentario.  
  
-   El valor con tipo de una instrucción de procesamiento es el contenido de la instrucción de procesamiento, sin el nombre de destino de la instrucción de procesamiento.  
  
-   El valor con tipo de un nodo de documento es su valor de cadena.  
  
 La siguiente información se aplica a los nodos de atributo y de elemento:  
  
-   Si un nodo de atributo se escribe con un tipo de esquema XML, su valor con tipo será el valor con tipo en consecuencia.  
  
-   Si el nodo de atributo no tiene tipo, su valor con tipo es igual a su valor de cadena que se devuelve como una instancia de **xdt: untypedAtomic**.  
  
-   Si el nodo de elemento no se ha escrito, su valor con tipo es igual a su valor de cadena que se devuelve como una instancia de **xdt: untypedAtomic**.  
  
 La siguiente información se aplica a los nodos de elemento con tipo:    
  
-   Si el elemento tiene un tipo de contenido simple, **data()** devuelve el valor con tipo del elemento.  
  
-   Si el nodo es de tipo complejo, incluyendo xs: anyType, **data()** devuelve un error estático.  
  
 Aunque el uso de la **data()** función es suele ser opcional, como se muestra en los ejemplos siguientes, especificando el **data()** función explícitamente aumenta la legibilidad de las consultas. Para obtener más información, consulte [conceptos básicos de XQuery](../xquery/xquery-basics.md).  
  
 No se puede especificar **data()** en XML generado, tal y como se muestra en la siguiente:  
  
```  
declare @x xml  
set @x = ''  
select @x.query('data(<SomeNode>value</SomeNode>)')  
```  
  
## <a name="examples"></a>Ejemplos  
 En este tema se ofrece ejemplos de XQuery con instancias XML almacenadas en varias **xml** columnas de tipo en la base de datos de AdventureWorks.  
  
### <a name="a-using-the-data-xquery-function-to-extract-typed-value-of-a-node"></a>A. Utilizar la función data() de XQuery para extraer el valor con tipo de un nodo  
 La consulta siguiente muestra cómo el **data()** función se utiliza para recuperar valores de un atributo, un elemento y un nodo de texto:  
  
```  
WITH XMLNAMESPACES (  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query(N'  
 for $pd in //p1:ProductDescription  
 return   
    <Root   
      ProductID = "{ data( ($pd//@ProductModelID)[1] ) }"   
      Feature =   "{ data( ($pd/p1:Features/wm:Warranty/wm:Description)[1] ) }" >  
    </Root>  
 ') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 El resultado es el siguiente:  
  
```  
<Root ProductID="19" Feature="parts and labor"/>  
```  
  
 Como se mencionó, la **data()** función es opcional cuando se crean atributos. Si no se especifica la **data()** función, se supone de forma implícita. La siguiente consulta genera los mismos resultados que la consulta anterior:  
  
```  
WITH XMLNAMESPACES (  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
      for $pd in //p1:ProductDescription  
         return   
          <Root    
                ProductID = "{ ($pd/@ProductModelID)[1] }"    
                Feature =   "{ ($pd/p1:Features/wm:Warranty/wm:Description)[1] }" >  
           </Root>  
 ') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 Los ejemplos siguientes muestran instancias en las que el **data()** función es necesaria.  
  
 En la siguiente consulta, **$pd / P1: Specifications / Material** devuelve el <`Material`> elemento. Además, **datos ($pd/P1: Specifications/Material)** devuelve datos de tipo carácter de tipo xdt: untypedAtomic, porque <`Material`> no tiene tipo. Cuando la entrada no tiene tipo, el resultado de **data()** se escribe como **xdt: untypedAtomic**.  
  
```  
SELECT CatalogDescription.query('  
declare namespace p1="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
      for $pd in //p1:ProductDescription  
         return   
          <Root>  
             { $pd/p1:Specifications/Material }  
             { data($pd/p1:Specifications/Material) }  
           </Root>  
 ') as Result  
FROM Production.ProductModel  
WHERE ProductModelID = 19  
```  
  
 El resultado es el siguiente:  
  
```  
<Root>  
  <Material>Almuminum Alloy</Material>Almuminum Alloy  
</Root>  
```  
  
 En la siguiente consulta, **data($pd/p1:Features/wm:Warranty)** devuelve un error estático, porque <`Warranty`> es un elemento de tipo complejo.  
  
```  
WITH XMLNAMESPACES (  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS p1,  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
  
SELECT CatalogDescription.query('  
 <Root>  
   {     /p1:ProductDescription/p1:Features/wm:Warranty }  
   { data(/p1:ProductDescription/p1:Features/wm:Warranty) }  
 </Root>  
 ') as Result  
FROM  Production.ProductModel  
WHERE ProductModelID = 23  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de XQuery con el tipo de datos xml](../xquery/xquery-functions-against-the-xml-data-type.md)  
  
  
