---
title: Tipos de datos de XPath (SQLXML)
description: Obtenga información sobre los tipos de datos de XPath en SQLXML 4,0 y cómo se comparan con los tipos de datos de Microsoft SQL Server y esquema XML (XSD).
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
author: MightyPen
ms.author: genemi
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 724290f48b0f33d586a797629766b36bae49ddb6
ms.sourcegitcommit: 75f767c7b1ead31f33a870fddab6bef52f99906b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/28/2020
ms.locfileid: "87332644"
---
# <a name="xpath-data-types-sqlxml-40"></a>Tipos de datos de XPath (SQLXML 4.0)
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], XPath y esquema XML (XSD) tienen tipos de datos muy diferentes. Por ejemplo, XPath no tiene tipos de datos enteros ni fecha, pero [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y XSD tienen muchos. XSD utiliza la precisión del nanosegundo para los valores de hora y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza a lo sumo una precisión de 1/300 de segundo. Por consiguiente, no siempre es posible asignar un tipo de datos a otro. Para obtener más información sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la asignación de tipos de datos a tipos de datos XSD, vea conversiones de tipos de [datos y la anotación sql: DataType &#40;SQLXML 4,0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 XPath tiene tres tipos de datos: **cadena**, **número**y **booleano**. El tipo de datos **Number** siempre es un punto flotante de doble precisión IEEE 754. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos **float (53)** es el más cercano al **número**de XPath. Sin embargo, **float (53)** no es exactamente IEEE 754. Por ejemplo, no se utiliza NaN (no es un número) ni infinito. Si se intenta convertir una cadena no numérica en **número** y se intenta dividir por cero, se producirá un error.  
  
## <a name="xpath-conversions"></a>Conversiones de XPath  
 Al utilizar una consulta de XPath como `OrderDetail[@UnitPrice > "10.0"]`, las conversiones de tipos de datos implícitas y explícitas pueden cambiar el significado de la consulta de manera sutil. Por consiguiente, es importante entender cómo se implementan los tipos de datos de XPath. La especificación del lenguaje XPath, XML Path Language (XPath) versión 1,0 W3C propuesto Recomendación 8 de octubre de 1999, se puede encontrar en el sitio web de W3C en http://www.w3.org/TR/1999/PR-xpath-19991008.html .  
  
 Los operadores de XPath se dividen en cuatro categorías:  
  
-   Operadores booleanos (and, or).  
  
-   Operadores relacionales ( \<, > , \<=, > =)  
  
-   Operadores de igualdad (=, !=)  
  
-   Operadores aritméticos (+, -, *, div, mod)  
  
 Cada categoría de operador convierte de manera diferente los operandos. Los operadores de XPath convierten implícitamente los operandos si es necesario. Los operadores aritméticos convierten los operandos en **números**y dan lugar a un valor numérico. Los operadores booleanos convierten sus operandos en **booleanos**y dan como resultado un valor booleano. Los operadores relacionales y operadores de igualdad generan un valor booleano. Sin embargo, tienen reglas de conversión distintas en función de los tipos de datos originales de sus operandos, como se muestra en esta tabla.  
  
|Operando|Operador relacional|Operador de igualdad|  
|-------------|-------------------------|-----------------------|  
|Los dos operandos son conjuntos de nodos.|TRUE si y solo si hay un nodo en un conjunto y un nodo en el segundo conjunto de modo que la comparación de sus valores de **cadena** sea true.|Igual.|  
|Uno es un conjunto de nodos y el otro es una **cadena**.|TRUE si y solo si hay un nodo en el conjunto de nodos tal que cuando se convierte en **Number**, la comparación de éste con la **cadena** convertida en **Number** es true.|TRUE si y solo si hay un nodo en el conjunto de nodos tal que cuando se convierte en **cadena**, la comparación de este con la **cadena** es true.|  
|Uno es un conjunto de nodos, el otro **número**.|TRUE si y solo si hay un nodo en el conjunto de nodos tal que cuando se convierte en **número**, la comparación de éste con el **número** es true.|Igual.|  
|Uno es un conjunto de nodos y el otro es un **valor booleano**.|TRUE si y solo si hay un nodo en el conjunto de nodos tal que cuando se convierte en un **valor booleano** y luego en un **número**, la comparación de éste con el **valor BOOLEANO** convertido en **número** es true.|TRUE si y solo si hay un nodo en el conjunto de nodos tal que cuando se convierte en un **valor booleano**, la comparación de éste con el **valor booleano** es true.|  
|Ninguno es un conjunto de nodos.|Convierta los dos operandos en **Number** y, a continuación, compare.|Convierta los dos operandos en un tipo común y, a continuación, compare. Se convierte en un **valor booleano** si es **booleano**, **número** si es **número**; de lo contrario, convertir en **cadena**.|  
  
> [!NOTE]  
>  Dado que los operadores relacionales XPath convierten siempre sus operandos en un **número**, no es posible realizar comparaciones de **cadenas** . Para incluir las comparaciones de fecha, SQL Server 2000 ofrece esta variación a la especificación XPath: cuando un operador relacional compara una **cadena** con una **cadena, un**conjunto de nodos en una **cadena**o un conjunto de nodos con valores de cadena en un conjunto de nodos con valores de cadena, se realiza una comparación de **cadenas** (no una comparación de **números** ).  
  
## <a name="node-set-conversions"></a>Conversiones de conjunto de nodos  
 Las conversiones de conjunto de nodos no son siempre intuitivas. Un conjunto de nodos se convierte en una **cadena** tomando el valor de cadena solo del primer nodo del conjunto. Un conjunto de nodos se convierte en **número** convirtiéndolo en una **cadena**y, a continuación, convirtiendo la **cadena** en un **número**. Un conjunto de nodos se convierte en un **valor booleano** comprobando su existencia.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no realiza la selección por posición en los conjuntos de nodos: por ejemplo, la consulta de XPath `Customer[3]` significa el tercer cliente; este tipo de selección por posición no se admite en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por tanto, no se implementan las conversiones de conjunto de nodos a**cadena** o de conjunto de nodos en**número** tal y como se describe en la especificación de XPath. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza la semántica "cualquiera" donde la especificación de XPath especifica la semántica "primero". Por ejemplo, según la especificación XPath de W3C, la consulta XPath `Order[OrderDetail/@UnitPrice > 10.0]` selecciona los pedidos con el primer **OrderDetail** que tiene un **UnitPrice** mayor que 10,0. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , esta consulta XPath selecciona los pedidos con cualquier **OrderDetail** que tenga un **UnitPrice** mayor que 10,0.  
  
 La conversión a un **valor booleano** genera una prueba de existencia; por lo tanto, la consulta XPath `Products[@Discontinued=true()]` es equivalente a la expresión SQL "Products. Discontinued is not null", no a la expresión SQL "Products. Discontinued = 1". Para que la consulta sea equivalente a la última expresión SQL, convierta primero el conjunto de nodos a un tipo no**booleano** , como **Number**. Por ejemplo, `Products[number(@Discontinued) = true()]`.  
  
 Dado que la mayoría de los operadores están definidos para ser TRUE si son TRUE para cualquiera o uno de los nodos del conjunto de nodos, estas operaciones siempre se evalúan como FALSE si el conjunto de nodos está vacío. Así, si A está vacío, `A = B` y `A != B` son FALSE y `not(A=B)` y `not(A!=B)` son TRUE.  
  
 Normalmente, un atributo o elemento que se asigna a una columna existe si el valor de esa columna en la base de datos no es **null**. Los elementos que se asignan a filas existen si cualquiera de sus elementos secundarios existe.  
  
> [!NOTE]  
>  Los elementos anotados con **is-Constant** siempre existen. Por consiguiente, los predicados XPath no se pueden usar en elementos **is-Constant** .  
  
 Cuando un conjunto de nodos se convierte en **cadena** o **número**, su tipo XDR (si existe) se inspecciona en el esquema anotado y ese tipo se utiliza para determinar la conversión que se requiere.  
  
## <a name="mapping-xdr-data-types-to-xpath-data-types"></a>Asignar tipos de datos de XDR a tipos de datos de XPath  
 El tipo de datos XPath de un nodo se deriva del tipo de datos XDR en el esquema, tal y como se muestra en la tabla siguiente (el nodo **EmployeeID** se utiliza con fines ilustrativos).  
  
|Tipo de datos XDR|Tipo de datos de XPath<br /><br /> equivalente|Conversión de SQL Server utilizada|  
|-------------------|------------------------------------|--------------------------------|  
|Nonebin.base64bin.hex|N/D|NingunaEmployeeID|  
|boolean|boolean|CONVERT (bit, IdEmpleado)|  
|number, int, float,i1, i2, i4, i8,r4, r8ui1, ui2, ui4, ui8|number|CONVERT(float(53), EmployeeID)|  
|id, idref, idrefsentity, entities, enumerationnotation, nmtoken, nmtokens, chardate, Timedate, Time.tz, string, uri, uuid|string|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|fixed14.4|N/D (no hay ningún tipo de datos de XPath que sea equivalente al tipo de datos fixed14.4 de XDR)|CONVERT(money, EmployeeID)|  
|date|string|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|time<br /><br /> time.tz|string|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
 Las conversiones de fecha y hora están diseñadas para funcionar si el valor se almacena en la base de datos mediante el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos **DateTime** o una **cadena**. Tenga en cuenta que el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de datos **DateTime** no usa **TimeZone** y tiene una precisión menor que el tipo de datos XML **Time** . Para incluir el tipo de datos **TimeZone** o una precisión adicional, almacene los datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando un tipo de **cadena** .  
  
 Cuando un nodo se convierte del tipo de datos de XDR al tipo de datos de XPath, a veces es necesaria una conversión adicional (de un tipo de datos de XPath a otro tipo de datos de XPath). Por ejemplo, considere esta consulta de XPath:  
  
```  
(@m + 3) = 4  
```  
  
 Si @m es del tipo de datos XDR **fijo** , la conversión del tipo de datos XDR al tipo de datos XPath se realiza mediante:  
  
```  
CONVERT(money, m)  
```  
  
 En esta conversión, el nodo `m` se convierte de **fijo 14,4** a **Money**. Sin embargo, si se agrega el valor 3, se requiere una conversión adicional:  
  
```  
CONVERT(float(CONVERT(money, m))  
```  
  
 La expresión de XPath se evalúa como:  
  
```  
CONVERT(float(CONVERT(money, m)) + CONVERT(float(53), 3) = CONVERT(float(53), 3)  
```  
  
 Como se muestra en la tabla siguiente, ésta es la misma conversión que se aplica para otras expresiones de XPath (como expresiones de literales o compuestas).  
  
|   | X es desconocido | X es una cadena | X es el número | X es un valor booleano |
| - | ------------ | ----------- | ----------- | ------------ |
| **string(X)** |CONVERT (nvarchar(4000), X, 126)|-|CONVERT (nvarchar(4000), X, 126)|CASE WHEN X THEN N'true' ELSE N'false' END|  
| **number(X)** |CONVERT (float(53), X)|CONVERT (float(53), X)|-|CASE WHEN X THEN 1 ELSE 0 END|  
| **boolean(X)** |-|LEN (X) > 0|X != 0|-|  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-convert-a-data-type-in-an-xpath-query"></a>A. Convertir un tipo de datos en una consulta de XPath  
 En la siguiente consulta XPath especificada en un esquema XSD anotado, la consulta selecciona todos los nodos **Employee** con el valor del atributo **EmployeeID** de E-1, donde "E-" es el prefijo especificado mediante la anotación **SQL: id-prefix** .  
  
 `Employee[@EmployeeID="E-1"]`  
  
 El predicado de la consulta es equivalente a la expresión de SQL:  
  
 `N'E-' + CONVERT(nvarchar(4000), Employees.EmployeeID, 126) = N'E-1'`  
  
 Dado **que EmployeeID** es uno de los valores de tipo de datos ID (**idref**, **IDREFS**, **NMTOKEN**, **NMTOKENS**, etc **.** ) en el esquema XSD, **EmployeeID** se convierte al tipo de datos XPath de **cadena** mediante las reglas de conversión descritas anteriormente.  
  
 `CONVERT(nvarchar(4000), Employees.EmployeeID, 126)`  
  
 El prefijo "E -" se agrega a la cadena y el resultado se compara entonces con `N'E-1'`.  
  
### <a name="b-perform-several-data-type-conversions-in-an-xpath-query"></a>B. Realizar varias conversiones de tipos de datos en una consulta de XPath  
 Considere esta consulta especificada de XPath en un esquema XSD anotado: `OrderDetail[@UnitPrice * @OrderQty > 98]`  
  
 Esta consulta XPath devuelve todos los **\<OrderDetail>** elementos que satisfacen el predicado `@UnitPrice * @OrderQty > 98` . Si el **UnitPrice** está anotado con un tipo de datos de **14,4 fijo** en el esquema anotado, este predicado es equivalente a la expresión SQL:  
  
 `CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice)) * CONVERT(float(53), OrderDetail.OrderQty) > CONVERT(float(53), 98)`  
  
 Para convertir los valores de la consulta de XPath, la primera conversión convierte el tipo de datos de XDR al tipo de datos de XPath. Dado que el tipo de datos XSD de **UnitPrice** es **fijo 14.4**, tal y como se describe en la tabla anterior, esta es la primera conversión que se usa:  
  
```  
CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 Dado que los operadores aritméticos convierten sus operandos en el tipo de datos XPath de **número** , se aplica la segunda conversión (de un tipo de datos de XPath a otro tipo de datos de XPath) en la que el valor se convierte en **float (53)** (**float (53)** está cerca del tipo de datos **Number** de XPath):  
  
```  
CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 Suponiendo que el atributo **OrderQty** no tiene ningún tipo de datos XSD, **OrderQty** se convierte en un tipo de datos XPath **numérico** en una sola conversión:  
  
```  
CONVERT(float(53), OrderDetail.OrderQty)  
```  
  
 Del mismo modo, el valor 98 se convierte al tipo de datos XPath **Number** :  
  
```  
CONVERT(float(53), 98)  
```  
  
> [!NOTE]  
>  Si el tipo de datos de XSD utilizado en el esquema es incompatible con el tipo de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] subyacente de la base de datos o si se realiza una conversión de tipo de datos de XPath imposible, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede devolver un error. Por ejemplo, si el **atributo EmployeeID** se anota con la anotación **id-prefix** , XPath `Employee[@EmployeeID=1]` genera un error, porque **EmployeeID** tiene la anotación **id-prefix** y no se puede convertir en **Number**.  
  
  
