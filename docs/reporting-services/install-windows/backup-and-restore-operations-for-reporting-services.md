---
title: Copia de seguridad y restaurar las operaciones para Reporting Services | Documentos de Microsoft
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
- reporting-services-sharepoint
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 43
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: e3247864547983779f4037eb963ba6721a2b7654
ms.contentlocale: es-es
ms.lasthandoff: 08/09/2017

---

# <a name="backup-and-restore-operations-for-reporting-services"></a>Operaciones de copia de seguridad y restauración de Reporting Services

  En este tema se ofrece información general acerca de todos los archivos de datos que se usan en una instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] y se describe cuándo y cómo se debe realizar una copia de seguridad de los mismos. La parte más importante de una estrategia de recuperación es desarrollar un plan de copias de seguridad y restauración de los archivos de base de datos del servidor de informes. Sin embargo, una estrategia de recuperación más completa incluiría copias de seguridad de las claves de cifrado, extensiones o ensamblados personalizados, archivos de configuración y archivos de origen para informes y modelos.  
  
 **[!INCLUDE[applies](../../includes/applies-md.md)]**  [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] | Modo de SharePoint de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]   
  
 A menudo se usan operaciones de copias de seguridad y restauración para mover la totalidad o una parte de la instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
-   Si se van a mover únicamente las bases de datos del servidor de informes, se pueden usar las operaciones de copias de seguridad y restauración, o de adjuntar y separar, para reubicar las bases de datos en una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diferente. Para obtener más información, vea [Mover las bases de datos del servidor de informes a otro equipo &#40;Modo nativo de SSRS&#41;](../../reporting-services/report-server/moving-the-report-server-databases-to-another-computer-ssrs-native-mode.md).  
  
-   El traspaso de una instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] a otro equipo se conoce como migración. Cuando se migra una instalación, se ejecuta el programa de instalación para instalar una nueva instancia del servidor de informes y luego copiar datos de instancia al nuevo equipo. Para obtener más información sobre la migración de una instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , vea los temas siguientes:  
  
    -   [Actualizar y migrar Reporting Services](../../reporting-services/install-windows/upgrade-and-migrate-reporting-services.md)  
  
    -   [Migrar una instalación de Reporting Services &#40;modo de SharePoint&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-sharepoint-mode.md)  
  
    -   [Migrar una instalación de Reporting Services &#40;modo nativo&#41;](../../reporting-services/install-windows/migrate-a-reporting-services-installation-native-mode.md)  
  
## <a name="backing-up-the-report-server-databases"></a>Realizar copias de seguridad de bases de datos del servidor de informes  
 Puesto que un servidor de informes es un servidor sin estado, todos los datos de aplicación se almacenan en las bases de datos **reportserver** y **reportservertempdb** que se ejecutan en una instancia del [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] . Para realizar una copia de seguridad de las bases de datos **reportserver** y **reportservertempdb** , use uno de los métodos admitidos para copias de seguridad de bases de datos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Éstas son algunas de las recomendaciones específicas de las bases de datos del servidor de informes:  
  
-   Utilice el modelo de recuperación completa para realizar la copia de seguridad de la base de datos **reportserver** .  
  
-   Utilice el modelo de recuperación simple para la copia de seguridad de la base de datos **reportservertempdb** .  
  
-   Puede utilizar distintas programaciones de copia de seguridad para cada base de datos. La copia de seguridad de **reportservertempdb** se realiza únicamente para evitar tener que volver a crearla en caso de un error de hardware. Si se produce un error de hardware, no es necesario recuperar los datos de **reportservertempdb**, pero sí se requiere la estructura de la tabla. Si se pierde **reportservertempdb**, la única forma de recuperarla es volver a crear la base de datos del servidor de informes. Si se vuelve a crear **reportservertempdb**, es importante que su nombre sea el mismo que el de la base de datos primaria del servidor de informes.  
  
 Para obtener más información sobre la copia de seguridad y la recuperación de bases de datos relacionales de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vea [Realizar copias de seguridad y restaurar bases de datos de SQL Server](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md).  
  
> [!IMPORTANT]  
>  Si el servidor de informes está en modo de SharePoint, hay bases de datos adicionales que preocuparte, incluidas las bases de datos de configuración de SharePoint y el [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] base de datos de alertas. En el modo de SharePoint, se crean tres bases de datos para cada aplicación de servicio de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] . Las bases de datos **reportserver**, **reportservertempdb**y **dataalerting** . Para obtener más información, vea [Copias de seguridad y restauración de aplicaciones de servicio de SharePoint para Reporting Services](../../reporting-services/report-server-sharepoint/backup-and-restore-reporting-services-sharepoint-service-applications.md).  
  
## <a name="backing-up-the-encryption-keys"></a>Realizar copias de seguridad de claves de cifrado  
 La primera vez que se configura una instalación de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] , se recomienda realizar una copia de seguridad de las claves de cifrado. Asimismo, se debería realizar una copia de seguridad de las claves siempre que se cambie la identidad de las cuentas de servicio o se cambie el nombre del equipo. Para obtener más información, vea [Hacer copia de seguridad y restaurar claves de cifrado de Reporting Services](../../reporting-services/install-windows/ssrs-encryption-keys-back-up-and-restore-encryption-keys.md). Para servidores de informes en modo de SharePoint, vea la sección "Administración de claves" de [Administrar una aplicación de servicio de SharePoint para Reporting Services](../../reporting-services/report-server-sharepoint/manage-a-reporting-services-sharepoint-service-application.md).  
  
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

## <a name="next-steps"></a>Pasos siguientes

[Base de datos de servidor de informes](../../reporting-services/report-server/report-server-database-ssrs-native-mode.md)   
[Archivos de configuración de Reporting Services](../../reporting-services/report-server/reporting-services-configuration-files.md)   
[RSKEYMGMT (utilidad)](../../reporting-services/tools/rskeymgmt-utility-ssrs.md)   
[Copiar bases de datos con Copias de seguridad y restauración](../../relational-databases/databases/copy-databases-with-backup-and-restore.md)   
[Administrar una base de datos del servidor de informes](../../reporting-services/report-server/administer-a-report-server-database-ssrs-native-mode.md)   
[Configurar y administrar las claves de cifrado](../../reporting-services/install-windows/ssrs-encryption-keys-manage-encryption-keys.md)  

¿Más preguntas? [Pruebe a formular el foro de Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
