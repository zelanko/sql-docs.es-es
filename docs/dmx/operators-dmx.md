---
title: Operadores (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5fd3bd36169f377b3f507609d94b5b209a9fb3bc
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2020
ms.locfileid: "83669729"
---
# <a name="operators-dmx"></a>Operadores (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Puede utilizar operadores de extensiones de minería de datos (DMX) para realizar operaciones aritméticas, de comparación, de concatenación y lógicas en una consulta en [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] utiliza operadores para realizar las siguientes acciones:  
  
-   Buscar valores u objetos que cumplan una condición determinada.  
  
-   Implementar una decisión entre columnas o expresiones.  
  
 DMX emplea varias categorías de operadores, que se describen en las siguientes secciones. Para obtener más información acerca de los operadores individuales, vea [extensiones de minería de datos &#40;referencia del operador DMX&#41;](../dmx/data-mining-extensions-dmx-operator-reference.md).  
  
|Categoría de operador|Tipo de operación|  
|-----------------------|-----------------------|  
|[Operadores aritméticos &#40;DMX&#41;](../dmx/operators-arithmetic.md)|Realizan sumas, restas, multiplicaciones o divisiones.|  
|[Operadores de comparación &#40;DMX&#41;](../dmx/operators-comparison.md)|Comparan un valor con otro valor o con una expresión.|  
|[Operadores lógicos &#40;DMX&#41;](../dmx/operators-logical.md)|Prueban si una condición es cierta, como AND, OR o NOT.|  
|[Operadores unarios &#40;DMX&#41;](../dmx/operators-unary.md)|Realizan una operación en un único operando.|  
  
 Puede utilizar operadores para combinar expresiones más sencillas de DMX y crear así expresiones más complejas. En las expresiones complejas, los operadores se evalúan en un orden que se basa en la definición de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] de la precedencia de operadores. Los operadores con mayor precedencia se ejecutan antes que los operadores con menor precedencia. Para obtener más información sobre las expresiones, vea [expresiones &#40;DMX&#41;](../dmx/expressions-dmx.md).  
  
 Cuando se combinan expresiones sencillas para formar una expresión compleja, el tipo de datos de la expresión resultante está determinado por la combinación de las reglas de los operadores con las reglas de la precedencia de tipo de datos. Si el resultado es un carácter o un valor de Unicode, [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] determina la intercalación del resultado mediante la combinación de las reglas de los operadores con las reglas de precedencia de la intercalación. También hay reglas que determinan la precisión, escala y longitud del resultado basándose en la precisión, escala y longitud de las expresiones sencillas.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Referencia de funciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referencia de instrucciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)   
 [Convenciones de sintaxis de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensiones de minería de datos &#40;DMX&#41; elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estructura y uso de las consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  
