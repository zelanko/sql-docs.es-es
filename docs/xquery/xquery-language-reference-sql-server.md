---
title: Referencia del lenguaje XQuery (SQL Server) | Documentos de Microsoft
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- XQuery
- XQuery, about XQuery
- xml data type [SQL Server], XQuery
- XML [SQL Server], XQuery
- queries [XML in SQL Server], XQuery
ms.assetid: 8a69344f-2990-4357-8160-cb26aac95b91
caps.latest.revision: 51
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 2a469f40cd2ddd585110aa853a9a2b532b46c8ee
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="xquery-language-reference-sql-server"></a>Referencia del lenguaje XQuery (SQL Server)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[tsql](../includes/tsql-md.md)]admite un subconjunto del lenguaje de XQuery que se usa para consultar el **xml** tipo de datos. Esta implementación de XQuery se basa en el borrador de trabajo de XQuery de julio de 2004. El lenguaje está siendo desarrollado por el World Wide Web Consortium (W3C), con la participación de los principales proveedores de bases de datos, incluido Microsoft. Dado que las especificaciones del W3C pueden someterse a futuras revisiones antes de convertirse en recomendaciones del W3C, esta implementación puede ser distinta de la recomendación final. En este tema se define de forma general la semántica y la sintaxis del subconjunto de XQuery admitido en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Para obtener más información, consulte el [especificación del lenguaje W3C XQuery 1.0](http://go.microsoft.com/fwlink/?LinkId=48846).  
  
 XQuery es un lenguaje que permite realizar consultas en datos XML estructurados o semiestructurados. Con el **xml** compatibilidad proporcionada en el tipo de datos del [!INCLUDE[ssDE](../includes/ssde-md.md)], documentos pueden almacenar en una base de datos y, a continuación, consultarse mediante XQuery.  
  
 XQuery se basa en el lenguaje para consultas XPath existente, con un incremento de la compatibilidad para lograr una mejor iteración, mejores resultados de la ordenación y la posibilidad de generar el XML necesario. XQuery opera según el modelo de datos XQuery. Se trata de una abstracción de documentos XML, y los resultados de XQuery pueden tener tipo o no tenerlo. La información del tipo se basa en los tipos proporcionados por el lenguaje para esquemas XML del W3C. Si no se dispone de información de tipos, XQuery trata los datos como sin tipo. Esto es similar al modo en que XPath versión 1.0 trata el XML.  
  
 Para consultar una instancia XML almacenada en una variable o columna de **xml** tipo, use la [métodos del tipo de datos xml](../t-sql/xml/xml-data-type-methods.md). Por ejemplo, puede declarar una variable de **xml** escriba y consultar mediante la **query()** método de la **xml** tipo de datos.  
  
```  
DECLARE @x xml  
SET @x = '<ROOT><a>111</a></ROOT>'  
SELECT @x.query('/ROOT/a')  
```  
  
 En el ejemplo siguiente, la consulta se especifica en la columna Instructions de **xml** tipo en la tabla ProductModel en la base de datos de AdventureWorks.  
  
```  
SELECT Instructions.query('declare namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";           
    /AWMI:root/AWMI:Location[@LocationID=10]  
') as Result   
FROM  Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 La consulta XQuery incluye la declaración de espacio de nombres, `declare namespace``AWMI=...`y la expresión de consulta, `/AWMI:root/AWMI:Location[@LocationID=10]`.  
  
 Tenga en cuenta que la consulta XQuery se especifica en la columna Instructions de **xml** tipo. El [método query()](../t-sql/xml/query-method-xml-data-type.md) de los datos xml tipo se utiliza para especificar la expresión XQuery.  
  
 La siguiente tabla enumera los temas relacionados que pueden ayudar a comprender la implementación de XQuery en [!INCLUDE[ssDE](../includes/ssde-md.md)].  
  
|Tema|Description|  
|-----------|-----------------|  
|[Datos XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)|Explica la compatibilidad con la **xml**tipo de datos en el [!INCLUDE[ssDE](../includes/ssde-md.md)] y los métodos que puede utilizar con este tipo de datos. El **xml** forms modelo de datos XQuery de entrada en la que se ejecutan las expresiones XQuery de tipo de datos.|  
|[Colecciones de esquemas XML &#40;SQL Server&#41;](../relational-databases/xml/xml-schema-collections-sql-server.md)|Describe cómo se puede asignar un tipo a las instancias XML almacenadas en una base de datos. Esto significa que se puede asociar una colección de esquemas XML con el **xml** columna de tipo. Todas las instancias almacenadas en la columna se validan y reciben un tipo según el esquema de la colección y proporcionan la información de tipos para XQuery.|  
|||  
  
> [!NOTE]  
>  La organización de esta sección se basa en las especificaciones del borrador de trabajo de XQuery del World Wide Web Consortium (W3C). Algunos de los diagramas que se ofrecen en esta sección se han tomado de esas especificaciones. En esta sección, se compara la implementación de Microsoft XQuery con las especificaciones del W3C, se describe en qué se diferencia Microsoft XQuery del W3C y se indican las características del W3C que no se admiten. La especificación W3C está disponible en [http://www.w3.org/TR/2004/WD-xquery-20040723](http://go.microsoft.com/fwlink/?LinkId=48846).  
  
## <a name="in-this-section"></a>En esta sección  
  
|Tema|Description|  
|-----------|-----------------|  
|[Conceptos básicos de XQuery](../xquery/xquery-basics.md)|Proporciona una visión general básica de los conceptos de XQuery, así como de la evaluación de expresiones (contexto estático y dinámico), la atomización, el valor booleano efectivo, el sistema de tipos XQuery, la coincidencia de tipos de secuencias y el control de errores.|  
|[Expresiones XQuery](../xquery/xquery-expressions.md)|Describe las expresiones principales de XQuery, expresiones de rutas de acceso, expresiones de secuencias, expresiones de comparación aritmética y lógicas, construcción de XQuery, expresión FLWOR, expresiones condicionales y cuantificadas, y diversas expresiones sobre tipos de secuencias.|  
|[Módulos y prólogos &#40; XQuery &#41;](../xquery/modules-and-prologs-xquery.md)|Describe el prólogo de las consultas XQuery.|  
|[Funciones de XQuery con el tipo de datos xml](../xquery/xquery-functions-against-the-xml-data-type.md)|Describe una lista de las funciones de XQuery admitidas.|  
|[Operadores XQuery con el tipo de datos xml](../xquery/xquery-operators-against-the-xml-data-type.md)|Describe los operadores XQuery admitidos.|  
|[Ejemplos adicionales de consultas XQuery con el tipo de datos xml](../xquery/additional-sample-xqueries-against-the-xml-data-type.md)|Proporciona más ejemplos de XQuery.|  
  
## <a name="see-also"></a>Vea también  
 [Datos XML &#40;SQL Server&#41;](../relational-databases/xml/xml-data-sql-server.md)   
 [Colecciones de esquemas XML &#40;SQL Server&#41;](../relational-databases/xml/xml-schema-collections-sql-server.md)   
 [Ejemplos de importación y exportación en bloque de documentos XML &#40;SQL Server&#41;](../relational-databases/import-export/examples-of-bulk-import-and-export-of-xml-documents-sql-server.md)  
  
  
