---
title: "SQL:Column() (función de XQuery) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: xquery
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- sql:column function
- sql:column() function
ms.assetid: e8f67bdf-b489-49a9-9d0f-2069c1750467
caps.latest.revision: "38"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: a2edc76979e76a83125a53bf98609f263c9b9051
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/05/2017
---
# <a name="xquery-extension-functions---sqlcolumn"></a>Funciones de XQuery extensión - SQL:Column()
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Como se describe en el tema, [enlazar datos relacionales dentro de XML](../t-sql/xml/binding-relational-data-inside-xml-data.md), puede usar el **SQL:Column()** funcionan cuando se utiliza [XML Data Type Methods](../t-sql/xml/xml-data-type-methods.md) para exponer un valor relacional dentro de XQuery.  
  
 Por ejemplo, el [método query() (tipo de datos XML)](../t-sql/xml/query-method-xml-data-type.md) se utiliza para especificar una consulta en una instancia XML que se almacena en una variable o columna de **xml** tipo. En algunos casos, es posible que desee que la consulta utilice valores de una columna no XML para obtener datos relacionales y XML al mismo tiempo. Para ello, use la **SQL:Column()** función.  
  
 El valor SQL se asignará al valor XQuery correspondiente y su tipo será un tipo base XQuery equivalente al tipo SQL correspondiente.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sql:column("columnName")  
```  
  
## <a name="remarks"></a>Comentarios  
 Tenga en cuenta que la referencia a una columna especificada en el **SQL:Column()** función dentro de una expresión XQuery hace referencia a una columna de la fila que se está procesando.  
  
 En [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], solo puede hacer referencia a un **xml** instrucción de inserción de la instancia en el contexto de la expresión de origen de un XML-DML; de lo contrario, no puede hacer referencia a las columnas que son de tipo **xml** o CLR tipo definido por el usuario.  
  
 El **SQL:Column()** función no se admite en las operaciones de combinación. En su lugar, se puede utilizar la operación APPLY.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-sqlcolumn-to-retrieve-the-relational-value-inside-xml"></a>A. Usar sql:column() para recuperar el valor relacional en XML  
 Al crear XML, el ejemplo siguiente muestra cómo recuperar valores de una columna relacional no XML para enlazar datos XML y relacionales.  
  
 La consulta crea XML con el formato siguiente:  
  
```  
<Product ProductID="771" ProductName="Mountain-100 Silver, 38" ProductPrice="3399.99" ProductModelID="19"   
  ProductModelName="Mountain 100" />  
```  
  
 Tenga en cuenta las siguientes observaciones acerca del XML creado:  
  
-   El **ProductID**, **ProductName**, y **ProductPrice** valores de atributo se obtienen de la **producto** tabla.  
  
-   El **ProductModelID** se recupera el valor del atributo de la **ProductModel** tabla.  
  
-   Para que la consulta sea más interesante, el **ProductModelName** se obtiene el valor del atributo de la **CatalogDescription** columna de **tipo xml**. Dado que no toda la información del catálogo de modelos de productos XML se almacena, la instrucción `if` se utiliza para recuperar el valor solo si existe.  
  
    ```  
    SELECT P.ProductID, CatalogDescription.query('  
    declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
           <Product   
               ProductID=       "{ sql:column("P.ProductID") }"  
               ProductName=     "{ sql:column("P.Name") }"  
               ProductPrice=    "{ sql:column("P.ListPrice") }"  
               ProductModelID= "{ sql:column("PM.ProductModelID") }" >  
               { if (not(empty(/pd:ProductDescription))) then  
                 attribute ProductModelName { /pd:ProductDescription[1]/@ProductModelName }  
                else   
                   ()  
    }  
            </Product>  
    ') as Result  
    FROM Production.ProductModel PM, Production.Product P  
    WHERE PM.ProductModelID = P.ProductModelID  
    AND   CatalogDescription is not NULL  
    ORDER By PM.ProductModelID  
    ```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   Dado que los valores se recuperan de dos tablas diferentes, la cláusula FROM especifica dos tablas. La condición en la cláusula WHERE filtra el resultado y recupera solo productos cuyos modelos disponen de descripciones de catálogo.  
  
-   El **espacio de nombres** palabra clave en el [prólogo de XQuery](../xquery/modules-and-prologs-xquery-prolog.md) define el prefijo de espacio de nombres XML, "pd", que se utiliza en el cuerpo de la consulta. Observe que los alias de tabla, "P" y "PM", se definen en la cláusula FROM de la propia consulta.  
  
-   El **SQL:Column()** función se utiliza para recuperar valores no XML dentro de XML.  
  
 Éste es el resultado parcial:  
  
```  
ProductID               Result  
-----------------------------------------------------------------  
771         <Product ProductID="771"                   ProductName="Mountain-100 Silver, 38"   
                  ProductPrice="3399.99" ProductModelID="19"   
                  ProductModelName="Mountain 100" />  
...  
```  
  
 La consulta siguiente crea XML que contiene información específica del producto. Esta información incluye ProductID, ProductName, ProductPrice y, si está disponible, ProductModelName para todos los productos que pertenecen a un modelo específico, ProductModelID=19. El XML, a continuación, se asigna a la @x variables de **xml** tipo.  
  
```  
declare @x xml  
SELECT @x = CatalogDescription.query('  
declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
       <Product   
           ProductID=       "{ sql:column("P.ProductID") }"  
           ProductName=     "{ sql:column("P.Name") }"  
           ProductPrice=    "{ sql:column("P.ListPrice") }"  
           ProductModelID= "{ sql:column("PM.ProductModelID") }" >  
           { if (not(empty(/pd:ProductDescription))) then  
             attribute ProductModelName { /pd:ProductDescription[1]/@ProductModelName }  
            else   
               ()  
}  
        </Product>  
')   
FROM Production.ProductModel PM, Production.Product P  
WHERE PM.ProductModelID = P.ProductModelID  
And P.ProductModelID = 19  
select @x  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de extensión de XQuery SQL Server](http://msdn.microsoft.com/library/4bc5d499-5fec-4c3f-b11e-5ab5ef9d8f97)   
 [Comparar XML con tipo y XML sin tipo](../relational-databases/xml/compare-typed-xml-to-untyped-xml.md)   
 [Datos XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Crear instancias de datos XML](../relational-databases/xml/create-instances-of-xml-data.md)   
 [métodos del tipo de datos xml](../t-sql/xml/xml-data-type-methods.md)   
 [Lenguaje de manipulación de datos XML &#40; XML DML &#41;](../t-sql/xml/xml-data-modification-language-xml-dml.md)  
  
  
