---
title: General (cuadro de diálogo de opciones de almacenamiento) (Analysis Services - datos multidimensionales) | Documentos de Microsoft
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
- sql12.asvs.cubeeditor.partitiondesigner.partitionstoragesettings.setstorageoptions.storage.f1
ms.assetid: ee1fac79-ae15-4c3c-9a98-33db04388817
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: d71e6c2ec49565c2db822d8bb96f26257ebf4f96
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36110844"
---
# <a name="general-storage-options-dialog-box-analysis-services---multidimensional-data"></a>General (cuadro de diálogo Opciones de almacenamiento) (Analysis Services - Datos multidimensionales)
  Utilice la pestaña **General** del cuadro de diálogo **Opciones de almacenamiento** de [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para definir los parámetros de configuración del modo de almacenamiento y del almacenamiento de caché automático para una dimensión, un cubo, un grupo de medida o una partición.  
  
> [!NOTE]  
>  Antes de modificar estos parámetros de configuración, debe estar familiarizado con la funcionalidad del modo de almacenamiento y del almacenamiento en caché automático. Para más información, vea [Almacenamiento en caché automático &#40;Particiones&#41;](multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
## <a name="options"></a>Opciones  
  
|Término|Definición|  
|----------|----------------|  
|**Modo de almacenamiento**|Seleccione el modo de almacenamiento que debe utilizarse para el objeto.<br /><br /> **MOLAP**<br /> El objeto utiliza almacenamiento OLAP multidimensional (MOLAP).<br /><br /> **HOLAP**<br /> El objeto utiliza almacenamiento OLAP híbrido (HOLAP).<br /><br /> **ROLAP**<br /> El objeto utiliza almacenamiento OLAP relacional (ROLAP).|  
|**Habilitar almacenamiento en caché automático**|Habilitar el almacenamiento en caché automático.<br /><br /> Nota: Si no se selecciona esta opción, todas las opciones, excepto **Modo de almacenamiento** , quedarán deshabilitadas.|  
|**Actualizar la caché cuando cambian los datos**|Utiliza el método de notificación seleccionado en la pestaña **Notificaciones** para actualizar la imagen MOLAP para el objeto siempre que se recibe una notificación. Para más información sobre la pestaña **Notificaciones**, vea [Notificaciones &#40;cuadro de diálogo Opciones de almacenamiento&#41; &#40;Analysis Services - Datos multidimensionales&#41;](notifications-storage-options-dialog-analysis-services-multidimensional-data.md).<br /><br /> Nota: Esta opción está deshabilitada, a menos que se seleccione **Habilitar almacenamiento en caché automático** .|  
|**Intervalo de latencia**|Establece el intervalo mínimo y las unidades de tiempo en que el objeto no tiene ninguna actividad antes de que el almacenamiento en caché automático empiece a crear la nueva imagen MOLAP para el objeto.<br /><br /> Nota: Esta opción está deshabilitada, a menos que se seleccione **Actualizar la caché cuando los datos cambien** .|  
|**Reemplazo de intervalo de latencia**|Establece el intervalo máximo y las unidades de tiempo en que, tras recibir una notificación para el objeto, el almacenamiento en caché automático empieza a crear una nueva imagen MOLAP para el objeto, independientemente de la actividad actual del proyecto. Las notificaciones que se reciben tras alcanzar este intervalo no cancelan el proceso de creación de la imagen MOLAP desencadenado por este intervalo.<br /><br /> Nota: Esta opción está deshabilitada, a menos que se seleccione **Actualizar la caché cuando los datos cambien** . También tenga en cuenta que no se debe establecer esta opción si **modo de almacenamiento** está establecido en **HOLAP**.|  
|**Quitar caché no actualizada**|Especifica el período que transcurre entre el inicio del proceso de creación de una nueva caché MOLAP y la eliminación de la caché MOLAP existente.<br /><br /> Nota: Esta opción está deshabilitada, a menos que se seleccione **Habilitar almacenamiento en caché automático** . También tenga en cuenta que no se debe establecer esta opción si **modo de almacenamiento** está establecida en HOLAP.|  
|**Latencia**|Selecciona el intervalo y las unidades de tiempo para el período que transcurre entre el inicio del proceso de creación de una nueva caché MOLAP y la eliminación de la caché MOLAP existente.<br /><br /> Nota: Esta opción está deshabilitada, a menos que se seleccione **Quitar caché no actualizada** . También tenga en cuenta que no se debe establecer esta opción si **modo de almacenamiento** está establecido en **HOLAP**.|  
|**Actualizar la caché periódicamente**|Actualiza la imagen MOLAP de forma periódica, independientemente de las notificaciones.<br /><br /> Nota: Esta opción está deshabilitada, a menos que se seleccione **Habilitar almacenamiento en caché automático** . También tenga en cuenta que no se debe establecer esta opción si **modo de almacenamiento** está establecido en **HOLAP**.|  
|**Volver a generar intervalo**|Selecciona el intervalo y las unidades de tiempo para el período en que, tras crear una nueva imagen MOLAP, [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] inicia de nuevo el proceso de imagen MOLAP para el objeto, independientemente de las notificaciones. Las notificaciones que se reciben tras alcanzar este intervalo no cancelan el proceso de creación de la imagen MOLAP desencadenado por este intervalo.<br /><br /> Nota: Esta opción está deshabilitada, a menos que se seleccione **Actualizar la caché periódicamente** . También tenga en cuenta que no se debe establecer esta opción si **modo de almacenamiento** está establecido en **HOLAP**.|  
|**Poner en línea inmediatamente**|Coloca los objetos en línea de forma inmediata. Si se establece esta opción, los objetos utilizan el almacenamiento ROLAP subyacente para resolver las entradas mientras se genera de nuevo la caché MOLAP. Si no se establece esta opción, los objetos solo pasan a estar en línea de nuevo una vez que se ha completado la caché MOLAP para el objeto.|  
|**Habilitar agregaciones ROLAP**|Utiliza vistas materializadas del origen de datos subyacente para almacenar agregaciones.<br /><br /> Nota: Si el origen de datos subyacente no admite vistas materializadas, se producirá un error cuando se procese el objeto.|  
|**Aplicar configuración a dimensiones**|Aplica los parámetros de configuración del modo de almacenamiento y del almacenamiento en caché automático a las dimensiones asociadas.|  
  
## <a name="see-also"></a>Vea también  
 [Cuadro de diálogo de opciones de almacenamiento &#40;Analysis Services - datos multidimensionales&#41;](storage-options-dialog-box-analysis-services-multidimensional-data.md)   
 [Las notificaciones &#40;cuadro de diálogo de opciones de almacenamiento&#41; &#40;Analysis Services - datos multidimensionales&#41;](notifications-storage-options-dialog-analysis-services-multidimensional-data.md)  
  
  