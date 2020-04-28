---
title: Funciones (DMX) | Microsoft Docs
ms.date: 06/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: dmx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: f68a66e778d44059a83ca6eca3cee35b4dffca9c
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68892762"
---
# <a name="functions-dmx"></a>Funciones (DMX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  Al utilizar extensiones de minería de datos (DMX) para consultar objetos [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]en, puede utilizar funciones para devolver más información que solo los valores de las columnas del modelo de minería de datos o del conjunto de datos de entrada. Por ejemplo, puede usar consultas DMX para devolver no solo el valor de predicción de una columna, sino también la probabilidad de que la predicción sea correcta. Además de las funciones DMX, también puede utilizar funciones de Microsoft Visual Basic para Aplicaciones (VBA) y de Microsoft Excel, y procedimientos almacenados.  
  
## <a name="dmx-functions"></a>Funciones DMX  
 Puede usar funciones DMX para realizar las tareas siguientes:  
  
-   Devolver predicciones.  
  
-   Devolver estadísticas acerca de una predicción, como la probabilidad y el soporte.  
  
-   Filtrar los resultados de una consulta.  
  
-   Reordenar una expresión de tabla.  
  
 La mayoría de las funciones DMX devuelven un valor escalar, como el soporte de una predicción, pero algunas devuelven un resultado tabular. Por ejemplo, la función PredictHistogram devuelve una tabla que contiene la compatibilidad y la probabilidad de cada estado de la columna de predicción especificada. Los resultados se muestran como una nueva columna tabular.  
  
 **Para obtener más información: funciones de** [predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md), [extensiones de minería de datos &#40;referencia de funciones DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)  
  
## <a name="visual-basic-for-applications-vba-and-excel-functions"></a>Funciones de Excel y Visual Basic para Aplicaciones (VBA)  
 Además de las funciones DMX, también puede llamar a diversas funciones de VBA y Excel desde las instrucciones DMX. Por ejemplo, puede utilizar la función lCase para modificar el modo en que se muestra la columna de Attribute_Name en el contenido del modelo de TM_Decision_Tree. Esto se muestra en el siguiente ejemplo de código.  
  
```  
SELECT lCase([Attribute_Name])   
FROM [TM_Decision_Tree].CONTENT  
```  
  
 Si existe la misma función en VBA y en Excel, debe prefijar el nombre de la función en la instrucción DMX con **VBA** o **Excel**. Por ejemplo, puede usar `VBA!Log` o. `Excel!Log` Si la función de VBA o Excel que desea usar también existe en DMX o MDX (Expresiones multidimensionales), o si la función contiene un signo de moneda ($), deberá usar corchetes ([]) como caracteres de escape para la función. Por ejemplo, la llamada a la función sería `[VBA!Format]`.  
  
## <a name="stored-procedures"></a>Procedimientos almacenados  
 Puede usar lenguajes de programación de Common Language Runtime para crear procedimientos almacenados que amplíen la funcionalidad de DMX. Por ejemplo, un modelo de minería de datos de árbol de regresión devuelve coeficientes, como A, B, etc., que describen la ecuación de regresión, pero el modelo no devuelve la propia ecuación, como un + BX = y. Sin embargo, puede escribir un procedimiento almacenado que use el objeto de modelo de minería de datos para navegar por el esquema de contenido y para devolver la ecuación de regresión como salida. Por lo tanto, una instrucción DMX puede devolver una lista de las ecuaciones de regresión como parte del resultado de la consulta.  
  
 **Para obtener más información: administración de** [ensamblados de modelos multidimensionales](https://docs.microsoft.com/analysis-services/multidimensional-models/multidimensional-model-assemblies-management)  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-reference.md)   
 [Referencia de funciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Referencia de operadores &#40;DMX&#41; de extensiones de minería de datos](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Referencia de instrucciones de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-statements.md)   
 [Convenciones de sintaxis de extensiones de minería de datos &#40;DMX&#41;](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensiones de minería de datos &#40;DMX&#41; elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funciones de predicción generales &#40;DMX&#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estructura y uso de las consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  
