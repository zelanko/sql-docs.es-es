---
title: Publicar informes | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], publishing
- publishing reports [Reporting Services]
ms.assetid: ef5a514e-e818-4041-a8b0-15835f9a046b
caps.latest.revision: 37
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: fec14c2f0d051259b45125c50c008f9850d02ad3
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37204985"
---
# <a name="publish-reports"></a>Publicar informes
  Desde[!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], puede publicar todos los informes y orígenes de datos compartidos en un proyecto de servidor de informes en un servidor de informes implementando el proyecto, o puede publicar un informe único. Para poder publicar un informe, debe especificar la dirección URL del servidor de informes de destino. Para más información, vea [Establecer propiedades de implementación &#40;Reporting Services&#41;](tools/set-deployment-properties-reporting-services.md).  
  
 Puede usar el [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] verzi [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] para abrir, modificar, obtener una vista previa, guardar y publicar ambos [!INCLUDE[ssRSversion2005](../includes/ssrsversion2005-md.md)] y [!INCLUDE[ssRSversion10](../includes/ssrsversion10-md.md)] informes. Para obtener más información, vea [Implementación y compatibilidad de versiones en las herramientas de datos de SQL Server &#40;SSRS&#41;](tools/deployment-and-version-support-in-sql-server-data-tools-ssrs.md).  
  
### <a name="to-publish-all-reports-in-a-project"></a>Para publicar todos los informes de un proyecto  
  
-   En el menú **Generar**, haga clic en **Implementar \<nombre del proyecto de informe>**. Como alternativa, en el Explorador de soluciones, haga clic con el botón derecho en el proyecto de informe y, después, haga clic en **Implementar**. El estado del proceso de publicación se puede ver en la ventana Resultados.  
  
    > [!NOTE]  
    >  Al implementar un proyecto del servidor de informes, también se implementan los orígenes de datos compartidos en el proyecto de informe.  
  
### <a name="to-publish-a-single-report"></a>Para publicar solo un informe  
  
-   En el Explorador de soluciones, haga clic con el botón derecho en el informe y, después, haga clic en **Implementar**. El estado del proceso de publicación se puede ver en la ventana Resultados.  
  
    > [!NOTE]  
    >  Al publicar un informe, también debe implementar los orígenes de datos compartidos que el informe utiliza.  
  
## <a name="see-also"></a>Vea también  
 [Publicar orígenes de datos e informes](reports/publishing-data-sources-and-reports.md)   
 [Obtener la vista previa de informes](reports/previewing-reports.md)   
 [Publicación de informes en un servidor de informes](reports/publishing-reports-to-a-report-server.md)   
 [Buscar, ver y administrar informes &#40;Generador de informes y SSRS&#41;](report-builder/finding-viewing-and-managing-reports-report-builder-and-ssrs.md)   
 [Exportar informes &#40;generador de informes y SSRS&#41;](report-builder/export-reports-report-builder-and-ssrs.md)  
  
  
