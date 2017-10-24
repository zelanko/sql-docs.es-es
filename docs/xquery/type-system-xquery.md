---
title: Tipo de sistema (XQuery) | Documentos de Microsoft
ms.custom: 
ms.date: 08/10/2016
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- sequence [XQuery]
- type system [XQuery]
- typed values [XQuery]
- XQuery, sequence
- string values [XQuery]
- XQuery, XPath data type namespace
- xdt prefix [XML in SQL Server]
- XQuery, type system
- built-in XML schema types [SQL Server]
- xs prefix [XML in SQL Server]
ms.assetid: 22d6f861-d058-47ee-b550-cbe9092dcb12
caps.latest.revision: 28
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e84467e5f4ec58e1601868f1406c8c7cfd972a94
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="type-system-xquery"></a>Sistema de tipos (XQuery)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  XQuery es un lenguaje con establecimiento inflexible de tipos para tipos de esquema y un lenguaje con establecimiento flexible de tipos para datos sin tipo. Los tipos predefinidos de XQuery son los siguientes:  
  
-   Tipos integrados de esquema XML en el **http://www.w3.org/2001/XMLSchema** espacio de nombres.  
  
-   Tipos definidos en el **http://www.w3.org/2004/07/xpath-datatypes** espacio de nombres.  
  
 En este tema también se trata lo siguiente:  
  
-   El valor con tipo y el valor de cadena de un nodo.  
  
-   El [datos función &#40; XQuery &#41; ](../xquery/data-accessor-functions-data-xquery.md) y [cadena Function &#40; XQuery &#41; ](../xquery/data-accessor-functions-string-xquery.md).  
  
-   La equiparación del tipo de secuencia devuelto por una expresión.  
  
## <a name="built-in-types-of-xml-schema"></a>Tipos integrados de esquema XML  
 Los tipos integrados de esquema XML tienen el prefijo de espacio de nombres predefinido xs. Algunos de estos tipos son **xs: Integer** y **xs: String**. Todos estos tipos integrados son compatibles y se pueden utilizar al crear una colección de esquemas XML.  
  
 Al consultar XML con tipo, el tipo estático y dinámico de los nodos se determina a partir de la colección de esquemas XML asociada a la columna o variable que se consulta. Para obtener más información acerca de los tipos estáticos y dinámicos, consulte [el contexto de expresión y evaluación de la consulta &#40; XQuery &#41; ](../xquery/expression-context-and-query-evaluation-xquery.md). Por ejemplo, la consulta siguiente se especifica en un tipo **xml** columna (`Instructions`). La expresión utiliza `instance of` para comprobar que el valor con tipo del atributo `LotSize` devuelto es de tipo `xs:decimal`.  
  
```  
SELECT Instructions.query('  
   DECLARE namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";  
   data(/AWMI:root[1]/AWMI:Location[@LocationID=10][1]/@LotSize)[1] instance of xs:decimal  
') AS Result  
FROM Production.ProductModel  
WHERE ProductModelID=7  
```  
  
 Esta información de tipos la proporciona la colección de esquemas XML asociada a la columna.  
  
## <a name="types-defined-in-xpath-data-types-namespace"></a>Tipos definidos en el espacio de nombres de tipos de datos XPath  
 Los tipos definidos en el **http://www.w3.org/2004/07/xpath-datatypes** espacio de nombres tienen el prefijo predefinido de **xdt**. La siguiente información se aplica a estos tipos:  
  
-   Estos tipos no se pueden utilizar al crear una colección de esquemas XML. Estos tipos se utilizan en el sistema de tipos XQuery y se utilizan para [XQuery y tipos estáticos](../xquery/xquery-and-static-typing.md). Puede convertir a los tipos atómicos, por ejemplo, **xdt: untypedAtomic**, en la **xdt** espacio de nombres.  
  
-   Al consultar XML sin tipo, el tipo estático y dinámico de nodos de elemento es **xdt: sin tipo**, y el tipo de valores de atributo es **xdt: untypedAtomic**. El resultado de un **query()** método genera XML sin tipo. Esto significa que los nodos XML se devuelven como **xdt: sin tipo** y **xdt: untypedAtomic**, respectivamente.  
  
-   El **xdt: daytimeduration** y **xdt: yearmonthduration** no se admiten tipos.  
  
 En el ejemplo siguiente, la consulta se especifica con una variable XML sin tipo. La expresión, `data(/a[1]`), devuelve una secuencia de un valor atómico. La función `data()` devuelve el valor con tipo del elemento `<a>`. Dado que se consulta XML sin tipo, el tipo de valor devuelto es `xdt:untypedAtomic`. Por tanto, `instance of` devuelve True.  
  
```  
DECLARE @x xml  
SET @x='<a>20</a>'  
SELECT @x.query( 'data(/a[1]) instance of xdt:untypedAtomic' )  
```  
  
 En lugar de recuperar el valor con tipo, la expresión (`/a[1]`) del ejemplo siguiente devuelve una secuencia de un elemento, el elemento `<a>`. La expresión `instance of` realiza la prueba de elementos para comprobar si el valor devuelto por la expresión es un nodo de elemento `xdt:untyped type`.  
  
```  
DECLARE @x xml  
SET @x='<a>20</a>'  
-- Is this an element node whose name is "a" and type is xdt:untyped.  
SELECT @x.query( '/a[1] instance of element(a, xdt:untyped?)')  
-- Is this an element node of type xdt:untyped.  
SELECT @x.query( '/a[1] instance of element(*, xdt:untyped?)')  
-- Is this an element node?  
SELECT @x.query( '/a[1] instance of element()')  
```  
  
> [!NOTE]  
>  Cuando se consulta una instancia XML con tipo y la expresión de la consulta incluye el eje principal, deja de estar disponible la información del tipo estático de los nodos resultantes. Sin embargo, el tipo dinámico sigue asociado a los nodos.  
  
## <a name="typed-value-vs-string-value"></a>Valor con tipo y valor de cadena  
 Cada nodo tiene un valor con tipo y un valor de cadena. Para los datos XML con tipo, la colección de esquemas XML asociada a la columna o variable que se consulta proporciona el tipo del valor con tipo. Para los datos XML sin tipo, el tipo del valor con tipo es **xdt: untypedAtomic**.  
  
 Puede usar el **data()** o **string()** función para recuperar el valor de un nodo:  
  
-   El [datos función &#40; XQuery &#41; ](../xquery/data-accessor-functions-data-xquery.md) devuelve el valor con tipo de un nodo.  
  
-   El [cadena Function &#40; XQuery &#41; ](../xquery/data-accessor-functions-string-xquery.md) devuelve el valor de cadena del nodo.  
  
 En la siguiente colección de esquemas XML, se define el elemento <`root`> del tipo entero:  
  
```  
CREATE XML SCHEMA COLLECTION SC AS N'  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="root" type="integer"/>  
</schema>'  
GO  
```  
  
 En el ejemplo siguiente, la expresión primero recupera el valor con tipo de `/root[1]` y, después, le suma `3`.  
  
```  
DECLARE @x xml(SC)  
SET @x='<root>5</root>'  
SELECT @x.query('data(/root[1]) + 3')  
```  
  
 En el ejemplo siguiente, la expresión genera un error, porque `string(/root[1])` en la expresión devuelve un valor de tipo cadena. A continuación, este valor se pasa a un operador aritmético que solo utiliza como operandos valores de tipo numérico.  
  
```  
-- Fails because the argument is string type (must be numeric primitive type).  
DECLARE @x xml(SC)  
SET @x='<root>5</root>'  
SELECT @x.query('string(/root[1]) + 3')  
```  
  
 En el ejemplo siguiente se calcula el total de los atributos `LaborHours`. El `data()` función recupera los valores con tipo de `LaborHours` atributos de todos los <`Location`> elementos para un modelo de producto. Según el esquema XML asociado a la `Instruction` columna, `LaborHours` es de **xs: decimal** tipo.  
  
```  
SELECT Instructions.query('   
DECLARE namespace AWMI="http://schemas.microsoft.com/sqlserver/2004/07/adventure-works/ProductModelManuInstructions";   
             sum(data(//AWMI:Location/@LaborHours))   
') AS Result   
FROM Production.ProductModel   
WHERE ProductModelID=7  
```  
  
 Esta consulta devuelve 12.75 como resultado.  
  
> [!NOTE]  
>  El uso explícito de la **data()** función en este ejemplo es solo para fines ilustrativos. Si no se especifica, **sum()** aplica implícitamente la **data()** función para extraer los valores con tipo de los nodos.  
  
## <a name="see-also"></a>Vea también  
 [Plantillas y permisos de SQL Server Profiler](../tools/sql-server-profiler/sql-server-profiler-templates-and-permissions.md)   
 [Conceptos básicos de XQuery](../xquery/xquery-basics.md)  
  
  

