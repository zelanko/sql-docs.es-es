---
title: Operaciones de copia de seguridad y restauración de Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- databases [Reporting Services], backing up
- databases [Reporting Services], restoring
- databases [Reporting Services], moving
- backing up databases [Reporting Services]
- moving databases
- restoring databases [Reporting Services]
- files [Reporting Services], restoring
- files [Reporting Services], backing up
ms.assetid: 157bc376-ab72-4c99-8bde-7b12db70843a
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 573ea25fdbb617f079fb71c08057294c5568d95c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48092495"
---
# <a name="backup-and-restore-operations-for-reporting-services"></a>Operaciones de copia de seguridad y restauración de Reporting Services
  En este tema se ofrece información general acerca de todos los archivos de datos que se usan en una instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y se describe cuándo y cómo se debe realizar una copia de seguridad de los mismos. La parte más importante de una estrategia de recuperación es desarrollar un plan de copias de seguridad y restauración de los archivos de base de datos del servidor de informes. Sin embargo, una estrategia de recuperación más completa incluiría copias de seguridad de las claves de cifrado, extensiones o ensamblados personalizados, archivos de configuración y archivos de origen para informes y modelos.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  Modo nativo de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] | Modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]  
  
 A menudo se usan operaciones de copias de seguridad y restauración para mover la totalidad o una parte de la instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
-   Si se van a mover únicamente las bases de datos del servidor de informes, se pueden usar las operaciones de copias de seguridad y restauración, o de adjuntar y separar, para reubicar las bases de datos en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diferente. Para más información, vea [Moving the Report Server Databases to Another Computer &#40;SSRS Native Mode&#41;](../report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md).  
  
-   El traspaso de una instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a otro equipo se conoce como migración. Cuando se migra una instalación, se ejecuta el programa de instalación para instalar una nueva instancia del servidor de informes y luego copiar datos de instancia al nuevo equipo. Para obtener más información sobre la migración de una instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , vea los temas siguientes:  
  
    -   [Actualizar y migrar Reporting Services](upgrade-and-migrate-reporting-services.md)  
  
    -   [Migrar una instalación de Reporting Services &#40;el modo de SharePoint&#41;](migrate-a-reporting-services-installation-sharepoint-mode.md)  
  
    -   [Migrar una instalación de Reporting Services &#40;modo nativo&#41;](migrate-a-reporting-services-installation-native-mode.md)  
  
## <a name="backing-up-the-report-server-databases"></a>Realizar copias de seguridad de bases de datos del servidor de informes  
 Puesto que un servidor de informes es un servidor sin estado, todos los datos de aplicación se almacenan en las bases de datos **reportserver** y **reportservertempdb** que se ejecutan en una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . Para realizar una copia de seguridad de las bases de datos **reportserver** y **reportservertempdb** , use uno de los métodos admitidos para copias de seguridad de bases de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Éstas son algunas de las recomendaciones específicas de las bases de datos del servidor de informes:  
  
-   Utilice el modelo de recuperación completa para realizar la copia de seguridad de la base de datos **reportserver** .  
  
-   Utilice el modelo de recuperación simple para la copia de seguridad de la base de datos **reportservertempdb** .  
  
-   Puede utilizar distintas programaciones de copia de seguridad para cada base de datos. La copia de seguridad de **reportservertempdb** se realiza únicamente para evitar tener que volver a crearla en caso de un error de hardware. Si se produce un error de hardware, no es necesario recuperar los datos de **reportservertempdb**, pero sí se requiere la estructura de la tabla. Si se pierde **reportservertempdb**, la única forma de recuperarla es volver a crear la base de datos del servidor de informes. Si se vuelve a crear **reportservertempdb**, es importante que su nombre sea el mismo que el de la base de datos primaria del servidor de informes.  
  
 Para obtener más información sobre la copia de seguridad y la recuperación de bases de datos relacionales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vea [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
> [!IMPORTANT]  
>  Si el servidor de informes de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] está en modo de SharePoint, hay que tener en cuenta otras bases de datos adicionales, incluidas las bases de datos de configuración de SharePoint y la base de datos de alertas de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . En el modo de SharePoint, se crean tres bases de datos para cada aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Las bases de datos **reportserver**, **reportservertempdb**y **dataalerting** . Para obtener más información, consulte [copia de seguridad y restauración de Reporting Services SharePoint aplicaciones de servicio](../backup-and-restore-reporting-services-sharepoint-service-applications.md)  
  
## <a name="backing-up-the-encryption-keys"></a>Realizar copias de seguridad de claves de cifrado  
 La primera vez que se configura una instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , se recomienda realizar una copia de seguridad de las claves de cifrado. Asimismo, se debería realizar una copia de seguridad de las claves siempre que se cambie la identidad de las cuentas de servicio o se cambie el nombre del equipo. Para obtener más información, vea [Hacer copia de seguridad y restaurar claves de cifrado de Reporting Services](ssrs-encryption-keys-back-up-and-restore-encryption-keys.md). Para servidores de informes de modo de SharePoint, vea la sección "Administración de claves" de [administrar una aplicación de servicio de Reporting Services SharePoint](../manage-a-reporting-services-sharepoint-service-application.md).  
  
## <a name="backing-up-the-configuration-files"></a>Realizar copias de seguridad de archivos de configuración  
 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] usa archivos de configuración para almacenar la configuración de aplicación. Debe realizarse una copia de seguridad de estos archivos la primera vez que se configura el servidor y después de que se implementen extensiones personalizadas. Debe realizar una copia de seguridad de los siguientes archivos:  
  
-   Rsreportserver.config  
  
-   Rssvrpolicy.config  
  
-   Rsmgrpolicy.config  
  
-   Reportingservicesservice.exe.config  
  
-   Web.config para aplicaciones [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] del Servidor de informes y del Administrador de informes.  
  
-   Machine.config de [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]  
  
## <a name="backing-up-data-files"></a>Realizar una copia de seguridad de archivos de datos  
 Realice una copia de seguridad de los archivos que cree y mantenga en el Diseñador de informes y en el Diseñador de modelos. Estos archivos incluyen archivos de definición de informe (.rdl), de modelo de informe (.smdl), de orígenes de datos compartidos (.rds), de vista de datos (.dv), de origen de datos (.ds), de proyecto de servidor de informes (.rptproj) y de solución de informes (.sln).  
  
 No olvide realizar una copia de seguridad de los archivos de script (.rss) que haya creado para las tareas de administración o implementación.  
  
 Compruebe que dispone de una copia de seguridad de las extensiones personalizadas y de los ensamblados personalizados que utilice.  
  
## <a name="see-also"></a>Vea también  
 [Base de datos del servidor de informes &#40;modo nativo de SSRS&#41;](../report-server/report-server-database-ssrs-native-mode.md)   
 [Archivos de configuración de Reporting Services](../report-server/reporting-services-configuration-files.md)   
 [Utilidad RSKeyMgmt &#40;SSRS&#41;](../tools/rskeymgmt-utility-ssrs.md)   
 [Copiar bases de datos con Copias de seguridad y restauración](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)   
 [Administrar una base de datos del servidor de informes &#40;Modo nativo de SSRS&#41;](../report-server/administer-a-report-server-database-ssrs-native-mode.md)   
 [Configurar y administrar las claves de cifrado &#40;Administrador de configuración de SSRS&#41;](ssrs-encryption-keys-manage-encryption-keys.md)  
  
  
