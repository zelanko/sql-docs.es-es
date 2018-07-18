---
title: Marcas de modelado (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 17280abc62cd75122fde1f54b321ca9b51a1b1d9
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "37992467"
---
# <a name="modeling-flags-dmx"></a>Marcas de modelado (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Puede utilizar marcas de modelado en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para proporcionar información adicional a un algoritmo de minería de datos acerca de los datos que se definen en una tabla de casos. El algoritmo puede usar esta información para crear un modelo de minería de datos más preciso. Puede definir marcas de modelado tanto en columnas de estructura de minería de datos como en columnas de modelos de minería de datos.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] admite las siguientes marcas de modelado:  
  
 **NOT NULL**  
 Los valores de la columna de atributos nunca deben incluir un valor NULL. Se producirá un error si [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] encuentra un valor NULL para esta columna de atributos durante el proceso de entrenamiento de modelos. Esta marca se define en una columna de estructura de minería de datos.  
  
 **REGRESSOR**  
 Indica que el algoritmo puede usar la columna especificada en la fórmula de regresión de algoritmos de regresión. Esta marca es compatible con los algoritmos de regresión lineal de [!INCLUDE[msCoName](../includes/msconame-md.md)] y árboles de decisión de [!INCLUDE[msCoName](../includes/msconame-md.md)] y se define en una columna de modelos de minería de datos.  
  
 **MODEL_EXISTENCE_ONLY**  
 Los valores de la columna de atributos no son tan importantes como la presencia del atributo. Esta marca se define en una columna de modelos de minería de datos.  
  
 Los algoritmos de terceros pueden admitir marcas de modelado adicionales. Para determinar un algoritmo de marcas de modelado que admite, use la **SUPPORTED_MODELING_FLAGS** de filas de esquema. También puede consultar los servicios de minería de datos en el servidor para determinar qué marcas de modelado se admiten en un algoritmo determinado. Por ejemplo, la consulta siguiente devuelve las marcas de modelado admitidas para el algoritmo de regresión lineal de Microsoft en el servidor actual:  
  
```  
SELECT SUPPORTED_MODELING_FLAGS  
FROM $SYSTEM.DMSCHEMA_MINING_SERVICES  
WHERE SERVICE_NAME = 'Microsoft_Linear_Regression'  
```  
  
 Resultados esperados:  
  
 NOT NULL,REGRESSOR  
  
## <a name="specifying-modeling-flags-on-a-mining-model"></a>Especificar las marcas de modelado en un modelo de minería de datos  
 Para obtener ejemplos de la sintaxis que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] admite para especificar una marca en una columna de estructura de minería de datos, vea [CREATE MINING STRUCTURE &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md).  
  
 Para obtener un ejemplo de la sintaxis para especificar un marcador de modelado en una columna de modelo de minería de datos, vea [ALTER MINING STRUCTURE &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md).  
  
 Para obtener más información sobre cómo trabajar con columnas del modelo de minería de datos, vea [columnas del modelo de minería de datos](../analysis-services/data-mining/mining-model-columns.md).  
  
## <a name="see-also"></a>Vea también  
 [Algoritmos de minería de datos &#40;Analysis Services - minería de datos&#41;](../analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de operadores](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensiones de minería de datos &#40;DMX&#41; convenciones de sintaxis](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estructura y el uso de consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  
