---
title: Enlazar datos relacionales dentro de datos XML | Microsoft Docs
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- relational data binding [SQL Server]
- XML [SQL Server], binding relational data
- xml data type [SQL Server], relational data binding
- binding relational data [XML in SQL Server]
- variables [XML in SQL Server], relational data binding
- columns [XML in SQL Server], relational data binding
ms.assetid: 03d013a9-b53f-46c3-9628-da77f099c74a
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 87dca9b5bcd70335a6121b1be1e49f4cc352826e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="binding-relational-data-inside-xml-data"></a>Enlazar datos relacionales dentro de datos XML
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Puede especificar [métodos de tipo de datos xml](../../t-sql/xml/xml-data-type-methods.md) con una variable de tipo de datos o columna **xml**. Por ejemplo, [query&#40;&#41; &#40;método de tipo de datos xml&#41;](../../t-sql/xml/query-method-xml-data-type.md) ejecuta la instrucción XQuery especificada con una instancia XML. Cuando se genera XML de esta manera, se puede utilizar un valor de un tipo de columna que no es XML o una variable Transact-SQL. Este proceso se conoce como enlazar datos relacionales dentro de XML.  
  
 Para enlazar datos relacionales no XML dentro de XML, el motor de base de datos de SQL Server proporciona estas seudofunciones:  
  
-   Función [sql:column&#40;&#41; &#40;XQuery&#41;](../../xquery/xquery-extension-functions-sql-column.md). Le permite usar los valores de una columna relacional en la expresión XQuery o XML DML.  
  
-   Función [sql:variable&#40;&#41; &#40;XQuery&#41;](../../xquery/xquery-extension-functions-sql-variable.md). Le permite utilizar el valor de una variable de SQL en la expresión XQuery o XML DML.  
  
 Estas funciones se pueden usar con métodos de tipo de datos **xml** siempre que se quiera exponer un valor relacional dentro de XML.  
  
 Estas funciones no se pueden usar para hacer referencia a datos en columnas o variables de tipo **xml**, de tipos definidos por el usuario CLR, datetime, smalldatetime, **text**, **ntext**, **sql_variant** e **image**.  
  
 Asimismo, este enlace es de solo lectura. En otras palabras, no se pueden escribir datos en las columnas que utilicen estas funciones. Por ejemplo, sql:variable("@x")="*cualquier expresión"* no está permitido.  
  
## <a name="example-cross-domain-query-using-sqlvariable"></a>Ejemplo: consulta entre dominios mediante sql:variable()  
 Este ejemplo muestra cómo **sql:variable()** puede permitir a una aplicación parametrizar una consulta. El ISBN se pasa mediante una variable SQL @isbn. Sustituyendo la constante por **sql:variable()**, la consulta sirve para buscar cualquier ISBN y no solo el que corresponde a 0-7356-1588-2.  
  
```  
DECLARE @isbn varchar(20)  
SET     @isbn = '0-7356-1588-2'  
SELECT  xCol  
FROM    T  
WHERE   xCol.exist ('/book/@ISBN[. = sql:variable("@isbn")]') = 1  
```  
  
 **sql:column()** se puede usar de manera similar y ofrece otras ventajas. Los índices de la columna favorecen la eficiencia, según lo decida el optimizador de consultas basado en costos. Además, la columna calculada puede almacenar una propiedad promocionada.  
  
## <a name="see-also"></a>Ver también  
 [Métodos del tipo de datos xml](../../t-sql/xml/xml-data-type-methods.md)  
  
  
