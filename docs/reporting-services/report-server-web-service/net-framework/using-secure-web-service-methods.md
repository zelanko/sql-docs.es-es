---
title: "Utilizando los métodos de servicio Web segura | Documentos de Microsoft"
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
helpviewer_keywords:
- SOAP [Reporting Services], secure connections
- Web service [Reporting Services], SOAP
- Report Server Web service, SOAP
- XML Web service [Reporting Services], SOAP
ms.assetid: 87329299-c2ea-4517-9148-d855726768a9
caps.latest.revision: 36
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: a6aab5e722e732096e9e4ffdf458ac25088e09ae
ms.openlocfilehash: 1222a4223f54eec0f6083790da4d0afebf353ec9
ms.contentlocale: es-es
ms.lasthandoff: 08/03/2017

---
# <a name="using-secure-web-service-methods"></a>Usar métodos de servicio web seguros
  Ciertos métodos de servicio web del servidor de informes pueden requerir una conexión segura al invocarlos. Los métodos que requieren una conexión segura están determinados por la **SecureConnectionLevel** en el archivo RSReportServer.config. El valor de esta opción es un número entero comprendido entre 0 y superior. Estos valores se describen en la siguiente tabla.  
  
|Level|Description|  
|-----------|-----------------|  
|**0**|Sin seguridad. Las llamadas realizadas a la API SOAP de Reporting Services no requieren una conexión segura.|  
|Mayor **0**|Seguro. Todas las llamadas realizadas a la API SOAP de Reporting Services requieren una conexión segura.|  
  
 Puede utilizar el método <xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A> del servicio web para devolver una lista de los métodos del servicio web que requieren una conexión segura según la configuración actual del servidor de informes. En un escenario SSL, debería evaluar la lista de métodos que devuelve <xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A> y cambiar el nombre de esquema de URI del servicio web por "https" o "http", según el método que se vaya a llamar.  
  
## <a name="see-also"></a>Vea también  
 [Creación de aplicaciones con el servicio Web y .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Servicio Web de servidor de informes](../../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
