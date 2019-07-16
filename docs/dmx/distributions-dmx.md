---
title: Distribuciones (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f4789a0e312decb2a46a9a1ba656fc5e4d3e9d47
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68070747"
---
# <a name="distributions-dmx"></a>Distribuciones (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  En [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], puede definir el contenido de las columnas en una estructura de minería de datos para modificar la forma en que los algoritmos procesan los datos de esas columnas cuando se crean modelos de minería de datos. Para algunos algoritmos, resulta útil definir la distribución de las columnas continuas antes de procesar el modelo, si se sabe que las columnas contienen distribuciones de valores comunes. Si no define las distribuciones, los modelos de minería de datos resultantes podrían generar predicciones menos precisas que si se definieran las distribuciones porque los algoritmos disponen de menos información con la que interpretar los datos.  
  
 Los algoritmos de minería de datos de [!INCLUDE[msCoName](../includes/msconame-md.md)] admiten los siguientes tipos de distribución:  
  
 **NORMAL**  
 Los valores de la columna continua forman un histograma con una distribución gaussiana normal.  
  
 **Logarítmica normal**  
 Los valores de la columna continua forman un histograma en el que el logaritmo de los valores tiene una distribución normal.  
  
 **UNIFORME**  
 Los valores de la columna continua forman una curva plana, en la que todos los valores tienen la misma probabilidad.  
  
 Para obtener más información acerca de [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmos de minería de datos, vea [algoritmos de minería de datos &#40;Analysis Services - minería de datos&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md). Los proveedores de algoritmos de terceros podrían admitir tipos de distribución adicionales. Para determinar qué tipos de distribución un algoritmo admite, use la **SUPPORTED_DISTRIBUTION_FLAGS** de filas de esquema.  
  
 Para obtener más información acerca de los tipos de distribución, consulte [distribuciones de columnas &#40;minería de datos&#41;](../analysis-services/data-mining/column-distributions-data-mining.md).  
  
## <a name="see-also"></a>Vea también  
 [Tipos de contenido &#40;minería de datos&#41;](../analysis-services/data-mining/content-types-data-mining.md)   
 [Referencia de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de operadores](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensiones de minería de datos &#40;DMX&#41; convenciones de sintaxis](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estructura y uso de las consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  
