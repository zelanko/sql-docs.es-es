---
title: "Modelo - métodos de servicio Web del servidor de informes | Documentos de Microsoft"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: d3e658c9-bb22-480b-a3d5-bcde8f537ab2
caps.latest.revision: 4
author: sabotta
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 350614f2ba7d522860c15a27456598aeb12c270a
ms.contentlocale: es-es
ms.lasthandoff: 06/13/2017

---
# <a name="model-methods---report-server-web-service"></a>Métodos del modelo - servicio de Web del servidor de informes
  Puede utilizar estos métodos para administrar los modelos.  
  
|Método|Acción|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.GenerateModel%2A>|Genera un modelo predeterminado encima de un origen de datos compartido.|  
|<xref:ReportService2010.ReportingService2010.GetModelItemPermissions%2A>|Recupera los permisos de usuario que están asociados al elemento de modelo.|  
|<xref:ReportService2010.ReportingService2010.GetModelItemPolicies%2A>|Recupera las directivas que están asociadas a un elemento de modelo.|  
|<xref:ReportService2010.ReportingService2010.GetUserModel%2A>|Devuelve la parte semántica de un modelo para el usuario actual.|  
|<xref:ReportService2010.ReportingService2010.InheritModelItemParentSecurity%2A>|Elimina las directivas que están asociadas a un elemento de modelo y hace que el elemento de modelo herede las directivas de su elemento primario.|  
|<xref:ReportService2010.ReportingService2010.ListModelDrillthroughReports%2A>|Enumera los informes detallados que están asociados a una entidad en un modelo.|  
|<xref:ReportService2010.ReportingService2010.ListModelItemChildren%2A>|Devuelve una matriz de elementos secundarios del elemento de modelo.|  
|<xref:ReportService2010.ReportingService2010.ListModelItemTypes%2A>|Devuelve una lista de los tipos de elemento de modelo admitidos.|  
|<xref:ReportService2010.ReportingService2010.ListModelPerspectives%2A>|Enumera los modelos y perspectivas que están disponibles para el usuario.|  
|<xref:ReportService2010.ReportingService2010.RegenerateModel%2A>|Actualiza un modelo existente según los cambios del esquema del origen de datos.|  
|<xref:ReportService2010.ReportingService2010.RemoveAllModelItemPolicies%2A>|Elimina todas las directivas que están asociadas a los elementos de modelo en el modelo especificado.|  
|<xref:ReportService2010.ReportingService2010.SetModelDrillthroughReports%2A>|Asocia un conjunto de informes detallados junto con un modelo.|  
|<xref:ReportService2010.ReportingService2010.SetModelItemPolicies%2A>|Establece las directivas de seguridad en un elemento de modelo.|  
  
## <a name="see-also"></a>Vea también  
 [Creación de aplicaciones con el servicio Web y .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Servicio Web de servidor de informes](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Métodos de servicio Web de servidor de informes](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)   
 [Referencia técnica &#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
