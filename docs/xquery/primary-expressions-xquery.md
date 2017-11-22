---
title: Expresiones principales (XQuery) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
dev_langs: XML
helpviewer_keywords:
- variable references [XQuery]
- primary expressions [XQuery]
- function calls [XQuery]
- expressions [XQuery], primary
- literals [XQuery]
- context item expressions [XQuery]
ms.assetid: d4183c3e-12b5-4ca0-8413-edb0230cb159
caps.latest.revision: "20"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 50e658782b81ffc82c662ec005b925d673be221d
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="primary-expressions-xquery"></a>Expresiones principales (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Las expresiones principales de XQuery incluyen literales, referencias de variables, expresiones de elementos de contexto, constructores y llamadas a funciones.  
  
## <a name="literals"></a>Literales  
 Los literales de XQuery pueden ser numéricos o de cadena. Un literal de cadena puede incluir referencias de entidades predefinidas. Una referencia de entidad es una secuencia de caracteres. La secuencia empieza con un "y" comercial (&amp;) que representa un solo carácter que, en otra situación, tendría un significado sintáctico. A continuación se exponen las referencias de entidades predefinidas de XQuery.  
  
|Referencia de entidad|Representa|  
|----------------------|----------------|  
|&lt;|\<|  
|&gt;|>|  
|&amp;|&|  
|&quot;|"|  
|&apos;|'|  
  
 Un literal de cadena también puede contener una referencia de carácter, una referencia de estilo XML a un carácter Unicode, que se identifica mediante su punto de código decimal o hexadecimal. Por ejemplo, el símbolo del Euro se puede representar la referencia de carácter, "&\#8364;".  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] utiliza la versión 1.0 de XML como base para el análisis.  
  
### <a name="examples"></a>Ejemplos  
 Los ejemplos siguientes ilustran la utilización de literales y las referencias de entidad y carácter.  
  
 Este código devuelve un error porque los caracteres `<'` y `'>` tienen un significado especial.  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query(' <SalaryRange>Salary > 50000 and < 100000</SalaryRange>')  
GO  
```  
  
 Si utiliza una referencia de entidad en su lugar, la consulta funcionará:  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query(' <SalaryRange>Salary > 50000 and < 100000</SalaryRange>')  
GO  
```  
  
 En el ejemplo siguiente se ilustra el uso de una referencia de carácter para representar el símbolo del euro.  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query(' <a>€12.50</a>')  
```  
  
 Éste es el resultado.  
  
 `<a>€12.50</a>`  
  
 En el ejemplo siguiente, la consulta está delimitada por apóstrofos. Por tanto, el apóstrofo del valor de cadena se representa mediante dos apóstrofos adyacentes.  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query('<a>I don''t know</a>')  
Go  
```  
  
 Éste es el resultado.  
  
 `<a>I don't know</a>`  
  
 Las funciones booleanas integradas, **true()** y **false()**, puede usarse para representar valores booleanos, como se muestra en el ejemplo siguiente.  
  
```  
DECLARE @var XML  
SET @var = ''  
SELECT @var.query('<a>{true()}</a>')  
GO  
```  
  
 El constructor de elemento directo especifica una expresión entre llaves. Ésta se reemplazará por su valor en el XML resultante.  
  
 Éste es el resultado.  
  
 `<a>true</a>`  
  
## <a name="variable-references"></a>Referencias de variable  
 Una referencia de variable en XQuery es un QName precedido de un signo $. Esta implementación solo admite las referencias de variable sin prefijo. Por ejemplo, en la consulta siguiente se define la variable `$i` en la expresión FLWOR:  
  
```  
DECLARE @var XML  
SET @var = '<root>1</root>'  
SELECT @var.query('  
 for $i in /root return data($i)')  
GO  
```  
  
 La consulta siguiente no funcionará porque se ha agregado un prefijo de espacio de nombres al nombre de la variable.  
  
```  
DECLARE @var XML  
SET @var = '<root>1</root>'  
SELECT @var.query('  
DECLARE namespace x="http://X";  
for $x:i in /root return data($x:i)')  
GO  
```  
  
 Puede usar la función de extensión de SQL:variable() para hacer referencia a las variables SQL, como se muestra en la siguiente consulta.  
  
```  
DECLARE @price money  
SET @price=2500  
DECLARE @x xml  
SET @x = ''  
SELECT @x.query('<value>{sql:variable("@price") }</value>')  
```  
  
 Éste es el resultado.  
  
 `<value>2500</value>`  
  
#### <a name="implementation-limitations"></a>Limitaciones de la implementación  
 Éstas son las limitaciones de la implementación:  
  
-   No se admiten las variables con prefijos de espacio de nombres.  
  
-   No se admite la importación de módulos.  
  
-   No se admiten las declaraciones de variables externas. Una solución consiste en utilizar el [:variable()](../xquery/xquery-extension-functions-sql-variable.md).  
  
## <a name="context-item-expressions"></a>Expresiones de elementos de contexto  
 El elemento de contexto es el elemento que se está procesando en el contexto de una expresión de ruta de acceso. Se inicializa en una instancia de tipo de datos XML distinta de NULL con el nodo de documento. También puede cambiarse mediante el método nodes(), en el contexto de las expresiones XPath o en los predicados [].  
  
 Una expresión que contiene un punto (.) devuelve el elemento de contexto. Por ejemplo, la consulta siguiente evalúa cada elemento <`a`> para detectar la presencia del atributo `attr`. Si el atributo está presente, se devuelve el elemento. Tenga en cuenta que la condición del predicado especifica que el nodo de contexto se especifica mediante un solo punto.  
  
```  
DECLARE @var XML  
SET @var = '<ROOT>  
<a>1</a>  
<a attr="1">2</a>  
</ROOT>'  
SELECT @var.query('/ROOT[1]/a[./@attr]')  
```  
  
 Éste es el resultado.  
  
 `<a attr="1">2</a>`  
  
## <a name="function-calls"></a>Llamadas a funciones  
 Puede llamar a funciones integradas de XQuery y el [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] funciones SQL:variable() y SQL:Column(). Para obtener una lista de funciones implementadas, consulte [funciones de XQuery con el tipo de datos xml](../xquery/xquery-functions-against-the-xml-data-type.md).  
  
#### <a name="implementation-limitations"></a>Limitaciones de la implementación  
 Éstas son las limitaciones de la implementación:  
  
-   No se admite la declaración de funciones en el prólogo de XQuery.  
  
-   No se admite la importación de funciones.  
  
## <a name="see-also"></a>Vea también  
 [Construcción de XML &#40; XQuery &#41;](../xquery/xml-construction-xquery.md)  
  
  
