---
title: Introducción a SQL Server Management Studio para Business Intelligence | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: ab38a4465ec03415f9c1d903419ccbe2b07e6a86
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52808477"
---
# <a name="introduction-to-sql-server-management-studio-for-business-intelligence"></a>Introducción a SQL Server Management Studio para Business Intelligence
  Para obtener acceso, configurar y administrar [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] y [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)], utilice [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. Aunque las tres tecnologías de Business Intelligence se basan en [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], las tareas administrativas asociadas a cada una de ellas son ligeramente diferentes.  
  
> [!NOTE]  
>  Para crear y modificar soluciones de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)]e [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] , utilice [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], no [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)]. [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)] es un entorno de desarrollo basado en [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[vsprvs](../includes/vsprvs-md.md)].  
  
## <a name="managing-analysis-services-solutions-using-sql-server-management-studio"></a>Administrar las soluciones de Analysis Services con SQL Server Management Studio  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] permite administrar los objetos de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] , por ejemplo, realizar copias de seguridad y procesar los objetos.  
  
 [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] proporciona un proyecto de Script de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] en el que se desarrollan y guardan los scripts escritos en expresiones multidimensionales (MDX), Extensiones de minería de Datos (DMX) y XML for Analysis (XMLA). Los proyectos de Scripts de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] se usan para realizar tareas de administración o para volver a crear objetos, como bases de datos y cubos, en instancias de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] . Por ejemplo, puede desarrollar un script XMLA en un proyecto de Script de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] que cree directamente los objetos nuevos en una instancia de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] existente. Los proyectos de Scripts de [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] se pueden guardar como parte de una solución e integrarlos con un control de código fuente.  
  
 Para obtener más información sobre cómo usar [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)], consulte [proyecto de Scripts de Analysis Services en SQL Server Management Studio](../analysis-services/instances/analysis-services-scripts-project-in-sql-server-management-studio.md).  
  
## <a name="managing-integration-services-solutions-using-sql-server-management-studio"></a>Administrar las soluciones de Integration Services con SQL Server Management Studio  
 [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] permite usar el servicio [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para administrar paquetes y supervisar los paquetes en ejecución. Además, se puede utilizar [!INCLUDE[ssManStudio](../includes/ssmanstudio-md.md)] para organizar los paquetes en carpetas; ejecutar, importar y exportar paquetes; migrar los paquetes de Servicios de transformación de datos (DTS); y actualizar los paquetes de [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] .  
  
## <a name="managing-reporting-services-projects-using-sql-server-management-studio"></a>Administrar proyectos de Reporting Services con SQL Server Management Studio  
 Utilice SQL Server Management Studio para habilitar las características de Reporting Services y administrar el servidor, las bases de datos, los roles y los trabajos.  
  
 Las programaciones compartidas se administran con la carpeta Programaciones compartidas y las bases de datos del servidor de informes (ReportServer, ReportServerTempdb) también se administran. También se crea un rol RSExecRole en la base de datos del sistema maestra cuando se mueve una base de datos del servidor de informes a un motor de base de datos de SQL Server nuevo o diferente ([!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../includes/ssde-md.md)]). Para obtener más información sobre estas tareas, vea los temas siguientes:  
  
-   [Reporting Services en SQL Server Management Studio &#40;SSRS&#41;](../reporting-services/tools/reporting-services-in-sql-server-management-studio-ssrs.md)  
  
-   [Administrar una base de datos del servidor de informes &#40;modo nativo de SSRS&#41;](../reporting-services/report-server/report-server-database-ssrs-native-mode.md)  
  
-   [Creación de RSExecRole](../reporting-services/security/create-the-rsexecrole.md)  
  
 También administra el servidor habilitando y configurando diversas características, estableciendo los servidores predeterminados y administrando los roles y los trabajos. Para obtener más información sobre estas tareas, vea los temas siguientes:  
  
-   [Establecer las propiedades del servidor de informes &#40;Management Studio&#41;](../reporting-services/tools/set-report-server-properties-management-studio.md)  
  
-   [Crear, eliminar o modificar un rol &#40;Management Studio&#41;](../reporting-services/security/role-definitions-create-delete-or-modify.md)  
  
-   [Habilitar y deshabilitar la impresión del lado cliente para Reporting Services](../reporting-services/report-server/enable-and-disable-client-side-printing-for-reporting-services.md)  
  
## <a name="see-also"></a>Vea también  
 [Crear modelos multidimensionales utilizando las herramientas de datos de SQL Server &#40;SSDT&#41;](../analysis-services/multidimensional-models/creating-multidimensional-models-using-sql-server-data-tools-ssdt.md)   
 [Reporting Services en SQL Server Data Tools &#40;SSDT&#41;](../reporting-services/tools/reporting-services-in-sql-server-data-tools-ssdt.md)  
  
  
