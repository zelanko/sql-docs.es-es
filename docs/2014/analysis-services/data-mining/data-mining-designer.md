---
title: Diseñador de minería de datos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data mining [Analysis Services], structure
- mining structures [Analysis Services], modifying
- data mining editor [Analysis Services]
- Data Mining Designer
- data mining [Analysis Services], modifying
ms.assetid: 2540db5b-2bf3-4b6c-87c8-79c48d71acce
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 010b9b18be2264add14bc5242ced6a57ed8fdcca
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48117395"
---
# <a name="data-mining-designer"></a>Data Mining Designer
  El Diseñador de minería de datos es el entorno principal en el que se trabaja con modelos de minería de datos en [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]. Puede obtener acceso al diseñador seleccionando una estructura de minería de datos existente o utilizando el Asistente para minería de datos para crear una nueva estructura y un nuevo modelo de minería de datos. Puede usar el Diseñador de minería de datos para realizar las tareas siguientes:  
  
-   Modificar la estructura y el modelo de minería de datos que se crearon inicialmente con el Asistente para minería de datos.  
  
-   Crear nuevos modelos basados en una estructura de minería de datos existente.  
  
-   Entrenar y examinar modelos de minería de datos.  
  
-   Comparar modelos mediante gráficos de precisión.  
  
-   Crear consultas de predicción basadas en modelos de minería de datos.  
  
## <a name="mining-structure-tab"></a>Pestaña Estructura de minería de datos  
 Utilice la pestaña **Estructura de minería de datos** para agregar columnas y modificar las propiedades de una estructura de minería de datos existente. Las tareas y los temas siguientes proporcionan más información sobre cómo trabajar con estructuras de minería de datos:  
  
 [Estructuras de minería de datos &#40;Analysis Services - minería de datos&#41;](mining-structures-analysis-services-data-mining.md)  
  
 [Tareas y procedimientos de las estructuras de minería de datos](mining-structure-tasks-and-how-tos.md)  
  
## <a name="mining-models-tab"></a>Pestaña Modelos de minería de datos  
 Utilice la pestaña **Modelos de minería de datos** para administrar modelos de minería de datos existentes y crear otros nuevos. Los modelos de minería de datos siempre se basan en una estructura de minería de datos existente.  
  
 En la pestaña **Modelos de minería de datos** , puede cambiar el tipo de algoritmo, agregar o quitar columnas asociadas con la estructura del modelo, ajustar propiedades de columna específicas del algoritmo, especificar el uso de la columna del modelo de minería de datos y ajustar parámetros de algoritmo asociados con el modelo de minería de datos. También puede procesar la estructura de minería de datos junto con los modelos seleccionados o con todos los modelos asociados.  
  
 Vea los temas siguientes para obtener más información sobre cómo trabajar con los modelos de minería de datos:  
  
 [Los modelos de minería de datos &#40;Analysis Services - minería de datos&#41;](mining-models-analysis-services-data-mining.md)  
  
 [Tareas y procedimientos de los modelos de minería de datos](mining-model-tasks-and-how-tos.md)  
  
## <a name="mining-model-viewer-tab"></a>Pestaña Visor de modelos de minería de datos  
 Utilice la pestaña **Visor de modelos de minería de datos** para explorar visualmente los modelos de minería de datos. Cada modelo de minería de datos está asociado con un visor personalizado que muestra el contenido específico de ese modelo. También puede ver el contenido del modelo de minería de datos utilizando el visor de contenido.  
  
 Vea los temas siguientes para obtener más información sobre cómo explorar los modelos de minería de datos con los visores de minería de datos:  
  
 [Visores de modelos de minería de datos](data-mining-model-viewers.md)  
  
 [Tareas y procedimientos del Visor de modelos de minería de datos](mining-model-viewer-tasks-and-how-tos.md)  
  
## <a name="mining-accuracy-chart-tab"></a>Pestaña Gráfico de precisión de minería de datos  
 Utilice la pestaña **Gráfico de precisión de minería de datos** para probar la precisión de predicción de un único modelo de minería de datos o para comparar la eficacia de varios modelos de minería de datos contenidos en una estructura de minería de datos. La pestaña contiene herramientas para filtrar los datos, seleccionar modelos y mostrar los resultados en un gráfico de elevación, en un gráfico de beneficios o en una matriz de clasificación.  
  
 Vea los siguientes temas para obtener más información acerca de la prueba y la validación de modelos de minería de datos:  
  
 [Pruebas y validación &#40;minería de datos&#41;](testing-and-validation-data-mining.md)  
  
 [Pruebas y validación tareas y procedimientos &#40;minería de datos&#41;](testing-and-validation-tasks-and-how-tos-data-mining.md)  
  
## <a name="mining-model-prediction-tab"></a>Pestaña Predicción de modelo de minería de datos  
 La pestaña **Predicción de modelo de minería de datos** incluye el Generador de consultas de predicción, que se puede usar para crear consultas de predicción DMX (Extensiones de minería de datos). La pestaña contiene herramientas para especificar modelos de minería de datos y tablas de entrada, asignar las columnas del modelo de minería de datos a las columnas de la tabla de entrada, agregar funciones a una consulta y especificar criterios para cada columna.  
  
 Tras diseñar una consulta, puede utilizar diferentes vistas de la pestaña para mostrar los resultados de la consulta y para modificarla manualmente. También puede guardar los resultados de la consulta en una tabla de una base de datos.  
  
 Vea los temas siguientes para obtener más información sobre cómo crear consultas de minería de datos:  
  
 [Consultas de minería de datos](data-mining-queries.md)  
  
 [Tareas y procedimientos de Consulta de minería de datos](data-mining-query-tasks-and-how-tos.md)  
  
## <a name="see-also"></a>Vea también  
 [Soluciones de minería de datos](data-mining-solutions.md)  
  
  
