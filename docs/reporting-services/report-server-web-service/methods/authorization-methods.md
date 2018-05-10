---
title: Métodos de autorización | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.component: report-server-web-service
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- security [Reporting Services], reports
- authorization [Reporting Services]
- reports [Reporting Services], security
- tasks [Reporting Services]
- roles [Reporting Services], methods
ms.assetid: 45e9cf2c-facf-4801-9482-c855403f42a8
caps.latest.revision: 42
author: markingmyname
ms.author: maghan
manager: kfile
ms.openlocfilehash: 479c1814a6ce52f3deec42d5ce84f40bc00278a1
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="authorization-methods"></a>Métodos de autorización
  Puede utilizar estos métodos para administrar tareas, roles y directivas en el servidor de informes.  
  
|Método|Acción|  
|------------|------------|  
|<xref:ReportService2010.ReportingService2010.CreateRole%2A>|Agrega un nuevo rol a la base de datos del servidor de informes. Este método se aplica solo al modo nativo.|  
|<xref:ReportService2010.ReportingService2010.DeleteRole%2A>|Elimina un rol de la base de datos del servidor de informes. Este método se aplica solo al modo nativo.|  
|<xref:ReportService2010.ReportingService2010.GetPermissions%2A>|Devuelve los permisos de usuario que están asociados a un elemento determinado en la base de datos del servidor de informes o biblioteca de SharePoint.|  
|<xref:ReportService2010.ReportingService2010.GetPolicies%2A>|Devuelve las directivas que están asociados a un elemento determinado en la base de datos del servidor de informes o biblioteca de SharePoint.|  
|<xref:ReportService2010.ReportingService2010.GetRoleProperties%2A>|Devuelve las propiedades de metadatos de rol y una colección de tareas asociadas.|  
|<xref:ReportService2010.ReportingService2010.GetSystemPermissions%2A>|Devuelve los permisos de sistema del usuario. Este método se aplica solo al modo nativo.|  
|<xref:ReportService2010.ReportingService2010.GetSystemPolicies%2A>|Devuelve las directivas del sistema, incluidos los grupos y roles a los que están asociados. Este método se aplica solo al modo nativo.|  
|<xref:ReportService2010.ReportingService2010.InheritParentSecurity%2A>|Elimina las directivas asociadas a un elemento determinado en la base de datos del servidor de informes y establece las directivas de seguridad para el elemento en las de su elemento primario.|  
|<xref:ReportService2010.ReportingService2010.IsSSLRequired%2A>|Devuelve un valor booleano que indica si el protocolo Capa de sockets seguros (SSL) se requiere para utilizar el extremo de <xref:ReportService2010>.|  
|<xref:ReportService2010.ReportingService2010.ListRoles%2A>|Devuelve los nombres y descripciones de los roles que administra el servidor de informes.|  
|<xref:ReportExecution2005.ReportExecutionService.ListSecureMethods%2A>|Devuelve una lista de los métodos del Protocolo simple de acceso a objetos (SOAP) en el extremo de <xref:ReportExecution2005> que requieren una conexión segura cuando se invocan. El valor **SecureConnectionLevel** del servidor de informes se usa para determinar qué métodos se devuelven.|  
|<xref:ReportService2010.ReportingService2010.ListTasks%2A>|Devuelve las tareas que son administradas por el servidor de informes.|  
|<xref:ReportService2010.ReportingService2010.SetPolicies%2A>|Establece las directivas que están asociadas a un elemento especificado.|  
|<xref:ReportService2010.ReportingService2010.SetRoleProperties%2A>|Establece las propiedades de los metadatos de rol y asocia un conjunto de tareas a un rol. Este método se aplica solo al modo nativo.|  
|<xref:ReportService2010.ReportingService2010.SetSystemPolicies%2A>|Establece la directiva del sistema que define los grupos y sus roles asociados. Este método se aplica solo al modo nativo.|  
  
## <a name="see-also"></a>Ver también  
 [Creación de aplicaciones con el servicio web y .NET Framework](../../../reporting-services/report-server-web-service/net-framework/building-applications-using-the-web-service-and-the-net-framework.md)   
 [Servicio web del servidor de informes](../../../reporting-services/report-server-web-service/report-server-web-service.md)   
 [Métodos del servicio web del servidor de informes](../../../reporting-services/report-server-web-service/methods/report-server-web-service-methods.md)   
 [Referencia técnica &#40;SSRS&#41;](../../../reporting-services/technical-reference-ssrs.md)  
  
  
