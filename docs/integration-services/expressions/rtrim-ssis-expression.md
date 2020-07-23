---
title: RTRIM (expresión de SSIS) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- RTRIM function
- trailing blanks
ms.assetid: 529bd43e-3f8a-4682-a33e-569176aa7fc4
author: chugugrace
ms.author: chugu
ms.openlocfilehash: c58da8b33c431f62f4567379beca8b5b12beea4f
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/22/2020
ms.locfileid: "86914951"
---
# <a name="rtrim-ssis-expression"></a>RTRIM (expresión de SSIS)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Devuelve una expresión de caracteres después de quitar los espacios finales.  
  
> [!NOTE]  
>  RTRIM no quita los caracteres de espacio en blanco, como los caracteres de tabulación o de salto de línea. Unicode proporciona puntos de código para muchos tipos distintos de espacios, pero su función solo reconoce el punto de código Unicode 0x0020. Cuando se convierten cadenas del juego de caracteres de doble byte (DBCS) a Unicode, éstas pueden incluir caracteres de espacio distintos de 0x0020 y la función no puede eliminarlos. Para eliminar cualquier tipo de espacio, puede utilizar el método RTrim de Microsoft Visual Basic .NET en un script ejecutado desde el componente Script.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
RTRIM(character expression)  
```  
  
## <a name="arguments"></a>Argumentos  
 *character_expression*  
 Expresión de caracteres de la que puede quitar espacios.  
  
## <a name="result-types"></a>Tipos de resultado  
 DT_WSTR  
  
## <a name="remarks"></a>Observaciones  
 RTRIM solo funciona con el tipo de datos DT_WSTR. Un argumento *character_expression* que sea un literal de cadena o una columna de datos con el tipo de datos DT_STR se convertirá implícitamente al tipo de datos DT_WSTR antes de que RTRIM realice su operación. Los otros tipos de datos deben convertirse explícitamente al tipo de datos DT_WSTR. Para obtener más información, vea [Tipos de datos de Integration Services](../../integration-services/data-flow/integration-services-data-types.md) y [Conversión &#40;expresión de SSIS&#41;](../../integration-services/expressions/cast-ssis-expression.md).  
  
 RTRIM devuelve un resultado NULL si el valor del argumento es NULL.  
  
## <a name="expression-examples"></a>Ejemplos de expresiones  
 Este ejemplo quita los espacios finales de un literal de cadena. El resultado devuelto es "Hello".  
  
```  
RTRIM("Hello   ")  
```  
  
 Este ejemplo quita los espacios finales de una concatenación de las columnas **FirstName** y **LastName** .  
  
```  
RTRIM(FirstName + " " + LastName)  
```  
  
 Este ejemplo quita los espacios finales de la variable **FirstName** .  
  
```  
RTRIM(@FirstName)  
```  
  
## <a name="see-also"></a>Consulte también  
 [LTRIM &#40;expresión de SSIS&#41;](../../integration-services/expressions/ltrim-ssis-expression.md)   
 [TRIM &#40;expresión de SSIS&#41;](../../integration-services/expressions/trim-ssis-expression.md)   
 [Funciones &#40;expresión de SSIS&#41;](../../integration-services/expressions/functions-ssis-expression.md)  
  
  
