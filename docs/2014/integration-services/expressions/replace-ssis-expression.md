---
title: REPLACE (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- replacing string expression
- REPLACE function
ms.assetid: a6837043-ea70-4c6a-9c7a-6868b02b2adc
author: chugugrace
ms.author: chugu
ms.openlocfilehash: f052e6aadcbd7bc2ed8f81e61a66c7cbb629c54a
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/26/2020
ms.locfileid: "85428292"
---
# <a name="replace-ssis-expression"></a>REPLACE (expresión de SSIS)
  Devuelve una expresión de caracteres tras reemplazar una cadena de caracteres dentro de la expresión por otra cadena de caracteres diferente o por la cadena vacía.  
  
> [!NOTE]  
>  La función REPLACE usa con frecuencia cadenas largas. Las consecuencias del truncamiento pueden controlarse o pueden dar lugar a una advertencia o un error. Para obtener más información, vea [Sintaxis &#40;SSIS&#41;](syntax-ssis.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
REPLACE(character_expression,searchstring,replacementstring)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Expresión de caracteres válida que busca la función.  
  
 *searchstring*  
 Expresión de caracteres válida que intenta encontrar la función.  
  
 *replacementstring*  
 Expresión de caracteres válida que se usa como expresión de reemplazo.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Observaciones  
 La longitud de *searchstring* no debe ser cero.  
  
 La longitud de *replacementstring* puede ser cero.  
  
 Los argumentos *searchstring* y *replacementstring* pueden utilizar variables y columnas.  
  
 REPLACE solo funciona con el tipo de datos DT_WSTR. Los argumentos*character_expression1, character_expression2* y *character_expression3* que son literales de cadena o columnas de datos con el tipo de datos DT_STR se convierten implícitamente al tipo de datos DT_WSTR antes de que REPLACE realice su operación. Los otros tipos de datos deben convertirse explícitamente al tipo de datos DT_WSTR. Para más información, vea [Conversión &#40;expresión de SSIS&#41;](cast-ssis-expression.md).  
  
 REPLACE devuelve un resultado NULL si alguno de los argumentos es NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo usa un literal de cadena. El resultado devuelto es "All Terrain Bike".  
  
```  
REPLACE("Mountain Bike", "Mountain","All Terrain")  
```  
  
 Este ejemplo quita la cadena "Bike" de la columna **Product** .  
  
```  
REPLACE(Product, "Bike","")  
```  
  
 Este ejemplo reemplaza los valores de la columna **DaysToManufacture** . La columna tiene un tipo de datos Integer y en la expresión se incluye la conversión de **DaysToManufacture** al tipo de datos DT_WSTR.  
  
```  
REPLACE((DT_WSTR,8)DaysToManufacture,"6","5")  
```  
  
## <a name="see-also"></a>Consulte también  
 [SUBSTRING &#40;expresión de SSIS&#41;](substring-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)  
  
  
