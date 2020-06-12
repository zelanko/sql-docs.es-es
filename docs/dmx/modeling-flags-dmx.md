---
title: Marcas de modelado (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: cf7389ee0097428bd5825c81abd36f3bdc5c02d2
ms.sourcegitcommit: 4cb53a8072dbd94a83ed8c7409de2fb5e2a1a0d9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/19/2020
ms.locfileid: "83667944"
---
# <a name="modeling-flags-dmx"></a>Marcas de modelado (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Puede utilizar marcas de modelado en [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] para proporcionar información adicional a un algoritmo de minería de datos acerca de los datos que se definen en una tabla de casos. El algoritmo puede usar esta información para crear un modelo de minería de datos más preciso. Puede definir marcas de modelado tanto en columnas de estructura de minería de datos como en columnas de modelos de minería de datos.  
  
 [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] admite las siguientes marcas de modelado:  
  
 **NO NULL**  
 Los valores de la columna de atributos nunca deben incluir un valor NULL. Se producirá un error si [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] encuentra un valor NULL para esta columna de atributos durante el proceso de entrenamiento de modelos. Esta marca se define en una columna de estructura de minería de datos.  
  
 **REGRESOR**  
 Indica que el algoritmo puede usar la columna especificada en la fórmula de regresión de algoritmos de regresión. Esta marca es compatible con los algoritmos de regresión lineal de [!INCLUDE[msCoName](../includes/msconame-md.md)] y árboles de decisión de [!INCLUDE[msCoName](../includes/msconame-md.md)] y se define en una columna de modelos de minería de datos.  
  
 **MODEL_EXISTENCE_ONLY**  
 Los valores de la columna de atributos no son tan importantes como la presencia del atributo. Esta marca se define en una columna de modelos de minería de datos.  
  
 Los algoritmos de terceros pueden admitir marcas de modelado adicionales. Para determinar qué marcas de modelado admite un algoritmo, use el conjunto de filas de esquema **SUPPORTED_MODELING_FLAGS** . También puede consultar los servicios de minería de datos en el servidor para determinar qué marcas de modelado se admiten en un algoritmo determinado. Por ejemplo, la consulta siguiente devuelve las marcas de modelado admitidas para el algoritmo de regresión lineal de Microsoft en el servidor actual:  
  
```  
SELECT SUPPORTED_MODELING_FLAGS  
FROM $SYSTEM.DMSCHEMA_MINING_SERVICES  
WHERE SERVICE_NAME = 'Microsoft_Linear_Regression'  
```  
  
 Resultados esperados:  
  
 NOT NULL,REGRESSOR  
  
## <a name="specifying-modeling-flags-on-a-mining-model"></a>Especificar las marcas de modelado en un modelo de minería de datos  
 Para obtener ejemplos de la sintaxis que [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] admite la especificación de una marca en una columna de estructura de minería de datos, vea [Create mining Structure &#40;DMX&#41;](../dmx/create-mining-structure-dmx.md).  
  
 Para obtener un ejemplo de la sintaxis para especificar un marcador de modelado en una columna de modelo de minería de datos, vea [ALTER Mining STRUCTURE &#40;DMX&#41;](../dmx/alter-mining-structure-dmx.md).  
  
 Para obtener más información sobre cómo trabajar con columnas del modelo de minería de datos, vea [columnas del modelo de minería de datos](https://docs.microsoft.com/analysis-services/data-mining/mining-model-columns).  
  
## <a name="see-also"></a>Consulte también  
 [Algoritmos de minería de datos &#40;Analysis Services:&#41;de minería de datos](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [Referencia de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Referencia de funciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referencia de operadores &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Referencia de instrucciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)   
 [Convenciones de sintaxis de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estructura y uso de las consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  
