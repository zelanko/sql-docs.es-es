---
title: Estructura y el uso de consultas de predicción DMX | Documentos de Microsoft
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: data-mining
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- prediction joins [DMX]
- empty prediction joins [DMX]
- natural prediction joins [DMX]
- DMX [Analysis Services], prediction queries
- prediction queries [DMX]
- queries [DMX], prediction queries
- singleton query predictions [DMX]
- Data Mining Extensions [Analysis Services], prediction queries
ms.assetid: 098bdaa6-9e7d-4e13-a9aa-eb17ce1750e6
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 5f25d8ecd230ca4d2e7aa6a694536e71f5dd0f4e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="structure-and-usage-of-dmx-prediction-queries"></a>Estructura y uso de las consultas de predicción DMX
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  En [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], puede usar la consulta de predicción de extensiones de minería de datos (DMX) para predecir valores de columna desconocido de un nuevo conjunto de datos, basándose en los resultados de un modelo de minería de datos.  
  
 El tipo de consulta utilizado depende de la información que desee obtener del modelo. Si desea crear predicciones sencillas en tiempo real, como por ejemplo para saber si el perfil de un cliente potencial de un sitio web se ajusta al perfil de un comprador de bicicletas, entonces deberá usar una consulta singleton. Si desea crear un lote de predicciones a partir de un conjunto de escenarios incluidos en un origen de datos, deberá usar una consulta de predicción normal.  
  
## <a name="prediction-types"></a>Tipos de predicción  
 Puede usar DMX para crear los siguientes tipos de predicción:  
  
 Combinación de predicción  
 Sirve para crear predicciones de datos de entrada basadas en los patrones existentes en el modelo de minería de datos. Esta instrucción de consulta debe ir seguida por un **ON** cláusula que proporciona las condiciones de combinación entre las columnas del modelo de minería de datos y las columnas de entrada.  
  
 Combinación de predicción natural  
 Sirve para crear predicciones basadas en nombres de columna del modelo de minería de datos que coinciden exactamente con los nombres de columna de la tabla en la que se realiza la consulta. Esta instrucción de consulta no requiere un **ON** cláusula, porque la condición de combinación se genera automáticamente basándose en los nombres coincidentes entre las columnas del modelo de minería de datos y las columnas de entrada.  
  
 Combinación de predicción vacía  
 Sirve para descubrir la predicción más probable, sin necesidad de proporcionar datos de entrada. Devuelve una predicción que está basada exclusivamente en el contenido del modelo de minería de datos.  
  
 Consulta singleton  
 Sirve para crear una predicción proporcionando los datos a la consulta. Esta instrucción resulta útil porque puede proporcionar un solo escenario a la consulta para recibir un resultado rápidamente. Por ejemplo, puede usar la consulta para predecir la probabilidad de que una persona del sexo femenino, de 35 años de edad y casada compre una bicicleta. Esta consulta no requiere un origen de datos externo.  
  
## <a name="query-structure"></a>Estructura de la consulta  
 Para generar una consulta de predicción en DMX, debe usar una combinación de los siguientes elementos:  
  
-   **SELECCIONE [FORMATO]**  
  
-   **TOP**  
  
-   **DE***\<modelo >***PREDICTION JOIN**   
  
-   **ON**  
  
-   **WHERE**  
  
-   **ORDENAR POR**  
  
 El **seleccione** elemento de una consulta de predicción define las columnas y conjunto de expresiones que se mostrarán en el resultado y pueden incluir los siguientes datos:  
  
-   **Predecir** o **PredictOnly** columnas del modelo de minería de datos.  
  
-   Cualquier columna de los datos de entrada que sirve para crear las predicciones.  
  
-   Funciones que devuelven una columna de datos.  
  
 El **FROM**  *\<modelo >* **PREDICTION JOIN** elemento define los datos de origen que se usará para crear la predicción. Para una consulta singleton, se trata de una serie de valores que se asignan a columnas. Para una combinación de predicción vacía, se deja en blanco.  
  
 El **ON** elemento asigna las columnas que se definen en el modelo de minería de datos a columnas de un conjunto de datos externo. No es necesario incluir este elemento si se va a crear una consulta de combinación de predicción vacía o una combinación de predicción natural.  
  
 Puede usar el **donde** cláusula para filtrar los resultados de una consulta de predicción. Puede usar un **arriba** o **ORDER BY** cláusula para seleccionar las predicciones más probables. Para obtener más información acerca del uso de estas cláusulas, vea [SELECT &#40; DMX &#41;](../dmx/select-dmx.md).  
  
 Para obtener más información acerca de la sintaxis de una instrucción de predicción, vea [SELECT FROM &#60; modelo &#62; COMBINACIÓN de PREDICCIÓN &#40; DMX &#41; ](../dmx/select-from-model-prediction-join-dmx.md) y [SELECT FROM &#60; modelo de &#62; &#40; DMX &#41;](../dmx/select-from-model-dmx.md).  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40; DMX &#41; Referencia](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de operadores](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Convenciones de sintaxis](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funciones de predicción generales &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  
