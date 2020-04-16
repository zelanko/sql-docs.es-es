---
title: Tipos de datos XPath (SQLXML)
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
ms.openlocfilehash: 089b2b006d0159c63e480c8627762ac37dec98b8
ms.sourcegitcommit: a3f5c3742d85d21f6bde7c6ae133060dcf1ddd44
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/15/2020
ms.locfileid: "75247088"
---
# <a name="xpath-data-types-sqlxml-40"></a>Tipos de datos de XPath (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], XPath y esquema XML (XSD) tienen tipos de datos muy diferentes. Por ejemplo, XPath no tiene tipos de datos enteros ni fecha, pero [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y XSD tienen muchos. XSD utiliza la precisión del nanosegundo para los valores de hora y [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza a lo sumo una precisión de 1/300 de segundo. Por consiguiente, no siempre es posible asignar un tipo de datos a otro. Para obtener más [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] información acerca de la asignación de tipos de datos a tipos de datos XSD, vea Coerciones de tipos de datos y Anotación de tipo de [datos &#40;SQLXML 4.0&#41;](../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 XPath tiene tres tipos de datos: **string**, **number**y **boolean .** El tipo de datos **numérico** es siempre un punto flotante de doble precisión IEEE 754. El [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]tipo de datos **float(53)** es el más cercano al **número**XPath. Sin embargo, **float(53)** no es exactamente IEEE 754. Por ejemplo, no se utiliza NaN (no es un número) ni infinito. Al intentar convertir una cadena no numérica en **número** e intentar dividir por cero, se produce un error.  
  
## <a name="xpath-conversions"></a>Conversiones de XPath  
 Al utilizar una consulta de XPath como `OrderDetail[@UnitPrice > "10.0"]`, las conversiones de tipos de datos implícitas y explícitas pueden cambiar el significado de la consulta de manera sutil. Por consiguiente, es importante entender cómo se implementan los tipos de datos de XPath. La especificación del lenguaje XPath, XML Path Language (XPath) versión 1.0 W3C Propuesta por la http://www.w3.org/TR/1999/PR-xpath-19991008.htmlRecomendación 8 de octubre de 1999, se puede encontrar en el sitio Web de W3C en .  
  
 Los operadores de XPath se dividen en cuatro categorías:  
  
-   Operadores booleanos (and, or).  
  
-   Operadores\<relacionales \<( , >, , >)  
  
-   Operadores de igualdad (=, !=)  
  
-   Operadores aritméticos (+, -, *, div, mod)  
  
 Cada categoría de operador convierte de manera diferente los operandos. Los operadores de XPath convierten implícitamente los operandos si es necesario. Los operadores aritméticos convierten sus operandos en **número**y dan como resultado un valor numérico. Los operadores booleanos convierten sus operandos en **booleanos**y dan como resultado un valor booleano. Los operadores relacionales y operadores de igualdad generan un valor booleano. Sin embargo, tienen reglas de conversión distintas en función de los tipos de datos originales de sus operandos, como se muestra en esta tabla.  
  
|Operando|Operador relacional|Operador de igualdad|  
|-------------|-------------------------|-----------------------|  
|Los dos operandos son conjuntos de nodos.|TRUESi y sólo si hay un nodo en un conjunto y un nodo en el segundo conjunto de modo que la comparación de sus valores de **cadena** es TRUE.|Igual.|  
|Uno es un conjunto de nodo, el otro una **cadena.**|TRUESi y sólo si hay un nodo en el conjunto de nodo de modo que cuando se convierte en **número**, la comparación de él con la **cadena** convertida en **número** es TRUE.|TRUESi y solo si hay un nodo en el conjunto de nodo de modo que cuando se convierte en **cadena**, la comparación de él con la **cadena** es TRUE.|  
|Uno es un conjunto de nodo, el otro un **número.**|TRUESi y sólo si hay un nodo en el conjunto de nodo de modo que cuando se convierte en **número**, la comparación de él con el **número** es TRUE.|Igual.|  
|Uno es un conjunto de datos, el otro un **booleano**.|TRUESi y sólo si hay un nodo en el conjunto de nodo de modo que cuando se convierte en **booleano** y, a continuación, en **número**, la comparación de él con el **booleano** convertido en **número** es TRUE.|TRUESi y solo si hay un nodo en el conjunto de nodo de modo que cuando se convierte en **booleano**, la comparación de él con el **booleano** es TRUE.|  
|Ninguno es un conjunto de nodos.|Convierta ambos operandos en **número** y, a continuación, compare.|Convierta los dos operandos en un tipo común y, a continuación, compare. Convertir a **booleano** si cualquiera de los dos es **booleano**, **número** si cualquiera es **número**; de lo contrario, convierta a **cadena**.|  
  
> [!NOTE]  
>  Dado que los operadores relacionales XPath siempre convierten sus operandos en **números,** las comparaciones de **cadenas** no son posibles. Para incluir comparaciones de fechas, SQL Server 2000 ofrece esta variación a la especificación XPath: cuando un operador relacional compara una **cadena** con una **cadena,** un conjunto de datos con una **cadena**o un conjunto de nodo con valores de cadena en un conjunto de nodo con valores de cadena, se realiza una comparación de **cadenas** (no **una** comparación numérica).  
  
## <a name="node-set-conversions"></a>Conversiones de conjunto de nodos  
 Las conversiones de conjunto de nodos no son siempre intuitivas. Un conjunto de datos se convierte en una **cadena** tomando el valor de cadena de solo el primer nodo del conjunto. Un conjunto de datos se convierte en **número** convirtiéndolo en **cadena**y, a continuación, convirtiendo **string** en **number**. Un conjunto de datos se convierte en **booleano** probando su existencia.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no realiza la selección por posición en los conjuntos de nodos: por ejemplo, la consulta de XPath `Customer[3]` significa el tercer cliente; este tipo de selección por posición no se admite en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Por lo tanto, las conversiones node-set-to-**string** o node-set-to-**number** como se describe en la especificación XPath no se implementan. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] utiliza la semántica "cualquiera" donde la especificación de XPath especifica la semántica "primero". Por ejemplo, en función de la especificación `Order[OrderDetail/@UnitPrice > 10.0]` XPath de W3C, la consulta XPath selecciona esos pedidos con el primer **OrderDetail** que tiene un **UnitPrice** mayor que 10.0. En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], esta consulta XPath selecciona los pedidos con cualquier **OrderDetail** que tenga un **UnitPrice** mayor que 10.0.  
  
 La conversión a **booleano** genera una prueba de existencia; Por lo tanto, `Products[@Discontinued=true()]` la consulta XPath es equivalente a la expresión SQL "Products.Discontinued no es null", no la expresión SQL "Products.Discontinued ? 1". Para que la consulta sea equivalente a esta última expresión SQL, primero convierta el conjunto de nodos en un tipo**no booleano,** como **number**. Por ejemplo, `Products[number(@Discontinued) = true()]`.  
  
 Dado que la mayoría de los operadores están definidos para ser TRUE si son TRUE para cualquiera o uno de los nodos del conjunto de nodos, estas operaciones siempre se evalúan como FALSE si el conjunto de nodos está vacío. Así, si A está vacío, `A = B` y `A != B` son FALSE y `not(A=B)` y `not(A!=B)` son TRUE.  
  
 Normalmente, existe un atributo o elemento que se asigna a una columna si el valor de esa columna de la base de datos no es **null.** Los elementos que se asignan a filas existen si cualquiera de sus elementos secundarios existe.  
  
> [!NOTE]  
>  Los elementos anotados con **is-constant** siempre existen. Por consiguiente, los predicados XPath no se pueden utilizar en elementos **is-constant.**  
  
 Cuando un conjunto de datos se convierte en **cadena** o **número,** su tipo XDR (si existe) se inspecciona en el esquema anotado y ese tipo se utiliza para determinar la conversión necesaria.  
  
## <a name="mapping-xdr-data-types-to-xpath-data-types"></a>Asignar tipos de datos de XDR a tipos de datos de XPath  
 El tipo de datos XPath de un nodo se deriva del tipo de datos XDR del esquema, como se muestra en la tabla siguiente (el nodo **EmployeeID** se utiliza con fines ilustrativos).  
  
|Tipo de datos XDR|Tipo de datos de XPath<br /><br /> equivalente|Conversión de SQL Server utilizada|  
|-------------------|------------------------------------|--------------------------------|  
|Nonebin.base64bin.hex|N/D|NingunaEmployeeID|  
|boolean|boolean|CONVERT (bit, IdEmpleado)|  
|number, int, float,i1, i2, i4, i8,r4, r8ui1, ui2, ui4, ui8|number|CONVERT(float(53), EmployeeID)|  
|id, idref, idrefsentity, entities, enumerationnotation, nmtoken, nmtokens, chardate, Timedate, Time.tz, string, uri, uuid|string|CONVERT(nvarchar(4000), EmployeeID, 126)|  
|fixed14.4|N/D (no hay ningún tipo de datos de XPath que sea equivalente al tipo de datos fixed14.4 de XDR)|CONVERT(money, EmployeeID)|  
|date|string|LEFT(CONVERT(nvarchar(4000), EmployeeID, 126), 10)|  
|time<br /><br /> time.tz|string|SUBSTRING(CONVERT(nvarchar(4000), EmployeeID, 126), 1 + CHARINDEX(N'T', CONVERT(nvarchar(4000), EmployeeID, 126)), 24)|  
  
 Las conversiones de fecha y hora están diseñadas para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]funcionar tanto si el valor se almacena en la base de datos mediante el tipo de datos **datetime** o una **cadena.** Tenga en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]cuenta que el tipo de datos **datetime** no utiliza **la zona horaria** y tiene una precisión menor que el tipo de datos de **hora** XML. Para incluir el tipo de datos de zona [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **horaria** o precisión adicional, almacene los datos con un tipo de **cadena.**  
  
 Cuando un nodo se convierte del tipo de datos de XDR al tipo de datos de XPath, a veces es necesaria una conversión adicional (de un tipo de datos de XPath a otro tipo de datos de XPath). Por ejemplo, considere esta consulta de XPath:  
  
```  
(@m + 3) = 4  
```  
  
 Si @m es del tipo de datos **fixed14.4** XDR, la conversión del tipo de datos XDR al tipo de datos XPath se realiza mediante:  
  
```  
CONVERT(money, m)  
```  
  
 En esta conversión, `m` el nodo se convierte de **fixed14.4** a **money**. Sin embargo, si se agrega el valor 3, se requiere una conversión adicional:  
  
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
||X es desconocido|X es **cadena**|X es **el número**|X es **booleano**|  
|string(X)|CONVERT (nvarchar(4000), X, 126)|-|CONVERT (nvarchar(4000), X, 126)|CASE WHEN X THEN N'true' ELSE N'false' END|  
|number(X)|CONVERT (float(53), X)|CONVERT (float(53), X)|-|CASE WHEN X THEN 1 ELSE 0 END|  
|boolean(X)|-|LEN(X) > 0|X != 0|-|  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-convert-a-data-type-in-an-xpath-query"></a>A. Convertir un tipo de datos en una consulta de XPath  
 En la siguiente consulta XPath especificada en un esquema XSD anotado, la consulta selecciona todos los nodos **Employee** con el valor de atributo **EmployeeID** de E-1, donde "E-" es el prefijo especificado mediante la anotación **sql:id-prefix.**  
  
 `Employee[@EmployeeID="E-1"]`  
  
 El predicado de la consulta es equivalente a la expresión de SQL:  
  
 `N'E-' + CONVERT(nvarchar(4000), Employees.EmployeeID, 126) = N'E-1'`  
  
 Dado que **EmployeeID** es uno de los valores de tipo de datos **id** (**idref**, **idrefs**, **nmtoken**, **nmtokens,** etc.) en el esquema XSD, **EmployeeID** se convierte en el tipo de datos XPath de **cadena** mediante las reglas de conversión descritas anteriormente.  
  
 `CONVERT(nvarchar(4000), Employees.EmployeeID, 126)`  
  
 El prefijo "E -" se agrega a la cadena y el resultado se compara entonces con `N'E-1'`.  
  
### <a name="b-perform-several-data-type-conversions-in-an-xpath-query"></a>B. Realizar varias conversiones de tipos de datos en una consulta de XPath  
 Considere esta consulta especificada de XPath en un esquema XSD anotado: `OrderDetail[@UnitPrice * @OrderQty > 98]`  
  
 Esta consulta XPath devuelve todos los `@UnitPrice * @OrderQty > 98` ** \<** elementos OrderDetail>que satisfacen el predicado. Si el **UnitPrice** se anota con un tipo de datos **fixed14.4** en el esquema anotado, este predicado es equivalente a la expresión SQL:  
  
 `CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice)) * CONVERT(float(53), OrderDetail.OrderQty) > CONVERT(float(53), 98)`  
  
 Para convertir los valores de la consulta de XPath, la primera conversión convierte el tipo de datos de XDR al tipo de datos de XPath. Dado que el tipo de datos XSD de **UnitPrice** es **fixed14.4**, como se describe en la tabla anterior, esta es la primera conversión que se utiliza:  
  
```  
CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 Dado que los operadores aritméticos convierten sus operandos al tipo de datos XPath **numérico,** la segunda conversión (de un tipo de datos XPath a otro tipo de datos XPath) se aplica en la que el valor se convierte en **float(53)** (**float(53)** está cerca del tipo de datos **de número** XPath):  
  
```  
CONVERT(float(53), CONVERT(money, OrderDetail.UnitPrice))   
```  
  
 Suponiendo que el atributo **OrderQty** no tiene ningún tipo de datos XSD, **OrderQty** se convierte en **un** tipo de datos XPath numérico en una sola conversión:  
  
```  
CONVERT(float(53), OrderDetail.OrderQty)  
```  
  
 De forma similar, el valor 98 se convierte al tipo de datos XPath **numérico:**  
  
```  
CONVERT(float(53), 98)  
```  
  
> [!NOTE]  
>  Si el tipo de datos de XSD utilizado en el esquema es incompatible con el tipo de datos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] subyacente de la base de datos o si se realiza una conversión de tipo de datos de XPath imposible, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede devolver un error. Por ejemplo, si el atributo **EmployeeID** se anota con `Employee[@EmployeeID=1]` anotación **id-prefix,** XPath genera un error, porque **EmployeeID** tiene la anotación **id-prefix** y no se puede convertir en **number**.  
  
  
