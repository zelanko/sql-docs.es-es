---
title: No se pudo cargar el archivo o ensamblado servicios de datos de Microsoft | Documentos de Microsoft
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9472fffb790d8d18ced8d2a528011927717aabc6
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/10/2018
ms.locfileid: "34026602"
---
# <a name="could-not-load-file-or-assembly-microsoft-data-services"></a>No se pudo cargar el archivo o ensamblado servicios de datos de Microsoft
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  En entornos de SharePoint 2010 que tienen PowerPivot para [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, este error se producirá si intenta realizar la exportación de una fuente de distribución de datos y el sistema no tiene la versión necesaria de Microsoft ADO.NET Data Services.  
  
## <a name="details"></a>Detalles  
  
|||  
|-|-|  
|Se aplica a|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint|  
|Versión del producto|[!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|  
|Causa|No se encontró ADO.NET Data Services 3.5 SP1.|  
|Texto del mensaje|No se puede cargar el archivo o ensamblado 'Microsoft.Data.Services, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089' ni una de sus dependencias. El sistema no encuentra el archivo especificado.|  
  
## <a name="explanation"></a>Explicación  
 SharePoint 2010 incluye un botón Exportar como fuente de distribución de datos que puede utilizar para exportar una lista de SharePoint como una fuente de distribución de datos XML. Además, tanto Reporting Services en el modo de SharePoint como [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint admiten las características de fuentes de distribución de datos que requieren ADO.NET Data Services.  
  
 Si no está instalado ADO.NET Data Services, este error se producirá al solicitar una fuente de distribución de datos.  
  
## <a name="user-action"></a>Acción del usuario  
  
1.  Vaya a la documentación de los requisitos de hardware y software para SharePoint 2010, [determinar requisitos de Hardware y Software (SharePoint 2010)](http://go.microsoft.com/fwlink/?LinkId=169734) (http://go.microsoft.com/fwlink/?LinkId=169734).  
  
2.  En **Instalar requisitos previos de software**, busque el vínculo de ADO.NET Data Services 3.5 correspondiente al sistema operativo que está usando.  
  
3.  Haga clic en el vínculo y ejecute el programa de instalación que instala el servicio.  
  
## <a name="see-also"></a>Vea también  
 [Implementación de las soluciones de Power Pivot en SharePoint](../../analysis-services/power-pivot-sharepoint/deploy-power-pivot-solutions-to-sharepoint.md)  
  
  
