---
title: Eliminar un origen de datos en el Explorador de soluciones (SSAS Multidimensional) | Documentos de Microsoft
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
- sql12.asvs.deleteobjects.f1
helpviewer_keywords:
- data sources [Analysis Services], deleting
- deleting data sources
- removing data sources
ms.assetid: b45441ef-f909-4736-98b9-cc80d0acac99
caps.latest.revision: 45
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 6dbf7b309db50ec291ccc956c2dc75522786616e
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36103160"
---
# <a name="delete-a-data-source-in-solution-explorer-ssas-multidimensional"></a>Eliminar un origen de datos en el Explorador de soluciones (SSAS multidimensional)
  Puede eliminar un objeto de orígenes de datos para quitarlo definitivamente de un proyecto de modelo multidimensional de Analysis Services.  
  
 En [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], los orígenes de datos proporcionan las bases con las que se construyen las vistas del origen de datos que, a su vez, se usan para definir dimensiones, cubos y estructuras de minería de datos en un proyecto o base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Por tanto, la eliminación de un origen de datos puede determinar que otros de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no sean válidos en un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Siembre debe revisar la lista de objetos dependientes que se proporcionan antes de eliminar el objeto.  
  
> [!IMPORTANT]  
>  En el modo en línea, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no puede eliminar de una base de datos de [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] los orígenes de datos de los que dependen otros objetos. Debe eliminar todos los objetos de la base de datos de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] que dependen de dicho origen de datos antes de eliminar este. Para obtener más información acerca del modo en línea, vea [Connect in Online Mode to an Analysis Services Database](connect-in-online-mode-to-an-analysis-services-database.md).  
  
### <a name="to-delete-a-data-source"></a>Para eliminar un origen de datos  
  
1.  En [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra el proyecto o conéctese a la base de datos de la que desea eliminar un origen de datos.  
  
2.  En el **Explorador de soluciones**, expanda la carpeta **Orígenes de datos** .  
  
3.  Haga clic con el botón derecho en el origen de datos y, después, haga clic en **Eliminar**. El cuadro de diálogo **Eliminar objetos**  aparece y muestra los objetos que se invalidarán si elimina el origen de datos. Revise esta lista cuidadosamente antes de hacer clic en **Aceptar** para eliminar el origen de datos.  
  
4.  Guarde el proyecto.  
  
     Tras eliminar un origen de datos de un proyecto de [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] , debe guardar el proyecto modificado ya que, de lo contrario, recibirá un mensaje de error la próxima vez que abra el proyecto, dado que el archivo XML subyacente del origen de datos eliminado no se encontrará cuando el proyecto trate de cargar el origen de datos eliminado.  
  
## <a name="see-also"></a>Vea también  
 [Orígenes de datos en modelos multidimensionales](data-sources-in-multidimensional-models.md)   
 [Orígenes de datos admitidos &#40;SSAS Multidimensional&#41;](supported-data-sources-ssas-multidimensional.md)  
  
  