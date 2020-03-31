---
title: FOR XML (SQL Server) | Microsoft Docs
ms.custom: fresh2019may
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: database-engine
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
author: MightyPen
ms.author: genemi
monikerRange: =azuresqldb-current||=azuresqldb-mi-current||>=sql-server-2016||>=sql-server-linux-2017||=sqlallproducts-allversions
ms.openlocfilehash: 5d497064378b7fe34c95ffe9c886144bb3523256
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "67943330"
---
# <a name="for-xml-sql-server"></a>FOR XML (SQL Server)

[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Una consulta SELECT devuelve los resultados como un conjunto de filas. Opcionalmente, se pueden recuperar resultados formales de una consulta SQL como XML especificando la cláusula FOR XML en la consulta. La cláusula FOR XML puede usarse en consultas de nivel superior y en subconsultas. La cláusula FOR XML de nivel superior solo puede usarse en la instrucción SELECT. En el caso de las subconsultas, FOR XML puede usarse en las instrucciones INSERT, UPDATE y DELETE. FOR XML también puede usarse en instrucciones de asignación.

En una cláusula FOR XML se especifica uno de estos modos:

- RAW
- AUTO
- EXPLICIT
- PATH

El modo RAW genera un único elemento \<row> por cada fila del conjunto de filas devuelto por la instrucción SELECT. Para generar una jerarquía XML se pueden escribir consultas FOR XML anidadas.

El modo AUTO genera anidamiento en el XML resultante utilizando heurística basada en la forma en que se especifica la instrucción SELECT. El control sobre la forma del XML generado es mínimo. Es posible escribir consultas FOR XML anidadas para generar una jerarquía XML más allá de la forma del XML generado mediante la heurística del modo AUTO.

El modo EXPLICIT concede un mayor control de la forma del XML. Es posible mezclar atributos y elementos con total libertad para decidir la forma del XML. Requiere un formato específico para el conjunto de filas resultante generado debido a la ejecución de la consulta. Después, el formato del conjunto de filas se asigna a una forma de XML. La eficacia del modo EXPLICIT reside en que se pueden mezclar atributos y elementos con total libertad, crear contenedores y propiedades complejas anidadas, crear valores separados por espacios (por ejemplo, el atributo OrderID puede tener una lista de valores de Id. de orden) y contenido mezclado.

Sin embargo, escribir consultas con el modo EXPLICIT puede ser un proceso complejo. Se pueden utilizar algunas de las características nuevas de FOR XML, como la posibilidad de escribir consultas anidadas FOR XML en modo RAW/AUTO/PATH y la directiva TYPE, en lugar de utilizar el modo EXPLICIT para generar las jerarquías. Las consultas FOR XML anidadas pueden generar el mismo XML que el modo EXPLICIT. Para obtener más información, vea [Usar consultas FOR XML anidadas](../../relational-databases/xml/use-nested-for-xml-queries.md) y [Directiva TYPE en consultas FOR XML](../../relational-databases/xml/type-directive-in-for-xml-queries.md).

El modo PATH, junto con la característica de las consultas anidadas FOR XML, proporciona la flexibilidad del modo EXPLICIT de una manera más sencilla.

Estos modos solamente tienen efecto en la ejecución de la consulta para la que se configuraron. No afectan a los resultados de ninguna de las consultas posteriores.

La cláusula FOR XML no es válida en una selección que se use junto con una cláusula FOR BROWSE.

## <a name="example"></a>Ejemplo

La siguiente instrucción `SELECT` recupera información de las tablas `Sales.Customer` y `Sales.SalesOrderHeader` de la base de datos `AdventureWorks2012` . Esta consulta especifica el modo `AUTO` en la cláusula `FOR XML` :

```sql
USE AdventureWorks2012
GO
SELECT Cust.CustomerID,
       OrderHeader.CustomerID,
       OrderHeader.SalesOrderID,
       OrderHeader.Status
FROM Sales.Customer Cust 
INNER JOIN Sales.SalesOrderHeader OrderHeader
ON Cust.CustomerID = OrderHeader.CustomerID
FOR XML AUTO;
```

## <a name="the-for-xml-clause-and-server-names"></a>La cláusula FOR XML y nombres de servidor

Cuando una instrucción SELECT con una cláusula FOR XML especifica un nombre de cuatro partes en la consulta, el nombre de servidor no se devuelve en el documento XML resultante cuando la consulta se ejecuta en el equipo local. Sin embargo, el nombre del servidor se devuelve como un nombre de cuatro partes cuando la consulta se ejecuta en un servidor de red.

Por ejemplo, considere esta consulta:

```sql
SELECT TOP 1 LastName
  FROM ServerName.AdventureWorks2012.Person.Person
  FOR XML AUTO;
```

&nbsp;

**Servidor local**: &nbsp; Cuando `ServerName` es un servidor local, la consulta devuelve el texto siguiente:

```xml
<AdventureWorks2012.Person.Person LastName="Achong" />  
```

&nbsp;

**Servidor de red**: &nbsp; Cuando `ServerName` es un servidor de red, la consulta devuelve el texto siguiente:

```xml
<ServerName.AdventureWorks2012.Person.Person LastName="Achong" />
```

&nbsp;

**Evitar la ambigüedad**: &nbsp; Se puede evitar esta ambigüedad potencial al especificar este alias:

```sql
SELECT TOP 1 LastName
  FROM ServerName.AdventureWorks2012.Person.Person x
  FOR XML AUTO;
```

La consulta con la ambigüedad eliminada devuelve ahora el texto siguiente:

```xml
<x LastName="Achong"/>
```

## <a name="see-also"></a>Consulte también

[Sintaxis básica de la cláusula FOR XML](../../relational-databases/xml/basic-syntax-of-the-for-xml-clause.md)  
[Usar el modo RAW con FOR XML](../../relational-databases/xml/use-raw-mode-with-for-xml.md)  
[Usar el modo AUTO con FOR XML](../../relational-databases/xml/use-auto-mode-with-for-xml.md)  
[Usar el modo EXPLICIT con FOR XML](../../relational-databases/xml/use-explicit-mode-with-for-xml.md)  
[Usar el modo PATH con FOR XML](../../relational-databases/xml/use-path-mode-with-for-xml.md)  
[OPENXML &#40;SQL Server&#41;](../../relational-databases/xml/openxml-sql-server.md)  
[Agregar espacios de nombres a consultas con WITH XMLNAMESPACES](../../relational-databases/xml/add-namespaces-to-queries-with-with-xmlnamespaces.md)
