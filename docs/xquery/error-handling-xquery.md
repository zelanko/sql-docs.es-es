---
title: Error de control (XQuery) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: sql
ms.component: xquery
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
dev_langs:
- XML
helpviewer_keywords:
- static errors
- errors [XQuery]
- XQuery, error handling
- dynamic errors [XQuery]
ms.assetid: 7dee3c11-aea0-4d10-9126-d54db19448f2
caps.latest.revision: 29
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: c7277c122c76ef2aa9ff6c82b4693faed6b409ab
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33076952"
---
# <a name="error-handling-xquery"></a>Control de errores (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  La especificación W3C permite emitir errores de tipo de forma estática o dinámica y define errores estáticos, dinámicos y de tipo.  
  
## <a name="compilation-and-error-handling"></a>Compilación y control de errores  
 Las expresiones XQuery e instrucciones XML DML sintácticamente incorrectas generan errores de compilación. En la fase de compilación, se comprueba la corrección del tipo estático de las expresiones XQuery y las instrucciones DML, y se utilizan esquemas XML para detectar inferencias de tipos para XML con tipo. Si una expresión puede generar un error en tiempo de ejecución debido a una infracción de seguridad de tipos, se producen errores de tipo estático. Ejemplos de errores estáticos son la suma de una cadena a un entero y la consulta de datos con tipo en un nodo no existente  
  
 Como desviación del estándar W3C, los errores en tiempo de ejecución de XQuery se convierten en secuencias vacías. Estas secuencias se pueden propagar al resultado de la consulta como XML vacío o NULL, dependiendo del contexto de invocación.  
  
 Una conversión explícita al tipo correcto permite a los usuarios resolver errores estáticos, aunque los errores de conversión en tiempo de ejecución se transformarán en secuencias vacías.  
  
## <a name="static-errors"></a>Errores estáticos  
 Los errores estáticos se devuelven utilizando el mecanismo de error de [!INCLUDE[tsql](../includes/tsql-md.md)]. En [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], los errores de tipo de XQuery se devuelven de forma estática. Para obtener más información, consulte [XQuery y tipos estáticos](../xquery/xquery-and-static-typing.md).  
  
## <a name="dynamic-errors"></a>Errores dinámicos  
 En XQuery, la mayoría de los errores dinámicos se asignan a una secuencia vacía ("()"). No obstante, existen dos excepciones: las condiciones de sobrecarga en funciones de agregado de XQuery y los errores de validación de XML-DML. Tenga en cuenta que la mayoría de los errores dinámicos se asignan a una secuencia vacía. De lo contrario, la ejecución de consultas que se aprovecha de los índices XML puede producir errores inesperados. Por tanto, para proporcionar una ejecución eficaz sin generar errores inesperados, [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] asigna los errores dinámicos a ().  
  
 A menudo, en una situación en la que el error dinámico se produciría dentro de un predicado, no emitir el error es no cambiar la semántica, porque () se asigna a False. Sin embargo, en algunos casos, devolver () en lugar de un error dinámico puede dar lugar a resultados inesperados. Los ejemplos siguientes lo muestran.  
  
### <a name="example-using-the-avg-function-with-a-string"></a>Ejemplo: utilizar la función avg() con una cadena  
 En el ejemplo siguiente, la [función avg](../xquery/aggregate-functions-avg.md) se llama para calcular la media de los tres valores. Uno de estos valores es una cadena. Puesto que la instancia XML en este caso no tiene tipo, todos los datos que contiene son de tipo atómico sin tipo. El **avg()** función convierte estos valores para **xs: Double** antes de calcular la Media. Sin embargo, el valor, `"Hello"`, no se puede convertir a **xs: Double** y crea un error dinámico. En este caso, en lugar de devolver un error dinámico, la conversión de `"Hello"` a **xs: Double** hace que una secuencia vacía. El **avg()** función omite este valor, calcula el promedio de los otros dos valores y devuelve 150.  
  
```  
DECLARE @x xml  
SET @x=N'<root xmlns:myNS="test">  
 <a>100</a>  
 <b>200</b>  
 <c>Hello</c>  
</root>'  
SELECT @x.query('avg(//*)')  
```  
  
### <a name="example-using-the-not-function"></a>Ejemplo: utilizar la función not  
 Cuando se usa el [no funcionen](../xquery/functions-on-boolean-values-not-function.md) en un predicado, por ejemplo, `/SomeNode[not(Expression)]`, y la expresión provoca un error dinámico, se devolverá una secuencia vacía en lugar de un error. Aplicar **not()** a la secuencia vacía, devuelve True, en lugar de un error.  
  
### <a name="example-casting-a-string"></a>Ejemplo: convertir una cadena  
 En el ejemplo siguiente, la cadena literal "NaN" se convierte a xs:string, y después a xs:double. El resultado es un conjunto de filas vacío. Aunque la cadena "NaN" no se puede convertir correctamente a xs:double, esto no se puede determinar hasta el tiempo de ejecución, porque la cadena se convierte primero a xs:string.  
  
```  
DECLARE @x XML  
SET @x = ''  
SELECT @x.query(' xs:double(xs:string("NaN")) ')  
GO  
```  
  
 En este ejemplo, sin embargo, se produce un error de tipo estático.  
  
```  
DECLARE @x XML  
SET @x = ''  
SELECT @x.query(' xs:double("NaN") ')  
GO  
```  
  
#### <a name="implementation-limitations"></a>Limitaciones de la implementación  
 El **fn:error()** no se admite la función.  
  
## <a name="see-also"></a>Vea también  
 [Referencia del lenguaje XQuery &#40;SQL Server&#41;](../xquery/xquery-language-reference-sql-server.md)   
 [Conceptos básicos de XQuery](../xquery/xquery-basics.md)  
  
  
