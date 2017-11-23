---
title: Tipos de datos de XPath (SQLXML 4.0) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: sqlxml
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-xml
ms.tgt_pltfrm: 
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
caps.latest.revision: "27"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d028ddf781edba7cc610966facc2e08b6bba58bb
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="xpath-data-types-sqlxml-40"></a>Tipos de datos de XPath (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)][!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], XPath y esquema XML (XSD) tienen tipos de datos muy diferentes. Por ejemplo, XPath no tiene tipos de datos enteros ni fecha, pero [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y XSD tienen muchos. XSD utiliza la precisión del nanosegundo para los valores de hora y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza a lo sumo una precisión de 1/300 de segundo. Por consiguiente, no siempre es posible asignar un tipo de datos a otro. Para obtener más información sobre la asignación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de datos a tipos de datos XSD, vea [conversiones de tipos de datos y la anotación SQL: DataType &#40; SQLXML 4.0 &#41; ](../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 XPath tiene tres tipos de datos: **cadena**, **número**, y **booleano**. El **número** tipo de datos siempre es un IEEE 754 doble punto flotante de precisión. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **float (53)** tipo de datos es la más parecida a XPath **número**. Sin embargo, **float (53)** no es exactamente IEEE 754. Por ejemplo, no se utiliza NaN (no es un número) ni infinito. Cualquier intento de convertir una cadena no numérica en **número** y dividir por cero da como resultado un error.  
  
## <a name="xpath-conversions"></a>Conversiones de XPath  
 Al utilizar una consulta de XPath como `OrderDetail[@UnitPrice > "10.0"]`, las conversiones de tipos de datos implícitas y explícitas pueden cambiar el significado de la consulta de manera sutil. Por consiguiente, es importante entender cómo se implementan los tipos de datos de XPath. Puede encontrar la especificación de lenguaje XPath, XML Path Language (XPath) version 1.0 W3C Proposed Recommendation 8 October 1999 (XML Path Language (XPath) versión 1.0, recomendación propuesta de W3W el 8 de octubre de 1999), en el sitio web de W3C en http://www.w3.org/TR/1999/PR-xpath-19991008.html.  
  
 Los operadores de XPath se dividen en cuatro categorías:  
  
-   Operadores booleanos (and, or).  
  
-   Operadores relacionales (\<, >, \<=, > =)  
  
-   Operadores de igualdad (=, !=)  
  
-   Operadores aritméticos (+, -, *, div, mod)  
  
 Cada categoría de operador convierte de manera diferente los operandos. Los operadores de XPath convierten implícitamente los operandos si es necesario. Operadores aritméticos convierten los operandos en **número**y el resultado en un valor numérico. Operadores booleanos convierten los operandos en **booleano**y el resultado en un valor booleano. Los operadores relacionales y operadores de igualdad generan un valor booleano. Sin embargo, tienen reglas de conversión distintas en función de los tipos de datos originales de sus operandos, como se muestra en esta tabla.  
  
|Operando|Operador relacional|Operador de igualdad|  
|-------------|-------------------------|-----------------------|  
|Los dos operandos son conjuntos de nodos.|TRUE si y solo si hay un nodo en un conjunto y un nodo en el segundo conjunto de forma que la comparación de sus **cadena** valores es TRUE.|Igual.|  
|Uno es un conjunto de nodos, el otro un **cadena**.|TRUE si y solo si hay un nodo en el conjunto de nodos tal que cuando se convierte en **número**, la comparación de éste con el **cadena** convertido en **número** es TRUE.|TRUE si y solo si hay un nodo en el conjunto de nodos tal que cuando se convierte en **cadena**, la comparación de éste con el **cadena** es TRUE.|  
|Uno es un conjunto de nodos, el otro un **número**.|TRUE si y solo si hay un nodo en el conjunto de nodos tal que cuando se convierte en **número**, la comparación de éste con el **número** es TRUE.|Igual.|  
|Uno es un conjunto de nodos, el otro un **booleano**.|TRUE si y solo si hay un nodo en el conjunto de nodos tal que cuando se convierte en **booleano** y, a continuación, **número**, la comparación de éste con el **booleano** convertido en **número** es TRUE.|TRUE si y solo si hay un nodo en el conjunto de nodos tal que cuando se convierte en **booleano**, la comparación de éste con el **booleano** es TRUE.|  
|Ninguno es un conjunto de nodos.|Convierta los dos operandos a **número** y, a continuación, comparar.|Convierta los dos operandos en un tipo común y, a continuación, compare. Convertir en **booleano** si se da alguna **booleano**, **número** si se da alguna **número**; en caso contrario, convertir en **cadena**.|  
  
> [!NOTE]  
>  Dado que los operadores relacionales de XPath convierten siempre los operandos en **número**, **cadena** comparaciones no son posibles. Para incluir las comparaciones de fecha, SQL Server 2000 ofrece esta variación a la especificación de XPath: cuando un operador relacional compara un **cadena** a una **cadena**, un conjunto de nodos a un **cadena**, o un conjunto de nodos con valores de cadena a un valor de cadena conjunto de nodos, un **cadena** comparación (no un **número** comparación) se lleva a cabo.  
  
## <a name="node-set-conversions"></a>Conversiones de conjunto de nodos  
 Las conversiones de conjunto de nodos no son siempre intuitivas. Un conjunto de nodos se convierte en una **cadena** tomando el valor de cadena de solo el primer nodo en el conjunto. Un conjunto de nodos se convierte en **número** mediante la conversión a **cadena**y, a continuación, convertir **cadena** a **número**. Un conjunto de nodos se convierte en **booleano** probando su existencia.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no realiza la selección por posición en los conjuntos de nodos: por ejemplo, la consulta de XPath `Customer[3]` significa el tercer cliente; este tipo de selección por posición no se admite en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por lo tanto, el nodo-establecer-a-**cadena** o nodo-establecer-a-**número** conversiones tal como se describe en la especificación de XPath no se implementan. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza la semántica "cualquiera" donde la especificación de XPath especifica la semántica "primero". Por ejemplo, basándose en la especificación XPath de W3C, la consulta XPath `Order[OrderDetail/@UnitPrice > 10.0]` selecciona los pedidos con el primer **OrderDetail** que tiene un **UnitPrice** mayor que 10.0. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta consulta XPath selecciona los pedidos con cualquier **OrderDetail** que tiene un **UnitPrice** mayor que 10.0.  
  
 Conversión a **booleano** genera una existencia prueba; por lo tanto, la consulta XPath `Products[@Discontinued=true()]` es equivalente a la expresión SQL "Products.Discontinued is not null", no la expresión de SQL "Products.Discontinued = 1". Para hacer que la consulta equivalente a la última expresión de SQL, primero convierta el conjunto de nodos a no**booleano** escriba, por ejemplo, **número**. Por ejemplo, `Products[number(@Discontinued) = true()]`.  
  
 Dado que la mayoría de los operadores están definidos para ser TRUE si son TRUE para cualquiera o uno de los nodos del conjunto de nodos, estas operaciones siempre se evalúan como FALSE si el conjunto de nodos está vacío. Así, si A está vacío, `A = B` y `A != B` son FALSE y `not(A=B)` y `not(A!=B)` son TRUE.  
  
 Normalmente, un atributo o elemento que se asigna a una columna existe si el valor de esa columna en la base de datos no es **null**. Los elementos que se asignan a filas existen si cualquiera de sus elementos secundarios existe.  
  
> [!NOTE]  
>  Elementos anotados con **constante es** siempre existe. Por lo tanto, no se puede usar XPath predicados en **constante es** elementos.  
  
 Cuando un conjunto de nodos se convierte en **cadena** o **número**, su tipo XDR (si existe) se inspecciona en el esquema anotado y ese tipo se utiliza para determinar la conversión necesaria.  
  
## <a name="mapping-xdr-data-types-to-xpath-data-types"></a>Asignar tipos de datos de XDR a tipos de datos de XPath  
 El tipo de datos de XPath de un nodo se deriva del tipo de datos XDR en el esquema, como se muestra en la tabla siguiente (el nodo **EmployeeID** se utiliza a modo de ilustración).  
  
|Tipo de datos XDR|Tipo de datos de XPath<br /><br /> equivalente|Conversión de SQL Server utilizada|  
|-------------------|------------------------------------|--------------------------------|  
|Nonebin.base64bin.hex|N/D|NoneEmployeeID|  
|boolean|boolean|CONVERT (bit, IdEmpleado)|  
|number, int, float,i1, i2, i4, i8,r4, r8ui1, ui2, ui4, ui8|number|CONVERT(float(53), EmployeeID)|  
|id, idref, idrefsentity, entities, enumerationnotation, nmtoken, nmtokens, chardate, Timedate, Time.tz, string, uri, uuid|string|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|fixed14.4|N/D (no hay ningún tipo de datos de XPath que sea equivalente al tipo de datos fixed14.4 de XDR)|CONVERT(money, EmployeeID)|  
|date|string|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|time<br /><br /> time.tz|string|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
 Las conversiones de fecha y hora están diseñadas para funcionar si el valor se almacena en la base de datos mediante la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** tipo de datos o un **cadena**. Tenga en cuenta que la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **datetime** tipo de datos no utiliza **zona horaria** y tiene una precisión menor que el XML **tiempo** tipo de datos. Para incluir la **zona horaria** tipo de datos o una precisión adicional, almacene los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con un **cadena** tipo.  
  
 Cuando un nodo se convierte del tipo de datos de XDR al tipo de datos de XPath, a veces es necesaria una conversión adicional (de un tipo de datos de XPath a otro tipo de datos de XPath). Por ejemplo, considere esta consulta de XPath:  
  
```  
(@m + 3) = 4  
```  
  
 Si @m reviste la **fixed14.4** tipo de datos XDR, la conversión del tipo de datos XDR al tipo de datos se realiza mediante el XPath:  
  
```  
CONVERT(money, m)  
```  
  
 En esta conversión, el nodo `m` se convierten de **fixed14.4** a **dinero**. Sin embargo, si se agrega el valor 3, se requiere una conversión adicional:  
  
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
||X es desconocido|X es **cadena**|X es **número**|X es **booleano**|  
|string(X)|CONVERT (nvarchar(4000), X, 126)|-|CONVERT (nvarchar(4000), X, 126)|CASE WHEN X THEN N'true' ELSE N'false' END|  
|number(X)|CONVERT (float(53), X)|CONVERT (float(53), X)|-|CASE WHEN X THEN 1 ELSE 0 END|  
|boolean(X)|-|LEN(X) > 0|X != 0|-|  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-convert-a-data-type-in-an-xpath-query"></a>A. Convertir un tipo de datos en una consulta de XPath  
 En la siguiente consulta XPath especificada en un esquema XSD anotado, la consulta selecciona todos los **empleado** nodos con el **EmployeeID** valor de atributo de e-1, donde "E-" es el prefijo especificado utilizando el **SQL: ID-prefijo** anotación.  
  
 `Employee[@EmployeeID="E-1"]`  
  
 El predicado de la consulta es equivalente a la expresión de SQL:  
  
 `N'E-' + CONVERT(nvarchar(4000), Employees.EmployeeID, 126) = N'E-1'`  
  
 Dado que **EmployeeID** es uno de los **identificador** (**idref**, **idrefs**, **nmtoken**,  **NMTOKENS**, y así sucesivamente) valores de tipo de datos en el esquema XSD, **EmployeeID** se convierte en el **cadena** tipo de datos de XPath usando las reglas de conversión descritas anteriormente.  
  
 `CONVERT(nvarchar(4000), Employees.EmployeeID, 126)`  
  
 El prefijo "E -" se agrega a la cadena y el resultado se compara entonces con `N'E-1'`.  
  
### <a name="b-perform-several-data-type-conversions-in-an-xpath-query"></a>B. Realizar varias conversiones de tipos de datos en una consulta de XPath  
 Considere esta consulta especificada de XPath en un esquema XSD anotado: `OrderDetail[@UnitPrice * @OrderQty > 98]`  
  
 Esta consulta XPath devuelve todos los  **\<OrderDetail >** elementos que satisfacen el predicado `@UnitPrice * @OrderQty > 98`. Si el **UnitPrice** se anota con un **fixed14.4** tipo de datos en el esquema anotado, este predicado es equivalente a la expresión SQL:  
  
 `CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice)) * CONVERT(float(53), OrderDetail.OrderQty) > CONVERT(float(53), 98)`  
  
 Para convertir los valores de la consulta de XPath, la primera conversión convierte el tipo de datos de XDR al tipo de datos de XPath. Porque el tipo de datos XSD de **UnitPrice** es **fixed14.4**, tal como se describe en la tabla anterior, se trata de la primera conversión que se utiliza:  
  
```  
CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 Dado que los operadores aritméticos convierten los operandos en la **número** tipo de datos de XPath, la segunda conversión (de un tipo de datos XPath a otro tipo de datos de XPath) se aplica en el que el valor se convierte en **float (53)**  (**float (53)** está cerca de la expresión XPath **número** tipo de datos):  
  
```  
CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 Suponiendo que la **OrderQty** atributo no tiene ningún tipo de datos XSD, **OrderQty** se convierte en una **número** tipo de datos de XPath en una conversión única:  
  
```  
CONVERT(float(53), OrderDetail.OrderQty)  
```  
  
 De forma similar, el valor 98 se convierte en el **número** tipo de datos de XPath:  
  
```  
CONVERT(float(53), 98)  
```  
  
> [!NOTE]  
>  Si el tipo de datos de XSD utilizado en el esquema es incompatible con el tipo de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] subyacente de la base de datos o si se realiza una conversión de tipo de datos de XPath imposible, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede devolver un error. Por ejemplo, si la **EmployeeID** se anota con el atributo **id-prefix** anotación, la expresión XPath `Employee[@EmployeeID=1]` genera un error, porque **EmployeeID** tiene el **id-prefix** anotación y no se puede convertir a **número**.  
  
  
