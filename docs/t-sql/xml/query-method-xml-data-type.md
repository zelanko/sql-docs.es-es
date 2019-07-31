---
title: query() (método del tipo de datos xml) | Microsoft Docs
ms.custom: ''
ms.date: 07/26/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- query method
- query() method
ms.assetid: f48f6f7b-219f-463a-bf36-bc10f21afaeb
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1d510ad8d52aedb46cf591712467c22c0929c42e
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68051260"
---
# <a name="query-method-xml-data-type"></a>query() (método de tipo de datos xml)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

Especifica una expresión XQuery en una instancia del tipo de datos **xml**. El resultado es de tipo **xml**. El método devuelve una instancia XML sin tipo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
query ('XQuery')  
```  
  
## <a name="arguments"></a>Argumentos  
XQuery  
Es una cadena, una expresión XQuery, que consulta nodos XML como, por ejemplo, elementos y atributos, en una instancia XML.  
  
## <a name="examples"></a>Ejemplos  
En esta sección se muestran ejemplos de cómo usar el método query() del tipo de datos **xml**.  
  
### <a name="a-using-the-query-method-against-an-xml-type-variable"></a>A. Usar el método query() con una variable de tipo xml  
El ejemplo siguiente declara una variable **@myDoc** de tipo **xml** y le asigna una instancia XML. Luego se usa el método **query()** para especificar una expresión XQuery en el documento.  
  
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
  
La siguiente salida muestra el resultado:  
  
```  
<Features>  
  <Warranty>1 year parts and labor</Warranty>  
  <Maintenance>3 year parts and labor extended maintenance is available</Maintenance>  
</Features>        
```  
  
### <a name="b-using-the-query-method-against-an-xml-type-column"></a>B. Usar el método query() con una columna de tipo XML  
En el ejemplo siguiente, el método **query()** se usa para especificar una expresión XQuery en la columna **CatalogDescription** de tipo **xml** de la base de datos **AdventureWorks**:  
  
```  
SELECT CatalogDescription.query('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
<Product ProductModelID="{ /PD:ProductDescription[1]/@ProductModelID }" />  
') as Result  
FROM Production.ProductModel  
where CatalogDescription.exist('  
declare namespace PD="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
declare namespace wm="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain";  
     /PD:ProductDescription/PD:Features/wm:Warranty ') = 1  
```  
  
Observe los siguientes elementos en la consulta anterior:  
  
-   CatalogDescription es una columna **xml** con tipo, lo que significa que tiene una colección de esquemas asociada con ella. En el [Prólogo de XQuery](../../xquery/modules-and-prologs-xquery-prolog.md), la palabra clave **namespace** define el prefijo que se va a usar posteriormente en el cuerpo de la consulta.  
  
-   El método **query()** crea XML, un elemento <`Product`> que tiene un atributo **ProductModelID**, en el que el valor de atributo **ProductModelID** se recupera a partir de la base de datos. Para obtener más información sobre la creación de XML, vea [Construcción de XML &#40;XQuery&#41;](../../xquery/xml-construction-xquery.md).  
  
-   El método [exist() (tipo de datos XML)](../../t-sql/xml/exist-method-xml-data-type.md) de la cláusula WHERE busca únicamente filas que contienen el elemento <`Warranty`> en el XML. La palabra clave **namespace** define de nuevo dos prefijos de espacio de nombres.  
  
La siguiente salida muestra el resultado parcial:  
  
```  
<Product ProductModelID="19"/>   
<Product ProductModelID="23"/>   
...  
```  
  
Observe que ambos métodos, query() y exist(), declaran el prefijo PD. En estos casos, puede utilizar WITH XMLNAMESPACES para definir los prefijos en primer lugar y utilizarlo en la consulta.  
  
```  
WITH XMLNAMESPACES 
(  
   'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS PD,  
   'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelWarrAndMain' AS WM
)  
SELECT CatalogDescription.query('<Product ProductModelID="{ /PD:ProductDescription[1]/@ProductModelID }" />')
       AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('/PD:ProductDescription/PD:Features/WM:Warranty ') = 1;

```  
  
## <a name="see-also"></a>Consulte también  
 [Agregar espacios de nombres a consultas con WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [Comparar XML con tipo y XML sin tipo](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Crear instancias de datos XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [métodos del tipo de datos xml](../../t-sql/xml/xml-data-type-methods.md)   
 [Lenguaje de manipulación de datos XML &#40;XML DML&#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
