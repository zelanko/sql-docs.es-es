---
title: FOR XML (SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, about FOR XML clause
- PATH FOR XML mode, construction
- EXPLICIT FOR XML mode
- RAW FOR XML mode
- retrieving XML data
- XML [SQL Server], FOR XML clause
- AUTO FOR XML mode
- XML [SQL Server], construction
ms.assetid: 2b6b5c61-c5bd-49d2-8c0c-b7cf15857906
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: d058a399d25d7049dc376b0590c65f27c9d8dc2b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205885"
---
# <a name="for-xml-sql-server"></a>FOR XML (SQL Server)
  Una consulta SELECT devuelve los resultados como un conjunto de filas. Opcionalmente, se pueden recuperar resultados formales de una consulta SQL como XML especificando la cláusula FOR XML en la consulta. La cláusula FOR XML puede usarse en consultas de nivel superior y en subconsultas. La cláusula FOR XML de nivel superior solo puede usarse en la instrucción SELECT. En el caso de las subconsultas, FOR XML puede usarse en las instrucciones INSERT, UPDATE y DELETE. También puede usarse en instrucciones de asignación.  
  
 En una cláusula FOR XML se especifica uno de estos modos:  
  
-   RAW  
  
-   AUTO  
  
-   EXPLICIT  
  
-   PATH  
  
 El modo RAW genera un único elemento \<row> por cada fila del conjunto de filas devuelto por la instrucción SELECT. Para generar una jerarquía XML se pueden escribir consultas FOR XML anidadas.  
  
 El modo AUTO genera anidamiento en el XML resultante utilizando heurística basada en la forma en que se especifica la instrucción SELECT. El control sobre la forma del XML generado es mínimo. Es posible escribir consultas FOR XML anidadas para generar una jerarquía XML más allá de la forma del XML generado mediante la heurística del modo AUTO.  
  
 El modo EXPLICIT concede un mayor control de la forma del XML. Es posible mezclar atributos y elementos con total libertad para decidir la forma del XML. Requiere un formato específico para el conjunto de filas resultante generado debido a la ejecución de la consulta. Después, el formato del conjunto de filas se asigna a una forma de XML. La eficacia del modo EXPLICIT reside en que se pueden mezclar atributos y elementos con total libertad, crear contenedores y propiedades complejas anidadas, crear valores separados por espacios (por ejemplo, el atributo OrderID puede tener una lista de valores de Id. de orden) y contenido mezclado.  
  
 Sin embargo, escribir consultas con el modo EXPLICIT puede ser un proceso complejo. Se pueden utilizar algunas de las características nuevas de FOR XML, como la posibilidad de escribir consultas anidadas FOR XML en modo RAW/AUTO/PATH y la directiva TYPE, en lugar de utilizar el modo EXPLICIT para generar las jerarquías. Las consultas FOR XML anidadas pueden generar el mismo XML que el modo EXPLICIT. Para obtener más información, vea [Usar consultas FOR XML anidadas](use-nested-for-xml-queries.md) y [Directiva TYPE en consultas FOR XML](type-directive-in-for-xml-queries.md).  
  
 El modo PATH, junto con la característica de las consultas anidadas FOR XML, proporciona la flexibilidad del modo EXPLICIT de una manera más sencilla.  
  
 Estos modos solamente tienen efecto en la ejecución de la consulta para la que se configuraron. No afectan a los resultados de ninguna de las consultas posteriores.  
  
 La cláusula FOR XML no es válida en una selección que se use junto con una cláusula FOR BROWSE.  
  
## <a name="example"></a>Ejemplo  
 La siguiente instrucción `SELECT` recupera información de las tablas `Sales.Customer` y `Sales.SalesOrderHeader` de la base de datos `AdventureWorks2012` . Esta consulta especifica el modo `AUTO` en la cláusula `FOR XML` :  
  
```  
USE AdventureWorks2012  
GO  
SELECT Cust.CustomerID,   
       OrderHeader.CustomerID,  
       OrderHeader.SalesOrderID,   
       OrderHeader.Status  
FROM Sales.Customer Cust   
INNER JOIN Sales.SalesOrderHeader OrderHeader  
ON Cust.CustomerID = OrderHeader.CustomerID  
FOR XML AUTO  
```  
  
## <a name="the-for-xml-clause-and-server-names"></a>La cláusula FOR XML y nombres de servidor  
 Cuando una instrucción SELECT con una cláusula FOR XML especifica un nombre de cuatro partes en la consulta, el nombre de servidor no se devuelve en el documento XML resultante cuando la consulta se ejecuta en el equipo local. Sin embargo, el nombre del servidor se devuelve como un nombre de cuatro partes cuando la consulta se ejecuta en un servidor de red.  
  
 Por ejemplo, considere esta consulta:  
  
```  
SELECT TOP 1 LastName  
FROM ServerName.AdventureWorks2012.Person.Person  
FOR XML AUTO  
```  
  
 Cuando `ServerName` es un servidor local, la consulta devuelve lo siguiente:  
  
```  
<AdventureWorks2012.Person.Person LastName="Achong" />  
```  
  
 Cuando `ServerName` es un servidor de red, la consulta devuelve lo siguiente:  
  
```  
<ServerName.AdventureWorks2012.Person.Person LastName="Achong" />  
```  
  
 Se puede evitar esta ambigüedad especificando este alias:  
  
```  
SELECT TOP 1 LastName  
FROM ServerName.AdventureWorks2012.Person.Person x  
FOR XML AUTO   
```  
  
 Esta consulta devuelve lo siguiente:  
  
```  
<x LastName="Achong"/>  
```  
  
## <a name="see-also"></a>Vea también  
 [Sintaxis básica de la cláusula FOR XML](basic-syntax-of-the-for-xml-clause.md)   
 [Usar el modo RAW con FOR XML](use-raw-mode-with-for-xml.md)   
 [Usar el modo AUTO con FOR XML](use-auto-mode-with-for-xml.md)   
 [Usar el modo EXPLICIT con FOR XML](use-explicit-mode-with-for-xml.md)   
 [Usar el modo PATH con FOR XML](use-path-mode-with-for-xml.md)   
 [OPENXML &#40;SQL Server&#41;](openxml-sql-server.md)   
 [Agregar espacios de nombres a consultas con WITH XMLNAMESPACES](add-namespaces-to-queries-with-with-xmlnamespaces.md)  
  
  
