---
title: Cuadro de diálogo filtro de conjunto de datos o filtro de modelo | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: a9602174-b7e2-4e16-8ded-dfd8eb9264d7
author: minewiskan
ms.author: owend
ms.openlocfilehash: fbc9c9b7a09b0d7f06db624be9d94978ab996621
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529021"
---
# <a name="data-set-filter-or-model-filter-dialog-box"></a>Cuadro de diálogo Filtro de conjunto de datos o Filtro de modelo
  Este cuadro de diálogo le ayuda a generar los filtros que puede aplicar a un conjunto de datos.  El conjunto de datos puede ser un conjunto de datos externo que se use para las pruebas, o los datos del caso para un modelo de minería. El nombre del cuadro de diálogo cambia en función de si el filtro está destinado a un conjunto de datos externo o a un modelo de minería.  
  
 Si aplica el filtro a un conjunto de datos nuevo, el modelo de minería de datos se evalúa utilizando solamente esos casos en el conjunto de datos que cumpla las condiciones. Si aplica el filtro al propio modelo de minería, el modelo se entrenará y se probará utilizando solamente los casos del conjunto de datos de pruebas existente que cumpla los criterios del filtro.  
  
-   El cuadro de diálogo **Filtro de conjunto de datos** está disponible en la pestaña **Selección de entrada** del diseñador **Gráfico de precisión de minería de datos** .  
  
-   El cuadro de diálogo **Filtro de modelos** está disponible en la pestaña **Modelos de minería de datos** del diseñador Minería de datos.  
  
-   La cuadrícula **Condiciones** contiene las columnas en las que puede especificar un nombre de columna o de tabla, un operador y los valores deseados. Mediante esta cuadrícula, básicamente está creando una cláusula WHERE.  
  
> [!TIP]  
>   Para probar la exactitud en un subconjunto de los datos de entrenamiento originales, puede agregar la vista del origen de datos que se usó para definir el conjunto de entrenamiento como datos de prueba externos y, a continuación, agregar las condiciones en la cuadrícula **Filtro de conjunto de datos** .  
  
 **Para más información:** [Prueba y validación &#40;minería de datos&#41;](data-mining/testing-and-validation-data-mining.md)  
  
## <a name="options"></a>Opciones  
 **Condiciones**  
 Muestra los nombres de tabla, seguidos de los nombres de columna y las condiciones.  
  
|Value|Descripción|  
|-----------|-----------------|  
|**Y/o**|Elija un operador para unir varias condiciones.|  
|**Columna de la estructura de minería de datos**|Haga clic para seleccionar un origen de datos y, a continuación, haga clic en las líneas sucesivas en la cuadrícula para agregar las columnas del origen de datos.<br /><br /> La primera línea de la cuadrícula especifica la vista del origen de datos. Después de seleccionar una vista del origen de datos, **Columna de la estructura de minería de datos** muestra un icono de tabla y el campo **Valor** muestra la combinación de todos los criterios que ha definido para este origen de datos.<br /><br /> Después de haber seleccionado un origen de datos, el cuadro **Columna de la estructura de minería de datos** proporciona una lista desplegable de columnas individuales del origen de datos.|  
|**Operador**|Seleccione un operador de la lista.|  
|**Valor**|Para las tablas, el campo **Valor** muestra la combinación de todos los filtros que se aplican al origen de datos. También puede hacer clic en el botón compilar **(...)** que se encuentra a la derecha del cuadro de texto para abrir el cuadro de diálogo **filtro** y generar una condición.|  
  
 **Expression**  
 Muestra el conjunto de criterios que generó con la cuadrícula.  
  
 **Editar consulta**  
 Cambia el modo de edición de filtro para que pueda escribir directamente una expresión de filtro en el cuadro de texto **Expresión** .  
  
> [!NOTE]  
>  Una vez realizados los cambios manuales en la expresión de filtro, no puede volver al modo de edición de cuadrícula, incluso después de haber guardado la expresión en el cuadro **expresión de filtro** en la pestaña **selección de entrada** . Si desea crear una expresión con la cuadrícula, debe eliminar la expresión de filtro existente y empezar de nuevo.  
  
 **Revertir modificaciones de consulta**  
 Restaura la cuadrícula a su estado anterior y cancela cualquier cambio que realizara en la expresión de filtro.  
  
## <a name="see-also"></a>Consulte también  
 [Tareas y procedimientos de prueba y validación &#40;&#41;de minería de datos](data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)   
 [Diseñador de gráficos de precisión de minería de datos &#40;&#41;de minería de datos](mining-accuracy-chart-designer-data-mining.md)  
  
  
