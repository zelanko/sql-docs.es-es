---
title: "Diseñador de minería de datos | Documentos de Microsoft"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data mining [Analysis Services], structure
- mining structures [Analysis Services], modifying
- data mining editor [Analysis Services]
- Data Mining Designer
- data mining [Analysis Services], modifying
ms.assetid: 2540db5b-2bf3-4b6c-87c8-79c48d71acce
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 4020ae2dd9bd8fa07a97f5817a0f06969fc0bb73
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="data-mining-designer"></a>Diseñador de minería de datos
  El Diseñador de minería de datos es el entorno principal en el que se trabaja con modelos de minería de datos en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Puede obtener acceso al diseñador seleccionando una estructura de minería de datos existente o utilizando el Asistente para minería de datos para crear una nueva estructura y un nuevo modelo de minería de datos. Puede usar el Diseñador de minería de datos para realizar las tareas siguientes:  
  
-   Modificar la estructura y el modelo de minería de datos que se crearon inicialmente con el Asistente para minería de datos.  
  
-   Crear nuevos modelos basados en una estructura de minería de datos existente.  
  
-   Entrenar y examinar modelos de minería de datos.  
  
-   Comparar modelos mediante gráficos de precisión.  
  
-   Crear consultas de predicción basadas en modelos de minería de datos.  
  
## <a name="mining-structure-tab"></a>Pestaña Estructura de minería de datos  
 Utilice la pestaña **Estructura de minería de datos** para agregar columnas y modificar las propiedades de una estructura de minería de datos existente. Las tareas y los temas siguientes proporcionan más información sobre cómo trabajar con estructuras de minería de datos:  
  
 [Estructuras de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)  
  
 [Tareas y procedimientos de las estructuras de minería de datos](../../analysis-services/data-mining/mining-structure-tasks-and-how-tos.md)  
  
## <a name="mining-models-tab"></a>Pestaña Modelos de minería de datos  
 Utilice la pestaña **Modelos de minería de datos** para administrar modelos de minería de datos existentes y crear otros nuevos. Los modelos de minería de datos siempre se basan en una estructura de minería de datos existente.  
  
 En la pestaña **Modelos de minería de datos** , puede cambiar el tipo de algoritmo, agregar o quitar columnas asociadas con la estructura del modelo, ajustar propiedades de columna específicas del algoritmo, especificar el uso de la columna del modelo de minería de datos y ajustar parámetros de algoritmo asociados con el modelo de minería de datos. También puede procesar la estructura de minería de datos junto con los modelos seleccionados o con todos los modelos asociados.  
  
 Vea los temas siguientes para obtener más información sobre cómo trabajar con los modelos de minería de datos:  
  
 [Modelos de minería de datos &#40;Analysis Services - Minería de datos&#41;](../../analysis-services/data-mining/mining-models-analysis-services-data-mining.md)  
  
 [Tareas y procedimientos de los modelos de minería de datos](../../analysis-services/data-mining/mining-model-tasks-and-how-tos.md)  
  
## <a name="mining-model-viewer-tab"></a>Pestaña Visor de modelos de minería de datos  
 Utilice la pestaña **Visor de modelos de minería de datos** para explorar visualmente los modelos de minería de datos. Cada modelo de minería de datos está asociado con un visor personalizado que muestra el contenido específico de ese modelo. También puede ver el contenido del modelo de minería de datos utilizando el visor de contenido.  
  
 Vea los temas siguientes para obtener más información sobre cómo explorar los modelos de minería de datos con los visores de minería de datos:  
  
 [Visores de modelos de minería de datos](../../analysis-services/data-mining/data-mining-model-viewers.md)  
  
 [Tareas y procedimientos del Visor de modelos de minería de datos](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)  
  
## <a name="mining-accuracy-chart-tab"></a>Pestaña Gráfico de precisión de minería de datos  
 Utilice la pestaña **Gráfico de precisión de minería de datos** para probar la precisión de predicción de un único modelo de minería de datos o para comparar la eficacia de varios modelos de minería de datos contenidos en una estructura de minería de datos. La pestaña contiene herramientas para filtrar los datos, seleccionar modelos y mostrar los resultados en un gráfico de elevación, en un gráfico de beneficios o en una matriz de clasificación.  
  
 Vea los siguientes temas para obtener más información acerca de la prueba y la validación de modelos de minería de datos:  
  
 [Prueba y validación &#40;minería de datos&#41;](../../analysis-services/data-mining/testing-and-validation-data-mining.md)  
  
 [Tareas y procedimientos de prueba y validación &#40;minería de datos&#41;](../../analysis-services/data-mining/testing-and-validation-tasks-and-how-tos-data-mining.md)  
  
## <a name="mining-model-prediction-tab"></a>Pestaña Predicción de modelo de minería de datos  
 La pestaña **Predicción de modelo de minería de datos** incluye el Generador de consultas de predicción, que se puede usar para crear consultas de predicción DMX (Extensiones de minería de datos). La pestaña contiene herramientas para especificar modelos de minería de datos y tablas de entrada, asignar las columnas del modelo de minería de datos a las columnas de la tabla de entrada, agregar funciones a una consulta y especificar criterios para cada columna.  
  
 Tras diseñar una consulta, puede utilizar diferentes vistas de la pestaña para mostrar los resultados de la consulta y para modificarla manualmente. También puede guardar los resultados de la consulta en una tabla de una base de datos.  
  
 Vea los temas siguientes para obtener más información sobre cómo crear consultas de minería de datos:  
  
 [Consultas de minería de datos](../../analysis-services/data-mining/data-mining-queries.md)  
  
 [Tareas y procedimientos de Consulta de minería de datos](../../analysis-services/data-mining/data-mining-query-tasks-and-how-tos.md)  
  
## <a name="see-also"></a>Vea también  
 [Soluciones de minería de datos](../../analysis-services/data-mining/data-mining-solutions.md)  
  
  
