---
title: Editar o eliminar particiones (Analysis Services-multidimensional) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- modifying partitions
- partitions [Analysis Services], modifying
ms.assetid: fb7a64ca-d021-4926-b92d-83476fbc40a3
author: minewiskan
ms.author: owend
ms.openlocfilehash: cad4c1f70743cafcc428835b3dcd11e2fa26ee79
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/09/2020
ms.locfileid: "84546778"
---
# <a name="edit-or-delete-partitions-analyisis-services---multidimensional"></a>Editar o eliminar particiones (Analysis Services - Multidimensional)
  Las particiones de cubo se modifican mediante la pestaña **Particiones** del Diseñador de cubos en [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)]. La pestaña **Particiones** presenta una lista de las particiones de todos los grupos de medida de un cubo. También muestra una lista de las particiones de reescritura que tienen habilitada esta característica.

 Para editar las particiones de cualquier grupo de medida, expanda el grupo de medida en la pestaña **particiones** . las particiones de un grupo de medida se enumeran por número ordinal en un formato de tabla con las columnas que se muestran en la tabla siguiente.

 Los parámetros de un grupo de medida vinculado deben editarse en el cubo de origen.

 La eliminación de particiones se realiza automáticamente al mezclar una partición de origen en una partición de destino. La partición especificada como origen se elimina una vez completada la mezcla. También puede eliminar particiones manualmente en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o en la pestaña Particiones de [!INCLUDE[ssBIDevStudio](../../../includes/ssbidevstudio-md.md)]. Haga clic con el botón derecho y elija **Eliminar**. Recuerde que al eliminar una partición también se eliminan los datos y las agregaciones. Como medida de precaución, asegúrese de tener una copia de seguridad reciente de la base de datos por si necesita invertir este paso posteriormente.

> [!NOTE]
>  O bien, puede usar scripts XMLA que automaticen las tareas para crear, mezclar y eliminar particiones. El script XMLA se puede crear y ejecutar en [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)]o en paquetes personalizados de SSIS que se ejecutan como una tarea programada. Para más información, consulte [Automate Analysis Services Administrative Tasks with SSIS](../instances/automate-analysis-services-administrative-tasks-with-ssis.md).

## <a name="partition-source"></a>Origen de la partición
 Especifica la tabla o la consulta con nombre origen de la partición. Para cambiar la tabla de origen, haga clic en la celda y, después, haga clic en el botón Examinar (**…**).

 ![Columna Origen del panel Partición](../media/ssas-partitionsource.png "Columna Origen del panel Partición")

 Si la partición se basa en una consulta, haga clic en el botón Examinar (**…**) para editar la consulta. Esto edita la propiedad **Origen** de la partición. Para obtener más información, vea [cambiar el origen de una partición para usar una tabla de hechos diferente](change-a-partition-source-to-use-a-different-fact-table.md).

 Puede especificar una tabla en la vista del origen de datos que tenga la misma estructura que la tabla de origen original (en el origen de datos externo del que se recuperan los datos). El origen puede encontrarse en cualquier origen de datos o vista del origen de datos de la base de datos de cubo.

## <a name="storage-settings"></a>Configuración de almacenamiento
 En el Diseñador de cubos, en la pestaña Particiones, puede hacer clic en **Configuración de almacenamiento** para elegir una de las configuraciones estándar de almacenamiento MOLAP, ROLAP u HOLAP, así como configurar valores personalizados para el modo de almacenamiento y el almacenamiento automático en caché. El valor predeterminado es MOLAP porque es el que ofrece el rendimiento de las consultas más rápido. Para más información sobre cada opción, vea [Establecer el almacenamiento de particiones &#40;Analysis Services - Multidimensional&#41;](set-partition-storage-analysis-services-multidimensional.md).

 El almacenamiento se puede configurar independientemente para cada partición de cada grupo de medida de un cubo. También puede configurar los valores de almacenamiento predeterminado de un cubo o un grupo de medida. El almacenamiento se configura en la pestaña **Particiones** del Asistente para cubos.

## <a name="see-also"></a>Consulte también
 [Crear y administrar una partición Local &#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md) [diseñar agregaciones &#40;Analysis Services-multidimensional&#41;](designing-aggregations-analysis-services-multidimensional.md) las [particiones de mezcla en Analysis Services &#40;SSAS-&#41;multidimensional](merge-partitions-in-analysis-services-ssas-multidimensional.md)


