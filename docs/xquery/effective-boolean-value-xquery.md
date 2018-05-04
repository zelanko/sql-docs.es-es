---
title: Valor booleano efectivo (XQuery) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: sql
ms.service: ''
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
- effective Boolean value [XQuery]
- Boolean values
- XQuery, effective Boolean values
- EBV
ms.assetid: 506682b1-b6c9-45e2-aa54-7abd5844c3f1
caps.latest.revision: 17
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 2933294f8cce97ab0c655ee4fc80954d8b40472c
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="effective-boolean-value-xquery"></a>Valor booleano efectivo (XQuery)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

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
 [Instrucción FLWOR e iteración &#40;XQuery&#41;](../xquery/flwor-statement-and-iteration-xquery.md)  
  
  
