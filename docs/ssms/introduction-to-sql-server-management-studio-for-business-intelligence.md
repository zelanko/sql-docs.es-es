---
title: Introducción a SQL Server Management Studio para BI | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Management Studio for Integration Services
- SQL Server Management Studio for Reporting Services
- SQL Server Management Studio for Analysis Services
ms.assetid: ffaa77b7-03d0-4d7a-aa42-c5091a4f2ceb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4f3ec990e48b6d9913db9e610fee6bfca6b9190a
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/15/2018
ms.locfileid: "51701371"
---
# <a name="introduction-to-sql-server-management-studio-for-business-intelligence"></a>Introducción a SQL Server Management Studio para Business Intelligence
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
Para obtener acceso, configurar y administrar [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)], [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] y [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], utilice [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Aunque las tres tecnologías de Business Intelligence se basan en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], las tareas administrativas asociadas a cada una de ellas son ligeramente diferentes.  
  
> [!NOTE]  
> Para crear y modificar soluciones de [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]e [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , utilice [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull_md.md)], no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull_md.md)] es un entorno de desarrollo basado en [!INCLUDE[msCoName](../includes/msconame_md.md)][!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
## <a name="managing-analysis-services-solutions-using-sql-server-management-studio"></a>Administrar las soluciones de Analysis Services con SQL Server Management Studio  
[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] permite administrar los objetos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] , por ejemplo, realizar copias de seguridad y procesar los objetos.  
  
[!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] proporciona un proyecto de Script de [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] en el que se desarrollan y guardan los scripts escritos en expresiones multidimensionales (MDX), Extensiones de minería de Datos (DMX) y XML for Analysis (XMLA). Los proyectos de Scripts de [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] se usan para realizar tareas de administración o para volver a crear objetos, como bases de datos y cubos, en instancias de [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] . Por ejemplo, puede desarrollar un script XMLA en un proyecto de Script de [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] que cree directamente los objetos nuevos en una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] existente. Los proyectos de Scripts de [!INCLUDE[ssASnoversion](../includes/ssasnoversion_md.md)] se pueden guardar como parte de una solución e integrarlos con un control de código fuente.  
  
Para más información sobre cómo usar [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], consulte [Desarrollar e implementar usando SQL Server Management Studio](../analysis-services/instances/analysis-services-scripts-project-in-sql-server-management-studio.md).  
  
## <a name="managing-integration-services-solutions-using-sql-server-management-studio"></a>Administrar las soluciones de Integration Services con SQL Server Management Studio  
[!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] permite usar el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para administrar paquetes y supervisar los paquetes en ejecución. Además, se puede utilizar [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] para organizar los paquetes en carpetas; ejecutar, importar y exportar paquetes; migrar los paquetes de Servicios de transformación de datos (DTS); y actualizar los paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
## <a name="managing-reporting-services-projects-using-sql-server-management-studio"></a>Administrar proyectos de Reporting Services con SQL Server Management Studio  
Utilice SQL Server Management Studio para habilitar las características de Reporting Services y administrar el servidor, las bases de datos, los roles y los trabajos.  
  
Las programaciones compartidas se administran con la carpeta Programaciones compartidas y las bases de datos del servidor de informes (ReportServer, ReportServerTempdb) también se administran. También se crea un rol RSExecRole en la base de datos del sistema maestra cuando se mueve una base de datos del servidor de informes a un motor de base de datos de SQL Server nuevo o diferente ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde_md.md)]). Para obtener más información sobre estas tareas, vea los temas siguientes:  
  
-   [Temas de procedimientos de Management Studio](https://msdn.microsoft.com/60685458-9108-47bf-820a-5e7db454d408)  
  
-   [Administrar una base de datos del servidor de informes](../reporting-services/report-server/administer-a-report-server-database-ssrs-native-mode.md)  
  
-   [Cómo crear RSExecRole](../reporting-services/security/create-the-rsexecrole.md)  
  
También administra el servidor habilitando y configurando diversas características, estableciendo los servidores predeterminados y administrando los roles y los trabajos. Para obtener más información sobre estas tareas, vea los temas siguientes:  
  
-   [Cómo establecer las propiedades del servidor de informes (Management Studio)](https://msdn.microsoft.com/1ed0f84b-b12a-4e49-b65c-a11a99f9093f)  
  
-   [Cómo crear, eliminar o modificar un rol (Management Studio)](https://msdn.microsoft.com/3d1d56e6-a283-44a7-8417-36cb4d2c74d1)  
  
-   [Habilitar y deshabilitar la impresión del lado cliente para Reporting Services](https://msdn.microsoft.com/0e709c96-7517-4547-8ef6-5632f8118524)  
  
## <a name="see-also"></a>Ver también  
[Desarrollar e implementar usando SQL Server Data Tools](../analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)  
[Reporting Services en SQL Server Data Tools](../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md)  
  
