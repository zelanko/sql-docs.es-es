---
title: Funciones (DMX) | Documentos de Microsoft
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- DMX
helpviewer_keywords:
- DMX [Analysis Services], functions
- VBA [DMX]
- stored procedures [DMX]
- functions [DMX]
- Excel [DMX]
- Data Mining Extensions [Analysis Services], functions
ms.assetid: 75ab6346-f4a4-4699-90f3-66d35f930ed7
caps.latest.revision: 39
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: b12a4a948dcb90c43eee52a01436ac0ca0c3f174
ms.contentlocale: es-es
ms.lasthandoff: 08/02/2017

---
# <a name="functions-dmx"></a>Funciones (DMX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cuando usa extensiones de minería de datos (DMX) para consultar objetos en [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], puede utilizar funciones para devolver más información que solo los valores de las columnas en el modelo de minería de datos o el conjunto de datos de entrada. Por ejemplo, puede usar consultas DMX para devolver no solo el valor de predicción de una columna, sino también la probabilidad de que la predicción sea correcta. Además de las funciones DMX, también puede utilizar funciones de Microsoft Visual Basic para Aplicaciones (VBA) y de Microsoft Excel, y procedimientos almacenados.  
  
## <a name="dmx-functions"></a>Funciones DMX  
 Puede usar funciones DMX para realizar las tareas siguientes:  
  
-   Devolver predicciones.  
  
-   Devolver estadísticas acerca de una predicción, como la probabilidad y el soporte.  
  
-   Filtrar los resultados de una consulta.  
  
-   Reordenar una expresión de tabla.  
  
 La mayoría de las funciones DMX devuelven un valor escalar, como el soporte de una predicción, pero algunas devuelven un resultado tabular. Por ejemplo, la función PredictHistogram devuelve una tabla que contiene la compatibilidad y probabilidad para cada estado de la columna predecible especificada. Los resultados se muestran como una nueva columna tabular.  
  
 **Para obtener más información:** [funciones de predicción generales &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md), [extensiones de minería de datos &#40; DMX &#41; Referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)  
  
## <a name="visual-basic-for-applications-vba-and-excel-functions"></a>Funciones de Excel y Visual Basic para Aplicaciones (VBA)  
 Además de las funciones DMX, también puede llamar a diversas funciones de VBA y Excel desde las instrucciones DMX. Por ejemplo, puede usar la función lCase para modificar cómo se muestra la columna Attribute_Name en el contenido del modelo TM_Decision_Tree. Esto se muestra en el siguiente ejemplo de código.  
  
```  
SELECT lCase([Attribute_Name])   
FROM [TM_Decision_Tree].CONTENT  
```  
  
 Si existe la misma función en VBA y Excel, se debe anteponer al nombre de función en la instrucción DMX **VBA** o **Excel**. Por ejemplo, usaría `VBA!Log` o `Excel!Log`. Si la función de VBA o Excel que desea usar también existe en DMX o MDX (Expresiones multidimensionales), o si la función contiene un signo de moneda ($), deberá usar corchetes ([]) como caracteres de escape para la función. Por ejemplo, la llamada a la función sería `[VBA!Format]`.  
  
## <a name="stored-procedures"></a>Procedimientos almacenados  
 Puede usar lenguajes de programación de Common Language Runtime para crear procedimientos almacenados que amplíen la funcionalidad de DMX. Por ejemplo, un modelo de minería de datos de árbol de regresión devuelve coeficientes, por ejemplo, A, B y así sucesivamente, que describen la ecuación de regresión, pero el modelo no devuelve la ecuación, como A + Bx = y. Sin embargo, puede escribir un procedimiento almacenado que use el objeto de modelo de minería de datos para navegar por el esquema de contenido y para devolver la ecuación de regresión como salida. Por lo tanto, una instrucción DMX puede devolver una lista de las ecuaciones de regresión como parte del resultado de la consulta.  
  
 **Para obtener más información:** [administración de ensamblados de modelos multidimensionales](../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)  
  
## <a name="see-also"></a>Vea también  
 [Extensiones de minería de datos &#40; DMX &#41; Referencia](../dmx/data-mining-extensions-dmx-reference.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de funciones](../dmx/data-mining-extensions-dmx-function-reference.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de operadores](../dmx/data-mining-extensions-dmx-operator-reference.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Referencia de instrucciones](../dmx/data-mining-extensions-dmx-statements.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Convenciones de sintaxis](../dmx/data-mining-extensions-dmx-syntax-conventions.md)   
 [Extensiones de minería de datos &#40; DMX &#41; Elementos de sintaxis](../dmx/data-mining-extensions-dmx-syntax-elements.md)   
 [Funciones de predicción generales &#40; DMX &#41;](../dmx/general-prediction-functions-dmx.md)   
 [Estructura y el uso de consultas de predicción DMX](../dmx/structure-and-usage-of-dmx-prediction-queries.md)   
 [Descripción de la instrucción Select de DMX](../dmx/understanding-the-dmx-select-statement.md)  
  
  

