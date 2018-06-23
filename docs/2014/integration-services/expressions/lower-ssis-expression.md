---
title: LOWER (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- converting uppercase to lowercase
- LOWER function
- uppercase characters [Integration Services]
- lowercase characters
ms.assetid: 109328e1-5604-40ff-895e-f2e7c13fff41
caps.latest.revision: 33
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: f375f8c81a7f1e279c1e74528cc7f92e61f93056
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103349"
---
# <a name="lower-ssis-expression"></a>LOWER (expresión de SSIS)
  Devuelve una expresión de caracteres después de convertir los caracteres en mayúsculas a minúsculas.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
LOWER(character_expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Expresión de caracteres para convertir a caracteres en minúsculas.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Notas  
 LOWER solo funciona con el tipo de datos DT_WSTR. Un argumento *character_expression* que sea un literal de cadena o una columna de datos con el tipo de datos DT_STR, se convertirá implícitamente al tipo de datos DT_WSTR antes de que LOWER realice su operación. Los otros tipos de datos deben convertirse explícitamente al tipo de datos DT_WSTR. Para obtener más información, vea [Tipos de datos de Integration Services](../data-flow/integration-services-data-types.md) y [Conversión &#40;expresión de SSIS&#41;](cast-ssis-expression.md).  
  
 LOWER devuelve un resultado NULL si el valor del argumento es NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo convierte un literal de cadena a caracteres en minúsculas. El resultado devuelto es "new york".  
  
```  
LOWER("New York")  
```  
  
 Este ejemplo convierte todos los caracteres de la columna de entrada **Color** , a excepción del primer carácter, a caracteres en minúsculas. Si el valor de Color es YELLOW, el resultado devuelto es "Yellow". Para obtener más información, vea [SUBSTRING &#40;expresión de SSIS&#41;](substring-ssis-expression.md).  
  
```  
LOWER(SUBSTRING(Color, 2, 15))  
```  
  
 Este ejemplo convierte el valor de la variable **CityName** a caracteres en minúsculas.  
  
```  
LOWER(@CityName)  
```  
  
## <a name="see-also"></a>Vea también  
 [SUPERIOR &#40;expresión de SSIS&#41;](upper-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](functions-ssis-expression.md)  
  
  