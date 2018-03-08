---
title: "exist() (método) (tipo de datos xml) | Documentos de Microsoft"
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- exist() method
- exist method
ms.assetid: a55b75e0-0a17-4787-a525-9b095410f7af
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 74fc65730d0c46858c282b9625c86d1ab651ec49
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="exist-method-xml-data-type"></a>exist() (método del tipo de datos xml)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve un **bits** que representa una de las condiciones siguientes:  
  
-   1, que representa True, si la expresión XQuery de una consulta devuelve un resultado no vacío, es decir, si devuelve al menos un nodo XML.  
  
-   0, que representa False, si devuelve un resultado vacío.  
  
-   NULL si el **xml** instancia del tipo de datos en la que se ejecutó la consulta contiene un valor nulo.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
exist (XQuery)   
```  
  
## <a name="arguments"></a>Argumentos  
 XQuery  
 Es una expresión XQuery, un literal de cadena.  
  
## <a name="remarks"></a>Comentarios  
  
> [!NOTE]  
>  El **exist()** método devuelve 1 para la expresión XQuery que devuelve un resultado no vacío. Si especifica la **true()** o **false()** funciones dentro de la **exist()** método, el **exist()** método devolverá 1, porque el funciones **true()** y **false()** devuelven booleanos True y False, respectivamente. En otras palabras, devuelven un resultado no vacío. Por lo tanto, **exist()** devolverá 1 (verdadero), tal como se muestra en el ejemplo siguiente:  
  
```  
declare @x xml;  
set @x='';  
select @x.exist('true()');   
```  
  
## <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes muestran cómo especificar el **exist()** método.  
  
### <a name="example-specifying-the-exist-method-against-an-xml-type-variable"></a>Ejemplo: especificar el método exist() con una variable de tipo xml  
 En el ejemplo siguiente, @x es un **xml** variable de tipo (xml sin tipo) y @f es una variable de tipo entero que almacena el valor devuelto por la **exist()** método. El **exist()** método devuelve True (1) si el valor de fecha almacenado en la instancia XML es `2002-01-01`.  
  
```  
declare @x xml;  
declare @f bit;  
set @x = '<root Somedate = "2002-01-01Z"/>';  
set @f = @x.exist('/root[(@Somedate cast as xs:date?) eq xs:date("2002-01-01Z")]');  
select @f;  
```  
  
 Comparar las fechas en el **exist()** método, tenga en cuenta lo siguiente:  
  
-   El código `cast as xs:date?` se utiliza para convertir el valor en **xs: Date** tipo para fines de comparación.  
  
-   El valor de la  **@Somedate**  atributo no tiene tipo. En la comparación de este valor, se convierte implícitamente al tipo del lado derecho de la comparación, el **xs: Date** tipo.  
  
-   En lugar de **convierte as xs:Date()**, puede usar el **xs:Date()** función constructora. Para obtener más información, vea [funciones constructoras &#40; XQuery &#41; ](../../xquery/constructor-functions-xquery.md).  
  
 El ejemplo siguiente es similar al anterior, con la diferencia de que tiene un elemento <`Somedate`>.  
  
```  
DECLARE @x xml;  
DECLARE @f bit;  
SET @x = '<Somedate>2002-01-01Z</Somedate>';  
SET @f = @x.exist('/Somedate[(text()[1] cast as xs:date ?) = xs:date("2002-01-01Z") ]')  
SELECT @f;  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   El **text()** método devuelve un nodo de texto que contiene el valor sin tipo `2002-01-01`. (El tipo XQuery es **xdt: untypedAtomic**.) Se debe convertir explícitamente este valor con tipo de **x** a **xsd: Date**, porque no se admite en este caso la conversión implícita.  
  
### <a name="example-specifying-the-exist-method-against-a-typed-xml-variable"></a>Ejemplo: especificar el método exist() con una variable xml con tipo  
 En el ejemplo siguiente se muestra el uso de la **exist()** método con un **xml** variable de tipo. Se trata de una variable XML con tipo, pues especifica el nombre de la colección del espacio de nombres del esquema, `ManuInstructionsSchemaCollection`.  
  
 En el ejemplo, un documento se asigna primero a esta variable con instrucciones de fabricación y, a continuación, el **exist()** método se usa para buscar si el documento incluye un <`Location`> elemento cuyo **LocationID**  valor de atributo es 50.  
  
 El **exist()** método especificado en el @x variable devuelve 1 (True) si las instrucciones de fabricación documento incluye un <`Location`> elemento que tiene `LocationID=50`. De lo contrario, el método devolverá 0 (False).  
  
```  
DECLARE @x xml (Production.ManuInstructionsSchemaCollection);  
SELECT @x=Instructions  
FROM Production.ProductModel  
WHERE ProductModelID=67;  
--SELECT @x  
DECLARE @f int;  
SET @f = @x.exist(' declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
    /AWMI:root/AWMI:Location[@LocationID=50]  
');  
SELECT @f;  
```  
  
### <a name="example-specifying-the-exist-method-against-an-xml-type-column"></a>Ejemplo: especificar el método exist() con una columna de tipo xml  
 La consulta siguiente recupera los Id. de modelo de producto cuyas descripciones de catálogo no incluyen las especificaciones, elemento <`Specifications`>:  
  
```  
SELECT ProductModelID, CatalogDescription.query('  
declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
    declare namespace  pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     /pd:ProductDescription[not(pd:Specifications)]'  
    ) = 1;  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   La cláusula WHERE selecciona únicamente las filas de la **ProductDescription** table que cumplen la condición especificada en el **CatalogDescription xml** columna de tipo.  
  
-   El **exist()** método en la cláusula WHERE devuelve 1 (verdadero) si el código XML no incluye ningún <`Specifications`> elemento. Tenga en cuenta el uso de la [not() (función de XQuery)](../../xquery/functions-on-boolean-values-not-function.md).  
  
-   El [función SQL:Column() (XQuery)](../../xquery/xquery-extension-functions-sql-column.md) función se utiliza para recuperar el valor de una columna no XML.  
  
-   Esta consulta devuelve un conjunto de filas vacío.  
  
 La consulta especifica **query()** y **exist()** métodos del tipo de datos xml y ambos métodos declaran los mismos espacios de nombres en el prólogo de la consulta. En este caso, puede utilizar WITH XMLNAMESPACES para declarar el prefijo y utilizarlo en la consulta.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' AS pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
     /pd:ProductDescription[not(pd:Specifications)]'  
    ) = 1;  
```  
  
## <a name="see-also"></a>Vea también  
 [Agregar espacios de nombres a consultas con WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)   
 [Comparar XML con tipo y XML sin tipo](../../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Crear instancias de datos XML](../../relational-databases/xml/create-instances-of-xml-data.md)   
 [Métodos de tipo de datos xml](../../t-sql/xml/xml-data-type-methods.md)   
 [Lenguaje de manipulación de datos XML &#40; XML DML &#41;](../../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
