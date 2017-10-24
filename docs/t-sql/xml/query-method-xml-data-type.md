---
title: "Método Query() (tipo de datos xml) | Documentos de Microsoft"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- query method
- query() method
ms.assetid: f48f6f7b-219f-463a-bf36-bc10f21afaeb
caps.latest.revision: 28
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Active
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: db0f9b1ffc4c6ca13084942144e13d64765d7019
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="query-method-xml-data-type"></a>query() (método de tipo de datos xml)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Especifica una expresión XQuery para una instancia de la **xml** tipo de datos. El resultado es de **xml** tipo. El método devuelve una instancia XML sin tipo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
query ('XQuery')  
```  
  
## <a name="arguments"></a>Argumentos  
 XQuery  
 Es una cadena, una expresión XQuery, que consulta nodos XML como, por ejemplo, elementos y atributos, en una instancia XML.  
  
## <a name="examples"></a>Ejemplos  
 Esta sección proporciona ejemplos de cómo utilizar el método query() de la **xml** tipo de datos.  
  
### <a name="a-using-the-query-method-against-an-xml-type-variable"></a>A. Usar el método query() con una variable de tipo xml  
 En el ejemplo siguiente se declara una variable  **@myDoc**  de **xml** escriba y le asigna una instancia XML. El **query()** método, a continuación, se utiliza para especificar una XQuery en el documento.  
  
 La consulta recupera el elemento secundario <`Features`> del elemento <`ProductDescription`>:  
  
```  
declare @myDoc xml  
set @myDoc = '<Root>  
<ProductDescription ProductID="1" ProductName="Road Bike">  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>  
</ProductDescription>  
</Root>'  
SELECT @myDoc.query('/Root/ProductDescription/Features')  
```  
  
 El resultado es el siguiente:  
  
```  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>        
```  
  
### <a name="b-using-the-query-method-against-an-xml-type-column"></a>B. Usar el método query() con una columna de tipo XML  
 En el ejemplo siguiente, la **query()** método se usa para especificar una XQuery en el **CatalogDescription** columna de **xml** escriba en el  **AdventureWorks** base de datos:  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
<Product ProductModelID="{ /PD:ProductDescription[1]/@ProductModelID }" />  
') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
     /PD:ProductDescription/PD:Features/wm:Warranty ') = 1  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   La columna CatalogDescription es un tipo **xml** columna. Esto quiere decir que tiene asociada una colección de esquemas. En el [prólogo de XQuery](../../xquery/modules-and-prologs-xquery-prolog.md), **espacio de nombres** palabra clave se utiliza para definir el prefijo que se utiliza posteriormente en el cuerpo de la consulta.  
  
-   El **query()** método construye XML, un <`Product`> elemento que tiene un **ProductModelID** atributo, en el que el **ProductModelID** es el valor de atributo recuperar de la base de datos. Para obtener más información acerca de la construcción de XML, vea [construcción XML &#40; XQuery &#41; ](../../xquery/xml-construction-xquery.md).  
  
-   El [método exist() (tipo de datos XML)](../../t-sql/xml/exist-method-xml-data-type.md) en la cláusula WHERE se utiliza para buscar únicamente las filas que contiene la <`Warranty`> elemento en el XML. Una vez más, la **espacio de nombres** palabra clave se utiliza para definir dos prefijos de espacio de nombres.  
  
 Éste es el resultado parcial:  
  
```  
<Product ProductModelID="19"/>   
<Product ProductModelID="23"/>   
...  
```  
  
 Observe que ambos métodos, query() y exist(), declaran el prefijo PD. En estos casos, puede utilizar WITH XMLNAMESPACES para definir los prefijos en primer lugar y utilizarlo en la consulta.  
  
```  
WITH XMLNAMESPACES (  
   'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD,  
   'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS wm)  
SELECT CatalogDescription.query('  
<Product ProductModelID="{ /PD:ProductDescription[1]/@ProductModelID }" />  
') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
     /PD:ProductDescription/PD:Features/wm:Warranty ') = 1  
```  
  
## <a name="see-also"></a>Vea también  
 [Agregar espacios de nombres a consultas con WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [Comparar XML con tipo y XML sin tipo](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Crear instancias de datos XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [métodos del tipo de datos xml](../../t-sql/xml/xml-data-type-methods.md)   
 [Lenguaje de manipulación de datos XML &#40; XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  

