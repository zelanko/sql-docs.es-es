---
title: Operadores (DMX) | Documentos de Microsoft
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 072d0a36a4803f4de1d50ba066e4e86e5d171c5c
ms.sourcegitcommit: 8f0faa342df0476884c3238e36ae3d9634151f87
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/07/2018
ms.locfileid: "34842888"
---
# <a name="operators-dmx"></a>Operadores (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Puede usar operadores de extensiones de minería de datos (DMX) para realizar aritmética, comparación, concatenación y operaciones lógicas de una consulta en [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utiliza operadores para realizar las siguientes acciones:  
  
-   Buscar valores u objetos que cumplan una condición determinada.  
  
-   Implementar una decisión entre columnas o expresiones.  
  
 DMX emplea varias categorías de operadores, que se describen en las siguientes secciones. Para obtener información adicional acerca de los operadores individuales, consulte [extensiones de minería de datos &#40;DMX&#41; Operator Reference](../dmx/data-mining-extensions-dmx-operator-reference.md).  
  
|Categoría de operador|Tipo de operación|  
|-----------------------|-----------------------|  
|[Operadores aritméticos &#40;DMX&#41;](../dmx/operators-arithmetic.md)|Realizan sumas, restas, multiplicaciones o divisiones.|  
|[Operadores de comparación &#40;DMX&#41;](../dmx/operators-comparison.md)|Comparan un valor con otro valor o con una expresión.|  
|[Operadores lógicos &#40;DMX&#41;](../dmx/operators-logical.md)|Prueban si una condición es cierta, como AND, OR o NOT.|  
|[Operadores unarios &#40;DMX&#41;](../dmx/operators-unary.md)|Realizan una operación en un único operando.|  
  
 Puede utilizar operadores para combinar expresiones más sencillas de DMX y crear así expresiones más complejas. En las expresiones complejas, los operadores se evalúan en un orden que se basa en la definición de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] de la precedencia de operadores. Los operadores con mayor precedencia se ejecutan antes que los operadores con menor precedencia. Para obtener más información acerca de las expresiones, vea [expresiones &#40;DMX&#41;](../dmx/expressions-dmx.md).  
  
 Cuando se combinan expresiones sencillas para formar una expresión compleja, el tipo de datos de la expresión resultante está determinado por la combinación de las reglas de los operadores con las reglas de la precedencia de tipo de datos. Si el resultado es un carácter o un valor de Unicode, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] determina la intercalación del resultado mediante la combinación de las reglas de los operadores con las reglas de precedencia de la intercalación. También hay reglas que determinan la precisión, escala y longitud del resultado basándose en la precisión, escala y longitud de las expresiones sencillas.  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40;DMX&#41; referencia](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; función referencia](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensiones de minería de datos &#40;DMX&#41; convenciones de sintaxis](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensiones de minería de datos &#40;DMX&#41; elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estructura y el uso de consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  
