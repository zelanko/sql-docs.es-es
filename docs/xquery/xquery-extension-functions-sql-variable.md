---
title: sql:variable() (Función) (XQuery) Microsoft Docs
description: Aprenda a utilizar la función extensión DeXQuery sql:variable() para exponer una variable que contiene un valor relacional SQL dentro de una expresión XQuery.
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.reviewer: ''
ms.technology: xml
ms.topic: language-reference
dev_langs:
- XML
helpviewer_keywords:
- sql:variable() function
- sql:variable function
ms.assetid: 6e2e5063-c1cf-4b5a-b642-234921e3f4f7
author: rothja
ms.author: jroth
ms.openlocfilehash: 8241e15643eb4aa25912451ddfed94699954797f
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2020
ms.locfileid: "81388605"
---
# <a name="xquery-extension-functions---sqlvariable"></a>Funciones de extensión de XQuery: sql:variable()
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Expone una variable que contiene un valor relacional SQL dentro de una expresión XQuery.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sql:variable("variableName") as xdt:anyAtomicType?  
```  
  
## <a name="remarks"></a>Observaciones  
 Como se describe en el tema Enlace de [datos relacionales dentro](../t-sql/xml/binding-relational-data-inside-xml-data.md)de XML , puede usar esta función cuando utilice [métodos](../t-sql/xml/xml-data-type-methods.md) de tipo de datos XML para exponer un valor relacional dentro de XQuery.  
  
 Por ejemplo, el [método query()](../t-sql/xml/query-method-xml-data-type.md) se utiliza para especificar una consulta en una instancia XML que se almacena en una variable o columna de tipo de datos **xml.** En ocasiones, es posible que también se desee que la consulta utilice valores de una variable [!INCLUDE[tsql](../includes/tsql-md.md)], o un parámetro, para combinar los datos relacionales y XML. Para ello, utilice la función **sql:variable.**  
  
 El valor SQL se asignará a un valor XQuery correspondiente y su tipo será un tipo base XQuery que es equivalente al tipo SQL correspondiente.  
  
 Solo puede hacer referencia a una instancia **xml** en el contexto de la expresión de origen de una instrucción insert XML-DML; de lo contrario, no puede hacer referencia a valores de tipo **xml** o un tipo definido por el usuario de Common Language Runtime (CLR).  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-the-sqlvariable-function-to-bring-a-transact-sql-variable-value-into-xml"></a>A. Usar la función sql:variable() para incorporar una variable Transact-SQL a XML  
 En el siguiente ejemplo se crea una instancia XML formada por los siguientes elementos:  
  
-   Un valor (`ProductID`) de una columna no XML. La [función sql:column()](../xquery/xquery-extension-functions-sql-column.md) se utiliza para enlazar este valor en el XML.  
  
-   Un valor (`ListPrice`) de una columna no XML de otra tabla. De nuevo, se utiliza `sql:column()` para enlazar este valor en el XML.  
  
-   Un valor (`DiscountPrice`) de una variable [!INCLUDE[tsql](../includes/tsql-md.md)]. El método `sql:variable()` se utiliza para enlazar este valor en el XML.  
  
-   Un valor`ProductModelName`( ) de una columna de tipo **xml** para que la consulta sea más interesante.  
  
 Esta es la consulta:  
  
```sql
DECLARE @price money  
  
SET @price=2500.00  
SELECT ProductID, Production.ProductModel.ProductModelID,CatalogDescription.query('  
declare namespace pd="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
  
       <Product   
           ProductID="{ sql:column("Production.Product.ProductID") }"  
           ProductModelID= "{ sql:column("Production.Product.ProductModelID") }"  
           ProductModelName="{/pd:ProductDescription[1]/@ProductModelName }"  
           ListPrice="{ sql:column("Production.Product.ListPrice") }"  
           DiscountPrice="{ sql:variable("@price") }"  
        />')   
FROM Production.Product   
JOIN Production.ProductModel  
ON Production.Product.ProductModelID = Production.ProductModel.ProductModelID  
WHERE ProductID=771  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   La función XQuery incluida en el método `query()` construye el XML.  
  
-   La `namespace` palabra clave se utiliza para definir un prefijo de espacio de nombres en [XQuery Prolog](../xquery/modules-and-prologs-xquery-prolog.md). Esto se hace porque el valor del atributo `ProductModelName` se recupera de la columna de tipo `CatalogDescription xml`, que tiene un esquema asociado a ella.  
  
 El resultado es el siguiente:  
  
```xml
<Product ProductID="771" ProductModelID="19"   
         ProductModelName="Mountain 100"   
         ListPrice="3399.99" DiscountPrice="2500" />  
```  
  
## <a name="see-also"></a>Consulte también  
 [Funciones de extensión XQuery de SQL Server](https://msdn.microsoft.com/library/4bc5d499-5fec-4c3f-b11e-5ab5ef9d8f97)   
 [Comparar XML con tipo con XML sin tipo](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Datos XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Crear instancias de datos XML](../relational-databases/xml/create-instances-of-xml-data.md)   
 [Métodos de tipo de datos xml](../t-sql/xml/xml-data-type-methods.md)   
 [Lenguaje de manipulación de datos XML &#40;XML DML&#41;](../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
