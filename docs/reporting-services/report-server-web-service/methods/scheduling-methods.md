---
title: "Métodos de programación | Microsoft Docs"
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
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- schedules [Reporting Services], methods
- reports [Reporting Services], scheduling
- shared schedules [Reporting Services], methods
- methods [Reporting Services], scheduling
ms.assetid: 68ae13f9-d91e-4572-a82a-8fa42001569e
caps.latest.revision: "35"
author: guyinacube
ms.author: asaxton
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: f9babec18539dac85568a4b15461a1c04f768098
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="scheduling-methods"></a>Métodos de programación
  Puede utilizar estos métodos para crear y administrar las programaciones compartidas para la ejecución y la entrega de informes, así como para almacenar en memoria caché los planes de actualización que utiliza el servidor de informes.  
  
|Método|Acción|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.CreateCacheRefreshPlan%2A>|Crea un plan de actualización de caché para un elemento.|  
|<xref:ReportService2010.ReportingService2010.CreateSchedule%2A>|Crea una nueva programación compartida.|  
|<xref:ReportService2010.ReportingService2010.DeleteCacheRefreshPlan%2A>|Elimina un plan de actualización de caché.|  
|<xref:ReportService2010.ReportingService2010.DeleteSchedule%2A>|Elimina una programación compartida según un identificador de programación concreto.|  
|<xref:ReportService2010.ReportingService2010.GetCacheRefreshPlanProperties%2A>|Devuelve las propiedades del plan de actualización de caché especificado.|  
|<xref:ReportService2010.ReportingService2010.GetScheduleProperties%2A>|Devuelve los valores de las propiedades de una programación compartida.|  
|<xref:ReportService2010.ReportingService2010.ListCacheRefreshPlans%2A>|Devuelve una lista de los planes de actualización de memoria caché asociada a un elemento de catálogo.|  
|<xref:ReportService2010.ReportingService2010.ListScheduledItems%2A>|Devuelve una lista de los elementos que están asociados a una programación compartida.|  
|<xref:ReportService2010.ReportingService2010.ListSchedules%2A>|Devuelve una lista de todas las programaciones compartidas en el servidor de informes o el sitio de SharePoint.|  
|<xref:ReportService2010.ReportingService2010.ListScheduleStates%2A>|Devuelve una lista de estados de programación admitidos.|  
|<xref:ReportService2010.ReportingService2010.PauseSchedule%2A>|Pausa la ejecución de una programación determinada.|  
|<xref:ReportService2010.ReportingService2010.ResumeSchedule%2A>|Reanuda una programación compartida que se ha pausado.|  
|<xref:ReportService2010.ReportingService2010.SetCacheRefreshPlanProperties%2A>|Establece las propiedades de un plan de actualización de caché.|  
|<xref:ReportService2010.ReportingService2010.SetScheduleProperties%2A>|Establece el valor de las propiedades de una programación compartida.|  
  
## <a name="see-also"></a>Vea también  
 [Creación de aplicaciones con el servicio Web y .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Servicio web del servidor de informes](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Métodos del servicio web del servidor de informes](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)   
 [Referencia técnica &#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
