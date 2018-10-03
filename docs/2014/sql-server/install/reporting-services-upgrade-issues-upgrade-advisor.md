---
title: (El Asesor de actualizaciones) de problemas de actualización de Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- Report Manager [Reporting Services], upgrade issues
- Reporting Services, upgrades
- upgrading Reporting Services
- report servers [Reporting Services], upgrade issues
ms.assetid: d9663f25-98d7-4508-ae3c-55a7277211bd
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: ed4ae6c15a16c3db009145f7daa995988ac04fbf
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227505"
---
# <a name="reporting-services-upgrade-issues-upgrade-advisor"></a>Problemas de actualización de Reporting Services (Asesor de actualizaciones)
  Los temas siguientes describen el [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] problemas que podrían afectar a la actualización a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Los temas describen acciones que se pueden llevar a cabo para mitigar el efecto de estos cambios en el entorno.  
  
 El Asesor de actualizaciones analiza una instalación del servidor de informes. Si solo se instalan componentes de cliente (por ejemplo, si el Diseñador de informes es el único componente de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] instalado en el equipo), no se notificará ningún problema.  
  
 Dependiendo de cómo configuró la instalación, puede encontrarse con problemas adicionales que el Asesor de actualizaciones no notificará. Estos problemas no impiden que se realice correctamente una actualización de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], pero pueden afectar a la forma en la que se ejecutan los informes y las aplicaciones una vez finalizada la actualización. Para obtener información sobre estos problemas, vea "Compatibilidad con versiones anteriores de Reporting Services" en los Libros en pantalla de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Si no puede utilizar el programa de instalación para actualizar una instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], puede instalar una instancia nueva de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y migrar la instalación existente a la nueva instancia. Para obtener más información, vea "Actualizar y migrar Reporting Services" en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] libros en pantalla [actualizar y migrar Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md).  
  
 Los temas siguientes describen problemas conocidos que son notificados por el Asesor de actualizaciones y que explican cómo puede modificar la instalación existente para permitir que se lleve a cabo correctamente la actualización.  
  
> [!IMPORTANT]  
>  El asesor de actualizaciones debe estar instalado en el servidor de informes para analizar una instancia de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] no admite el análisis remoto.  
>   
>  Para obtener más información, consulte [Installing Upgrade Advisor](../../../2014/sql-server/install/installing-upgrade-advisor.md).  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Certificados de cliente en el sitio web de servidor de informes &#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/client-certificates-on-the-report-server-web-site-upgrade-advisor.md)  
  
-   [Se han detectado extensiones personalizadas en el servidor de informes &#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/custom-extensions-were-detected-on-the-report-server-upgrade-advisor.md)  
  
-   [Se detectaron elementos de informe personalizado en el servidor de informes &#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/custom-report-items-were-detected-on-the-report-server-upgrade-advisor.md)  
  
-   [No se detectaron componentes de compatibilidad con versiones anteriores de IIS &#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/iis-backward-compatibility-components-were-not-detected-upgrade-advisor.md)  
  
-   [Restricción de dirección IP detectada &#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/ip-address-restriction-detected-upgrade-advisor.md)  
  
-   [Filtros ISAPI ha detectado en el sitio del servidor de informes &#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/isapi-filters-detected-on-the-report-server-site-upgrade-advisor.md)  
  
-   [Se detectaron extensiones obsoletas en el equipo del servidor de informes &#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/obsolete-extensions-were-detected-on-the-report-server-computer-upgrade-advisor.md)  
  
-   [Base de datos de servidor de informes no está configurado &#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/report-server-database-is-not-configured-upgrade-advisor.md)  
  
-   [Grupo de servicio Web de servidor de informes de SQL Server 2005 detectado &#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/sql-server-2005-report-server-web-service-group-detected-upgrade-advisor.md)  
  
-   [No se especifican los directorios virtuales &#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/virtual-directories-are-unspecified-upgrade-advisor.md)  
  
-   [Directorio virtual con un método de autenticación no admitido &#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/virtual-directory-has-unsupported-authentication-method-upgrade-advisor.md)  
  
-   [Cambios en los límites de CPU y memoria de SQL Server Standard y Enterprise &#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/cpu-memory-limits-changes-sql-server-standard-enterprise-upgrade-advisor.md)  
  
-   [Cuentas de dominio necesarias para la granja de SharePoint &#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/domain-accounts-required-for-sharepoint-farm-upgrade-advisor.md)  
  
-   [Servidor de informes de exploración directa del &#40;Asesor de actualizaciones&#41;](../../../2014/sql-server/install/direct-browsing-to-report-server-upgrade-advisor.md)  
  
-   [Microsoft SharePoint 2007 está instalado &#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/microsoft-sharepoint-2007-is-installed-upgrade-advisor.md)  
  
-   [Microsoft SQL Server Reporting Services servicio compartido de SharePoint está instalado en paralelo &#40;Upgrade Advisor&#41;](../../../2014/sql-server/install/sql-server-reporting-services-sharepoint-shared-service-side-by-side-upgrade-advisor.md)  
  
-   [Intercalación de servidor del motor de base de datos incompatible &#40;Asesor de actualizaciones&#41;](../../../2014/sql-server/install/incompatible-database-engine-server-collation-upgrade-advisor.md)  
  
-   [Otros problemas de actualización de Reporting Services](../../../2014/sql-server/install/other-reporting-services-upgrade-issues.md)  
  
  
