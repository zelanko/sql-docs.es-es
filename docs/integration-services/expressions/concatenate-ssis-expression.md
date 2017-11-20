---
title: "+ (Concatenar) (Expresión de SSIS) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: expressions
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- concatenation [Integration Services]
- + (concatenate operator)
- concatenate operator (+)
ms.assetid: 0fed6334-7a4f-42dc-a611-191fcaa0e443
caps.latest.revision: 37
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: ba1fcd0a00289d7c2f97fa344be196885c7e7451
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="-concatenate-ssis-expression"></a>+ (Concatenar) (expresión de SSIS)
  Concatena dos expresiones en una expresión.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
character_expression1 + character_expression2  
  
```  
  
## <a name="arguments"></a>Argumentos  
 *expression1, expression2*  
 Cualquier expresión válida con tipo de datos DT_STR, DT_WSTR, DT_TEXT, DT_NTEXT o DT_IMAGE.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Comentarios  
 La expresión puede usar los tipos de datos DT_STR y DT_WSTR, o uno de los dos.  
  
 La concatenación de los tipos de datos DT_STR y DT_WSTR devuelve un resultado de tipo DT_WSTR. La longitud de la cadena es la suma de las longitudes de las cadenas originales expresadas en caracteres.  
  
 Solo se pueden concatenar datos con los tipos de datos de cadena DT_STR y DT_WSTR o con los tipos de datos de bloque de objetos binarios grandes (BLOB) DT_TEXT, DT_NTEXT y DT_IMAGE. Los otros tipos de datos deben convertirse explícitamente en uno de estos tipos de datos antes de que se produzca la concatenación. Para obtener más información sobre conversiones válidas entre tipos de datos, vea [Conversión &#40;expresión de SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 Ambas expresiones deben tener el mismo tipo de datos o una expresión debe poder convertirse implícitamente al tipo de datos de la otra expresión. Por ejemplo, si se concatena la cadena "Order date is " y la columna **OrderDate** , los valores de **OrderDate** se convierten implícitamente a un tipo de datos de cadena. Para concatenar dos valores numéricos, ambos valores deben convertirse explícitamente a un tipo de datos de cadena.  
  
 En una concatenación solo se puede usar un tipo de datos BLOB: DT_TEXT, DT_NTEXT o DT_IMAGE.  
  
 Si alguno de los elementos es NULL, el resultado será NULL.  
  
 Los literales de cadena deben escribirse entre comillas.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo concatena los valores de las columnas **FirstName** y **LastName** e inserta un espacio entre ellos.  
  
```  
FirstName + ' ' + LastName  
```  
  
 En este ejemplo se concatenan las variables **ZIPCode** y **ZIPCode+4**. Ambas variables tienen un tipo de datos de cadena. **ZIPCode+4** debe escribirse entre corchetes porque el nombre de la variable incluye el carácter +.  
  
```  
@ZIPCcode + "-" + @[ZipCode+4]  
```  
  
## <a name="see-also"></a>Vea también  
 [Prioridad y asociatividad](../../integration-services/expressions/operator-precedence-and-associativity.md)   
 [Operadores &#40; Expresión de SSIS &#41;](../../integration-services/expressions/operators-ssis-expression.md)  
  
  

