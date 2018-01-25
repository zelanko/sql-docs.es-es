---
title: Enlazar datos relacionales dentro de datos XML | Documentos de Microsoft
ms.custom: 
ms.date: 07/26/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|xml
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
helpviewer_keywords:
- relational data binding [SQL Server]
- XML [SQL Server], binding relational data
- xml data type [SQL Server], relational data binding
- binding relational data [XML in SQL Server]
- variables [XML in SQL Server], relational data binding
- columns [XML in SQL Server], relational data binding
ms.assetid: 03d013a9-b53f-46c3-9628-da77f099c74a
caps.latest.revision: "36"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 87dca9b5bcd70335a6121b1be1e49f4cc352826e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/25/2018
---
# <a name="binding-relational-data-inside-xml-data"></a>Enlazar datos relacionales dentro de datos XML
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Puede especificar [métodos del tipo de datos xml](../../t-sql/xml/xml-data-type-methods.md) contra un **xml** variable o columna de tipo de datos. Por ejemplo, el [de consultas &#40; &#41; Método &#40; tipo de datos xml &#41; ](../../t-sql/xml/query-method-xml-data-type.md) ejecuta la instrucción XQuery especificada en una instancia XML. Cuando se genera XML de esta manera, se puede utilizar un valor de un tipo de columna que no es XML o una variable Transact-SQL. Este proceso se conoce como enlazar datos relacionales dentro de XML.  
  
 Para enlazar datos relacionales no XML dentro de XML, el motor de base de datos de SQL Server proporciona estas seudofunciones:  
  
-   [SQL: column &#40; &#41; Función &#40; XQuery &#41; ](../../xquery/xquery-extension-functions-sql-column.md) Le permite usar los valores de una columna relacional en la expresión XQuery o XML DML.  
  
-   [SQL: variable &#40; &#41; Función &#40; XQuery &#41; ](../../xquery/xquery-extension-functions-sql-variable.md) . Le permite utilizar el valor de una variable de SQL en la expresión XQuery o XML DML.  
  
 Puede utilizar estas funciones con **xml** métodos del tipo de datos siempre que desee exponer un valor relacional dentro de XML.  
  
 No se puede utilizar estas funciones para hacer referencia a datos en columnas o variables de la **xml**, definido por el usuario CLR tipos, datetime, smalldatetime, **texto**, **ntext**, **sql_variant**, y **imagen** tipos.  
  
 Asimismo, este enlace es de solo lectura. En otras palabras, no se pueden escribir datos en las columnas que utilicen estas funciones. Por ejemplo, sql:variable("@x") = "*alguna expresión"* no está permitido.  
  
## <a name="example-cross-domain-query-using-sqlvariable"></a>Ejemplo: consulta entre dominios mediante sql:variable()  
 Este ejemplo se muestra cómo **SQL:variable()** puede permitir que una aplicación parametrizar una consulta. El ISBN se pasa mediante el uso de una variable de SQL @isbn. Si se reemplaza la constante con **SQL:variable()**, la consulta se puede utilizar para buscar cualquier ISBN y no sólo a aquellas cuyo ISBN es 0-7356-1588-2.  
  
```  
DECLARE @isbn varchar(20)  
SET     @isbn = '0-7356-1588-2'  
SELECT  xCol  
FROM    T  
WHERE   xCol.exist ('/book/@ISBN[. = sql:variable("@isbn")]') = 1  
```  
  
 **SQL:Column()** puede utilizarse de forma similar y ofrece ventajas adicionales. Los índices de la columna favorecen la eficiencia, según lo decida el optimizador de consultas basado en costos. Además, la columna calculada puede almacenar una propiedad promocionada.  
  
## <a name="see-also"></a>Vea también  
 [Métodos del tipo de datos xml](../../t-sql/xml/xml-data-type-methods.md)  
  
  
