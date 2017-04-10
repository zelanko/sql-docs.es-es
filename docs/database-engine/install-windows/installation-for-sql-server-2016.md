---
title: "Instalaci&#243;n de SQL Server 2016 | Microsoft Docs"
ms.custom: ""
ms.date: "04/13/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.portal.Installation.f1"
helpviewer_keywords: 
  - "instalar SQL Server, instalación inicial"
  - "instalación [SQL Server]"
  - "instalación inicial [SQL Server 2008]"
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
caps.latest.revision: 34
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 34
---
# Instalaci&#243;n de SQL Server 2016
  El Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona un único árbol de características para instalar todos los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]  
  
-   [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]  
  
-   Componentes de conectividad  
  
 A partir de SQL Server 2016, las Herramientas de administración de SQL Server ya no se instalan desde el árbol de características principales; para obtener más detalles, vea [Instalar las Herramientas de administración de SQL Server con SSMS](Install%20SQL%20Server%20Management%20Tools%20\(SSMS\).md).  
  
 Puede instalar cada componente individualmente o seleccionar una combinación de los componentes enumerados anteriormente. Para efectuar la mejor selección entre las ediciones y los componentes disponibles en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Ediciones y componentes de SQL Server 2016](../../sql-server/editions-and-components-of-sql-server-2016.md) y [Características compatibles con las ediciones de SQL Server 2016](../Topic/Features%20Supported%20by%20the%20Editions%20of%20SQL%20Server%202016.md).  
  
## En esta sección  
 Independientemente de si utiliza el Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el símbolo del sistema para instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el programa de instalación incluirá los siguientes pasos:  
  
 [Planear una instalación de SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)  
 Describe cómo preparar el equipo para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Requisitos de hardware y software  
  
-   Requisitos del Comprobador de configuración del sistema y problemas de bloqueo.  
  
-   Consideraciones relativas a la seguridad  
  
 [Instalar SQL Server 2016](../../database-engine/install-windows/install-sql-server-2016.md)  
 Describe las opciones de instalación para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Referencia de la interfaz de usuario del programa de instalación de SQL Server](../Topic/SQL%20Server%20Setup%20User%20Interface%20Reference.md)  
 Se describen las opciones de instalación presentadas por el Asistente para instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Actualizar a SQL Server 2016](../../database-engine/install-windows/upgrade-to-sql-server-2016.md)  
 Describe las opciones para actualizar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Desinstalar SQL Server 2016](../../sql-server/install/uninstall-sql-server-2016.md)  
 Describe los procedimientos para desinstalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
 [Instalación de clúster de conmutación por error de SQL Server](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 Esta sección de la documentación del programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] explica cómo instalar y configurar el clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Instalar las características de SQL Server 2016 Business Intelligence](../../sql-server/install/install-sql-server-2016-business-intelligence-features.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] características que son parte de la plataforma Microsoft BI incluyen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y varias aplicaciones cliente que se usan para crear datos analíticos o para trabajar con ellos. Esta sección de la documentación del programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] explica cómo instalar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## Más información  
 [Instalar las características de SQL Server BI con SharePoint &#40;Power Pivot y Reporting Services&#41;](../Topic/Install%20SQL%20Server%20BI%20Features%20with%20SharePoint%20\(Power%20Pivot%20and%20Reporting%20Services\).md)  
 En esta sección se explica cómo instalar las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un entorno de SharePoint. Identifica qué características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están disponibles para una versión y edición concreta de SharePoint. También incluye los procedimientos de instalación de [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint y Reporting Services en modo de SharePoint.  
  
 ![ssrs_fyi_note](../../analysis-services/instances/install-windows/media/ssrs-fyi-note.png) Instale la nueva base de datos de ejemplo, [Wide World Importers](https://msdn.microsoft.com/library/mt734199(v=sql.1).aspx). 
  
 [Otras bases de datos de ejemplo y ejemplos de SQL Server](http://sqlserversamples.codeplex.com/)  
 Describe cómo instalar y configurar ejemplos y bases de datos de ejemplo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
Vaya al [centro de actualizaciones de SQL Server](https://msdn.microsoft.com/library/ff803383.aspx) para obtener vínculos e información sobre todas las versiones compatibles de [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)].  
  
## Vea también  
 [Novedades de la instalación de SQL Server](../../sql-server/install/what-s-new-in-sql-server-installation.md)   
 [Requisitos de hardware y software para instalar SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md)  
  
  