---
title: Usar métodos de servicio web seguros | Microsoft Docs
description: Exija una conexión segura para los métodos del servicio web del servidor de informes con la opción SecureConnectionLevel del archivo de configuración RSReportServer.
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-server-web-service
ms.topic: reference
helpviewer_keywords:
- SOAP [Reporting Services], secure connections
- Web service [Reporting Services], SOAP
- Report Server Web service, SOAP
- XML Web service [Reporting Services], SOAP
ms.assetid: 87329299-c2ea-4517-9148-d855726768a9
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: c29c7d6d1a8fb8be7edff1203073c4c84d2e197c
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2020
ms.locfileid: "81487414"
---
# <a name="using-secure-web-service-methods"></a>Usar métodos de servicio web seguros
  Ciertos métodos de servicio web del servidor de informes pueden requerir una conexión segura al invocarlos. La opción **SecureConnectionLevel** determina los métodos que requieren una conexión segura en el archivo RSReportServer.config. El valor de esta opción es un número entero comprendido entre 0 y superior. Estos valores se describen en la siguiente tabla.  
  
|Nivel|Descripción|  
|-----------|-----------------|  
|**0**|Sin seguridad. Las llamadas realizadas a la API SOAP de Reporting Services no requieren una conexión segura.|  
|Mayor que **0**|Seguro. Todas las llamadas realizadas a la API SOAP de Reporting Services requieren una conexión segura.|  
  
 Puede utilizar el método <xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A> del servicio web para devolver una lista de los métodos del servicio web que requieren una conexión segura según la configuración actual del servidor de informes. En un escenario TLS, debería evaluar la lista de métodos que devuelve <xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A> y cambiar el nombre de esquema de URI del servicio web por "https" o "http", según el método que se vaya a llamar.  
  
## <a name="see-also"></a>Consulte también  
 [Creación de aplicaciones con el servicio web y .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Servicio web del servidor de informes](../../../reporting-services/report-server-web-service/report-server-web-service.md)  
  
  
