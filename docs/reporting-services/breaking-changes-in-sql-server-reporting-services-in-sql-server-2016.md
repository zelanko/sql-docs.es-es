---
title: Cambios substanciales de SQL Server Reporting Services en SQL Server 2016 | Microsoft Docs
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- Me.Value references
- Reporting Services, backward compatibility
- breaking changes [Reporting Services]
ms.assetid: 39c7aafd-dcb9-4317-b8f7-d15828eb4f9a
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 41aad02f9f5b65dd1cf1474abd0c152f3face8c0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65503950"
---
# <a name="breaking-changes-in-sql-server-reporting-services-in-sql-server-2016"></a>Cambios substanciales de SQL Server Reporting Services en SQL Server 2016

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016](../includes/ssrs-appliesto-2016.md)] [!INCLUDE [ssrs-appliesto-not-2017](../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../includes/ssrs-previous-versions.md)]

En este tema se describen los principales cambios realizados en [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]. Estos cambios pueden provocar errores en las aplicaciones, en los scripts o en las funcionalidades basados en versiones anteriores de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Podría encontrarlos al actualizar, o en scripts o informes personalizados.

## <a name="security-extensions"></a>Extensiones de seguridad

Las extensiones de seguridad personalizadas necesitan alguna modificación para funcionar con el nuevo [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)]. Las extensiones de seguridad necesitan usar la interfaz IAuthenticationExtension2.

## <a name="wmi-provider"></a>Proveedor WMI

La aplicación [!INCLUDE[ssRSWebPortal](../includes/ssrswebportal.md)] cambia su nombre de "ReportManager" a "ReportServerWebApp".

## <a name="next-steps"></a>Pasos siguientes

[Cambios de comportamiento de SQL Server Reporting Services en SQL Server 2016](../reporting-services/behavior-changes-to-sql-server-reporting-services-in-sql-server-2016.md)  
[Novedades de Reporting Services (SSRS)](../reporting-services/what-s-new-in-sql-server-reporting-services-ssrs.md)   
[Características en desuso de SQL Server Reporting Services en SQL Server 2016](../reporting-services/deprecated-features-in-sql-server-reporting-services-ssrs.md)    
[Funcionalidad de SQL Server Reporting Services descontinuada en SQL Server 2016](../reporting-services/discontinued-functionality-to-sql-server-reporting-services-in-sql-server.md)  

¿Tiene alguna pregunta más? [Puede plantear sus dudas en el foro de Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231).
