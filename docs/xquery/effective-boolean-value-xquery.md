---
title: Valor booleano efectivo (XQuery) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
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
- effective Boolean value [XQuery]
- Boolean values
- XQuery, effective Boolean values
- EBV
ms.assetid: 506682b1-b6c9-45e2-aa54-7abd5844c3f1
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b80d848571d645e6d12e512455ecaa3d66be32ce
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="effective-boolean-value-xquery"></a>Valor booleano efectivo (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Éstos son los valores booleanos efectivos:  
  
-   False si el operando es una secuencia vacía o un valor booleano false.  
  
-   De lo contrario, el valor es true.  
  
 El valor booleano efectivo puede calcularse para expresiones que devuelven un único valor booleano, una secuencia de nodo o una secuencia vacía. Tenga en cuenta que el valor booleano se calcula de forma implícita, cuando se procesan los siguientes tipos de expresiones:  
  
-   Expresiones lógicas  
  
-   El [no funcionen](../xquery/functions-on-boolean-values-not-function.md)  
  
-   La cláusula WHERE de una expresión FLWOR  
  
-   [Expresiones condicionales](../xquery/conditional-expressions-xquery.md)  
  
-   [Expresiones cuantificadas](../xquery/quantified-expressions-xquery.md)  
  
 A continuación se muestra un ejemplo de un valor booleano efectivo. Cuando el **si** se procesa la expresión, se determina el valor booleano efectivo de la condición. Como `/a[1]` devuelve una secuencia vacía, el valor booleano efectivo es false. El resultado se devuelve como XML con un nodo de texto (false).  
  
```  
value is false  
DECLARE @x XML  
SET @x = '<b/>'  
SELECT @x.query('if (/a[1]) then "true" else "false"')  
go  
```  
  
 En el siguiente ejemplo, el valor booleano efectivo es true, porque la expresión devuelve una secuencia no vacía.  
  
```  
DECLARE @x XML  
SET @x = '<a/>'  
SELECT @x.query('if (/a[1]) then "true" else "false"')  
go  
```  
  
 Al consultar escrito **xml** columnas o variables, puede tener nodos de tipo booleano. El **data()** en este caso, devuelve un valor booleano. Si la expresión de consulta devuelve un valor booleano true, el valor booleano efectivo será true, tal y como se muestra en el siguiente ejemplo. En el ejemplo también se ilustra lo siguiente:  
  
-   Se crea una colección de esquemas XML. El elemento \<b > de la colección es de tipo booleano.  
  
-   Un tipo **xml** variable se crea y se consultan.  
  
-   La expresión `data(/b[1])` devuelve un valor booleano true. Por tanto, el valor booleano efectivo en este caso es true.  
  
-   La expresión `data(/b[2])` devuelve un valor booleano false. Por tanto, el valor booleano efectivo en este caso es false.  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="http://www.w3.org/2001/XMLSchema">  
      <element name="s" type="string"/>  
      <element name="b" type="boolean"/>  
</schema>'  
go  
DECLARE @x XML(SC)  
SET @x = '<b>true</b><b>false</b>'  
SELECT @x.query('if (data(/b[1])) then "true" else "false"')  
SELECT @x.query('if (data(/b[2])) then "true" else "false"')  
go  
```  
  
## <a name="see-also"></a>Vea también  
 [Conceptos básicos de XQuery](../xquery/xquery-basics.md)   
 [Instrucción FLWOR e iteración &#40; XQuery &#41;](../xquery/flwor-statement-and-iteration-xquery.md)  
  
  
