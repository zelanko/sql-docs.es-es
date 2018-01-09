---
title: "Usar la obtención de detalles desde los visores del modelo | Documentos de Microsoft"
ms.custom: 
ms.date: 03/01/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: data-mining
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e5e065ad-c688-4c2c-8c82-7f3038e04915
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 31ac0cffe6656c5d644b5424b56f150572dc9af6
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 01/08/2018
---
# <a name="use-drillthrough-from-the-model-viewers"></a>Usar la obtención de detalles desde los visores de modelos
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]Según el tipo de modelo, puede usar los visores de exploración de obtención de detalles en el **Visor de modelos de minería de datos** pestaña del Diseñador de minería de datos para explorar los casos usados en el modelo de minería de datos o para ver columnas adicionales en la estructura de minería de datos. Aunque muchos tipos de modelos no admiten la obtención de detalles debido a que los patrones del modelo no se pueden vincular directamente con casos concretos, los tipos de modelos siguientes sí lo hacen.  
  
 Tenga en cuenta que se debe haber habilitado la obtención de detalles en el modelo, y que debe disponer de los permisos apropiados. Es posible que la opción para obtener detalles también esté deshabilitada si el modelo se encuentra en un estado no procesado, independientemente de si el modelo se procesó previamente y tiene contenido. Para recuperar los datos de los casos del modelo mediante la obtención de detalles, la memoria caché de la estructura y del modelo debe estar actualizada.  
  
### <a name="use-drillthrough-in-the-microsoft-tree-viewer"></a>Utilizar la obtención de detalles en el Visor de árboles de Microsoft  
  
1.  En el Diseñador de minería de datos, seleccione un modelo de árboles de decisión y, a continuación, seleccione **Examinar modelo** para abrir el modelo en el **Visor de árboles de Microsoft**. En SQL Server Management Studio, haga clic con el botón derecho en el modelo y seleccione **Examinar**.  
  
2.  Haga clic con el botón derecho en cualquier nodo del gráfico de árbol y seleccione **Explorar en profundidad**.  
  
3.  Seleccione una de las opciones siguientes: **Solo columnas de modelos** o **Columnas de modelo y estructura**. Si no dispone de los permisos apropiados, es posible que alguna opción no esté disponible.  
  
4.  Se abre el cuadro de diálogo **Explorar en profundidad** , que muestra los datos de los casos o de la estructura. La barra de título del cuadro de diálogo también contiene una descripción que identifica el nodo desde el que se ejecutó la consulta de obtención de detalles.  
  
5.  Haga clic con el botón derecho en cualquier lugar de los resultados y seleccione **Copiar todo** para guardar los resultados en el Portapapeles.  
  
### <a name="use-drillthrough-in-the-microsoft-cluster-viewer"></a>Utilizar la obtención de detalles en el Visor de clústeres de Microsoft  
  
1.  En el Diseñador de minería de datos, seleccione un modelo de agrupación en clústeres y, a continuación, seleccione **Examinar modelo** para abrir el modelo en el **Visor de clústeres de Microsoft**. En SQL Server Management Studio, haga clic con el botón derecho en el modelo y seleccione **Examinar**.  
  
2.  En la pestaña **Clúster** , haga clic con el botón derecho en cualquier nodo.  
  
3.  Seleccione **Obtener detalles**y, a continuación, seleccione una de las opciones siguientes: **Solo columnas de modelos** o **Columnas de modelo y estructura**. Si no dispone de los permisos apropiados, es posible que alguna opción no esté disponible.  
  
4.  Se abre el cuadro de diálogo **Explorar en profundidad** , que muestra los datos de los casos o de la estructura. La barra de título del cuadro de diálogo también contiene una descripción que identifica el clúster para los casos.  
  
5.  Haga clic con el botón derecho en cualquier lugar de los resultados y seleccione **Copiar todo** para guardar los resultados en el Portapapeles.  
  
### <a name="use-drillthrough-in-the-microsoft-association-rules-viewer"></a>Utilizar la obtención de detalles en el Visor de reglas de asociación de Microsoft  
  
1.  En el Diseñador de minería de datos, seleccione un modelo de asociación y, a continuación, seleccione **Examinar modelo** para abrir el modelo en el **Visor de reglas de asociación de Microsoft**. En SQL Server Management Studio, haga clic con el botón derecho en el modelo y seleccione **Examinar**.  
  
2.  En la pestaña **Reglas** , haga clic con el botón derecho en cualquier fila que represente una regla. En la pestaña **Conjuntos de elementos** , haga clic en cualquier fila que contenga un conjunto de elementos.  
  
3.  Seleccione **Obtener detalles**y, a continuación, seleccione una de las opciones siguientes: **Solo columnas de modelos** o **Columnas de modelo y estructura**. Si no dispone de los permisos apropiados, es posible que alguna opción no esté disponible.  
  
4.  Se abre el cuadro de diálogo **Explorar en profundidad** , que muestra los datos de los casos o de la estructura. La barra de título del cuadro de diálogo también contiene una descripción que identifica el nombre de la regla.  
  
5.  Haga clic con el botón derecho en cualquier lugar de los resultados y seleccione **Copiar todo** para guardar los resultados completos del caso en el Portapapeles. También puede seleccionar **Copiar** para copiar solo el caso seleccionado. Si el modelo contiene una columna de tabla anidada, solo se pegará el nombre de dicha columna; si desea recuperar los valores de datos almacenados dentro de esta columna para cada caso, deberá crear una consulta en el contenido del modelo.  
  
### <a name="use-drillthrough-in-the-microsoft-sequence-cluster-viewer"></a>Utilizar la obtención de detalles en el Visor de clústeres de secuencia de Microsoft  
  
1.  En el Diseñador de minería de datos, seleccione un modelo de agrupación en clústeres y, a continuación, seleccione **Examinar modelo** para abrir el modelo en el **Visor de clústeres de Microsoft**. En SQL Server Management Studio, haga clic con el botón derecho en el modelo y seleccione **Examinar**.  
  
2.  En la **pestaña Diagrama del clúster**, haga clic con el botón derecho en un nodo que represente a un clúster. En la pestaña **Perfiles del clúster** , haga clic en cualquier lugar de un perfil de clúster o en el clúster que represente a la población total del modelo.  
  
3.  Seleccione **Obtener detalles**y, a continuación, seleccione una de las opciones siguientes: **Solo columnas de modelos** o **Columnas de modelo y estructura**. Si no dispone de los permisos apropiados, es posible que alguna opción no esté disponible.  
  
4.  Se abre el cuadro de diálogo **Explorar en profundidad** , que muestra los datos de los casos o de la estructura. La barra de título del cuadro de diálogo también contiene una descripción que identifica el clúster para los casos.  
  
5.  Haga clic con el botón derecho en cualquier lugar de los resultados y seleccione **Copiar todo** para guardar los resultados en el Portapapeles. Si el modelo contiene una columna de tabla anidada, solo se pegará el nombre de dicha columna; si desea recuperar los valores de datos almacenados dentro de esta columna para cada caso, deberá crear una consulta en el contenido del modelo.  
  
## <a name="see-also"></a>Vea también  
 [Tareas y procedimientos del Visor de modelos de minería de datos](../../analysis-services/data-mining/mining-model-viewer-tasks-and-how-tos.md)   
 [Obtención de detalles en modelos de minería de datos](../../analysis-services/data-mining/drillthrough-on-mining-models.md)   
 [Obtención de detalles en estructuras de minería de datos](../../analysis-services/data-mining/drillthrough-on-mining-structures.md)  
  
  
