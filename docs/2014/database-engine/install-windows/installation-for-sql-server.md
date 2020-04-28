---
title: Instalación de SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 09/09/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
f1_keywords:
- sql12.portal.Installation.f1
helpviewer_keywords:
- installing SQL Server, initial installation
- installation [SQL Server]
- initial installation [SQL Server]
ms.assetid: edd75f68-dc62-4479-a596-57ce8ad632e5
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 96afef098b711c65e1bcb46d5f687c95061f2c94
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "75228412"
---
# <a name="installation-for-sql-server-2014"></a>Instalación de SQL Server 2014
 ## <a name="download-sql-server-2014-express"></a>[Descargar SQL Server 2014 Express](http://www.hanselman.com/blog/DownloadSQLServerExpress.aspx)
  **Gracias a [Scott Hanselman](http://www.hanselman.com/) por recopilar todos los vínculos de paquete del instalador en un solo lugar.**
  
  El Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] proporciona un único árbol de características para instalar todos los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] :  
  
-   [!INCLUDE[ssDE](../../includes/ssde-md.md)]  
  
-   [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]  
  
-   [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
-   [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]  
  
-   [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]  
  
-   [!INCLUDE[ssDQSnoversion](../../includes/ssdqsnoversion-md.md)]  
  
-   Herramientas de administración  
  
-   Componentes de conectividad  
  
 Puede instalar cada componente individualmente o seleccionar una combinación de los componentes enumerados anteriormente. Para elegir la mejor opción entre las ediciones y los componentes disponibles [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]en, consulte [ediciones y componentes de SQL Server 2014](../../sql-server/editions-and-components-of-sql-server-2016.md) y [características compatibles con las ediciones de SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md). [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] está disponible en las ediciones de 32 bits y de 64 bits.
 
 **Pruébelo:**  
  
-   ¿Tiene una cuenta de Azure?  Después, vaya **[aquí](https://ms.portal.azure.com/?flight=1#create/Microsoft.SQLServer2016RTMEnterpriseWindowsServer2012R2)** para poner en marcha una máquina Virtual con SQL Server 2014 Service Pack 1 (SP1) ya instalado. Para obtener más información sobre SQL Server 2014 (SP1), consulte la información sobre la [versión de SQL Server 2014 Service Pack 1](https://support.microsoft.com/kb/3058865).  
  
## <a name="in-this-section"></a>En esta sección  
 Independientemente de si utiliza el Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el símbolo del sistema para instalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], el programa de instalación incluirá los siguientes pasos:  
  
 [Planear una instalación de SQL Server](../../sql-server/install/planning-a-sql-server-installation.md)  
 Describe cómo preparar el equipo para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Requisitos de hardware y software  
  
-   Requisitos del Comprobador de configuración del sistema y problemas de bloqueo.  
  
-   Consideraciones relativas a la seguridad  
  
 [Instalar SQL Server 2014](install-sql-server.md)  
 Describe las opciones de instalación para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Actualizar a SQL Server 2014](upgrade-sql-server.md)  
 Describe las opciones para actualizar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Desinstalar SQL Server 2014](../../sql-server/install/uninstall-sql-server.md)  
 Describe los procedimientos para desinstalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
 [Instalación de clúster de conmutación por error de SQL Server](../../sql-server/failover-clusters/install/sql-server-failover-cluster-installation.md)  
 Esta sección de la documentación del programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] explica cómo instalar y configurar el clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 [Instalar las características de SQL Server 2014 BI](../../sql-server/install/install-sql-server-business-intelligence-features.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] características que son parte de la plataforma Microsoft BI incluyen [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]y varias aplicaciones cliente que se usan para crear datos analíticos o para trabajar con ellos. Esta sección de la documentación del programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] explica cómo instalar [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] y [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)].  
  
## <a name="related-sections"></a>Secciones relacionadas  
 [Temas de procedimientos de instalación](../../sql-server/install/installation-how-to-topics.md)  
 Proporciona vínculos a temas de procedimientos para instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] con el Asistente para la instalación, desde el símbolo del sistema, utilizando los archivos de configuración y usando SysPrep.  
  
 [Instalar características de SQL Server BI con SharePoint &#40;PowerPivot y Reporting Services&#41;](../../sql-server/install/install-sql-server-bi-features-sharepoint-powerpivot-reporting-services.md)  
 En esta sección se explica cómo instalar las características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en un entorno de SharePoint. Identifica qué características de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] están disponibles para una versión y edición concreta de SharePoint. También incluye los procedimientos de instalación de PowerPivot para SharePoint y Reporting Services en modo de SharePoint.  
  
 [Instalación de los ejemplos y las bases de datos de ejemplo de SQL Server](https://sqlserversamples.codeplex.com/)  
 Describe cómo instalar y configurar ejemplos y bases de datos de ejemplo de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="see-also"></a>Consulte también  
 [Novedades de SQL Server instalación](../../sql-server/install/what-s-new-in-sql-server-installation.md)   
 [Requisitos de hardware y software para instalar SQL Server 2014](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)  
  
