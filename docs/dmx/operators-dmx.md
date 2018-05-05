---
title: Operadores (DMX) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- operators [DMX]
- DMX [Analysis Services], operators
- Data Mining Extensions [Analysis Services], operators
ms.assetid: e453e570-1ad1-4604-892f-6130308936ac
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: d55ce9059ddee559ae6c9d214f5a8b05457abb86
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
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
 [Extensiones de minería de datos &#40;DMX&#41; Referencia](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; Referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; Referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensiones de minería de datos &#40;DMX&#41; Convenciones de sintaxis](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensiones de minería de datos &#40;DMX&#41; Elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estructura y el uso de consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  
