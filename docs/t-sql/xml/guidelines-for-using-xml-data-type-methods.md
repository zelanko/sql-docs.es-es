---
title: Directrices para usar los métodos del tipo de datos xml | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- xml data type [SQL Server], methods
- methods [XML in SQL Server]
ms.assetid: 1a483aa1-42de-4c88-a4b8-c518def3d496
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 4b16a7d07358ff1c561bc840a958e24205688b86
ms.sourcegitcommit: c8f7e9f05043ac10af8a742153e81ab81aa6a3c3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/17/2018
ms.locfileid: "39083377"
---
# <a name="guidelines-for-using-xml-data-type-methods"></a>Directrices para utilizar los métodos del tipo de datos xml
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  En este tema se describen instrucciones para usar los métodos de tipo de datos **xml**.  
  
## <a name="the-print-statement"></a>La instrucción PRINT  
 Los métodos del tipo de datos **xml** no se pueden usar en la instrucción PRINT, como se muestra en el ejemplo siguiente. Los métodos del tipo de datos **xml** se tratan como subconsultas y éstas no están permitidas en la instrucción PRINT. Como resultado, el ejemplo siguiente devuelve un error:  
  
```  
DECLARE @x xml  
SET @x = '<root>Hello</root>'  
PRINT @x.value('/root[1]', 'varchar(20)') -- will not work because this is treated as a subquery (select top 1 col from table)   
```  
  
 Una solución es asignar primero el resultado del método **value()** a una variable de tipo **xml** y, después, especificar la variable en la consulta.  
  
```  
DECLARE @x xml  
DECLARE @c varchar(max)  
SET @x = '<root>Hello</root>'  
SET @c = @x.value('/root[1]', 'varchar(11)')  
PRINT @c                                                        
```  
  
## <a name="the-group-by-clause"></a>La cláusula GROUP BY   
 Los métodos del tipo de datos **xml** se tratan internamente como subconsultas. Como GROUP BY requiere un valor escalar y no permite agregados ni subconsultas, no se pueden especificar los métodos del tipo de datos **xml** en la cláusula GROUP BY. Una solución es llamar a una función definida por el usuario que utilice métodos XML en su interior.  
  
## <a name="reporting-errors"></a>La notificación de errores  
 Al informar de errores, los métodos del tipo de datos **xml** generan un único error con el formato siguiente:  
  
```  
Msg errorNumber, Level levelNumber, State stateNumber:  
XQuery [database.table.method]: description_of_error  
```  
  
 Por ejemplo:  
  
```  
Msg 2396, Level 16, State 1:  
XQuery [xmldb_test.xmlcol.query()]: Attribute may not appear outside of an element  
```  
  
## <a name="singleton-checks"></a>Comprobaciones de singleton  
 Los pasos de ubicación, los parámetros de funciones y los operadores que requieren singleton devolverán un error si el compilador no puede determinar si se garantiza un singleton en tiempo de ejecución. Este problema es frecuente con datos sin tipo. Por ejemplo, la búsqueda de un atributo requiere un elemento primario singleton. Es suficiente con un ordinal que seleccione un solo nodo primario. Es posible que la evaluación de una combinación **node()**-**value()** para extraer valores de atributos no requiera la especificación del ordinal. Esto se muestra en el ejemplo siguiente.  
  
### <a name="example-known-singleton"></a>Ejemplo: singleton conocido  
 En este ejemplo, el método **nodes()** genera una fila distinta para cada elemento <`book`>. El método **value()** que se evalúa en un nodo <`book`> extrae el valor de \@genre y, siendo un atributo, es un singleton.  
  
```  
SELECT nref.value('@genre', 'varchar(max)') LastName  
FROM   T CROSS APPLY xCol.nodes('//book') AS R(nref)  
```  
  
 El esquema XML se utiliza para comprobar el tipo del XML con tipo. Si se especifica un nodo como singleton en el esquema XML, el compilador usa esa información y no se produce ningún error. En caso contrario, se necesita un ordinal que seleccione un solo nodo. En particular, el uso de ejes descendant-or-self (//), como en /book//title, pierde inferencia de cardinalidad de singleton para el elemento \<title>, incluso si el esquema XML especifica que sea así. Por tanto, se debe volver a escribir como (/book//title)[1].  
  
 Es importante ser consciente de la diferencia entre //first-name[1] y (//first-name)[1] para la comprobación de tipos. La primera expresión devuelve una secuencia de nodos \<first-name> en la que cada nodo es el nodo \<first-name> que está más a la izquierda entre los de su mismo nivel. La última expresión devuelve el primer nodo singleton \<first-name> por orden de los documentos en la instancia XML.  
  
### <a name="example-using-value"></a>Ejemplo: utilizar value()  
 La siguiente consulta en una columna XML sin tipo da como resultado un error de compilación estático. Esto se debe a que **value()** espera un nodo singleton como primer argumento y el compilador no puede determinar si solo va a aparecer un nodo \<last-name> en tiempo de ejecución:  
  
```  
SELECT xCol.value('//author/last-name', 'nvarchar(50)') LastName  
FROM   T  
```  
  
 A continuación, se ofrece una solución que debe contemplar:  
  
```  
SELECT xCol.value('//author/last-name[1]', 'nvarchar(50)') LastName  
FROM   T  
```  
  
 No obstante, esta solución no resuelve el error, ya que pueden aparecer varios nodos <`author`> en cada instancia XML. Resulta útil volver a escribir lo siguiente:  
  
```  
SELECT xCol.value('(//author/last-name/text())[1]', 'nvarchar(50)') LastName  
FROM   T  
```  
  
 Esta consulta devuelve el valor del primer elemento `<last-name>` de cada instancia XML.  
  
## <a name="see-also"></a>Ver también  
 [Métodos del tipo de datos xml](../../t-sql/xml/xml-data-type-methods.md)  
  
  
