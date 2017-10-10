---
title: Editar o eliminar particiones (Analysis Services - Multidimensional) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- modifying partitions
- partitions [Analysis Services], modifying
ms.assetid: fb7a64ca-d021-4926-b92d-83476fbc40a3
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 4a253d7cc22d90a06369a914b7aec8b4a8ec315f
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="edit-or-delete-partitions-analyisis-services---multidimensional"></a>Editar o eliminar particiones (Analysis Services - Multidimensional)
  Las particiones de cubo se modifican mediante la pestaña **Particiones** del Diseñador de cubos en [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. La pestaña **Particiones** presenta una lista de las particiones de todos los grupos de medida de un cubo. También muestra una lista de las particiones de reescritura que tienen habilitada esta característica.  
  
 Para editar las particiones de cualquier grupo de medida, expanda el grupo de medida en la pestaña **Particiones** . Las particiones de un grupo de medida aparecen ordenadas en una tabla por número ordinal, con las columnas incluidas en la tabla que aparece a continuación.  
  
 Los parámetros de un grupo de medida vinculado deben editarse en el cubo de origen.  
  
 La eliminación de particiones se realiza automáticamente al mezclar una partición de origen en una partición de destino. La partición especificada como origen se elimina una vez completada la mezcla. También puede eliminar particiones manualmente en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o en la pestaña Particiones de [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]. Haga clic con el botón derecho y elija **Eliminar**. Recuerde que al eliminar una partición también se eliminan los datos y las agregaciones. Como medida de precaución, asegúrese de tener una copia de seguridad reciente de la base de datos por si necesita invertir este paso posteriormente.  
  
> [!NOTE]  
>  O bien, puede usar scripts XMLA que automaticen las tareas para crear, mezclar y eliminar particiones. El script XMLA se puede crear y ejecutar en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]o en paquetes personalizados de SSIS que se ejecutan como una tarea programada. Para más información, consulte [Automatizar tareas administrativas de Analysis Services con SSIS](../../analysis-services/instances/automate-analysis-services-administrative-tasks-with-ssis.md).  
  
## <a name="partition-source"></a>Origen de la partición  
 Especifica la tabla o la consulta con nombre origen de la partición. Para cambiar la tabla de origen, haga clic en la celda y, después, haga clic en el botón Examinar (**…**).  
  
 ![Columna de origen en el panel de la partición](../../analysis-services/multidimensional-models/media/ssas-partitionsource.png "columna de origen en el panel de partición")  
  
 Si la partición se basa en una consulta, haga clic en el botón Examinar (**…**) para editar la consulta. Esto edita la propiedad **Origen** de la partición. Para más información, consulte [Cambiar el origen de una partición para usar una tabla de hechos diferente](../../analysis-services/multidimensional-models/change-a-partition-source-to-use-a-different-fact-table.md).  
  
 Puede especificar una tabla en la vista del origen de datos que tenga la misma estructura que la tabla de origen original (en el origen de datos externo del que se recuperan los datos). El origen puede encontrarse en cualquier origen de datos o vista del origen de datos de la base de datos de cubo.  
  
## <a name="storage-settings"></a>Configuración de almacenamiento  
 En el Diseñador de cubos, en la pestaña Particiones, puede hacer clic en **Configuración de almacenamiento** para elegir una de las configuraciones estándar de almacenamiento MOLAP, ROLAP u HOLAP, así como configurar valores personalizados para el modo de almacenamiento y el almacenamiento automático en caché. El valor predeterminado es MOLAP porque es el que ofrece el rendimiento de las consultas más rápido. Para más información sobre cada opción, vea [Establecer el almacenamiento de particiones &#40;Analysis Services - Multidimensional&#41;](../../analysis-services/multidimensional-models/set-partition-storage-analysis-services-multidimensional.md).  
  
 El almacenamiento se puede configurar independientemente para cada partición de cada grupo de medida de un cubo. También puede configurar los valores de almacenamiento predeterminado de un cubo o un grupo de medida. El almacenamiento se configura en la pestaña **Particiones** del Asistente para cubos.  
  
## <a name="see-also"></a>Vea también  
 [Crear y administrar una partición local &#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/create-and-manage-a-local-partition-analysis-services.md)   
 [Diseñar agregaciones &#40; Analysis Services - Multidimensional &#41;](../../analysis-services/multidimensional-models/designing-aggregations-analysis-services-multidimensional.md)   
 [Mezclar particiones en Analysis Services &#40;SSAS - Multidimensional&#41;](../../analysis-services/multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md)  
  
  
