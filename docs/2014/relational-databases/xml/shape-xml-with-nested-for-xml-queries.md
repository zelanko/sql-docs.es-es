---
title: Dar forma a XML con consultas FOR XML anidadas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML query
- queries [XML in SQL Server], nested FOR XML
- XML [SQL Server], FOR XML queries
ms.assetid: 8dc42c05-16e8-4b7b-a5d3-550b55acae26
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e0a5fded413944c304dfe02675b3577b699adfc0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63231232"
---
# <a name="shape-xml-with-nested-for-xml-queries"></a>Dar forma a XML con consultas FOR XML anidadas
  En el ejemplo siguiente se consulta la tabla `Production.Product` para recuperar los valores `ListPrice` y `StandardCost` de un producto específico. Para hacer interesante la consulta, se devuelven ambos precios en un elemento <`Price`>, y cada elemento <`Price`> tiene un atributo `PriceType`.  
  
## <a name="example"></a>Ejemplo  
 Ésta es la forma esperada del XML:  
  
```  
<xsd:schema xmlns:schema="urn:schemas-microsoft-com:sql:SqlRowSet2" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:sqltypes="https://schemas.microsoft.com/sqlserver/2004/sqltypes" targetNamespace="urn:schemas-microsoft-com:sql:SqlRowSet2" elementFormDefault="qualified">  
  <xsd:import namespace="https://schemas.microsoft.com/sqlserver/2004/sqltypes" schemaLocation="https://schemas.microsoft.com/sqlserver/2004/sqltypes/sqltypes.xsd" />  
  <xsd:element name="Production.Product" type="xsd:anyType" />  
</xsd:schema>  
<Production.Product xmlns="urn:schemas-microsoft-com:sql:SqlRowSet2" ProductID="520">  
  <Price xmlns="" PriceType="ListPrice">133.34</Price>  
  <Price xmlns="" PriceType="StandardCost">98.77</Price>  
</Production.Product>  
```  
  
 Esta es la consulta FOR XML anidada:  
  
```  
USE AdventureWorks2012;  
GO  
SELECT Product.ProductID,   
          (SELECT 'ListPrice' as PriceType,   
                   CAST(CAST(ListPrice as NVARCHAR(40)) as XML)   
           FROM    Production.Product Price   
           WHERE   Price.ProductID=Product.ProductID   
           FOR XML AUTO, TYPE),  
          (SELECT  'StandardCost' as PriceType,   
                   CAST(CAST(StandardCost as NVARCHAR(40)) as XML)   
           FROM    Production.Product Price   
           WHERE   Price.ProductID=Product.ProductID   
           FOR XML AUTO, TYPE)  
FROM Production.Product  
WHERE ProductID=520  
for XML AUTO, TYPE, XMLSCHEMA  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   La instrucción SELECT externa construye el elemento <`Product`> que tiene un atributo **ProductID** y dos secundarios <`Price`>.  
  
-   Las dos instrucciones SELECT internas construyen dos elementos <`Price`>, cada uno con un atributo **PriceType** y XML que devuelve el precio del producto.  
  
-   La directiva XMLSCHEMA de la instrucción SELECT externa genera el esquema XSD insertado que describe la forma del XML resultante.  
  
 Para hacer interesante la consulta, puede escribir la consulta FOR XML y después escribir una consulta XQuery para el resultado con el fin de cambiar la forma del XML, como se muestra en la siguiente consulta:  
  
```  
SELECT ProductID,   
 ( SELECT p2.ListPrice, p2.StandardCost  
   FROM Production.Product p2   
   WHERE Product.ProductID = p2.ProductID  
   FOR XML AUTO, ELEMENTS XSINIL, type ).query('  
                                   for $p in /p2/*  
                                   return   
                                    <Price PriceType = "{local-name($p)}">  
                                     { data($p) }  
                                    </Price>  
                                  ')  
FROM Production.Product  
WHERE ProductID = 520  
FOR XML AUTO, TYPE  
```  
  
 En el ejemplo anterior se utiliza el método `query()` del tipo de datos `xml` para consultar el XML devuelto por la consulta FOR XML interna y construir el resultado esperado.  
  
 Éste es el resultado:  
  
```  
<Production.Product ProductID="520">  
  <Price PriceType="ListPrice">133.3400</Price>  
  <Price PriceType="StandardCost">98.7700</Price>  
</Production.Product>  
```  
  
## <a name="see-also"></a>Vea también  
 [Usar consultas FOR XML anidadas](use-nested-for-xml-queries.md)  
  
  
