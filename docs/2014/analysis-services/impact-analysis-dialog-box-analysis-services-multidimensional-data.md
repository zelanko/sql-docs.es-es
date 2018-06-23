---
title: Impacto en el cuadro de diálogo de análisis (Analysis Services - datos multidimensionales) | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.asvs.process.impactanalysisdialog.f1
ms.assetid: 208268eb-4e14-44db-9c64-6f74b776adb6
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: da3a687a637dee6b3b9df59eecebf957f06e64be
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36102944"
---
# <a name="impact-analysis-dialog-box-analysis-services---multidimensional-data"></a>Cuadro de diálogo Análisis de impacto (Analysis Services - Datos multidimensionales)
  Use el cuadro de diálogo **Análisis de impacto** en [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] y [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] para identificar y, opcionalmente, procesar objetos dependientes que se ven afectados si se procesan los objetos enumerados en el cuadro de diálogo **Proceso** . Para mostrar el cuadro de diálogo **Análisis de impacto** , haga clic en **Análisis de impacto** en el cuadro de diálogo **Proceso** .  
  
> [!NOTE]  
>  Un objeto aparecerá más de una vez si se ve afectado de más de una forma.  
  
## <a name="options"></a>Opciones  
 **Lista de objetos**  
 Muestra una lista de objetos dependientes en una cuadrícula. La cuadrícula contiene las columnas siguientes:  
  
 **Nombre de objeto**  
 Muestra el nombre del objeto dependiente que puede ser necesario procesar. El icono que se muestra a la izquierda del nombre indica el tipo de objeto.  
  
 **Tipo**  
 Muestra el tipo del objeto dependiente que puede ser necesario procesar.  
  
 **Tipo de impacto**  
 Muestra el efecto que tiene sobre el objeto dependiente el procesamiento de los objetos del cuadro de diálogo **Proceso** . En la tabla siguiente se enumeran los posibles efectos del procesamiento y se indica si se origina una advertencia o un error.  
  
|Impacto|de mensaje|  
|------------|-------------|  
|El objeto se desactivará (no se procesa)|Advertencia|  
|El objeto podría no ser válido|Error|  
|La agregación podría eliminarse|Advertencia|  
|La agregación flexible podría eliminarse|Advertencia|  
|Los índices se eliminarán|Advertencia|  
|Los objetos que no son secundarios se procesarán|Advertencia|  
  
 **Objeto de proceso**  
 Seleccione los objetos dependientes que desea procesar en la operación de procesamiento. Los objetos dependientes que no se seleccionen deberán procesarse después de finalizar la operación de procesamiento. En caso contrario, no se podrán utilizar.  
  
## <a name="see-also"></a>Vea también  
 [Diseñadores y cuadros de diálogo de Analysis Services &#40;datos multidimensionales&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Cuadro de diálogo procesar &#40;Analysis Services - datos multidimensionales&#41;](process-dialog-box-analysis-services-multidimensional-data.md)  
  
  