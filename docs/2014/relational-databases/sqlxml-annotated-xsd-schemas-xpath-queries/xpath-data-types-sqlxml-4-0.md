---
title: Tipos de datos de XPath (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- mapping XDR types to XPath types [SQLXML]
- data types [XPath]
- arithmetic operators
- mapping data types [SQLXML]
- relational operators [SQLXML]
- node-set [SQLXML]
- data types [SQLXML], XPath
- XPath operators [SQLXML]
- XDR data type [SQLXML]
- equality operators [SQLXML]
- XPath conversions [SQLXML]
- converting data types [SQLXML]
- Boolean operators
- XPath queries [SQLXML], data types
- XPath data types [SQLXML]
- operators [SQLXML]
ms.assetid: a90374bf-406f-4384-ba81-59478017db68
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 3cd2e8af1630fed8dd996a951e904bef0266b300
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/01/2020
ms.locfileid: "82702983"
---
# <a name="xpath-data-types-sqlxml-40"></a>Tipos de datos de XPath (SQLXML 4.0)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], XPath y esquema XML (XSD) tienen tipos de datos muy diferentes. Por ejemplo, XPath no tiene tipos de datos enteros ni fecha, pero [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y XSD tienen muchos. XSD utiliza la precisión del nanosegundo para los valores de hora y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza a lo sumo una precisión de 1/300 de segundo. Por consiguiente, no siempre es posible asignar un tipo de datos a otro. Para obtener más información sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la asignación de tipos de datos a tipos de datos XSD, vea conversiones de tipos de [datos y la anotación sql: DataType &#40;SQLXML 4,0&#41;](../sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 XPath tiene tres tipos de datos: `string`, `number` y `boolean`. El tipo de datos `number` siempre es un IEEE 754 en punto flotante de doble precisión. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `float(53)` tipo de datos es el más cercano a XPath `number` . Sin embargo, `float(53)` no es exactamente IEEE 754. Por ejemplo, no se utiliza NaN (no es un número) ni infinito. Cualquier intento de convertir una cadena no numérica en `number` o de dividir por cero da como resultado un error.  
  
## <a name="xpath-conversions"></a>Conversiones de XPath  
 Al utilizar una consulta de XPath como `OrderDetail[@UnitPrice > "10.0"]`, las conversiones de tipos de datos implícitas y explícitas pueden cambiar el significado de la consulta de manera sutil. Por consiguiente, es importante entender cómo se implementan los tipos de datos de XPath. La especificación del lenguaje XPath, XML Path Language (XPath) versión 1,0 W3C propuesto Recomendación 8 de octubre de 1999, se puede encontrar en el sitio web de W3C en http://www.w3.org/TR/1999/PR-xpath-19991008.html .  
  
 Los operadores de XPath se dividen en cuatro categorías:  
  
-   Operadores booleanos (and, or).  
  
-   Operadores relacionales ( \< , >, \< =, >=)  
  
-   Operadores de igualdad (=, !=)  
  
-   Operadores aritméticos (+, -, *, div, mod)  
  
 Cada categoría de operador convierte de manera diferente los operandos. Los operadores de XPath convierten implícitamente los operandos si es necesario. Los operadores aritméticos convierten los operandos en `number` y generan un valor numérico. Los operadores booleanos convierten los operandos en `boolean` y generan un valor booleano. Los operadores relacionales y operadores de igualdad generan un valor booleano. Sin embargo, tienen reglas de conversión distintas en función de los tipos de datos originales de sus operandos, como se muestra en esta tabla.  
  
|Operando|Operador relacional|Operador de igualdad|  
|-------------|-------------------------|-----------------------|  
|Los dos operandos son conjuntos de nodos.|TRUE si y solo si hay un nodo en un conjunto y un nodo en el segundo conjunto tal que la comparación de sus valores `string` es TRUE.|Igual.|  
|Uno es un conjunto de nodos, el otro un `string`.|TRUE si y solo si hay un nodo en el conjunto de nodos tal que cuando se convierte en `number`, la comparación de éste con el `string` convertido en `number` es TRUE.|TRUE si y solo si hay un nodo en el conjunto de nodos tal que cuando se convierte en `string`, la comparación de éste con el `string` es TRUE.|  
|Uno es un conjunto de nodos, el otro un `number`.|TRUE si y solo si hay un nodo en el conjunto de nodos tal que cuando se convierte en `number`, la comparación de éste con el `number` es TRUE.|Igual.|  
|Uno es un conjunto de nodos, el otro un `boolean`.|TRUE si y solo si hay un nodo en el conjunto de nodos tal que cuando se convierte en `boolean` y luego en `number`, la comparación de éste con el `boolean` convertido en `number` es TRUE.|TRUE si y solo si hay un nodo en el conjunto de nodos tal que cuando se convierte en `boolean`, la comparación de éste con el `boolean` es TRUE.|  
|Ninguno es un conjunto de nodos.|Convierta los dos operandos en `number` y, a continuación, compare.|Convierta los dos operandos en un tipo común y, a continuación, compare. Convierta en `boolean` si es `boolean`, en `number` si es `number`; de lo contrario, convierta en `string`.|  
  
> [!NOTE]  
>  Dado que los operadores relacionales de XPath convierten siempre los operandos en `number`, las comparaciones de `string` no son posibles. Para incluir las comparaciones de fecha, SQL Server 2000 ofrece esta variación a la especificación de XPath: cuando un operador relacional compara un `string` con un `string`, un conjunto de nodos con un `string` o un conjunto de nodos con valores de cadena con un conjunto de nodos con valores de cadena, se realiza una comparación de `string` (no una comparación de `number`).  
  
## <a name="node-set-conversions"></a>Conversiones de conjunto de nodos  
 Las conversiones de conjunto de nodos no son siempre intuitivas. Un conjunto de nodos se convierte en un `string` tomando el valor de cadena de únicamente primer nodo del conjunto. Un conjunto de nodos se convierte en `number` convirtiéndolo en `string` y convirtiendo luego el `string` en `number`. Un conjunto de nodos se convierte en `boolean` probando su existencia.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no realiza la selección por posición en los conjuntos de nodos: por ejemplo, la consulta de XPath `Customer[3]` significa el tercer cliente; este tipo de selección por posición no se admite en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por consiguiente, las conversiones de conjunto de nodos en `string` o de conjunto de nodos en `number` descritas en la especificación de XPath no se implementan. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza la semántica "cualquiera" donde la especificación de XPath especifica la semántica "primero". Por ejemplo, según la especificación XPath de W3C, la consulta XPath `Order[OrderDetail/@UnitPrice > 10.0]` selecciona los pedidos con el primer **OrderDetail** que tiene un **UnitPrice** mayor que 10,0. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , esta consulta XPath selecciona los pedidos con cualquier **OrderDetail** que tenga un **UnitPrice** mayor que 10,0.  
  
 La conversión a `boolean` genera una prueba de existencia; por consiguiente, la consulta de XPath `Products[@Discontinued=true()]` es equivalente a la expresión de SQL "Products.Discontinued is not null", no a la expresión de SQL "Products.Discontinued = 1". Para hacer la consulta equivalente a la última expresión de SQL, primero convierta el conjunto de nodos a un tipo que no sea `boolean`, como `number`. Por ejemplo, `Products[number(@Discontinued) = true()]`.  
  
 Dado que la mayoría de los operadores están definidos para ser TRUE si son TRUE para cualquiera o uno de los nodos del conjunto de nodos, estas operaciones siempre se evalúan como FALSE si el conjunto de nodos está vacío. Así, si A está vacío, `A = B` y `A != B` son FALSE y `not(A=B)` y `not(A!=B)` son TRUE.  
  
 Normalmente, un atributo o elemento que se asigna a una columna existe si el valor de esa columna de la base de datos no es `null`. Los elementos que se asignan a filas existen si cualquiera de sus elementos secundarios existe.  
  
> [!NOTE]  
>  Los elementos anotados con `is-constant` siempre existen. Por consiguiente, los predicados XPath no se pueden utilizar en los elementos `is-constant`.  
  
 Cuando un conjunto de nodos se convierte en `string` o `number`, su tipo XDR (si existe) se inspecciona en el esquema anotado y ese tipo se utiliza para determinar la conversión que se requiere.  
  
## <a name="mapping-xdr-data-types-to-xpath-data-types"></a>Asignar tipos de datos de XDR a tipos de datos de XPath  
 El tipo de datos XPath de un nodo se deriva del tipo de datos XDR en el esquema, tal y como se muestra en la tabla siguiente (el nodo **EmployeeID** se utiliza con fines ilustrativos).  
  
|Tipo de datos XDR|Tipo de datos de XPath<br /><br /> equivalente|Conversión de SQL Server utilizada|  
|-------------------|------------------------------------|--------------------------------|  
|Nonebin.base64bin.hex|N/D|NingunaEmployeeID|  
|booleano|booleano|CONVERT (bit, IdEmpleado)|  
|number, int, float,i1, i2, i4, i8,r4, r8ui1, ui2, ui4, ui8|número|CONVERT(float(53), EmployeeID)|  
|id, idref, idrefsentity, entities, enumerationnotation, nmtoken, nmtokens, chardate, Timedate, Time.tz, string, uri, uuid|string|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|fixed14.4|N/D (no hay ningún tipo de datos de XPath que sea equivalente al tipo de datos fixed14.4 de XDR)|CONVERT(money, EmployeeID)|  
|fecha|string|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|time<br /><br /> time.tz|string|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
 Las conversiones de fecha y hora están diseñadas para funcionar si el valor se almacena en la base de datos mediante el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `datetime` tipo de datos o `string` . Tenga en cuenta que el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] `datetime` tipo de datos no utiliza `timezone` y tiene una precisión menor que el `time` tipo de datos XML. Para incluir el tipo de datos `timezone` o una precisión adicional, almacene los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utilizando un tipo `string`.  
  
 Cuando un nodo se convierte del tipo de datos de XDR al tipo de datos de XPath, a veces es necesaria una conversión adicional (de un tipo de datos de XPath a otro tipo de datos de XPath). Por ejemplo, considere esta consulta de XPath:  
  
```  
(@m + 3) = 4  
```  
  
 Si @m es del `fixed14.4` tipo de datos XDR, la conversión del tipo de datos XDR al tipo de datos XPath se realiza mediante:  
  
```  
CONVERT(money, m)  
```  
  
 En esta conversión, el nodo `m` se convierte de `fixed14.4` en `money`. Sin embargo, si se agrega el valor 3, se requiere una conversión adicional:  
  
```  
CONVERT(float(CONVERT(money, m))  
```  
  
 La expresión de XPath se evalúa como:  
  
```  
CONVERT(float(CONVERT(money, m)) + CONVERT(float(53), 3) = CONVERT(float(53), 3)  
```  
  
 Como se muestra en la tabla siguiente, ésta es la misma conversión que se aplica para otras expresiones de XPath (como expresiones de literales o compuestas).  
  
||||||  
|-|-|-|-|-|  
||X es desconocido|X es de tipo `string`|X es de tipo `number`|X es de tipo `boolean`|  
|string(X)|CONVERT (nvarchar(4000), X, 126)|-|CONVERT (nvarchar(4000), X, 126)|CASE WHEN X THEN N'true' ELSE N'false' END|  
|number(X)|CONVERT (float(53), X)|CONVERT (float(53), X)|-|CASE WHEN X THEN 1 ELSE 0 END|  
|boolean(X)|-|LEN (X) > 0|X != 0|-|  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-convert-a-data-type-in-an-xpath-query"></a>A. Convertir un tipo de datos en una consulta de XPath  
 En la siguiente consulta XPath especificada en un esquema XSD anotado, la consulta selecciona todos los nodos **Employee** con el valor del atributo **EmployeeID** de E-1, donde "E-" es el prefijo especificado utilizando la `sql:id-prefix` anotación.  
  
 `Employee[@EmployeeID="E-1"]`  
  
 El predicado de la consulta es equivalente a la expresión de SQL:  
  
 `N'E-' + CONVERT(nvarchar(4000), Employees.EmployeeID, 126) = N'E-1'`  
  
 Dado que **EmployeeID** es uno de los `id` valores de tipo de datos ( `idref` , `idrefs` ,,, etc. `nmtoken` `nmtokens` ) en el esquema XSD, **EmployeeID** se convierte al `string` tipo de datos XPath mediante las reglas de conversión descritas anteriormente.  
  
 `CONVERT(nvarchar(4000), Employees.EmployeeID, 126)`  
  
 El prefijo "E -" se agrega a la cadena y el resultado se compara entonces con `N'E-1'`.  
  
### <a name="b-perform-several-data-type-conversions-in-an-xpath-query"></a>B. Realizar varias conversiones de tipos de datos en una consulta de XPath  
 Considere esta consulta especificada de XPath en un esquema XSD anotado: `OrderDetail[@UnitPrice * @OrderQty > 98]`  
  
 Esta consulta XPath devuelve todos los elementos de la ** \<>OrderDetail** que satisfacen el predicado `@UnitPrice * @OrderQty > 98` . Si **UnitPrice** se anota con un `fixed14.4` tipo de datos en el esquema anotado, este predicado es equivalente a la expresión SQL:  
  
 `CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice)) * CONVERT(float(53), OrderDetail.OrderQty) > CONVERT(float(53), 98)`  
  
 Para convertir los valores de la consulta de XPath, la primera conversión convierte el tipo de datos de XDR al tipo de datos de XPath. Dado que el tipo de datos XSD de **UnitPrice** es `fixed14.4` , tal y como se describe en la tabla anterior, esta es la primera conversión que se usa:  
  
```  
CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 Dado que los operadores aritméticos convierten los operandos al tipo de datos `number` de XPath, se aplica la segunda conversión (de un tipo de datos de XPath a otro tipo de datos de XPath) en la que el valor se convierte a `float(53)` (`float(53)` se aproxima al tipo de datos `number` de XPath):  
  
```  
CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 Suponiendo que el atributo **OrderQty** no tiene ningún tipo de datos XSD, **OrderQty** se convierte en un `number` tipo de datos de XPath en una sola conversión:  
  
```  
CONVERT(float(53), OrderDetail.OrderQty)  
```  
  
 De igual forma, el valor 98 se convierte en el tipo de datos `number` de XPath:  
  
```  
CONVERT(float(53), 98)  
```  
  
> [!NOTE]  
>  Si el tipo de datos de XSD utilizado en el esquema es incompatible con el tipo de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] subyacente de la base de datos o si se realiza una conversión de tipo de datos de XPath imposible, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede devolver un error. Por ejemplo, si el atributo **EmployeeID** se anota con la `id-prefix` anotación, el XPath `Employee[@EmployeeID=1]` genera un error, porque **EmployeeID** tiene la `id-prefix` anotación y no se puede convertir en `number` .  
  
  
