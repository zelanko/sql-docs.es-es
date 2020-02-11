---
title: Operadores aritméticos (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e78241252733e8298c0bc727f9c45dd6df2768ac
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "68008215"
---
# <a name="operators---arithmetic"></a>Operadores: aritméticos
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Puede utilizar operadores aritméticos en extensiones de minería de datos (DMX) para cálculos aritméticos en [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], incluidas la suma, la resta, la multiplicación y la división.  
  
 En la tabla siguiente se describen los operadores aritméticos que admite DMX.  
  
|Operator|Descripción|  
|--------------|-----------------|  
|[+ &#40;agregar&#41; &#40;DMX&#41;](../dmx/add-dmx.md)|Suma dos números.|  
|[-&#40;resta&#41; &#40;DMX&#41;](../dmx/subtract-dmx.md)|Resta un número de otro.|  
|[&#42; &#40;multiplicar&#41; &#40;DMX&#41;](../dmx/multiply-dmx.md)|Multiplica un número por otro.|  
|[&#40;dividir&#41; &#40;DMX&#41;](../dmx/divide-dmx.md)|Divide un número entre otro.|  
  
 Las siguientes reglas determinan el orden de precedencia para operadores aritméticos en una expresión DMX:  
  
-   Cuando hay varios operadores aritméticos en una expresión, primero se calculan las multiplicaciones y divisiones, y, después, las restas y las sumas.  
  
-   Cuando todos los operadores aritméticos de una expresión tienen el mismo nivel de precedencia, el orden de ejecución es de izquierda a derecha.  
  
-   Las expresiones que están entre paréntesis tienen prioridad sobre las demás operaciones.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Referencia de funciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referencia de operadores &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Referencia de instrucciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)   
 [Convenciones de sintaxis de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensiones de minería de datos &#40;DMX&#41; elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Expresiones &#40;DMX&#41;](../dmx/expressions-dmx.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Operadores &#40;DMX&#41;](../dmx/operators-dmx.md)   
 [Estructura y uso de las consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  
