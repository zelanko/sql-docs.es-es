---
title: Instalar SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- installing SQL Server, preparing to install
- installation [SQL Server]
ms.assetid: 0300e777-d56b-4d10-9c33-c9ebd2489ee5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7b9fb6be3970ea12ce3252e70f7773f1687dbe83
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/07/2019
ms.locfileid: "57578361"
---
# <a name="install-sql-server-2014"></a>Instalar SQL Server 2014
## <a name="download-sql-server-2014-expresshttpwwwhanselmancomblogdownloadsqlserverexpressaspx"></a>[Descargue SQL Server 2014 Express](http://www.hanselman.com/blog/DownloadSQLServerExpress.aspx)
  **Agradecimiento a [Scott Hanselman](http://www.hanselman.com/) para recopilar todos los vínculos de paquete del instalador en un solo lugar.**
  
 En este tema se proporciona información general de las distintas opciones de instalación de que se dispone para instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]. Para obtener más información acerca de los diversos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componentes que pueden instalarse y el proceso de instalación, consulte [instalación de SQL Server 2014](installation-for-sql-server.md).  
> **Nota:** [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está disponible en las ediciones de 32 bits y 64 bits. Las ediciones de 64 bits y de 32 bits de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se instalan a través del Asistente para la instalación o en un símbolo del sistema. Para obtener más información acerca de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] componentes, consulte [ediciones y componentes de SQL Server 2014](../../sql-server/editions-and-components-of-sql-server-2016.md) y [características compatibles con las ediciones de SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md).  
  
 De forma predeterminada, las bases de datos y el código de ejemplo no se instalan como parte del programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para instalar las bases de datos y el código de ejemplo para las ediciones de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que no son Express, vea el [sitio web de CodePlex](https://go.microsoft.com/fwlink/?LinkId=87843). Para obtener información sobre la compatibilidad de las bases de datos y el código muestra de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)], vea [Información general sobre bases de datos y ejemplos](https://go.microsoft.com/fwlink/?LinkId=110391).  
  
 Antes de instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], revise los requisitos de instalación, las comprobaciones de la configuración del sistema y las consideraciones de seguridad. Para más información, consulte [Planning a SQL Server Installation](../../sql-server/install/planning-a-sql-server-installation.md). Revise los temas de la próxima sección para obtener información sobre los distintos escenarios de instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
  
## <a name="install-includesscurrentincludessscurrent-mdmd-components"></a>Instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] componentes  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Acerca del motor de base de datos de SQL Server](../sql-server-database-engine-overview.md)|Describe cómo instalar y configurar el [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].|  
|[Instalar la replicación de SQL Server](install-sql-server-replication.md)|Describe cómo instalar y configurar la replicación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Instalar Distributed Replay](../../tools/distributed-replay/install-distributed-replay-overview.md)|Enumera los temas para instalar la característica Distributed Replay.|  
|[Instalar las herramientas de administración de SQL Server](../../sql-server/install/install-sql-server-management-tools.md)|Describe cómo instalar y configurar las herramientas de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .|  
|[Instalar SQL Server PowerShell](install-sql-server-powershell.md)|Describe las consideraciones para instalar los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] PowerShell.|  
  
## <a name="how-to-install-includesscurrentincludessscurrent-mdmd"></a>Cómo instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]  
  
|Título|Descripción|  
|-----------|-----------------|  
|[Temas de procedimientos de instalación](../../sql-server/install/installation-how-to-topics.md)|Proporciona vínculos a temas de procedimientos para instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] con el Asistente para la instalación, desde el símbolo del sistema, utilizando los archivos de configuración y usando SysPrep.|  
|[Instalación de SQL Server 2014 en Server Core](install-sql-server-on-server-core.md)|Vea este tema para instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en Windows Server Core.|  
|[Validar una instalación de SQL Server](validate-a-sql-server-installation.md)|Revise el uso del informe de SQL Discovery para comprobar la versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] instaladas en el equipo.|  
|[Comprobar los parámetros del Comprobador de configuración del sistema](check-parameters-for-the-system-configuration-checker.md)|Describe la función del Comprobador de la configuración del sistema (SCC).|  
  
## <a name="configuration"></a>Configuración  
  
|Tema|Descripción|  
|-----------|-----------------|  
|[Configure the Windows Firewall to Allow SQL Server Access (Configurar el Firewall de Windows para permitir el acceso a SQL Server)](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|En este tema se proporciona información general de la configuración del firewall y de cómo configurar Firewall de Windows.|  
|[Configurar un equipo de host múltiple para el acceso a SQL Server](../../sql-server/install/configure-a-multi-homed-computer-for-sql-server-access.md)|En este tema se describe cómo configurar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y Firewall de Windows con seguridad avanzada para proporcionar las conexiones de red a una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un entorno de host múltiple.|  
|[Configurar Firewall de Windows para permitir el acceso a Analysis Services](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|Puede seguir los pasos proporcionados en este tema para configurar el puerto y el firewall para permitir el acceso a [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] o a PowerPivot para SharePoint.|  
  
## <a name="related-sections"></a>Secciones relacionadas  
 [Instalar las características de BI de SQL Server 2014](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 Las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que son parte de la plataforma [!INCLUDE[msCoName](../../includes/msconame-md.md)] BI incluyen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] y varias aplicaciones cliente que se usan para crear datos analíticos o para trabajar con ellos. Esta sección de la documentación del programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] explica cómo instalar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)], [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)] y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
 [Instalación de clúster de conmutación por error de SQL Server](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 Esta sección de la documentación del programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] explica cómo instalar y configurar el clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Vea también  
 [Planear una instalación de SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)   
 [Actualización a SQL Server 2014](upgrade-sql-server.md)   
 [Desinstalar SQL Server 2014](../../sql-server/install/uninstall-sql-server.md)   
 [Soluciones de alta disponibilidad &#40;SQL Server&#41;](../../sql-server/failover-clusters/high-availability-solutions-sql-server.md)  
  
  
