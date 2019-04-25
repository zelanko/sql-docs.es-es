---
title: Usar métodos de servicio web seguros | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services
ms.topic: reference
helpviewer_keywords:
- SOAP [Reporting Services], secure connections
- Web service [Reporting Services], SOAP
- Report Server Web service, SOAP
- XML Web service [Reporting Services], SOAP
ms.assetid: 87329299-c2ea-4517-9148-d855726768a9
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: e88a164602f9bbe6ad42c3897285a484cac94466
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62518665"
---
# <a name="using-secure-web-service-methods"></a>Usar métodos de servicio web seguros
  Ciertos métodos de servicio web del servidor de informes pueden requerir una conexión segura al invocarlos. La opción `SecureConnectionLevel` determina los métodos que requieren una conexión segura en el archivo RSReportServer.config. El valor de esta opción es un número entero comprendido entre 0 y superior. Estos valores se describen en la siguiente tabla.  
  
|Nivel|Descripción|  
|-----------|-----------------|  
|**0**|Sin seguridad. Las llamadas realizadas a la API SOAP de Reporting Services no requieren una conexión segura.|  
|Mayor que **0**|Seguro. Todas las llamadas realizadas a la API SOAP de Reporting Services requieren una conexión segura.|  
  
 Puede utilizar el método <xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A> del servicio web para devolver una lista de los métodos del servicio web que requieren una conexión segura según la configuración actual del servidor de informes. En un escenario SSL, debería evaluar la lista de métodos que devuelve <xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A> y cambiar el nombre de esquema de URI del servicio web por "https" o "http", según el método que se vaya a llamar.  
  
## <a name="see-also"></a>Vea también  
 [Creación de aplicaciones con el servicio web y .NET Framework](building-applications-using-the-web-service-and-the-net-framework.md)   
 [Servicio web del servidor de informes](../report-server-web-service.md)  
  
  
