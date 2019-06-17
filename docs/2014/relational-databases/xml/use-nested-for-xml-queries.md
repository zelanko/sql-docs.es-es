---
title: Usar consultas FOR XML anidadas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- FOR XML clause, nested FOR XML queries
- queries [XML in SQL Server], nested FOR XML
- nested FOR XML queries
ms.assetid: 7604161a-a958-446d-b102-7dee432979d0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f7a06d30f25f5c78236fe30f148b254ee817dfc0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63232405"
---
# <a name="use-nested-for-xml-queries"></a>Usar consultas FOR XML anidadas
  El `xml` tipo de datos y el [directiva TYPE en consultas FOR XML](type-directive-in-for-xml-queries.md) permiten que el XML devuelto por las consultas FOR XML para procesarse en el servidor, así como en el cliente.  
  
## <a name="processing-with-xml-type-variables"></a>Procesar con variables de tipo xml  
 Puede asignar el resultado de la consulta FOR XML a una variable de tipo `xml`, o utilizar XQuery para consultar el resultado y asignarlo a una variable de tipo `xml` para seguir procesándolo.  
  
```  
DECLARE @x xml  
SET @x=(SELECT ProductModelID, Name  
        FROM Production.ProductModel  
        WHERE ProductModelID=122 or ProductModelID=119  
        FOR XML RAW, TYPE)  
SELECT @x  
-- Result  
--<row ProductModelID="122" Name="All-Purpose Bike Stand" />  
--<row ProductModelID="119" Name="Bike Wash" />  
```  
  
 También puede procesar el XML devuelto en la variable, `@x`, utilizando alguno de los métodos de tipo de datos `xml`. Por ejemplo, puede recuperar el valor del atributo `ProductModelID` al usar el [método value()](/sql/t-sql/xml/value-method-xml-data-type).  
  
```  
DECLARE @i int;  
SET @i = (SELECT @x.value('/row[1]/@ProductModelID[1]', 'int'));  
SELECT @i;  
```  
  
 En el siguiente ejemplo, el resultado de la consulta `FOR XML` se devuelve como un tipo `xml` porque se ha especificado la directiva `TYPE` en la cláusula `FOR XML`.  
  
```  
SELECT ProductModelID, Name  
FROM Production.ProductModel  
WHERE ProductModelID=119 or ProductModelID=122  
FOR XML RAW, TYPE,ROOT('myRoot');  
  
```  
  
 Éste es el resultado:  
  
```  
<myRoot>  
  <row ProductModelID="122" Name="All-Purpose Bike Stand" />  
  <row ProductModelID="119" Name="Bike Wash" />  
</myRoot>  
```  
  
 Puesto que el resultado es de tipo `xml`, puede especificar uno de los métodos de tipo de datos `xml` directamente para este XML, como se muestra en la siguiente consulta. En la consulta, se usa el [método query() de tipo de datos xml](/sql/t-sql/xml/query-method-xml-data-type) para recuperar el primer elemento secundario <`row`> del elemento <`myRoot`>.  
  
```  
SELECT  (SELECT ProductModelID, Name  
         FROM Production.ProductModel  
         WHERE ProductModelID=119 or ProductModelID=122  
         FOR XML RAW, TYPE,ROOT('myRoot')).query('/myRoot[1]/row[1]');  
  
```  
  
 Éste es el resultado:  
  
```  
<row ProductModelID="122" Name="All-Purpose Bike Stand" />  
```  
  
## <a name="returning-inner-for-xml-query-results-to-outer-queries-as-xml-type-instances"></a>Devolver resultados de consultas FOR XML internas a consultas externas como instancias de tipo xml  
 Puede escribir consultas `FOR XML` anidadas en las que el resultado de la consulta interna se devuelve como un tipo `xml` a la consulta externa. Por ejemplo:  
  
```  
SELECT Col1,   
       Col2,   
       ( SELECT Col3, Col4   
        FROM  T2  
        WHERE T2.Col = T1.Col  
        ...  
        FOR XML AUTO, TYPE )  
FROM T1  
WHERE ...  
FOR XML AUTO, TYPE;  
```  
  
 Observe lo siguiente en la consulta anterior:  
  
-   El XML generado por la consulta `FOR XML` interna se agrega al XML generado por la consulta `FOR XML`externa.  
  
-   En la siguiente consulta interna se especifica la directiva `TYPE` . Por lo tanto, los datos XML devueltos por la consulta interna son de tipo `xml`. Si no se especifica la directiva TYPE, el resultado de la consulta `FOR XML` interna se devuelve como `nvarchar(max)` y se crean entidades de los datos XML.  
  
## <a name="controlling-the-shape-of-resulting-xml-data"></a>Controlar la forma de los datos XML resultantes  
 Las consultas FOR XML anidadas ofrecen mayor control en la definición de la forma de los datos XML resultantes. Es posible utilizar consultas FOR XML anidadas para construir XML parcialmente centrado en atributos y parcialmente centrado en elementos.  
  
 Para obtener más información sobre cómo especificar XML centrado en atributos y XML centrado en elementos para las consultas FOR XML anidadas, vea [Comparación de la consulta FOR XML con la consulta FOR XML anidada](../xml/for-xml-query-compared-to-nested-for-xml-query.md) y [Dar forma a XML con consultas FOR XML anidadas](../xml/shape-xml-with-nested-for-xml-queries.md).  
  
 Puede generar jerarquías XML que incluyen elementos del mismo nivel si especifica consultas FOR XML en modo AUTO anidadas. Para obtener más información, vea [Generar elementos del mismo nivel con una consulta de modo AUTO anidada](../xml/generate-siblings-with-a-nested-auto-mode-query.md).  
  
 Con independencia del modo que se utilice, las consultas FOR XML anidadas proporcionan mayor control en la descripción de la forma del XML resultante. Se pueden usar en lugar de las consultas en modo EXPLICIT.  
  
## <a name="examples"></a>Ejemplos  
 Los temas siguientes proporcionan ejemplos de consultas FOR XML anidadas.  
  
 [Comparación de la consulta FOR XML con la consulta FOR XML anidada](../xml/for-xml-query-compared-to-nested-for-xml-query.md)  
 Compara una consulta FOR XML de un solo nivel con una consulta FOR XML anidada. Este ejemplo incluye una demostración de cómo especificar XML centrado en atributos y XML centrado en elementos como resultado de la consulta.  
  
 [Generar elementos del mismo nivel con una consulta de modo AUTO anidada](../xml/generate-siblings-with-a-nested-auto-mode-query.md)  
 Muestra cómo generar elementos del mismo nivel con una consulta en modo AUTO anidada.  
  
 [Usar consultas FOR XML anidadas en ASP.NET](use-nested-for-xml-queries-in-asp-net.md)  
 Muestra cómo una aplicación ASPX puede utilizar FOR XML para devolver XML de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Dar forma a XML con consultas FOR XML anidadas](../xml/shape-xml-with-nested-for-xml-queries.md)  
 Muestra cómo utilizar consultas FOR XML anidadas para controlar la estructura de un documento XML creado por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
