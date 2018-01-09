---
title: "Operadores aritméticos (DMX) | Documentos de Microsoft"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: DMX
helpviewer_keywords: arithmetic operators
ms.assetid: befe4f0c-e5dd-4ae1-b88e-6ac7aab2181a
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: c256882453ca3536a21babb2d87b774e9aab3d6d
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="operators---arithmetic"></a>Operadores - aritmética
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Puede utilizar operadores aritméticos en las extensiones de minería de datos (DMX) para realizar cálculos aritméticos en [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], como suma, resta, multiplicación y división.  
  
 En la tabla siguiente se describen los operadores aritméticos que admite DMX.  
  
|Operador|Description|  
|--------------|-----------------|  
|[+ &#40; Agregar &#41; &#40; DMX &#41;](../dmx/add-dmx.md)|Suma dos números.|  
|[-&#40; Restar &#41; &#40; DMX &#41;](../dmx/subtract-dmx.md)|Resta un número de otro.|  
|[&#42; &#40; Multiplicar &#41; &#40; DMX &#41;](../dmx/multiply-dmx.md)|Multiplica un número por otro.|  
|[&#40; división &#41; &#40; DMX &#41;](../dmx/divide-dmx.md)|Divide un número entre otro.|  
  
 Las siguientes reglas determinan el orden de precedencia para operadores aritméticos en una expresión DMX:  
  
-   Cuando hay varios operadores aritméticos en una expresión, primero se calculan las multiplicaciones y divisiones, y, después, las restas y las sumas.  
  
-   Cuando todos los operadores aritméticos de una expresión tienen el mismo nivel de precedencia, el orden de ejecución es de izquierda a derecha.  
  
-   Las expresiones entre paréntesis tienen prioridad sobre todas las demás operaciones.  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40; DMX &#41; Referencia](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de operadores](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Convenciones de sintaxis](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Expresiones &#40; DMX &#41;](../dmx/expressions-dmx.md)   
 [Funciones de predicción generales &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [Operadores &#40; DMX &#41;](../dmx/operators-dmx.md)   
 [Estructura y el uso de consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  
