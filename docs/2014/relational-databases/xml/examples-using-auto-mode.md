---
title: 'Ejemplos: Usar el modo AUTO | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- AUTO FOR XML mode, examples
ms.assetid: 11e8d0e4-df8a-46f8-aa21-9602d4f26cad
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 6ad357c6dd37e45200f497a053b6a3a0579adfa9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37208615"
---
# <a name="examples-using-auto-mode"></a>Ejemplos: Usar el modo AUTO
  Los siguientes ejemplos ilustran el uso del modo AUTO. Muchas de estas consultas se especifican utilizando los documentos XML de instrucciones de fabricación de bicicletas almacenados en la columna Instructions de la tabla ProductModel en la base de datos de ejemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] .  
  
## <a name="example-retrieving-customer-order-and-order-detail-information"></a>Ejemplo: recuperar información de cliente, pedido y detalle del pedido  
 Esta consulta recupera información del cliente, pedidos y pedidos detallados de un cliente específico.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Cust.CustomerID,   
       OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       Detail.SalesOrderID, Detail.LineTotal, Detail.ProductID,   
       Product.Name,  
       Detail.OrderQty  
FROM Sales.Customer AS Cust  
INNER JOIN Sales.SalesOrderHeader AS OrderHeader   
    ON Cust.CustomerID = OrderHeader.CustomerID  
INNER JOIN Sales.SalesOrderDetail AS Detail  
    ON OrderHeader.SalesOrderID = Detail.SalesOrderID  
INNER JOIN Production.Product AS Product  
    ON Product.ProductID = Detail.ProductID  
WHERE Cust.CustomerID IN (29672, 29734)  
ORDER BY OrderHeader.CustomerID,  
         OrderHeader.SalesOrderID  
FOR XML AUTO;  
```  
  
 Dado que la consulta identifica los alias de tabla `Cust`, `OrderHeader`, `Detail`y `Product` , el modo `AUTO` genera los elementos correspondientes. De nuevo, el orden en que se identifican las tablas mediante las columnas especificadas en la cláusula `SELECT` determina la jerarquía de estos elementos.  
  
 El resultado parcial es el siguiente.  
  
 `<Cust CustomerID="29672">`  
  
 `<OrderHeader CustomerID="29672" SalesOrderID="43660">`  
  
 `<Detail SalesOrderID="43660" LineTotal="874.794000" ProductID="758" OrderQty="1">`  
  
 `<Product Name="Road-450 Red, 52" />`  
  
 `</Detail>`  
  
 `<Detail SalesOrderID="43660" LineTotal="419.458900" ProductID="762" OrderQty="1">`  
  
 `<Product Name="Road-650 Red, 44" />`  
  
 `</Detail>`  
  
 `</OrderHeader>`  
  
 `<OrderHeader CustomerID="29672" SalesOrderID="47660">`  
  
 `<Detail SalesOrderID="47660" LineTotal="469.794000" ProductID="765" OrderQty="1">`  
  
 `<Product Name="Road-650 Black, 58" />`  
  
 `</Detail>`  
  
 `</OrderHeader>`  
  
 `<OrderHeader CustomerID="29672" SalesOrderID="49857">`  
  
 `<Detail SalesOrderID="49857" LineTotal="44.994000" ProductID="852" OrderQty="1">`  
  
 `<Product Name="Women's Tights, S" />`  
  
 `</Detail>`  
  
 `</OrderHeader>`  
  
 `...`  
  
 `</Cust>`  
  
## <a name="example-specifying-group-by-and-aggregate-functions"></a>Ejemplo: Especificar GROUP BY y funciones de agregado  
 La consulta siguiente devuelve los identificadores de cliente individuales y el número de pedidos que ha solicitado el cliente.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT C.CustomerID, COUNT(*) AS NoOfOrders  
FROM Sales.Customer AS C  
INNER JOIN Sales.SalesOrderHeader AS SOH  
On C.CustomerID = SOH.CustomerID  
GROUP BY C.CustomerID  
FOR XML AUTO;This is the partial result:  
```  
  
 `<I CustomerID="11000" NoOfOrders="3" />`  
  
 `<I CustomerID="11001" NoOfOrders="3" />`  
  
 `...`  
  
## <a name="example-specifying-computed-columns-in-auto-mode"></a>Ejemplo: especificar columnas calculadas en el modo AUTO  
 Esta consulta devuelve nombres de cliente individuales concatenados y la información de los pedidos. La columna calculada se asigna al nivel más interno de ese punto, el elemento <`SOH`> en este ejemplo. Los nombres de cliente concatenados se agregan como atributos del elemento <`SOH`> en el resultado.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT P.FirstName + ' ' + P.LastName AS Name,  
       SOH.SalesOrderID  
FROM Sales.Customer AS C  
INNER JOIN Sales.SalesOrderHeader AS SOH  
    ON  C.CustomerID = SOH.CustomerID  
INNER JOIN Person.Person AS P  
    ON P.BusinessEntityID = C.PersonID  
FOR XML AUTO;  
```  
  
 Éste es el resultado parcial:  
  
```  
<SOH Name="Jon Yang" SalesOrderID="43793" />  
<SOH Name="Eugene Huang" SalesOrderID="43767" />  
```  
  
 Para recuperar los elementos <`IndividualCustomer`> que tienen el atributo `Name` que contiene la información de encabezado de cada pedido de ventas como un subelemento, la consulta se escribe de nuevo utilizando una instrucción sub select. La selección interna crea una tabla `IndividualCustomer` temporal con la columna calculada que contiene los nombres de los clientes individuales. Esta tabla se combina después con la tabla `SalesOrderHeader` para obtener el resultado.  
  
 Observe que la tabla `Sales.Customer` almacena información de clientes individuales, incluido el valor `PersonID` del cliente. Este `PersonID` se utiliza después para buscar el nombre de contacto en la tabla `Person.Person` .  
  
```  
SELECT IndividualCustomer.Name, SOH.SalesOrderID  
FROM (SELECT FirstName+ ' '+LastName AS Name, C.PersonID, C.CustomerID  
      FROM Sales.Customer AS C, Person.Person AS P  
      WHERE C.PersonID = P.BusinessEntityID) AS IndividualCustomer  
LEFT OUTER JOIN  Sales.SalesOrderHeader AS SOH  
   ON IndividualCustomer.CustomerID = SOH.CustomerID  
ORDER BY IndividualCustomer.CustomerID, SOH.CustomerIDFOR XML AUTO;  
```  
  
 Éste es el resultado parcial:  
  
 `<IndividualCustomer Name="Jon Yang">`  
  
 `<SOH SalesOrderID="43793" />`  
  
 `<SOH SalesOrderID="51522" />`  
  
 `<SOH SalesOrderID="57418" />`  
  
 `</IndividualCustomer>`  
  
 `...`  
  
 `...`  
  
## <a name="example-returning-binary-data"></a>Ejemplo: devolver datos binarios  
 Esta consulta devuelve una fotografía del producto de la tabla `ProductPhoto` . `ThumbNailPhoto` es una columna `varbinary(max)` de la tabla `ProductPhoto`. De manera predeterminada, el modo `AUTO` devuelve a los datos binarios una referencia que es una dirección URL relativa de la raíz virtual de la base de datos donde se ejecuta la consulta. Se debe especificar el atributo clave `ProductPhotoID` para identificar la imagen. Al recuperar la referencia de una imagen como se muestra en este ejemplo, también debe especificarse la clave principal en la cláusula `SELECT` para identificar una fila de forma única.  
  
```  
SELECT ProductPhotoID, ThumbNailPhoto  
FROM   Production.ProductPhoto   
WHERE ProductPhotoID=70  
FOR XML AUTO;  
```  
  
 El resultado es el siguiente:  
  
 `-- result`  
  
 `<Production.ProductPhoto`  
  
 `ProductPhotoID="70"`  
  
 `ThumbNailPhoto= "dbobject/Production.ProductPhoto[@ProductPhotoID='70']/@ThumbNailPhoto" />`  
  
 La misma consulta se ejecuta con la opción `BINARY BASE64` . La consulta devuelve los datos binarios en formato codificado en base64.  
  
```  
SELECT ProductPhotoID, ThumbNailPhoto  
FROM   Production.ProductPhoto   
WHERE ProductPhotoID=70  
FOR XML AUTO, BINARY BASE64;  
```  
  
 El resultado es el siguiente:  
  
 `-- result`  
  
 `<Production.ProductPhoto ProductPhotoID="70" ThumbNailPhoto="Base64 encoded photo" />`  
  
 De forma predeterminada, cuando se utiliza el modo AUTO para recuperar datos binarios, se devuelve una referencia a una dirección URL relativa a la raíz virtual de la base de datos donde se ejecutó la consulta en lugar de datos binarios. Esto ocurre si no se especifica la opción BINARY BASE64.  
  
 Cuando el modo AUTO devuelve una referencia de URL a los datos binarios de bases de datos que no distinguen mayúsculas y minúsculas y donde un nombre de tabla o columna especificado en la consulta no coincide con el nombre de tabla o columna de la base de datos, se ejecuta la consulta. Sin embargo, las mayúsculas o minúsculas devueltas en la referencia no serán coherentes. Por ejemplo:  
  
```  
SELECT ProductPhotoID, ThumbnailPhoto  
FROM   Production.ProductPhoto   
WHERE  ProductPhotoID=70  
FOR XML AUTO;  
```  
  
 El resultado es el siguiente:  
  
 `<Production.PRODUCTPHOTO`  
  
 `PRODUCTPHOTOID="70"`  
  
 `THUMBNAILPHOTO= "dbobject/Production.PRODUCTPHOTO[@ProductPhotoID='70']/@ThumbNailPhoto" />`  
  
 Eso puede ser un problema especialmente cuando se ejecutan consultas dbobject en una base de datos que distingue mayúsculas y minúsculas. Para evitarlo, el formato de mayúsculas y minúsculas del nombre de tabla o columna especificado en las consultas debe coincidir con el formato de mayúsculas y minúsculas del nombre de tabla o columna de la base de datos.  
  
## <a name="example-understanding-the-encoding"></a>Ejemplo: descripción de la codificación  
 Este ejemplo muestra varias codificaciones que tienen lugar en el resultado.  
  
 Cree esta tabla:  
  
```  
CREATE TABLE [Special Chars] (Col1 char(1) primary key, [Col#&2] varbinary(50));  
```  
  
 Agregue los siguientes datos a la tabla:  
  
```  
INSERT INTO [Special Chars] VALUES ('&', 0x20), ('#', 0x20);  
```  
  
 Esta consulta devuelve los datos de la tabla. El modo FOR XML AUTO está especificado. Los datos binarios se devuelven como una referencia.  
  
```  
SELECT * FROM [Special Chars] FOR XML AUTO;  
```  
  
 El resultado es el siguiente:  
  
 `<Special_x0020_Chars`  
  
 `Col1="#"`  
  
 `Col_x0023__x0026_2="dbobject/Special_x0020_Chars[@Col1='#']/@Col_x0023__x0026_2"`  
  
 `/>`  
  
 `<Special_x0020_Chars`  
  
 `Col1="&"`  
  
 `Col_x0023__x0026_2="dbobject/Special_x0020_Chars[@Col1='&']/@Col_x0023__x0026_2"`  
  
 `/>`  
  
 Éste es el proceso para codificar caracteres especiales en el resultado:  
  
-   En el de resultado de la consulta, los caracteres especiales XML y URL de los nombres del elemento y atributo devueltos se codifican mediante el valor hexadecimal del carácter Unicode correspondiente. En el resultado anterior, el nombre de elemento <`Special Chars`> se devuelve como <`Special_x0020_Chars`>. El nombre del atributo <`Col#&2`> se devuelve como <`Col_x0023__x0026_2`>. Los caracteres especiales XML y URL están codificados.  
  
-   Si los valores de los elementos o atributos contienen alguna de las cinco entidades de carácter XML estándar (', "", \<, > y &), estos caracteres XML especiales se codifican siempre mediante la codificación de caracteres XML. En el resultado anterior, el valor `&` del valor de atributo <`Col1`> está codificado como `&`. Sin embargo, el carácter # permanece como #, porque es un carácter XML válido y no un carácter XML especial.  
  
-   Si los valores de los elementos o atributos contienen caracteres especiales de dirección URL que tienen un significado especial en la dirección URL, solo se codifican en el valor DBOBJECT de la dirección URL y únicamente cuando el carácter especial forma parte de un nombre de columna o tabla. En el resultado, el carácter `#` que forma parte del nombre de la tabla `Col#&2` se codifica como `_x0023_ in the DBOJBECT URL`.  
  
## <a name="see-also"></a>Vea también  
 [Usar el modo AUTO con FOR XML](use-auto-mode-with-for-xml.md)  
  
  
