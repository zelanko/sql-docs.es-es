---
title: REPLICATE (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: expressions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- REPLICATE function
ms.assetid: e7a37b93-6d1d-42d5-9a65-de1790abf6a5
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 06026b418fac119f45868425e0a75d53fb514144
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="replicate-ssis-expression"></a>REPLICATE (expresión de SSIS)
  Devuelve una expresión de caracteres replicada un determinado número de veces. El argumento *times* debe devolver un entero.  
  
> [!NOTE]  
>  La función REPLICATE utiliza con frecuencia cadenas largas y, por consiguiente, es más probable que incurra en el límite de 4.000 caracteres en la longitud de la expresión. Si el resultado de la evaluación de una expresión tiene el tipo de datos DT_WSTR o DT_STR de Integration Services, la expresión se truncará a 4.000 caracteres. Si el tipo de resultado de una subexpresión es DT_STR o DT_WSTR, dicha subexpresión se truncará también a 4.000 caracteres, independientemente del tipo de resultado de la expresión general. Las consecuencias del truncamiento pueden controlarse o pueden dar lugar a una advertencia o un error. Para obtener más información, vea [Sintaxis &#40;SSIS&#41;](../../integration-services/expressions/syntax-ssis.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
REPLICATE(character_expression,times)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Expresión de caracteres que se va a replicar.  
  
 *times*  
 Expresión de tipo entero que especifica el número de veces que se va a replicar *character_expression* .  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Notas  
 Si el valor de *times* es cero, la función devuelve una cadena de longitud cero.  
  
 Si el valor de *times* es un número negativo, la función devuelve un error.  
  
 El argumento *times* también puede utilizar variables y columnas.  
  
 REPLICATE solo funciona con el tipo de datos DT_WSTR. Un argumento *character_expression* que sea un literal de cadena o una columna de datos con el tipo de datos DT_STR se convertirá implícitamente al tipo de datos DT_WSTR antes de que REPLICATE realice su operación. Los otros tipos de datos deben convertirse explícitamente al tipo de datos DT_WSTR. Para obtener más información, vea [Tipos de datos de Integration Services](../../integration-services/data-flow/integration-services-data-types.md) y [Conversión &#40;expresión de SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 REPLICATE devuelve un resultado NULL si alguno de los argumentos es NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo replica un literal de cadena tres veces. El resultado devuelto es "Mountain BikeMountain BikeMountain Bike".  
  
```  
REPLICATE("Mountain Bike", 3)  
```  
  
 Este ejemplo replica los valores de la columna **Name** tantas veces como indique el valor de la variable **Times** . Si el valor de **Times** es 3 y el valor de **Name** es "Touring Front Wheel", el resultado devuelto será "Touring Front WheelTouring Front WheelTouring Front Wheel".  
  
```  
REPLICATE(Name, @Times)  
```  
  
 Este ejemplo replica el valor de la variable **Name** tantas veces como indique el valor de la columna **Times** . **Times** contiene un tipo de datos no entero y la expresión incluye una conversión explícita a un tipo de datos entero. Si el valor de **Name** es Helmet y el valor de **Times** es 2, la cadena devuelta es "HelmetHelmet".  
  
```  
REPLICATE(@Name, (DT_I4(Times))  
```  
  
## <a name="see-also"></a>Ver también  
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
