---
title: Cuadro de diálogo Análisis de impacto (Analysis Services-datos multidimensionales) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- sql12.asvs.process.impactanalysisdialog.f1
ms.assetid: 208268eb-4e14-44db-9c64-6f74b776adb6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0c08690cd2f5b77471392cab3aad1587b4cb0f9a
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "66080749"
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
  
 **Type**  
 Muestra el tipo del objeto dependiente que puede ser necesario procesar.  
  
 **Tipo de impacto**  
 Muestra el efecto que tiene sobre el objeto dependiente el procesamiento de los objetos del cuadro de diálogo **Proceso** . En la tabla siguiente se enumeran los posibles efectos del procesamiento y se indica si se origina una advertencia o un error.  
  
|Impacto|Message|  
|------------|-------------|  
|El objeto se desactivará (no se procesa)|Advertencia|  
|El objeto podría no ser válido|Error|  
|La agregación podría eliminarse|Advertencia|  
|La agregación flexible podría eliminarse|Advertencia|  
|Los índices se eliminarán|Advertencia|  
|Los objetos que no son secundarios se procesarán|Advertencia|  
  
 **Objeto de proceso**  
 Seleccione los objetos dependientes que desea procesar en la operación de procesamiento. Los objetos dependientes que no se seleccionen deberán procesarse después de finalizar la operación de procesamiento. En caso contrario, no se podrán utilizar.  
  
## <a name="see-also"></a>Consulte también  
 [Analysis Services diseñadores y cuadros de diálogo &#40;datos multidimensionales&#41;](analysis-services-designers-and-dialog-boxes-multidimensional-data.md)   
 [Cuadro de diálogo procesar &#40;Analysis Services-datos multidimensionales&#41;](process-dialog-box-analysis-services-multidimensional-data.md)  
  
  
