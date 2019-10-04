---
title: Problemas de actualización de Reporting Services (Asesor de actualizaciones) | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Report Manager [Reporting Services], upgrade issues
- Reporting Services, upgrades
- upgrading Reporting Services
- report servers [Reporting Services], upgrade issues
ms.assetid: d9663f25-98d7-4508-ae3c-55a7277211bd
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 75c3bda5d15e3930fcdeba9ca73d70128fd90336
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952059"
---
# <a name="reporting-services-upgrade-issues-upgrade-advisor"></a>Problemas de actualización de Reporting Services (Asesor de actualizaciones)
  En los temas siguientes se describen los problemas [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que pueden afectar a la actualización a @no__t 2. Los temas describen acciones que se pueden llevar a cabo para mitigar el efecto de estos cambios en el entorno.  
  
 El Asesor de actualizaciones analiza una instalación del servidor de informes. Si solo se instalan componentes de cliente (por ejemplo, si el Diseñador de informes es el único componente de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado en el equipo), no se notificará ningún problema.  
  
 Dependiendo de cómo configuró la instalación, puede encontrarse con problemas adicionales que el Asesor de actualizaciones no notificará. Estos problemas no impiden que se realice correctamente una actualización de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], pero pueden afectar a la forma en la que se ejecutan los informes y las aplicaciones una vez finalizada la actualización. Para obtener información sobre estos problemas, vea "Compatibilidad con versiones anteriores de Reporting Services" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Si no puede utilizar el programa de instalación para actualizar una instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], puede instalar una instancia nueva de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y migrar la instalación existente a la nueva instancia. Para obtener más información, vea "actualizar y migrar Reporting Services" en los libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [actualizar y migrar Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).  
  
 Los temas siguientes describen problemas conocidos que son notificados por el Asesor de actualizaciones y que explican cómo puede modificar la instalación existente para permitir que se lleve a cabo correctamente la actualización.  
  
> [!IMPORTANT]  
>  El asesor de actualizaciones debe estar instalado en el servidor de informes para analizar una instancia de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no admite el análisis remoto.  
>   
>  Para obtener más información, vea [instalar el asesor de actualizaciones](../../../2014/sql-server/install/installing-upgrade-advisor.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Certificados de cliente en el asesor de actualizaciones &#40;del sitio web del servidor de informes&#41;](../../../2014/sql-server/install/client-certificates-on-the-report-server-web-site-upgrade-advisor.md)  
  
-   [Se han detectado extensiones personalizadas en el asesor &#40;de actualizaciones del servidor de informes&#41;](../../../2014/sql-server/install/custom-extensions-were-detected-on-the-report-server-upgrade-advisor.md)  
  
-   [Se detectaron elementos de informe personalizados en el &#40;Asesor de actualizaciones del servidor de informes&#41;](../../../2014/sql-server/install/custom-report-items-were-detected-on-the-report-server-upgrade-advisor.md)  
  
-   [No se detectaron &#40;componentes de compatibilidad con versiones anteriores de IIS. Asesor de actualizaciones&#41;](../../../2014/sql-server/install/iis-backward-compatibility-components-were-not-detected-upgrade-advisor.md)  
  
-   [Asesor de actualizaciones de &#40;restricción de direcciones IP detectadas&#41;](../../../2014/sql-server/install/ip-address-restriction-detected-upgrade-advisor.md)  
  
-   [Filtros ISAPI detectados en el asesor de &#40;actualizaciones de sitios del servidor de informes&#41;](../../../2014/sql-server/install/isapi-filters-detected-on-the-report-server-site-upgrade-advisor.md)  
  
-   [Se detectaron extensiones obsoletas en el asesor de &#40;actualizaciones de equipos del servidor de informes&#41;](../../../2014/sql-server/install/obsolete-extensions-were-detected-on-the-report-server-computer-upgrade-advisor.md)  
  
-   [El asesor de actualizaciones no está &#40;configurado en la base de datos del servidor de informes&#41;](../../../2014/sql-server/install/report-server-database-is-not-configured-upgrade-advisor.md)  
  
-   [SQL Server 2005 Grupo de servicios web del servidor &#40;de informes detectó el asesor de actualizaciones&#41;](../../../2014/sql-server/install/sql-server-2005-report-server-web-service-group-detected-upgrade-advisor.md)  
  
-   [Los directorios virtuales son el &#40;Asesor de actualizaciones no especificado&#41;](../../../2014/sql-server/install/virtual-directories-are-unspecified-upgrade-advisor.md)  
  
-   [El directorio virtual tiene el asesor de actualizaciones &#40;del método de autenticación no admitido&#41;](../../../2014/sql-server/install/virtual-directory-has-unsupported-authentication-method-upgrade-advisor.md)  
  
-   [Cambios en los límites de CPU y memoria para SQL Server Standard &#40;y el asesor de actualizaciones empresariales&#41;](../../../2014/sql-server/install/cpu-memory-limits-changes-sql-server-standard-enterprise-upgrade-advisor.md)  
  
-   [Cuentas de dominio necesarias para el &#40;Asesor de actualizaciones de granja de SharePoint&#41;](../../../2014/sql-server/install/domain-accounts-required-for-sharepoint-farm-upgrade-advisor.md)  
  
-   [Exploración directa del Asesor de actualizaciones &#40;del servidor de informes&#41;](../../../2014/sql-server/install/direct-browsing-to-report-server-upgrade-advisor.md)  
  
-   [Microsoft SharePoint 2007 está instalado &#40;en el asesor de actualizaciones&#41;](../../../2014/sql-server/install/microsoft-sharepoint-2007-is-installed-upgrade-advisor.md)  
  
-   [Microsoft SQL Server Reporting Services el servicio compartido de SharePoint está instalado en &#40;paralelo Upgrade Advisor&#41;](../../../2014/sql-server/install/sql-server-reporting-services-sharepoint-shared-service-side-by-side-upgrade-advisor.md)  
  
-   [Asesor de &#40;actualizaciones de intercalación de servidor motor de base de datos incompatible&#41;](../../../2014/sql-server/install/incompatible-database-engine-server-collation-upgrade-advisor.md)  
  
-   [Otros problemas de actualización de Reporting Services](../../../2014/sql-server/install/other-reporting-services-upgrade-issues.md)  
  
  
