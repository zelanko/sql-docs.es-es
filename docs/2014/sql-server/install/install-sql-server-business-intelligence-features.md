---
title: Instalar las características de BI de SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 67399b24-e48a-49f3-9dd4-32d78c6a2ece
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 3fec33fe160d5ee901eefda541133e6c7b9610b0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48116965"
---
# <a name="install-sql-server-2014-bi-features"></a>Instalar las características de SQL Server 2014 BI
  Las características de SQL Server que forman parte de la plataforma Microsoft Business Intelligence incluyen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]y varias aplicaciones cliente que se usan para crear datos analíticos o para trabajar con ellos. En esta sección de la documentación del programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se explica cómo instalar estas características.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] se pueden instalar como servidores independientes, en configuraciones escaladas o como aplicaciones de servicio compartido en una granja de SharePoint. Al instalar los servicios en una granja de servidores, se habilitan las características de BI que solo están disponibles en SharePoint, incluido [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint y [!INCLUDE[ssCrescent](../../includes/sscrescent-md.md)], el diseñador de informes interactivo ad hoc de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] que se ejecuta en bases de datos de modelo tabular de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Si ya está familiarizado con los pasos de instalación para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o PowerPivot para SharePoint, puede ir directamente a las listas de comprobación para obtener información sobre cómo habilitar escenarios concretos. Para obtener más información, consulte [listas de comprobación para instalar las características de BI con SharePoint](checklists-for-installing-bi-features-with-sharepoint.md).  
  
## <a name="contents"></a>Contenido  
 En esta sección:  
  
|Vínculo|Tarea|  
|----------|----------|  
|[Listas de comprobación para instalar características de BI con SharePoint](checklists-for-installing-bi-features-with-sharepoint.md)|Si ya sabe lo que desea instalar y está familiarizado con los pasos de instalación para [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint, puede usar las listas de comprobación de esta sección para obtener orientación sobre el orden de instalación, los requisitos de cuentas y permisos, y los pasos para implementar topologías avanzadas, incluidas implementaciones de varios servidores y de varias características.|  
|[Instalar las características SQL Server BI con SharePoint &#40;PowerPivot y Reporting Services&#41;](install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md)|En esta sección se explica cómo instalar las características de SQL Server en un entorno de SharePoint. Identifica qué características de SQL Server están disponibles para una versión y edición concreta de SharePoint. También incluye los procedimientos de instalación de PowerPivot para SharePoint y Reporting Services en modo de SharePoint.|  
|[Instalar Analysis Services en el modo de minería de datos y multidimensional](install-analysis-services-in-multidimensional-and-data-mining-mode.md)<br /><br /> [Instalar Analysis Services en modo tabular](../../analysis-services/instances/install-windows/install-analysis-services.md)<br /><br /> [Instalar Data Quality Services](../../data-quality-services/install-windows/install-data-quality-services.md)<br /><br /> [Instalar Integration Services](../../integration-services/install-windows/install-integration-services.md)<br /><br /> [Instalar Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)<br /><br /> [Instalar el servidor de informes en modo nativo de Reporting Services](../../reporting-services/install-windows/install-reporting-services-native-mode-report-server.md)|Esta sección proporciona indicaciones para instalar Analysis Services, Integration Services, Master Data Services y Reporting Services, donde Analysis Services y Reporting Services se instalan sin SharePoint. Esto se denomina a veces *modo nativo*, y es el escenario más común de instalación de Reporting Services y Analysis Services. En esta sección obtendrá información sobre las opciones de instalación que determinan directamente el contexto operativo del servidor. En Reporting Services, puede tratarse de un servidor preconfigurado o de un servidor que requiere varios pasos de configuración para poder utilizarlo. Para Analysis Services, las opciones de instalación que seleccione determinarán el tipo de proyecto que puede implementar en el servidor.|  
|[Comprobar o solucionar problemas de instalación de características de BI de SQL Server](../../../2014/sql-server/install/verify-or-troubleshoot-sql-server-bi-feature-installation-problems.md)|Esta sección incluye los pasos para comprobar una instalación. También proporciona vínculos a la información de resolución de problemas en Internet.|  
  
## <a name="related-content"></a>Contenido relacionado  
  
|Vínculo|Tarea|  
|----------|----------|  
|[Actualizar a SQL Server 2014](../../database-engine/install-windows/upgrade-sql-server.md)<br /><br /> [Actualizar Analysis Services](../../database-engine/install-windows/upgrade-analysis-services.md)<br /><br /> [Actualizar PowerPivot para SharePoint](../../database-engine/install-windows/upgrade-power-pivot-for-sharepoint.md)<br /><br /> [Actualizar y migrar Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)|Siga las instrucciones de esta sección para actualizar los servidores y el contenido de una versión anterior a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].|  
|[Desinstalar SQL Server 2014](uninstall-sql-server.md)<br /><br /> [Desinstalar PowerPivot para SharePoint](../../../2014/sql-server/install/uninstall-power-pivot-for-sharepoint.md)<br /><br /> [Desinstalar Reporting Services](../../../2014/sql-server/install/uninstall-reporting-services.md)|Use las instrucciones de esta sección para desinstalar las características de BI.|  
  
## <a name="see-also"></a>Vea también  
 [¿Qué novedades &#40;Reporting Services&#41;](../../../2014/reporting-services/what-s-new-reporting-services.md)   
 [Novedades de Analysis Services y Business Intelligence](../../analysis-services/what-s-new-in-analysis-services.md)   
 [Instalar a SQL Server 2014](../../database-engine/install-windows/install-sql-server.md)   
 [Actualizar a SQL Server 2014](../../database-engine/install-windows/upgrade-sql-server.md)  
  
  
