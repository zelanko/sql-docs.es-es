---
title: Estructura y uso de las consultas de predicción DMX | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: e2aaeedff9eb0d22d6a7175641177f803379adaa
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970293"
---
# <a name="structure-and-usage-of-dmx-prediction-queries"></a>Estructura y uso de las consultas de predicción DMX
[!INCLUDE[ssas](../includes/applies-to-version/ssas.md)]

  En [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , puede utilizar la consulta de predicción de extensiones de minería de datos (DMX) para predecir valores de columna desconocidos en un nuevo conjunto de datos, en función de los resultados de un modelo de minería de datos.  
  
 El tipo de consulta utilizado depende de la información que desee obtener del modelo. Si desea crear predicciones sencillas en tiempo real, como por ejemplo para saber si el perfil de un cliente potencial de un sitio web se ajusta al perfil de un comprador de bicicletas, entonces deberá usar una consulta singleton. Si desea crear un lote de predicciones a partir de un conjunto de escenarios incluidos en un origen de datos, deberá usar una consulta de predicción normal.  
  
## <a name="prediction-types"></a>Tipos de predicción  
 Puede usar DMX para crear los siguientes tipos de predicción:  
  
 Combinación de predicción  
 Sirve para crear predicciones de datos de entrada basadas en los patrones existentes en el modelo de minería de datos. Esta instrucción de consulta debe ir seguida de una cláusula on que proporcione las condiciones de combinación entre las columnas del modelo de minería de datos y las columnas **de** entrada.  
  
 Combinación de predicción natural  
 Sirve para crear predicciones basadas en nombres de columna del modelo de minería de datos que coinciden exactamente con los nombres de columna de la tabla en la que se realiza la consulta. Esta instrucción de consulta no requiere una cláusula ON, porque la condición **de** combinación se genera automáticamente en función de los nombres coincidentes entre las columnas del modelo de minería de datos y las columnas de entrada.  
  
 Combinación de predicción vacía  
 Sirve para descubrir la predicción más probable, sin necesidad de proporcionar datos de entrada. Devuelve una predicción que está basada exclusivamente en el contenido del modelo de minería de datos.  
  
 Consulta singleton  
 Sirve para crear una predicción proporcionando los datos a la consulta. Esta instrucción resulta útil porque puede proporcionar un solo escenario a la consulta para recibir un resultado rápidamente. Por ejemplo, puede usar la consulta para predecir la probabilidad de que una persona del sexo femenino, de 35 años de edad y casada compre una bicicleta. Esta consulta no requiere un origen de datos externo.  
  
## <a name="query-structure"></a>Estructura de la consulta  
 Para generar una consulta de predicción en DMX, debe usar una combinación de los siguientes elementos:  
  
-   **SELECT [APLANAD]**  
  
-   **TOP**  
  
-   **Desde** *\<model>* **combinación de predicción**      
  
-   **ON**  
  
-   **WHERE**  
  
-   **ORDER BY**  
  
 El elemento **Select** de una consulta de predicción define las columnas y expresiones que aparecerán en el conjunto de resultados, y puede incluir los datos siguientes:  
  
-   **Predecir** o **PredictOnly** columnas del modelo de minería de datos.  
  
-   Cualquier columna de los datos de entrada que sirve para crear las predicciones.  
  
-   Funciones que devuelven una columna de datos.  
  
 El elemento **from** *\<model>* **join de predicción** define los datos de origen que se van a utilizar para crear la predicción. Para una consulta singleton, se trata de una serie de valores que se asignan a columnas. Para una combinación de predicción vacía, se deja en blanco.  
  
 El elemento **on** asigna las columnas definidas en el modelo de minería de datos a las columnas de un conjunto de datos externo. No es necesario incluir este elemento si se va a crear una consulta de combinación de predicción vacía o una combinación de predicción natural.  
  
 Puede usar la cláusula **Where** para filtrar los resultados de una consulta de predicción. Puede usar una cláusula **Top** o **order by** para seleccionar las predicciones más probables. Para obtener más información sobre el uso de estas cláusulas, consulte [seleccionar &#40;DMX&#41;](../dmx/select-dmx.md).  
  
 Para obtener más información sobre la sintaxis de una instrucción de predicción, vea [seleccionar desde &#60;modelo&#62; combinación de predicción &#40;dmx&#41;](../dmx/select-from-model-prediction-join-dmx.md) y [Seleccione entre &#60;modelo&#62; &#40;DMX ](../dmx/select-from-model-dmx.md)&#41;.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Referencia de funciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referencia de operadores &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Referencia de instrucciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)   
 [Convenciones de sintaxis de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensiones de minería de datos &#40;DMX&#41; elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  
