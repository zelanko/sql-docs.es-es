---
title: No se pudo cargar el archivo o ensamblado &#39;Microsoft.AnalysisServices.SharePoint.Integration&#39; | Documentos de Microsoft
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6e350b67-5e18-4b90-8fb7-a0109cbb27b7
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 59a210726cb772d3f6feadb5e9440f2d09ac4dcf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36112775"
---
# <a name="could-not-load-file-or-assembly-39microsoftanalysisservicessharepointintegration39"></a>No se pudo cargar el archivo o ensamblado &#39;Microsoft.AnalysisServices.SharePoint.Integration&#39;
  En entornos de SharePoint 2010 que tienen PowerPivot para SharePoint, este error se producirá si la solución del nivel de aplicación para PowerPivot no se implementó correctamente.  
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Se aplica a|PowerPivot para SharePoint|  
|Versión del producto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|La solución Powerpivotwebapp no está implementada o no se implementó correctamente.|  
|Texto del mensaje|No se pudo cargar el archivo o ensamblado 'Microsoft.AnalysisServices.SharePoint.Integration'|  
  
## <a name="explanation"></a>Explicación  
 PowerPivot para SharePoint utiliza paquetes de soluciones para implementar sus características en un servidor de SharePoint. Una de las soluciones no se implementó correctamente. Como resultado, este error aparece siempre que se intenta abrir la Galería de PowerPivot u otras páginas de aplicaciones de PowerPivot en un sitio de SharePoint.  
  
## <a name="user-action"></a>Acción del usuario  
 Implementar el paquete de soluciones.  
  
1.  En Administración central, en Configuración del sistema, haga clic en **Administrar soluciones del conjunto de servidores**.  
  
2.  Haga clic en **Powerpivotwebapp**.  
  
3.  Haga clic en **Implementar solución**.  
  
4.  Elija la aplicación web con la que se está produciendo este error. Si hay más de una, implemente de nuevo la solución para todas.  
  
5.  Haga clic en **Aceptar**.  
  
## <a name="see-also"></a>Vea también  
 [Implementar soluciones de PowerPivot para SharePoint](deploy-power-pivot-solutions-to-sharepoint.md)  
  
  