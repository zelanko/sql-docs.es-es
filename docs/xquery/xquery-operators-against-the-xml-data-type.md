---
title: Operadores de XQuery con el tipo de datos xml | Documentos de Microsoft
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: sql
ms.service: ''
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- XQuery, operators
- operators [XQuery]
- xml data type [SQL Server], XQuery
ms.assetid: 39ca3d2e-e928-4333-872b-75c4ccde8e79
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 11141d97e487b0e8c25141b40b4a667b0bb04cbb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="xquery-operators-against-the-xml-data-type"></a>Operadores XQuery con el tipo de datos XML
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  XQuery admite los operadores siguientes:  
  
-   Operadores numéricos (+, -, *, div, mod)  
  
-   Operadores de comparación de valores (eq, ne, lt, gt, le, ge)  
  
-   Operadores de comparación general (=,! =, \<, >, \<=, > =)  
  
 Para obtener más información acerca de estos operadores, vea [expresiones de comparación &#40;XQuery&#41;](../xquery/comparison-expressions-xquery.md)  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-using-general-operators"></a>A. Utilizar operadores generales  
 Esta consulta ilustra el uso de operadores generales que se aplican a secuencias y también para comparar secuencias. La consulta recupera una secuencia de números de teléfono para cada cliente de la **AdditionalContactInfo** columna de la **póngase en contacto con** tabla. Después, esta secuencia se compara con la secuencia de dos números de teléfono ("111-111-1111", "222-2222").  
  
 La consulta utiliza la **=** operador de comparación. Cada nodo de la secuencia en el lado derecho de la **=** operador se compara con cada nodo en la secuencia en el lado izquierdo. Si los nodos coinciden, la comparación de nodo es **TRUE**. Después, el valor se convierte a int y se compara con 1, y la consulta devuelve el Id. de cliente.  
  
```  
WITH XMLNAMESPACES (  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactInfo' AS ACI,  
'http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ContactTypes' AS ACT)  
SELECT ContactID   
FROM   Person.Contact  
WHERE  AdditionalContactInfo.value('  
      //ACI:AdditionalContactInfo//ACT:telephoneNumber/ACT:number =   
          ("111-111-1111", "222-2222")',  
      'bit')= cast(1 as bit)  
```  
  
 Hay otra forma de observar cómo funciona la consulta anterior: cada valor de número de teléfono teléfono recuperado de la **AdditionalContactInfo** columna se compara con el conjunto de dos números de teléfono. Si el valor está en el conjunto, se devuelve ese cliente en el resultado.  
  
### <a name="b-using-a-numeric-operator"></a>B. Utilizar un operador numérico  
 El operador + de esta consulta es un operador de valor, porque se aplica a un solo elemento. Por ejemplo, el valor 1 se suma a un tamaño de lote devuelto por la consulta:  
  
```  
SELECT ProductModelID, Instructions.query('  
     declare namespace   
 AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
     for $i in (/AWMI:root/AWMI:Location)[1]  
     return   
       <Location LocationID="{ ($i/@LocationID) }"  
                   LotSize  = "{  number($i/@LotSize) }"  
                   LotSize2 = "{ number($i/@LotSize) + 1 }"  
                   LotSize3 = "{ number($i/@LotSize) + 2 }" >  
  
       </Location>  
') as Result  
FROM Production.ProductModel  
where ProductModelID=7  
```  
  
### <a name="c-using-a-value-operator"></a>C. Utilizar un operador de valor  
 La consulta siguiente recupera los elementos <`Picture`> de un modelo de producto donde el tamaño de la fotografía es "small":  
  
```  
SELECT CatalogDescription.query('  
     declare namespace PD="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
     for $P in /PD:ProductDescription/PD:Picture[PD:Size eq "small"]  
     return  
           $P  
    ') as Result  
FROM Production.ProductModel  
where ProductModelID=19  
```  
  
 Dado que tanto los operandos para el **eq** operador son valores atómicos, el operador de valor se utiliza en la consulta. Puede escribir la misma consulta mediante el operador de comparación general ( **=** ).  
  
## <a name="see-also"></a>Vea también  
 [Funciones de XQuery con el tipo de datos xml](../xquery/xquery-functions-against-the-xml-data-type.md)   
 [Datos XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Referencia del lenguaje XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)  
  
  
