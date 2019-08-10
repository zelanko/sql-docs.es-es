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
ms.openlocfilehash: a610f3aed7f520163dc4e2b30651d8b0397ef644
ms.sourcegitcommit: a1adc6906ccc0a57d187e1ce35ab7a7a951ebff8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/09/2019
ms.locfileid: "68893930"
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
  
 Los algoritmos de terceros pueden admitir marcas de modelado adicionales. Para determinar qué marcas de modelado admite un algoritmo, use el conjunto de filas de esquema **SUPPORTED_MODELING_FLAGS** . También puede consultar los servicios de minería de datos en el servidor para determinar qué marcas de modelado se admiten en un algoritmo determinado. Por ejemplo, la consulta siguiente devuelve las marcas de modelado admitidas para el algoritmo de regresión lineal de Microsoft en el servidor actual:  
  
```  
SELECT SUPPORTED_MODELING_FLAGS  
FROM $SYSTEM.DMSCHEMA_MINING_SERVICES  
WHERE SERVICE_NAME = 'Microsoft_Linear_Regression'  
```  
  
 Resultados esperados:  
  
 NOT NULL,REGRESSOR  
  
## <a name="specifying-modeling-flags-on-a-mining-model"></a>Especificar las marcas de modelado en un modelo de minería de datos  
 Para obtener ejemplos de la sintaxis [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que admite la especificación de una marca en una columna de estructura de minería de datos, vea [Create Mining Structure &#40;&#41;DMX](../dmx/create-mining-structure-dmx.md).  
  
 Para obtener un ejemplo de la sintaxis para especificar un marcador de modelado en una columna de modelo de minería de datos, vea [ALTER Mining Structure &#40;&#41;DMX](../dmx/alter-mining-structure-dmx.md).  
  
 Para obtener más información sobre cómo trabajar con columnas del modelo de minería de datos, vea [columnas del modelo de minería de datos](https://docs.microsoft.com/analysis-services/data-mining/mining-model-columns).  
  
## <a name="see-also"></a>Vea también  
 [Algoritmos de minería de datos &#40;Analysis Services: Minería de datos&#41;](https://docs.microsoft.com/analysis-services/data-mining/data-mining-algorithms-analysis-services-data-mining)   
 [Referencia de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Elementos de sintaxis &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Referencia de funciones &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referencia del operador &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Referencia de la &#40;instrucción&#41; DMX de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-statements.md)   
 [Convenciones de sintaxis &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Funciones &#40;de predicción generales DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estructura y uso de las consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  
