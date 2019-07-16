---
title: Estructura y el uso de consultas de predicción DMX | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 99d8ef98ad4e86bce0e1beff819a8d140662aaf7
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67938067"
---
# <a name="structure-and-usage-of-dmx-prediction-queries"></a>Estructura y uso de las consultas de predicción DMX
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  En [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], puede usar la consulta de predicción de extensiones de minería de datos (DMX) para predecir valores de columna desconocidos de un nuevo conjunto de datos, basándose en los resultados de un modelo de minería de datos.  
  
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
  
-   **SELECCIONE [APLANADO]**  
  
-   **TOP**  
  
-   **DESDE** *\<modelo >* **PREDICTION JOIN**  
  
-   **ON**  
  
-   **WHERE**  
  
-   **ORDER BY**  
  
 El **seleccione** elemento de una consulta de predicción define las columnas y expresiones que se mostrarán en el resultado y pueden incluir los siguientes datos:  
  
-   **Predecir** o **PredictOnly** columnas del modelo de minería de datos.  
  
-   Cualquier columna de los datos de entrada que sirve para crear las predicciones.  
  
-   Funciones que devuelven una columna de datos.  
  
 El **FROM**  *\<modelo >* **PREDICTION JOIN** elemento define los datos de origen que se usará para crear la predicción. Para una consulta singleton, se trata de una serie de valores que se asignan a columnas. Para una combinación de predicción vacía, se deja en blanco.  
  
 El **ON** elemento asigna las columnas que se definen en el modelo de minería de datos a columnas en un conjunto de datos externo. No es necesario incluir este elemento si se va a crear una consulta de combinación de predicción vacía o una combinación de predicción natural.  
  
 Puede usar el **donde** cláusula para filtrar los resultados de una consulta de predicción. Puede usar un **superior** o **ORDER BY** cláusula para seleccionar las predicciones más probables. Para obtener más información sobre el uso de estas cláusulas, vea [seleccione &#40;DMX&#41;](../dmx/select-dmx.md).  
  
 Para obtener más información sobre la sintaxis de una instrucción de predicción, vea [SELECT FROM &#60;modelo&#62; PREDICTION JOIN &#40;DMX&#41; ](../dmx/select-from-model-prediction-join-dmx.md) y [SELECT FROM &#60;modelo&#62; &#40;DMX &#41;](../dmx/select-from-model-dmx.md).  
  
## <a name="see-also"></a>Vea también  
 [Referencia de Extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de operadores](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensiones de minería de datos &#40;DMX&#41; referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensiones de minería de datos &#40;DMX&#41; convenciones de sintaxis](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensiones de minería de datos &#40;DMX&#41; elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  
