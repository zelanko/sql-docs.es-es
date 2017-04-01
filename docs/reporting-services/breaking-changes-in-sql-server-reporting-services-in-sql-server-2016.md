---
title: "Cambios substanciales de SQL Server Reporting Services en SQL Server 2016 | Microsoft Docs"
ms.date: "03/15/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "referencias de Me.Value"
  - "Reporting Services, compatibilidad con versiones anteriores"
  - "cambios recientes [Reporting Services]"
ms.assetid: 39c7aafd-dcb9-4317-b8f7-d15828eb4f9a
caps.latest.revision: 121
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 116
---
# Cambios substanciales de SQL Server Reporting Services en SQL Server 2016
  En este tema se describen los principales cambios realizados en [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Estos cambios pueden provocar errores en las aplicaciones, en los scripts o en las funcionalidades basados en versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Podría encontrarlos al actualizar, o en scripts o informes personalizados.  
  
  ## Extensiones de seguridad
  
  Las extensiones de seguridad personalizadas necesitan alguna modificación para funcionar con el nuevo [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]. Las extensiones de seguridad necesitan usar la interfaz IAuthenticationExtension2.
  
  ## Proveedor WMI
  
  La aplicación [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] cambia su nombre de "ReportManager" a "ReportServerWebApp".
  
## Vea también  
 [Cambios de comportamiento de SQL Server Reporting Services en SQL Server 2016](http://msdn.microsoft.com/es-es/2a767f0f-84f2-4099-8784-1e37790f858e)   
 [Novedades de Reporting Services &#40;SSRS&#41;](../Topic/What's%20New%20in%20Reporting%20Services%20\(SSRS\).md)   
 [Características en desuso de SQL Server Reporting Services en SQL Server 2016](http://msdn.microsoft.com/es-es/3876c01e-f81d-4cce-9104-5106a8c369e6)   
 [Funcionalidad de SQL Server Reporting Services no incluida en SQL Server 2016](http://msdn.microsoft.com/es-es/d529cc96-3483-480b-9bfc-bd28b1d0ef52)  
  
  