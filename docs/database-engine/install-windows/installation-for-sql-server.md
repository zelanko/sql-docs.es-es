---
title: "Instalación de SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 09/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: install-windows
ms.reviewer: 
ms.suite: sql
ms.technology:
- setup-install
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.portal.Installation.f1
helpviewer_keywords:
- installing SQL Server, initial installation
- installation [SQL Server]
- initial installation [SQL Server]
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
caps.latest.revision: 
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 8fe0874d637f1597814bf14c8d12d111ece4cee1
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/09/2018
---
# <a name="sql-server-installation"></a>Instalación de SQL Server

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

El Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona un único árbol de características para instalar todos los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
-   [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]  
-   [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]  
-   Componentes de conectividad  
  
A partir de [!INCLUDE[ss2016](../../includes/sssql15-md.md)], las Herramientas de administración de SQL Server ya no se instalan desde el árbol de características principales; para obtener más detalles, vea [Descarga de SQL Server Management Studio (SSMS)](../../ssms/download-sql-server-management-studio-ssms.md).  
  
Puede instalar cada componente individualmente o seleccionar una combinación de los componentes enumerados anteriormente. Para efectuar la mejor selección entre las ediciones y los componentes disponibles en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea las características compatibles en su versión de SQL Server:

- [Ediciones y características admitidas de [!INCLUDE[ss2017](../../includes/sssqlv14-md.md)]](~/sql-server/editions-and-components-of-sql-server-2017.md).  
- [Ediciones y características admitidas de [!INCLUDE[ss2016](../../includes/sssql15-md.md)]](~/sql-server/editions-and-components-of-sql-server-2016.md).  
- [Características compatibles con las ediciones de [!INCLUDE[ss2014](../../includes/sssql14-md.md)]](http://technet.microsoft.com/library/cc645993(v=sql.120).aspx)
  
## <a name="in-this-section"></a>En esta sección  
Independientemente de si utiliza el Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el símbolo del sistema para instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el programa de instalación incluirá los siguientes pasos:  
  
[Planear una instalación de SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)  
Describe cómo preparar el equipo para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Requisitos de hardware y software  
-   Requisitos del Comprobador de configuración del sistema y problemas de bloqueo.  
-   Consideraciones relativas a la seguridad  
  
[Instalar SQL Server](../../database-engine/install-windows/install-sql-server.md)  
 Describe las opciones de instalación para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
[Referencia de la interfaz de usuario del programa de instalación de SQL Server](http://msdn.microsoft.com/library/183b5cdd-962e-41ca-8064-ea44f622c77d)  
 Se describen las opciones de instalación presentadas por el Asistente para instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
[Actualizar SQL Server](../../database-engine/install-windows/upgrade-sql-server.md)  
 Describe las opciones para actualizar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
[Desinstalar SQL Server](../../sql-server/install/uninstall-sql-server.md)  
 Describe los procedimientos para desinstalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
[Instalación de clúster de conmutación por error de SQL Server](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 Esta sección de la documentación del programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] explica cómo instalar y configurar el clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
[Instalar las características de SQL Server Business Intelligence](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] características que son parte de la plataforma Microsoft BI incluyen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]y varias aplicaciones cliente que se usan para crear datos analíticos o para trabajar con ellos. Esta sección de la documentación del programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] explica cómo instalar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="more-information"></a>Más información
[Instalar las características de SQL Server BI con SharePoint &#40;Power Pivot y Reporting Services&#41;](http://msdn.microsoft.com/library/3166107c-30c2-468e-bb1b-bb42b79b37c3)  
 En esta sección se explica cómo instalar las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un entorno de SharePoint. Identifica qué características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están disponibles para una versión y edición concreta de SharePoint. También incluye los procedimientos de instalación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint y Reporting Services en modo de SharePoint.  
  
![ssrs_fyi_note](../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png) Instale la nueva base de datos de ejemplo, [Wide World Importers](https://msdn.microsoft.com/library/mt734199(v=sql.1).aspx). 
  
[Otras bases de datos de ejemplo y ejemplos de SQL Server](http://sqlserversamples.codeplex.com/)  
 Describe cómo instalar y configurar ejemplos y bases de datos de ejemplo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
Vaya al [centro de actualizaciones de SQL Server](https://msdn.microsoft.com/library/ff803383.aspx) para obtener vínculos e información sobre todas las versiones compatibles de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].  
  
## <a name="see-also"></a>Ver también  
[Novedades de la instalación de SQL Server](../../sql-server/install/what-s-new-in-sql-server-installation.md)   
[Requisitos de hardware y software para instalar SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
