---
title: Pestaña selección (vista de gráfico de precisión de minería de datos) de entrada | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dm.miningmodeleditor.accuracychart.columnmapping.f1
ms.assetid: f8b1193c-5c86-4c7e-8e35-158d293184fa
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: eb5abde47c5da9405f7768f1167496fdd603f04f
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36203066"
---
# <a name="input-selection-tab-mining-accuracy-chart-view"></a>Pestaña Selección de entrada (vista Gráfico de precisión de minería de datos)
  Utilice la pestaña **Selección de entrada** del diseñador **Gráfico de precisión de minería de datos** para especificar el origen de datos que se utiliza para probar el modelo y generar el gráfico de precisión.  
  
 **Para más información:** [Prueba y validación &#40;minería de datos&#41;](data-mining/testing-and-validation-data-mining.md)  
  
## <a name="options"></a>Opciones  
 **Sincronizar columnas y valores de** **predicción**  
 Seleccione esta opción para coordinar los atributos de predicción de la cuadrícula a fin de que se deriven de la misma columna de estructura de minería de datos de predicción, incluso aunque tengan un nombre diferente, durante el entrenamiento del modelo.  
  
 **Nota** : esta opción no está seleccionada de forma predeterminada. Solamente debería activar esta casilla en los casos en los que sepa que dos columnas de estructura de minería de datos se derivan del mismo origen multidimensional o relacional subyacente, y en los que las columnas contengan los mismos estados o se hayan discretizado del mismo modo.  
  
 **Seleccione columnas del modelo de predicción de minería de datos que se mostrarán en el gráfico de elevación**  
 Cuadrícula que contiene columnas para controlar qué modelos se incluyen en el gráfico de elevación y cómo se utilizan en éste.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Mostrar**|Active la casilla situada junto al nombre de cada columna de predicción del modelo de minería que desee mostrar en el gráfico.<br /><br /> Si el gráfico es demasiado complejo para verlo con facilidad, borre el cuadro situado al lado de una o varias columnas para simplificar el gráfico.<br /><br /> Nota: No se pueden crear gráficos de precisión hasta que haya al menos una columna seleccionada.|  
|**Modelo de minería de datos**|Muestra los modelos de minería contenidos en la estructura de minería.|  
|**Nombre de columna de predicción**|Seleccione una columna de predicción que esté contenida dentro de los modelos de minería de datos que se utilizarán para crear el gráfico de elevación.|  
|**Valor de predicción**|Seleccione un valor para la columna de predicción. Si deja esta opción en blanco, el gráfico de elevación predice en qué medida será satisfactoria la realización del modelo para todos los estados de la columna de predicción.|  
  
 **Seleccionar un conjunto de datos que se usará para el gráfico de precisión**  
 Grupo de opciones que contiene tres opciones para especificar los datos de las pruebas de precisión.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**Usar casos de prueba de modelo de minería de datos**|Utilice el conjunto de pruebas que se creó cuando dividió la estructura de minería de datos, y aplique el filtro que se define en el modelo. Para más información sobre filtros de modelos, vea [Filters for Mining Models &#40;Analysis Services - Data Mining&#41;](data-mining/mining-models-analysis-services-data-mining.md)|  
|**Usar casos de prueba de estructura de minería de datos**|Utilice el conjunto de pruebas que se creó cuando dividió la estructura de minería de datos.|  
|**Especificar otro conjunto de datos**|Especifique una tabla de una vista del origen de datos existente para utilizar como conjunto de datos de pruebas.|  
  
## <a name="filtering-options"></a>Opciones de filtrado  
 Si selecciona la opción **Especificar otro conjunto de datos**, puede definir una vista del origen de datos y crear filtros para aplicarlos a esos datos. Al crear un filtro, está creando una cláusula WHERE en la consulta que devuelve los datos de pruebas de la vista del origen de datos.  
  
 **Nota** : no puede especificar un filtro en el modelo de minería con la pestaña **Selección de entrada** . Para crear un filtro de modelo, haga clic en la pestaña **Modelos de minería de datos** y modifique las propiedades del modelo.  
  
 Si no creó un conjunto de exclusiones para las pruebas cuando creó la estructura de minería de datos, puede seleccionar esta opción y, a continuación, especificar la vista del origen de datos original como conjunto de pruebas. Con esta solución alternativa, puede establecer también filtros en el conjunto de datos original.  
  
 **Especificar una asignación de columna**  
 Abre el cuadro de diálogo **Especificar asignación de columnas**, en el que se selecciona el origen de datos, se especifican el caso y las tablas anidadas y se asignan columnas de datos externas a las columnas de estructura de minería de datos.  
  
 Para más información, vea [Cuadro de diálogo Especificar asignación de columna &#40;gráfico de precisión de minería de datos&#41;](specify-column-mapping-dialog-box-mining-accuracy-chart.md).  
  
 **Expresión de filtro**  
 Muestra la condición de filtro que se generó con los editores de filtro.  
  
 **Abrir Editor de filtros**  
 Abre el cuadro de diálogo **Filtro de conjunto de datos** , que le permite seleccionar las tablas externas y establecer condiciones en las columnas de la tabla de casos, y el cuadro de diálogo **Filtro** , que le ayuda a generar las condiciones que se aplican a las columnas individuales de la tabla seleccionada, o a las columnas de las tablas anidadas.  
  
## <a name="see-also"></a>Vea también  
 [Pruebas y las tareas de validación y procedimientos &#40;minería de datos&#41;](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [Diseñador de gráficos de precisión de minería de datos &#40;minería de datos&#41;](mining-accuracy-chart-designer-data-mining.md)   
 [Aplicar un filtro a un modelo de minería de datos](data-mining/apply-a-filter-to-a-mining-model.md)   
 [Filtros para modelos de minería de datos de &#40;Analysis Services: minería de datos&#41;](data-mining/mining-models-analysis-services-data-mining.md)  
  
  