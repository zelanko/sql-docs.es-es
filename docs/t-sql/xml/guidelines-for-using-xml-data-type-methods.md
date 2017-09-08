---
title: "Directrices para usar métodos de tipo de datos xml | Documentos de Microsoft"
ms.custom: 
ms.date: 03/04/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e02d385d699c1c26d44f2e7383584416c2d9dd5c
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="guidelines-for-using-xml-data-type-methods"></a>Directrices para utilizar los métodos del tipo de datos xml
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Este tema describen las instrucciones para utilizar el **xml** métodos del tipo de datos.  
  
## <a name="the-print-statement"></a>La instrucción PRINT  
 El **xml** métodos del tipo de datos no se puede usar en la instrucción PRINT, como se muestra en el ejemplo siguiente. El **xml** métodos del tipo de datos se tratan como subconsultas y no se permiten subconsultas en la instrucción PRINT. Como resultado, el ejemplo siguiente devuelve un error:  
  
```  
DECLARE @x xml  
SET @x = '<root>Hello</root>'  
PRINT @x.value('/root[1]', 'varchar(20)') -- will not work because this is treated as a subquery (select top 1 col from table)   
```  
  
 Una solución consiste en asignar primero el resultado de la **value()** método a una variable de **xml** escriba y, a continuación, especifique la variable en la consulta.  
  
```  
DECLARE @x xml  
DECLARE @c varchar(max)  
SET @x = '<root>Hello</root>'  
SET @c = @x.value('/root[1]', 'varchar(11)')  
PRINT @c                                                        
```  
  
## <a name="the-group-by-clause"></a>La cláusula GROUP BY   
 El **xml** métodos del tipo de datos se tratan internamente como subconsultas. Dado que GROUP BY requiere un valor escalar y no permite agregados ni subconsultas, no se puede especificar el **xml** métodos del tipo de datos en la cláusula GROUP BY. Una solución es llamar a una función definida por el usuario que utilice métodos XML en su interior.  
  
## <a name="reporting-errors"></a>La notificación de errores  
 Al informar de errores, **xml** métodos del tipo de datos generan un único error con el siguiente formato:  
  
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
 Los pasos de ubicación, los parámetros de funciones y los operadores que requieren singleton devolverán un error si el compilador no puede determinar si se garantiza un singleton en tiempo de ejecución. Este problema es frecuente con datos sin tipo. Por ejemplo, la búsqueda de un atributo requiere un elemento primario singleton. Es suficiente con un ordinal que seleccione un solo nodo primario. La evaluación de una **node()**-**value()** combinación para extraer valores de atributo no puede requerir la especificación del ordinal. Esto se muestra en el ejemplo siguiente.  
  
### <a name="example-known-singleton"></a>Ejemplo: singleton conocido  
 En este ejemplo, el **nodos()** método genera una fila independiente para cada <`book`> elemento. El **value()** método que se evalúa en un <`book`> nodo extrae el valor de @genre y un atributo, es un singleton.  
  
```  
SELECT nref.value('@genre', 'varchar(max)') LastName  
FROM   T CROSS APPLY xCol.nodes('//book') AS R(nref)  
```  
  
 El esquema XML se utiliza para comprobar el tipo del XML con tipo. Si se especifica un nodo como singleton en el esquema XML, el compilador usa esa información y no se produce ningún error. En caso contrario, se necesita un ordinal que seleccione un solo nodo. En particular, el uso de eje descendant-or-self (/ /) eje, como se muestra en/book / / title, pierde inferencia de cardinalidad de singleton para el \<título > elemento, incluso si el esquema XML especifica que sea así. Por tanto, se debe volver a escribir como (/book//title)[1].  
  
 Es importante ser consciente de la diferencia entre //first-name[1] y (//first-name)[1] para la comprobación de tipos. La primera expresión devuelve una secuencia de \<first-name > nodos en el que cada nodo es el extremo izquierdo \<first-name > nodo entre sus elementos relacionados. La última expresión devuelve el primer singleton \<first-name > nodo en orden del documento en la instancia XML.  
  
### <a name="example-using-value"></a>Ejemplo: utilizar value()  
 La siguiente consulta en una columna XML sin tipo resulta estático, errores de compilación. Esto es porque **value()** espera un nodo singleton como el primer argumento y el compilador no puede determinar si un solo \<last-name > nodo se producirá en tiempo de ejecución:  
  
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
  
## <a name="see-also"></a>Vea también  
 [Métodos del tipo de datos xml](../../t-sql/xml/xml-data-type-methods.md)  
  
  
