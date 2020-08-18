---
description: Distribuciones (DMX)
title: Distribuciones (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f0aef6ed4b98241b07e84aa11ed6408c600d6ee7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88414201"
---
# <a name="distributions-dmx"></a>Distribuciones (DMX)
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  En [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , puede definir el contenido de las columnas de una estructura de minería de datos para influir en el modo en que los algoritmos procesan los datos de esas columnas cuando se crean modelos de minería de datos. Para algunos algoritmos, resulta útil definir la distribución de las columnas continuas antes de procesar el modelo, si se sabe que las columnas contienen distribuciones de valores comunes. Si no define las distribuciones, los modelos de minería de datos resultantes podrían generar predicciones menos precisas que si se definieran las distribuciones porque los algoritmos disponen de menos información con la que interpretar los datos.  
  
 Los algoritmos de minería de datos de [!INCLUDE[msCoName](../includes/msconame-md.md)] admiten los siguientes tipos de distribución:  
  
 **SIN**  
 Los valores de la columna continua forman un histograma con una distribución gaussiana normal.  
  
 **Logarítmica normal**  
 Los valores de la columna continua forman un histograma en el que el logaritmo de los valores tiene una distribución normal.  
  
 **PRINCIPIOS**  
 Los valores de la columna continua forman una curva plana, en la que todos los valores tienen la misma probabilidad.  
  
 Para obtener más información acerca de los [!INCLUDE[msCoName](../includes/msconame-md.md)] algoritmos de minería de datos, vea [algoritmos de minería de datos &#40;Analysis Services-data mining&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining). Los proveedores de algoritmos de terceros podrían admitir tipos de distribución adicionales. Para determinar qué tipos de distribución admite un algoritmo, use el conjunto de filas de esquema **SUPPORTED_DISTRIBUTION_FLAGS** .  
  
 Para obtener más información acerca de los tipos de distribución, vea [distribuciones de columnas &#40;&#41;de minería de datos ](https://docs.microsoft.com/analysis-services/data-mining/column-distributions-data-mining).  
  
## <a name="see-also"></a>Consulte también  
 [Tipos de contenido &#40;minería de datos&#41;](https://docs.microsoft.com/analysis-services/data-mining/content-types-data-mining)   
 [Referencia de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Referencia de funciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referencia de operadores &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Referencia de instrucciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)   
 [Convenciones de sintaxis de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estructura y uso de las consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  
