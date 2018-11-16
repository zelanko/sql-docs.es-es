---
title: 'Ejemplos: Usar el modo PATH | Microsoft Docs'
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- PATH FOR XML mode, examples
ms.assetid: 3564e13b-9b97-49ef-8cf9-6a78677b09a3
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 53b6625786fda63e5616b83edd0c1915f49a67e3
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51674454"
---
# <a name="examples-using-path-mode"></a>Ejemplos: Usar el modo PATH
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  El ejemplo siguiente ilustra el uso del modo PATH en la creación de XML a partir de una consulta SELECT. Muchas de estas consultas se especifican usando los documentos XML de instrucciones de fabricación de bicicletas almacenados en la columna Instructions de la tabla ProductModel.  
  
## <a name="specifying-a-simple-path-mode-query"></a>Especificar una consulta sencilla de modo PATH  
 Esta consulta especifica un modo FOR XML PATH.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT   
       ProductModelID,  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 OR ProductModelID=119  
FOR XML PATH;  
GO  
```  
  
 El resultado siguiente es XML centrado en elementos en el que cada valor de columna del conjunto de filas resultante se agrupa en un elemento. Puesto que la cláusula `SELECT` no especifica ningún alias para los nombres de columna, los nombres de elemento secundario generados son los mismos que los nombres de columna correspondientes de la cláusula `SELECT`. Para cada fila del conjunto de filas se agrega una etiqueta <`row`>.  
  
 `<row>`  
  
 `<ProductModelID>122</ProductModelID>`  
  
 `<Name>All-Purpose Bike Stand</Name>`  
  
 `</row>`  
  
 `<row>`  
  
 `<ProductModelID>119</ProductModelID>`  
  
 `<Name>Bike Wash</Name>`  
  
 `</row>`  
  
 El resultado siguiente es el mismo que el de la consulta de modo `RAW` con la opción `ELEMENTS` especificada. Devuelve XML centrado en elementos con un elemento <`row`> predeterminado para cada fila del conjunto de resultados.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID,  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 OR ProductModelID=119  
FOR XML RAW, ELEMENTS;  
```  
  
 También puede especificar el nombre del elemento de fila para sobrescribir el valor <`row`> predeterminado. Por ejemplo, la consulta siguiente devuelve el elemento <`ProductModel`> para cada fila del conjunto de filas.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID,  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119  
FOR XML PATH ('ProductModel');  
GO  
```  
  
 El XML resultante tendrá un nombre de elemento de fila especificado.  
  
 `<ProductModel>`  
  
 `<ProductModelID>122</ProductModelID>`  
  
 `<Name>All-Purpose Bike Stand</Name>`  
  
 `</ProductModel>`  
  
 `<ProductModel>`  
  
 `<ProductModelID>119</ProductModelID>`  
  
 `<Name>Bike Wash</Name>`  
  
 `</ProductModel>`  
  
 Si especifica una cadena de longitud cero, no se generará el elemento de ajuste.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID,  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 OR ProductModelID=119  
FOR XML PATH ('');  
GO  
```  
  
 El resultado es el siguiente:  
  
 `<ProductModelID>122</ProductModelID>`  
  
 `<Name>All-Purpose Bike Stand</Name>`  
  
 `<ProductModelID>119</ProductModelID>`  
  
 `<Name>Bike Wash</Name>`  
  
## <a name="specifying-xpath-like-column-names"></a>Especificar nombres de columna de tipo XPath  
 En la consulta siguiente, el nombre de columna `ProductModelID` especificado empieza por "\@" y no incluye una marca de barra diagonal ("/"). Por tanto, se creará en el XML resultante un atributo del elemento <`row`> que tenga el valor de columna correspondiente.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID AS "@id",  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 OR ProductModelID=119  
FOR XML PATH ('ProductModelData');  
GO  
```  
  
 El resultado es el siguiente:  
  
 `< ProductModelData id="122">`  
  
 `<Name>All-Purpose Bike Stand</Name>`  
  
 `</ ProductModelData >`  
  
 `< ProductModelData id="119">`  
  
 `<Name>Bike Wash</Name>`  
  
 `</ ProductModelData >`  
  
 Puede agregar un solo elemento de nivel superior especificando la opción `root` en `FOR XML`.  
  
```  
SELECT ProductModelID AS "@id",  
       Name  
FROM Production.ProductModel  
WHERE ProductModelID=122 or ProductModelID=119  
FOR XML PATH ('ProductModelData'), root ('Root');  
GO  
```  
  
 Para generar una jerarquía, puede incluir sintaxis del tipo PATH. Por ejemplo, si cambia el nombre de la columna `Name` por "SomeChild/ModelName", obtendrá XML con una jerarquía, tal y como se muestra en este resultado:  
  
 `<Root>`  
  
 `<ProductModelData id="122">`  
  
 `<SomeChild>`  
  
 `<ModelName>All-Purpose Bike Stand</ModelName>`  
  
 `</SomeChild>`  
  
 `</ProductModelData>`  
  
 `<ProductModelData id="119">`  
  
 `<SomeChild>`  
  
 `<ModelName>Bike Wash</ModelName>`  
  
 `</SomeChild>`  
  
 `</ProductModelData>`  
  
 `</Root>`  
  
 Además del identificador y el nombre del modelo de producto, la consulta siguiente recupera las ubicaciones con instrucciones de fabricación para el modelo de producto. Puesto que la columna Instructions es de tipo **xml** , se especifica el método **query()** del tipo de datos **xml** para recuperar la ubicación.  
  
```  
SELECT ProductModelID AS "@id",  
       Name,  
       Instructions.query('declare namespace MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
                /MI:root/MI:Location   
              ') AS ManuInstr  
FROM Production.ProductModel  
WHERE ProductModelID = 7  
FOR XML PATH ('ProductModelData'), root ('Root');  
GO  
```  
  
 El resultado parcial es el siguiente. Puesto que la consulta especifica ManuInstr como nombre de columna, el XML devuelto por el método **query()** se ajusta en una etiqueta <`ManuInstr`> como se muestra a continuación:  
  
 `<Root>`  
  
 `<ProductModelData id="7">`  
  
 `<Name>HL Touring Frame</Name>`  
  
 `<ManuInstr>`  
  
 `<MI:Location xmlns:MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"`  
  
 `<MI:step>...</MI:step>...`  
  
 `</MI:Location>`  
  
 `...`  
  
 `</ManuInstr>`  
  
 `</ProductModelData>`  
  
 `</Root>`  
  
 En la consulta FOR XML anterior, puede incluir espacios de nombres para los elementos <`Root`> y <`ProductModelData`>. Para ello, defina en primer lugar el prefijo de enlace de espacios de nombres mediante WITH XMLNAMESPACES y prefijos en la consulta FOR XML. Para obtener más información, vea [Agregar espacios de nombres a consultas con WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md).  
  
```  
USE AdventureWorks2012;  
GO  
WITH XMLNAMESPACES (  
   'uri1' AS ns1,    
   'uri2' AS ns2,  
   'https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions' as MI)  
SELECT ProductModelID AS "ns1:ProductModelID",  
       Name           AS "ns1:Name",  
       Instructions.query('  
                /MI:root/MI:Location   
              ')   
FROM Production.ProductModel  
WHERE ProductModelID=7  
FOR XML PATH ('ns2:ProductInfo'), root('ns1:root');  
GO  
```  
  
 Observe que el prefijo `MI` también se define en `WITH XMLNAMESPACES`. Como resultado, el método **query()** del tipo **xml** especificado no define el prefijo en el prólogo de la consulta. El resultado es el siguiente:  
  
 `<ns1:root xmlns:MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions" xmlns="uri2" xmlns:ns2="uri2" xmlns:ns1="uri1">`  
  
 `<ns2:ProductInfo>`  
  
 `<ns1:ProductModelID>7</ns1:ProductModelID>`  
  
 `<ns1:Name>HL Touring Frame</ns1:Name>`  
  
 `<MI:Location xmlns:MI="https://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions"`  
  
 `LaborHours="2.5" LotSize="100" MachineHours="3" SetupHours="0.5" LocationID="10" xmlns="">`  
  
 `<MI:step>`  
  
 `Insert <MI:material>aluminum sheet MS-2341</MI:material> into the <MI:tool>T-85A framing tool</MI:tool>.`  
  
 `</MI:step>`  
  
 `...`  
  
 `</MI:Location>`  
  
 `...`  
  
 `</ns2:ProductInfo>`  
  
 `</ns1:root>`  
  
## <a name="generating-a-value-list-using-path-mode"></a>Generar una lista de valores con el modo PATH  
 Esta consulta crea una lista de valores de Id. de productos para cada modelo de producto. Además, crea elementos anidados <`ProductName`> para cada Id. de producto, tal y como se muestra en este fragmento de XML:  
  
 `<ProductModelData ProductModelID="7" ProductModelName="..."`  
  
 `ProductIDs="product id list in the product model" >`  
  
 `<ProductName>...</ProductName>`  
  
 `<ProductName>...</ProductName>`  
  
 `...`  
  
 `</ProductModelData>`  
  
 Esta es la consulta que crea el XML deseado:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID     AS "@ProductModelID",  
       Name               AS "@ProductModelName",  
      (SELECT ProductID AS "data()"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
       FOR XML PATH ('')) AS "@ProductIDs",  
       (SELECT Name AS "ProductName"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
        FOR XML PATH ('')) AS "ProductNames"  
FROM   Production.ProductModel  
WHERE  ProductModelID= 7 or ProductModelID=9  
FOR XML PATH('ProductModelData');  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   El primer `SELECT` anidado devuelve una lista de ProductID usando `data()` como nombre de columna. La consulta especifica una cadena vacía como nombre del elemento de fila en `FOR XML PATH`, por lo que no se generará ningún elemento. En su lugar, se asignará la lista de valores al atributo `ProductID` .  
  
-   El segundo `SELECT` anidado recupera nombres para los productos del modelo de producto. Genera elementos <`ProductName`> que se devuelven ajustados en el elemento <`ProductNames`>, puesto que la consulta especifica `ProductNames` como nombre de columna.  
  
 Éste es el resultado parcial:  
  
 `<ProductModelData PId="7"`  
  
 `ProductModelName="HL Touring Frame"`  
  
 `ProductIDs="885 887 ...">`  
  
 `<ProductNames>`  
  
 `<ProductName>HL Touring Frame - Yellow, 60</ProductName>`  
  
 `<ProductName>HL Touring Frame - Yellow, 46</ProductName></ProductNames>`  
  
 `...`  
  
 `</ProductModelData>`  
  
 `<ProductModelData PId="9"`  
  
 `ProductModelName="LL Road Frame"`  
  
 `ProductIDs="722 723 724 ...">`  
  
 `<ProductNames>`  
  
 `<ProductName>LL Road Frame - Black, 58</ProductName>`  
  
 `<ProductName>LL Road Frame - Black, 60</ProductName>`  
  
 `<ProductName>LL Road Frame - Black, 62</ProductName>`  
  
 `...`  
  
 `</ProductNames>`  
  
 `</ProductModelData>`  
  
 La subconsulta que crea los nombres de producto devuelve el resultado como una cadena para la que se crea una entidad y que a continuación se agrega al XML. Si agrega la directiva de tipo, `FOR XML PATH (''), type`, la subconsulta devuelve el resultado como un tipo **xml** y no se crea ninguna entidad.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT ProductModelID AS "@ProductModelID",  
      Name AS "@ProductModelName",  
      (SELECT ProductID AS "data()"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
       FOR XML PATH ('')  
       ) AS "@ProductIDs",  
       (  
       SELECT Name AS "ProductName"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
       FOR XML PATH (''), type  
       ) AS "ProductNames"  
  
FROM Production.ProductModel  
WHERE ProductModelID= 7 OR ProductModelID=9  
FOR XML PATH('ProductModelData');  
```  
  
## <a name="adding-namespaces-in-the-resulting-xml"></a>Agregar espacios de nombres en el XML resultante  
 Tal y como se describe en el tema [Agregar espacios de nombres mediante WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md), puede usar WITH XMLNAMESPACES para incluir espacios de nombres en las consultas de modo PATH. Por ejemplo, los nombres especificados en la cláusula SELECT incluyen prefijos de espacio de nombres. La siguiente consulta de modo `PATH` crea XML con espacios de nombres.  
  
```  
SELECT 'en'    as "English/@xml:lang",  
       'food'  as "English",  
       'ger'   as "German/@xml:lang",  
       'Essen' as "German"  
FOR XML PATH ('Translation')  
GO  
```  
  
 El atributo `@xml:lang` agregado al elemento <`English`> se define en el espacio de nombres xml predefinido.  
  
 El resultado es el siguiente:  
  
 `<Translation>`  
  
 `<English xml:lang="en">food</English>`  
  
 `<German xml:lang="ger">Essen</German>`  
  
 `</Translation>`  
  
 La consulta siguiente es parecida al ejemplo C, con la diferencia de que usa `WITH XMLNAMESPACES` para incluir espacios de nombres en el XML resultante. Para obtener más información, vea [Agregar espacios de nombres a consultas con WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md).  
  
```  
USE AdventureWorks2012;  
GO  
WITH XMLNAMESPACES ('uri1' AS ns1,  DEFAULT 'uri2')  
SELECT ProductModelID AS "@ns1:ProductModelID",  
      Name AS "@ns1:ProductModelName",  
      (SELECT ProductID AS "data()"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
       FOR XML PATH ('')  
       ) AS "@ns1:ProductIDs",  
       (  
       SELECT ProductID AS "@ns1:ProductID",   
              Name AS "@ns1:ProductName"  
       FROM   Production.Product  
       WHERE  Production.Product.ProductModelID =   
              Production.ProductModel.ProductModelID  
       FOR XML PATH , type   
       ) AS "ns1:ProductNames"  
FROM Production.ProductModel  
WHERE ProductModelID= 7 OR ProductModelID=9  
FOR XML PATH('ProductModelData'), root('root');  
```  
  
 El resultado es el siguiente:  
  
 `<root xmlns="uri2" xmlns:ns1="uri1">`  
  
 `<ProductModelData ns1:ProductModelID="7" ns1:ProductModelName="HL Touring Frame" ns1:ProductIDs="885 887 888 889 890 891 892 893">`  
  
 `<ns1:ProductNames>`  
  
 `<row xmlns="uri2" xmlns:ns1="uri1" ns1:ProductID="885" ns1:ProductName="HL Touring Frame - Yellow, 60" />`  
  
 `<row xmlns="uri2" xmlns:ns1="uri1" ns1:ProductID="887" ns1:ProductName="HL Touring Frame - Yellow, 46" />`  
  
 `...`  
  
 `</ns1:ProductNames>`  
  
 `</ProductModelData>`  
  
 `<ProductModelData ns1:ProductModelID="9" ns1:ProductModelName="LL Road Frame" ns1:ProductIDs="722 723 724 725 726 727 728 729 730 736 737 738">`  
  
 `<ns1:ProductNames>`  
  
 `<row xmlns="uri2" xmlns:ns1="uri1" ns1:ProductID="722" ns1:ProductName="LL Road Frame - Black, 58" />`  
  
 `...`  
  
 `</ns1:ProductNames>`  
  
 `</ProductModelData>`  
  
 `</root>`  
  
## <a name="see-also"></a>Ver también  
 [Usar el modo PATH con FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
  
  
