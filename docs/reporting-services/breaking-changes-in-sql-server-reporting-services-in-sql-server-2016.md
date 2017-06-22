---
title: Cambios importantes en SQL Server Reporting Services en SQL Server 2016 | Documentos de Microsoft
ms.date: 03/15/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Me.Value references
- Reporting Services, backward compatibility
- breaking changes [Reporting Services]
ms.assetid: 39c7aafd-dcb9-4317-b8f7-d15828eb4f9a
caps.latest.revision: 121
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 36ec7d7f1aa78e08f7fa4b63e8ca6525afe1c215
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="breaking-changes-in-sql-server-reporting-services-in-sql-server-2016"></a>Cambios substanciales de SQL Server Reporting Services en SQL Server 2016
  En este tema se describen los principales cambios realizados en [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Estos cambios pueden provocar errores en las aplicaciones, en los scripts o en las funcionalidades basados en versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Podría encontrarlos al actualizar, o en scripts o informes personalizados.  
  
  ## <a name="security-extensions"></a>Extensiones de seguridad
  
  Las extensiones de seguridad personalizadas necesitan alguna modificación para funcionar con el nuevo [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]. Las extensiones de seguridad necesitan usar la interfaz IAuthenticationExtension2.
  
  ## <a name="wmi-provider"></a>Proveedor WMI
  
  La aplicación [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] cambia su nombre de "ReportManager" a "ReportServerWebApp".
  
## <a name="see-also"></a>Vea también 

[Cambios de comportamiento en SQL Server Reporting Services en SQL Server 2016](../reporting-services/behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)

[Novedades de Reporting Services (SSRS)](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)
 
[Características en desuso de SQL Server Reporting Services en SQL Server 2016](../reporting-services/deprecated-features-in-sql-server-reporting-services-ssrs.md)
  
[Funcionalidad de SQL Server Reporting Services no incluida en SQL Server 2016](../reporting-services/discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)



