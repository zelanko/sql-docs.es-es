---
title: "LEFT (expresión de SSIS) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5634dbfb-740d-4c93-8fd5-2854cc741327
caps.latest.revision: 12
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: aad5c2de4903b5ad79fd5087be7801a8195e943f
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="left-ssis-expression"></a>LEFT (expresión de SSIS)
  Devuelve el número de caracteres especificado de la parte más a la izquierda de la expresión de caracteres dada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
LEFT(character_expression,number)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Expresión de caracteres de la que se van a extraer caracteres.  
  
 *number*  
 Expresión entera que indica el número de caracteres que se van a devolver.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Comentarios  
 Si *number* es mayor que la longitud de *character_expression*, la función devuelve *character_expression*.  
  
 Si el valor de *number* es cero, la función devuelve una cadena de longitud cero.  
  
 Si el valor de *number* es un número negativo, la función devuelve un error.  
  
 El argumento *number* admite variables y columnas.  
  
 LEFT solo funciona con el tipo de datos DT_WSTR. Un argumento *character_expression* que sea un literal de cadena o una columna de datos con el tipo de datos DT_STR se convertirá implícitamente al tipo de datos DT_WSTR antes de que LEFT realice su operación. Los otros tipos de datos deben convertirse explícitamente al tipo de datos DT_WSTR. Para obtener más información, vea [Tipos de datos de Integration Services](../../integration-services/data-flow/integration-services-data-types.md) y [Conversión &#40;expresión de SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 LEFT devuelve un resultado NULL si alguno de los argumentos es NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 En el siguiente ejemplo se utiliza un literal de cadena. El resultado devuelto es `"Mountain"`.  
  
```  
LEFT("Mountain Bike", 8)  
```  
  
## <a name="see-also"></a>Vea también  
 [DERECHA &#40; Expresión de SSIS &#41;](../../integration-services/expressions/right-ssis-expression.md)   
 [Funciones &#40; Expresión de SSIS &#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  

