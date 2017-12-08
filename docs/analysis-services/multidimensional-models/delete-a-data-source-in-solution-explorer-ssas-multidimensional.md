---
title: Eliminar un origen de datos en el Explorador de soluciones (SSAS Multidimensional) | Documentos de Microsoft
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: sql13.asvs.deleteobjects.f1
helpviewer_keywords:
- data sources [Analysis Services], deleting
- deleting data sources
- removing data sources
ms.assetid: b45441ef-f909-4736-98b9-cc80d0acac99
caps.latest.revision: "46"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8e3a98d8d962d3f0bdbe3a818d8496ecdb8a1a94
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="delete-a-data-source-in-solution-explorer-ssas-multidimensional"></a>Eliminar un origen de datos en el Explorador de soluciones (SSAS multidimensional)
  Puede eliminar un objeto de orígenes de datos para quitarlo definitivamente de un proyecto de modelo multidimensional de Analysis Services.  
  
 En [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], los orígenes de datos proporcionan las bases con las que se construyen las vistas del origen de datos que, a su vez, se usan para definir dimensiones, cubos y estructuras de minería de datos en un proyecto o base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Por tanto, la eliminación de un origen de datos puede determinar que otros de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no sean válidos en un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Siembre debe revisar la lista de objetos dependientes que se proporcionan antes de eliminar el objeto.  
  
> [!IMPORTANT]  
>  En el modo en línea, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no puede eliminar de una base de datos de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] los orígenes de datos de los que dependen otros objetos. Debe eliminar todos los objetos de la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que dependen de dicho origen de datos antes de eliminar este. Para obtener más información acerca del modo en línea, vea [Connect in Online Mode to an Analysis Services Database](../../analysis-services/multidimensional-models/connect-in-online-mode-to-an-analysis-services-database.md).  
  
### <a name="to-delete-a-data-source"></a>Para eliminar un origen de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto o conéctese a la base de datos de la que desea eliminar un origen de datos.  
  
2.  En el **Explorador de soluciones**, expanda la carpeta **Orígenes de datos** .  
  
3.  Haga clic con el botón derecho en el origen de datos y, después, haga clic en **Eliminar**. El cuadro de diálogo **Eliminar objetos**  aparece y muestra los objetos que se invalidarán si elimina el origen de datos. Revise esta lista cuidadosamente antes de hacer clic en **Aceptar** para eliminar el origen de datos.  
  
4.  Guarde el proyecto.  
  
     Tras eliminar un origen de datos de un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , debe guardar el proyecto modificado ya que, de lo contrario, recibirá un mensaje de error la próxima vez que abra el proyecto, dado que el archivo XML subyacente del origen de datos eliminado no se encontrará cuando el proyecto trate de cargar el origen de datos eliminado.  
  
## <a name="see-also"></a>Vea también  
 [Orígenes de datos en modelos multidimensionales](../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)   
 [Orígenes de datos admitidos &#40;SSAS - Multidimensionales&#41;](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
  
