---
title: Agregar espacios de nombres a consultas con WITH XMLNAMESPACES | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: xml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- ELEMENTS XSINIL directive
- adding namespaces
- XSINIL directive
- default namespaces
- queries [XML in SQL Server], WITH XMLNAMESPACES clause
- predefined namespaces [XML in SQL Server]
- FOR XML clause, WITH XMLNAMESPACES clause
- namespaces [XML in SQL Server]
- xml data type [SQL Server], WITH XMLNAMESPACES clause
- WITH XMLNAMESPACES clause
ms.assetid: 2189cb5e-4460-46c5-a254-20c833ebbfec
caps.latest.revision: 19
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: da7122abb272847f5951d3f8d0ed5157fde82088
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="add-namespaces-to-queries-with-with-xmlnamespaces"></a>Agregar espacios de nombres a consultas con WITH XMLNAMESPACES
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  [WITH XMLNAMESPACES (Transact-SQL)](../../t-sql/xml/with-xmlnamespaces.md) proporciona compatibilidad con los URI de espacio de nombres de la siguiente manera:  
  
-   Hace que las asignaciones de prefijos de espacio de nombres a los URI estén disponibles al [generar XML mediante FOR XML](../../relational-databases/xml/for-xml-sql-server.md) .  
  
-   Hace que las asignaciones de espacios de nombres a los URI estén disponibles para el contexto de espacio de nombres estático de los [métodos del tipo de datos xml](../../t-sql/xml/xml-data-type-methods.md).  
  
## <a name="using-with-xmlnamespaces-in-the-for-xml-queries"></a>Utilizar WITH XMLNAMESPACES en las consultas FOR XML  
 WITH XMLNAMESPACES permite incluir espacios de nombres XML en las consultas FOR XML. Por ejemplo, considere la siguiente consulta FOR XML:  
  
```  
SELECT ProductID, Name, Color  
FROM   Production.Product  
WHERE  ProductID=316 or ProductID=317  
FOR XML RAW  
```  
  
 El resultado es el siguiente:  
  
```  
<row ProductID="316" Name="Blade" />  
<row ProductID="317" Name="LL Crankarm" Color="Black" />  
  
```  
  
 Para agregar espacios de nombres al XML generado por la consulta FOR XML, especifique primero las asignaciones de los prefijos de espacio de nombres a los URI mediante la cláusula WITH NAMESPACES. A continuación, utilice los prefijos de espacio de nombres para especificar los nombres en la consulta, como se muestra en la siguiente consulta modificada. Tenga en cuenta que la cláusula WITH XMLNAMESPACES especifica la asignación del prefijo de espacio de nombres (`ns1`) al URI (`uri`). Después, el prefijo `ns1` se usa para especificar los nombres de elementos y atributos que la cláusula FOR XML debe generar.  
  
```  
WITH XMLNAMESPACES ('uri' as ns1)  
SELECT ProductID as 'ns1:ProductID',  
       Name      as 'ns1:Name',   
       Color     as 'ns1:Color'  
FROM Production.Product  
WHERE ProductID=316 or ProductID=317  
FOR XML RAW ('ns1:Prod'), ELEMENTS  
  
```  
  
 El resultado XML incluye los prefijos de espacio de nombres:  
  
```  
<ns1:Prod xmlns:ns1="uri">  
  <ns1:ProductID>316</ns1:ProductID>  
  <ns1:Name>Blade</ns1:Name>  
</ns1:Prod>  
<ns1:Prod xmlns:ns1="uri">  
  <ns1:ProductID>317</ns1:ProductID>  
  <ns1:Name>LL Crankarm</ns1:Name>  
  <ns1:Color>Black</ns1:Color>  
</ns1:Prod>  
  
```  
  
 La siguiente información se aplica a la cláusula WITH XMLNAMESPACES:  
  
-   Se admite solamente en los modos RAW, AUTO y PATH de las consultas FOR XML. No se admite el modo EXPLICIT.  
  
-   Afecta a los prefijos de espacio de nombres de las consultas FOR XML y a los métodos del tipo de datos **xml** , pero no al analizador XML. Por ejemplo, la consulta siguiente devuelve un error porque el documento XML no tiene ninguna declaración de espacio de nombres para el prefijo myNS.  
  
-   Las directivas FOR XML, XMLSCHEMA y XMLDATA no se pueden utilizar con una cláusula WITH XMLNAMESPACES.  
  
    ```  
    CREATE TABLE T (x xml)  
    go  
    WITH XMLNAMESPACES ('http://abc' as myNS )  
    INSERT INTO T VALUES('<myNS:root/>')  
    ```  
  
## <a name="using-the-xsinil-directive"></a>Utilizar la directiva XSINIL  
 No se puede definir el prefijo xsi en la cláusula WITH XMLNAMESPACES si se utiliza la directiva ELEMENTS XSINIL. En su lugar, se agrega automáticamente cuando se utiliza ELEMENTS XSINIL. La consulta siguiente usa ELEMENTS XSINIL, que genera XML centrado en elementos donde los valores NULL se asignan a elementos que tienen el atributo **xsi:nil** establecido en True.  
  
```  
WITH XMLNAMESPACES ('uri' as ns1)  
SELECT ProductID as 'ns1:ProductID',  
       Name      as 'ns1:Name',   
       Color     as 'ns1:Color'  
FROM Production.Product  
WHERE ProductID=316   
FOR XML RAW, ELEMENTS XSINIL  
```  
  
 El resultado es el siguiente:  
  
```  
<row xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:ns1="uri">  
  <ns1:ProductID>316</ns1:ProductID>  
  <ns1:Name>Blade</ns1:Name>  
  <ns1:Color xsi:nil="true" />  
</row>  
```  
  
## <a name="specifying-default-namespaces"></a>Especificar espacios de nombres predeterminados  
 En lugar de declarar un prefijo de espacio de nombres, se puede declarar un espacio de nombres predeterminado mediante la palabra clave DEFAULT. En la consulta FOR XML, enlazará el espacio de nombres predeterminado con los nodos XML del XML resultante. En el ejemplo siguiente, WITH XMLNAMESPACES especifica dos prefijos de espacio de nombres definidos con un espacio de nombres predeterminado.  
  
```  
WITH XMLNAMESPACES ('uri1' as ns1,   
                    'uri2' as ns2,  
                    DEFAULT 'uri2')  
SELECT ProductID,   
      Name,  
      Color  
FROM Production.Product   
WHERE ProductID=316 or ProductID=317  
FOR XML RAW ('ns1:Product'), ROOT('ns2:root'), ELEMENTS  
```  
  
 La consulta FOR XML genera XML centrado en elementos. Observe que la consulta utiliza los prefijos de espacio de nombres para asignar nombres a los nodos. En la cláusula SELECT, ProductID, Name y Color no especifican un nombre con ningún prefijo. Por lo tanto, los elementos correspondientes en el XML resultante pertenecen al espacio de nombres predeterminado.  
  
```  
<ns2:root xmlns="uri2" xmlns:ns2="uri2" xmlns:ns1="uri1">  
  <ns1:Product>  
    <ProductID>316</ProductID>  
    <Name>Blade</Name>  
  </ns1:Product>  
  <ns1:Product>  
    <ProductID>317</ProductID>  
    <Name>LL Crankarm</Name>  
    <Color>Black</Color>  
  </ns1:Product>  
</ns2:root>  
```  
  
 La consulta siguiente es similar a la anterior, con la diferencia de que se especifica el modo AUTO de FOR XML.  
  
```  
WITH XMLNAMESPACES ('uri1' as ns1,  'uri2' as ns2,DEFAULT 'uri2')  
SELECT ProductID,   
      Name,  
      Color  
FROM Production.Product as "ns1:Product"  
WHERE ProductID=316 or ProductID=317  
FOR XML AUTO, ROOT('ns2:root'), ELEMENTS  
```  
  
## <a name="using-predefined-namespaces"></a>Utilizar espacios de nombres predefinidos  
 Si se utilizan espacios de nombres predefinidos, excepto los espacios de nombres xml y xsi cuando se utiliza ELEMENTS XSINIL, es necesario especificar explícitamente el enlace con el espacio de nombres por medio de WITH XMLNAMESPACES. En la consulta siguiente se define explícitamente el enlace entre el prefijo de espacio de nombres y el URI para el espacio de nombres predefinido (`urn:schemas-microsoft-com:xml-sql`).  
  
```  
WITH XMLNAMESPACES ('urn:schemas-microsoft-com:xml-sql' as sql)  
SELECT 'SELECT * FROM Customers FOR XML AUTO, ROOT("a")' AS "sql:query"  
FOR XML PATH('sql:root')  
```  
  
 Éste es el resultado. Los usuarios de SQLXML están familiarizados con esta plantilla XML. Para obtener más información, vea [Conceptos de programación en SQLXML 4.0](../../relational-databases/sqlxml/sqlxml-4-0-programming-concepts.md).  
  
```  
<sql:root xmlns:sql="urn:schemas-microsoft-com:xml-sql">  
  <sql:query>SELECT * FROM Customers FOR XML AUTO, ROOT("a")</sql:query>  
</sql:root>  
```  
  
 Solo se puede utilizar el prefijo de espacio de nombres xml sin definirlo explícitamente en WITH XMLNAMESPACES, como se muestra en la siguiente consulta en modo PATH. Por otra parte, si se declara el prefijo, debe estar enlazado con el espacio de nombres http://www.w3.org/XML/1998/namespace. Los nombres especificados en la cláusula SELECT hacen referencia al prefijo de espacio de nombres xml que no se define explícitamente mediante WITH XMLNAMESPACES.  
  
```  
SELECT 'en'    as "English/@xml:lang",  
       'food'  as "English",  
       'ger'   as "German/@xml:lang",  
       'Essen' as "German"  
FOR XML PATH ('Translation')  
go  
```  
  
 Los atributos @xml:lang usan el espacio de nombres xml predefinido. Debido a que la versión 1.0 de XML no requiere la declaración explícita del enlace del espacio de nombres xml, el resultado no incluirá una declaración explícita del enlace de espacio de nombres.  
  
 El resultado es el siguiente:  
  
```  
<Translation>  
  <English xml:lang="en">food</English>  
  <German xml:lang="ger">Essen</German>  
</Translation>  
```  
  
## <a name="using-with-xmlnamespaces-with-the-xml-data-type-methods"></a>Utilizar WITH XMLNAMESPACES con los métodos del tipo de datos xml  
 Los [métodos del tipo de datos xml](../../t-sql/xml/xml-data-type-methods.md) especificados en una consulta SELECT, o en UPDATE en el caso del método **modify()** , deben repetir la declaración del espacio de nombres en el prólogo. Esto puede resultar lento. Por ejemplo, la consulta siguiente recupera los identificadores de modelo de producto cuyas descripciones de catálogo no incluyen la especificación. Es decir, el elemento <`Specifications`> existe.  
  
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
     /pd:ProductDescription[(pd:Specifications)]'  
    ) = 1  
```  
  
 En la consulta anterior, los métodos **query()** y **exist()** declaran el mismo espacio de nombres en el prólogo. Por ejemplo:  
  
```  
declare namespace pd="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription";  
```  
  
 Alternativamente, se puede declarar primero WITH XMLNAMESPACES y utilizar los prefijos de espacio de nombres en la consulta. En este caso, los métodos **query()** y **exist()** no tienen que incluir las declaraciones de espacio de nombres en el prólogo.  
  
```  
WITH XMLNAMESPACES ('http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelDescription' as pd)  
SELECT ProductModelID, CatalogDescription.query('  
    <Product   
        ProductModelID= "{ sql:column("ProductModelID") }"   
        />  
') AS Result  
FROM Production.ProductModel  
WHERE CatalogDescription.exist('  
     /pd:ProductDescription[(pd:Specifications)]'  
    ) = 1  
Go  
```  
  
 Debe tenerse en cuenta que una declaración explícita en el prólogo de una consulta XQuery reemplazará el prefijo de espacio de nombres y el espacio de nombres predeterminado del elemento definidos en la cláusula WITH.  
  
## <a name="see-also"></a>Ver también  
 [métodos del tipo de datos xml](../../t-sql/xml/xml-data-type-methods.md)   
 [Referencia del lenguaje XQuery &#40;SQL Server&#41;](../../xquery/xquery-language-reference-sql-server.md)   
 [WITH XMLNAMESPACES &#40;Transact-SQL&#41;](../../t-sql/xml/with-xmlnamespaces.md)   
 [FOR XML &#40;SQL Server&#41;](../../relational-databases/xml/for-xml-sql-server.md)  
  
  
