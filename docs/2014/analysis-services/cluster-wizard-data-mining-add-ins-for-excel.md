---
title: Asistente para clúster (complementos de minería de datos para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- clustering [data mining]
ms.assetid: 85b25625-a7ab-4960-9f9c-df22e8ecae37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d93f676aec67b5d791924cbbda8f71a966d5bbc2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66087808"
---
# <a name="cluster-wizard-data-mining-add-ins-for-excel"></a>Asistente para clúster (Complementos de minería de datos para Excel)
  ![Asistente para clúster, cinta de opciones Minería de datos](media/dmc-cluster.gif "Asistente para clúster, cinta de opciones Minería de datos")  
  
 El Asistente para clúster ayuda a crear un modelo que detecta las filas que comparten características similares y las agrupa para maximizar la distancia entre los grupos. Este asistente resulta útil para buscar patrones en todo tipo de datos.  
  
 El Asistente para clúster utiliza el algoritmo de clústeres de Microsoft y puede personalizarse en gran medida. Funciona en los datos de una tabla de Excel, un intervalo de Excel o una consulta de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. La herramienta [detectar categorías](detect-categories-table-analysis-tools-for-excel.md) proporciona una funcionalidad similar, proporcionada en las herramientas de análisis de tabla para Excel. Sin embargo, la herramienta Detectar categorías no se puede personalizar y debe usar los datos de las tablas de Excel.  
  
## <a name="using-the-cluster-wizard"></a>Usar el Asistente para clúster  
  
1.  En la cinta de opciones minería de datos, haga clic en **clúster**y, a continuación, en **siguiente**.  
  
2.  En la página **seleccionar datos de origen** , seleccione una tabla o un rango de Excel. O bien especifique un origen de datos externo.  
  
     Si utiliza un origen de datos externo, puede crear vistas personalizadas o pegar el texto personalizado de la consulta, y guardar el conjunto de datos como un origen de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
3.  En la página **agrupación en clústeres** , puede personalizar la forma en que se compila el modelo.  
  
    -   En **número de segmentos**, puede indicar al asistente que cree un número fijo de categorías o dejar que detecte automáticamente el número óptimo de agrupaciones.  
  
    -   Revise la lista de columnas de la lista **columnas de entrada** y anule la selección de las columnas que no sean útiles en la creación de patrones. Las columnas que debe excluir son los números de identificación, los nombres de cliente, etcétera.  
  
4.  Opcionalmente, haga clic en **parámetros** para cambiar los parámetros del algoritmo y personalizar el comportamiento del modelo de agrupación en clústeres.  
  
5.  En la página **dividir datos en conjuntos de entrenamiento y de prueba** , especifique la cantidad de datos que se van a conservar para las pruebas. El resto se utiliza siempre para entrenar el modelo.  
  
     La configuración predeterminada es tener un 30 % de datos de prueba y un 70 % de datos de entrenamiento.  
  
6.  En la página **Finalizar** , proporcione un nombre descriptivo para el conjunto de datos y el modelo, y establezca las siguientes opciones que controlan cómo se trabaja con el modelo terminado:  
  
    -   **Examinar modelo**. Cuando se selecciona esta opción, en cuanto el asistente finaliza el procesamiento del modelo, se abre una ventana **examinar** para ayudarle a explorar los resultados. El contenido del visor depende del tipo de modelo que creó. Para obtener más información, vea [examinar un modelo de agrupación en clústeres](browsing-a-clustering-model.md).  
  
    -   **Habilitar la obtención de detalles**. Seleccione esta opción para ver los datos subyacentes desde el modelo terminado. Esta opción solo está disponible si se crea un modelo de árbol de decisión.  
  
    -   **Usar modelo temporal**. Si selecciona esta opción, el modelo no se guardará en el servidor. Se eliminan los modelos temporales al cerrar Excel.  
  
## <a name="more-about-clustering-models"></a>Más información sobre los modelos de agrupación en clústeres  
 Para cambiar el algoritmo de clústeres usado por este asistente, haga clic en **Opciones avanzadas** y use el cuadro de diálogo **parámetros de algoritmo** .  
  
 El algoritmo de clústeres de Microsoft proporciona estos métodos de clúster:  
  
-   Mediana-k escalable o sin escala.  
  
-   Maximización de la expectativa (EM), escalable o sin escala.  
  
 También puede utilizar el parámetro CLUSTER_SEED para controlar el valor inicial y asegurarse de que los modelos repetidos con el mismo conjunto de datos tienen los mismos resultados.  
  
### <a name="requirements"></a>Requisitos  
 Para usar el Asistente para clúster, debe estar conectado a una base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Para obtener más información, vea [conectarse a los datos de origen &#40;cliente de minería de datos para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
## <a name="see-also"></a>Consulte también  
 [Crear un modelo de minería de datos](creating-a-data-mining-model.md)   
 [Detectar categorías &#40;herramientas de análisis de tabla para Excel&#41;](detect-categories-table-analysis-tools-for-excel.md)  
  
  
