---
title: No se pudo cargar 'Microsoft.AnalysisServices.SharePoint.Integration' | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
ms.assetid: 6e350b67-5e18-4b90-8fb7-a0109cbb27b7
caps.latest.revision: "7"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: c48acc5178a8e17f47e14205cab10f14bf1a2d1d
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="could-not-load-microsoftanalysisservicessharepointintegration"></a>No se pudo cargar Microsoft.AnalysisServices.SharePoint.Integration
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]En entornos de SharePoint 2010 que tienen [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, este error se producirá si la solución de nivel de aplicación para [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no se implementó correctamente.  
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Se aplica a|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint|  
|Versión del producto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|La solución Powerpivotwebapp no está implementada o no se implementó correctamente.|  
|Texto del mensaje|No se pudo cargar el archivo o ensamblado 'Microsoft.AnalysisServices.SharePoint.Integration'|  
  
## <a name="explanation"></a>Explicación  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint utiliza paquetes de soluciones para implementar sus características en un servidor de SharePoint. Una de las soluciones no se implementó correctamente. Como resultado, este error aparece siempre que se intenta abrir la Galería de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] u otras páginas de aplicaciones de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] en un sitio de SharePoint.  
  
## <a name="user-action"></a>Acción del usuario  
 Implementar el paquete de soluciones.  
  
1.  En Administración central, en Configuración del sistema, haga clic en **Administrar soluciones del conjunto de servidores**.  
  
2.  Haga clic en **Powerpivotwebapp**.  
  
3.  Haga clic en **Implementar solución**.  
  
4.  Elija la aplicación web con la que se está produciendo este error. Si hay más de una, implemente de nuevo la solución para todas.  
  
5.  Haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Implementar las soluciones de Power Pivot en SharePoint](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md)  
  
  
