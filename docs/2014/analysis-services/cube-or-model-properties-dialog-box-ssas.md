---
title: Cubo o modelo de cuadro de diálogo de propiedades (SSAS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.sqlserverstudio.cubeproperties.f1
ms.assetid: 97e367f9-f95a-4163-add1-c74fd22db249
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 404dd6cd6c47f89b3a8e12acd6048aecae0c7098
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62679575"
---
# <a name="cube-or-model-properties-dialog-box-ssas"></a>Propiedades del cubo o Propiedades del modelo (cuadro de diálogo) (SSAS)
  Utilice el cuadro de diálogo **Propiedades de la base de datos** de [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para establecer las propiedades de un cubo o una base de datos de modelos. Para mostrar este cuadro de diálogo, haga clic con el botón derecho en un cubo o en un modelo del **Explorador de objetos** y seleccione **Propiedades**.  
  
 Este cuadro de diálogo tiene también pestañas para las propiedades siguientes:  
  
-   [Editor de formulario de acción de informe &#40;pestaña acciones, Diseñador de cubos&#41; &#40;Analysis Services - datos multidimensionales&#41;](report-action-form-editor-cube-designer-analysis-services-multidimensional-data.md)  
  
-   [Configuración de errores de procesamiento de dimensiones, particiones y cubos &#40;SSAS - multidimensionales&#41;](multidimensional-models/error-configuration-for-cube-partition-and-dimension-processing.md)  
  
-   [Almacenamiento en caché automático &#40;cuadro de diálogo Propiedades de la partición&#41; &#40;SSMS&#41;](proactive-caching-partition-properties-dialog-box-ssms.md)  
  
## <a name="options"></a>Opciones  
  
|Término|Definición|  
|----------|----------------|  
|**Name**|Muestra el nombre del cubo o del modelo.|  
|**ID**|Muestra el identificador del cubo o del modelo.|  
|**Descripción**|Muestra la descripción del cubo o del modelo.|  
|**Marca de tiempo de creación**|Muestra la fecha y la hora de creación del cubo o del modelo.|  
|**Última actualización de esquema**|Muestra la fecha y la hora en la que se actualizaron por última vez los metadatos del cubo o del modelo.|  
|**Modo de procesamiento de caché de script**|Selecciona el modo de procesamiento que se va a utilizar para la memoria caché de scripts del cubo o del modelo. Para obtener más información acerca de los valores de esta propiedad, vea <xref:Microsoft.AnalysisServices.Cube.ScriptCacheProcessingMode%2A>.|  
|**Modo de procesamiento**|Selecciona el modo de procesamiento que se va a utilizar para el cubo o el modelo. Para obtener más información acerca de los valores de esta propiedad, vea <xref:Microsoft.AnalysisServices.Cube.ProcessingMode%2A>.|  
|**Ubicación de almacenamiento**|Escriba la carpeta que se va a usar como la ubicación de almacenamiento predeterminada para los grupos de medida y las particiones asociadas con el cubo o el modelo, o haga clic en el botón de puntos suspensivos (**...**) para mostrar el cuadro de diálogo **Buscar carpeta remota** y seleccionar una carpeta. Para obtener más información sobre el cuadro de diálogo **Buscar carpeta remota**, vea [Cuadro de diálogo Buscar carpeta remota &#40;Analysis Services - Datos multidimensionales&#41;](browse-for-remote-folder-dialog-box-analysis-services-multidimensional-data.md).<br /><br /> Para obtener más información acerca de los valores de esta propiedad, vea <xref:Microsoft.AnalysisServices.Cube.StorageLocation%2A>.|  
|**Estado**|Muestra el estado de procesamiento del cubo o del modelo. Para obtener más información acerca de los valores de esta propiedad, vea <xref:Microsoft.AnalysisServices.ProcessableMajorObject.State%2A>.|  
|**LastProcessed**|Muestra la fecha y la hora en la que se procesó por última vez el cubo o el modelo.|  
  
## <a name="see-also"></a>Vea también  
 [Diseñadores y cuadros de diálogo de Analysis Services &#40;datos multidimensionales&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Objetos de cubo &#40;Analysis Services - datos multidimensionales&#41;](multidimensional-models-olap-logical-cube-objects/cube-objects-analysis-services-multidimensional-data.md)  
  
  
