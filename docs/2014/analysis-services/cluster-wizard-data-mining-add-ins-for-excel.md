---
title: Asistente (complementos de minería de datos para Excel de datos) del clúster | Microsoft Docs
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
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "66087808"
---
# <a name="cluster-wizard-data-mining-add-ins-for-excel"></a>Asistente para clúster (Complementos de minería de datos para Excel)
  ![Asistente para clúster de la cinta de opciones minería de datos](media/dmc-cluster.gif "Asistente para clúster de la cinta de opciones minería de datos")  
  
 El Asistente para clúster ayuda a crear un modelo que detecta las filas que comparten características similares y las agrupa para maximizar la distancia entre los grupos. Este asistente resulta útil para buscar patrones en todo tipo de datos.  
  
 El Asistente para clúster utiliza el algoritmo de clústeres de Microsoft y puede personalizarse en gran medida. Funciona en los datos de una tabla de Excel, un intervalo de Excel o una consulta de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Proporciona una funcionalidad similar el [detectar categorías](detect-categories-table-analysis-tools-for-excel.md) herramienta, incluida en las herramientas de análisis de tabla para Excel. Sin embargo, la herramienta Detectar categorías no se puede personalizar y debe usar los datos de las tablas de Excel.  
  
## <a name="using-the-cluster-wizard"></a>Usar el Asistente para clúster  
  
1.  En la cinta de opciones minería de datos, haga clic en **clúster**y, a continuación, haga clic en **siguiente**.  
  
2.  En el **seleccionar datos de origen** , seleccione una tabla de Excel o un intervalo. O bien especifique un origen de datos externo.  
  
     Si utiliza un origen de datos externo, puede crear vistas personalizadas o pegar el texto personalizado de la consulta, y guardar el conjunto de datos como un origen de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
3.  En el **clústeres** página, puede personalizar la manera en que se basa el modelo.  
  
    -   Para **número de segmentos**, puede indicar al Asistente para crear un número fijo de categorías o dejarle que detecte automáticamente el número óptimo de agrupaciones.  
  
    -   Revise la lista de columnas en el **columnas de entrada** enumerar y anule la selección de las columnas que no son útiles en la creación de patrones. Las columnas que debe excluir son los números de identificación, los nombres de cliente, etcétera.  
  
4.  Si lo desea, haga clic en **parámetros** para cambiar los parámetros del algoritmo y personalizar el comportamiento del modelo de agrupación en clústeres.  
  
5.  En el **dividir los datos en conjuntos de prueba y entrenamiento** , especifique la cantidad de datos son suficientes para las pruebas. El resto se utiliza siempre para entrenar el modelo.  
  
     La configuración predeterminada es tener un 30 % de datos de prueba y un 70 % de datos de entrenamiento.  
  
6.  En el **finalizar** página, proporcione un nombre descriptivo para el conjunto de datos y el modelo y establecer las siguientes opciones que controlan cómo trabajar con el modelo terminado:  
  
    -   **Examinar modelo**. Cuando se selecciona esta opción, tan pronto como el asistente finaliza el procesamiento del modelo, se abre un **examinar** ventana que le ayudarán a explorar los resultados. El contenido del visor depende del tipo de modelo que creó. Para obtener más información, consulte [examinar un modelo de agrupación en clústeres](browsing-a-clustering-model.md).  
  
    -   **Habilitar obtención de detalles**. Seleccione esta opción para ver los datos subyacentes desde el modelo terminado. Esta opción solo está disponible si se crea un modelo de árbol de decisión.  
  
    -   **Usar modelo temporal**. Si selecciona esta opción, el modelo no se guardará en el servidor. Se eliminan los modelos temporales al cerrar Excel.  
  
## <a name="more-about-clustering-models"></a>Más información acerca de los modelos de clústeres  
 Puede cambiar el algoritmo de agrupación en clústeres utilizado por este asistente, haga clic en **avanzadas** y el uso de la **parámetros de algoritmo** cuadro de diálogo.  
  
 El algoritmo de clústeres de Microsoft proporciona estos métodos de clúster:  
  
-   Mediana-k escalable o sin escala.  
  
-   Maximización de la expectativa (EM), escalable o sin escala.  
  
 También puede utilizar el parámetro CLUSTER_SEED para controlar el valor inicial y asegurarse de que los modelos repetidos con el mismo conjunto de datos tienen los mismos resultados.  
  
### <a name="requirements"></a>Requisitos  
 Para usar el Asistente para clúster, debe estar conectado a una base de datos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Para obtener más información, consulte [conectarse a los datos de origen &#40;cliente de minería de datos para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
## <a name="see-also"></a>Vea también  
 [Creación de un modelo de minería de datos](creating-a-data-mining-model.md)   
 [Detectar categorías &#40;herramientas de análisis de tabla para Excel&#41;](detect-categories-table-analysis-tools-for-excel.md)  
  
  
