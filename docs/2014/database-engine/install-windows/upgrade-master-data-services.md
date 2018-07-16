---
title: Actualizar Master Data Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 9c3543f3-3eb9-455d-a9bf-f17e9506ad21
caps.latest.revision: 23
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ad77c531a5ea83cc5d65b5be17e9cc231f00abe1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2018
ms.locfileid: "37235795"
---
# <a name="upgrade-master-data-services"></a>Actualizar Master Data Services
  Existen cuatro escenarios para actualizarse a Microsoft [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2. Elija el escenario que se corresponde con su situación.  
  
-   [Actualizar sin actualización del motor de base de datos](#noengine)  
  
-   [Actualizar con actualización del motor de base de datos](#engine)  
  
-   [Actualización en un escenario de dos equipos](#twocomputer)  
  
-   [Actualización con restauración de una base de datos desde la copia de seguridad](#restore)  
  
> [!IMPORTANT]  
>  -   No se admite la actualización desde la versión [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP1 a la versión CTP2.  
> -   Realice una copia de la base de datos antes de realizar cualquier actualización.  
> -   El proceso de actualización vuelve a crear los procedimientos almacenados y actualiza las tablas que usa [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]. Cualquier personalización que haya realizado en alguno de estos componentes se podría perder.  
> -   Los paquetes de implementación de modelos solo se pueden usar en la edición de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en la que se crearon. No se puede implementar paquetes de implementación de modelo que creó en [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] / [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
> -   Puede seguir usando el [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] versión SP1 de Master Data Services complemento para Excel después de actualizar Master Data Services y Data Quality Services para [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP2. Sin embargo, las versiones anteriores del complemento de Master Data Services para Excel no funcionarán después de actualizar a SQL Server 2014 CTP2. Puede descargar el [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] versión SP1 de Master Data Services complemento para Excel desde [aquí](http://go.microsoft.com/fwlink/?LinkId=328664).  
  
##  <a name="noengine"></a> Actualizar sin actualización del motor de base de datos  
 Este escenario se puede considerar una instalación en paralelo, porque ambos [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] / [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] y [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] se instalan en paralelo, en el mismo equipo o en equipos independientes.  
  
 En este escenario se sigue usando [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] para hospedar la base de datos de MDS. Sin embargo, debe actualizar el esquema de la base de datos de MDS y, posteriormente, crear una aplicación web de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para tener acceso a la base de datos de MDS. La aplicación web de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ya no puede tener acceso a la base de datos de MDS.  
  
 Si opta por instalar [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y una versión anterior de SQL Server ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]/[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) en el mismo equipo, puede hacerlo porque los archivos se instalan en una ubicación diferente.  
  
-   En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], los archivos se instalan de forma predeterminada en *unidad*:\Archivos de programa\Microsoft SQL Server\120\Master Data Services.  
  
-   En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], los archivos se instalan de forma predeterminada en *unidad*:\Archivos de programa\Microsoft SQL Server\110\Master Data Services.  
  
-   En [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], los archivos se instalan de forma predeterminada en *unidad*:\Archivos de programa\Microsoft SQL Server\Master Data Services.  
  
 Para realizar esta tarea, complete los siguientes pasos.  
  
1.  Instale [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] y cualquier otra característica que desee.  
  
    1.  Abra el Asistente para la instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    2.  En el panel izquierdo, haga clic en **Instalación**.  
  
    3.  En el panel derecho, haga clic en **Nueva instalación independiente de SQL Server o agregar características a una instalación existente**.  
  
    4.  En la página de **Selección de características** , seleccione **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** y cualquier otra característica que desee instalar.  
  
    5.  Finalice el asistente.  
  
2.  Una vez completada la instalación, actualice el esquema de la base de datos de MDS.  
  
    1.  Abra el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] verzi [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
        > [!IMPORTANT]  
        >  Para actualizar el esquema de base de datos de MDS, debe haber iniciado sesión con la cuenta de administrador que se especificó cuando se creó la base de datos de MDS. En la base de datos de MDS, en mdm.tblUser, el usuario tiene el valor de **Id.** establecido en **1**. Para obtener información acerca de cómo cambiar este usuario, consulte [cambiar la cuenta de administrador del sistema &#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md).  
  
    2.  En el panel izquierdo, haga clic en **Configuración de base de datos**.  
  
    3.  En el panel derecho, haga clic en **Seleccionar base de datos** e indique la información de su [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] instancia de base de datos.  
  
    4.  Haga clic en **Actualizar base de datos** para iniciar el **Asistente para actualizar base de datos**. Para más información, vea [Asistente para actualizar base de datos &#40;Administrador de configuración de Master Data Services&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md).  
  
3.  Una vez completada la actualización, cree una aplicación web de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    1.  Abra el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] verzi [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
    2.  En el panel izquierdo, haga clic en **Configuración web**.  
  
    3.  En el panel derecho, en la lista de **Sitio web** , seleccione una de las opciones siguientes:  
  
        -   **Sitio web predeterminado**y, después, haga clic en **Crear aplicación**.  
  
        -   **Crear nuevo sitio**. Se creará automáticamente una aplicación web cuando se cree el sitio web.  
  
        > [!IMPORTANT]  
        >  La aplicación web de MDS existente de una versión anterior de SQL Server ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) se puede seleccionar en la versión de SQL Server versión 2014 del Administrador de configuración de Master Data Services. No debe seleccionar la aplicación web existente y en su lugar debe crear una aplicación web de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para MDS. De lo contrario, al intentar asociar la aplicación web a la base de datos actualizada de MDS recibirá un error que indica que no se puede tener acceso a la página solicitada porque los datos de configuración relacionados para la página no son válidos.  
        >   
        >  Si desea utilizar el mismo nombre (alias) para la aplicación web de MDS que la aplicación web existente ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]), debe eliminar primero la aplicación web y el grupo de aplicaciones asociado de IIS y crear después una aplicación web con el mismo nombre mediante la versión de SQL Server 2014 del Administrador de configuración de Master Data Services. Para obtener más información sobre cómo quitar una aplicación web y grupos de aplicaciones de IIS, vea [Quitar una aplicación (IIS)](http://go.microsoft.com/fwlink/?LinkId=323537) y [Quitar un grupo de aplicaciones (IIS)](http://go.microsoft.com/fwlink/?LinkId=323538).  
  
4.  Asocie ahora la nueva aplicación web a la base de datos de MDS actualizada.  
  
    1.  En la sección **Asociar aplicación a base de datos** , haga clic en **Seleccionar**.  
  
    2.  Seleccione la base de datos de MDS.  
  
    3.  Haga clic en **Aplicar**.  
  
##  <a name="engine"></a> Actualizar con actualización del motor de base de datos  
 En este escenario se actualizará el motor de base de datos y la aplicación de [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o SQL Server 2012 a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
 Para realizar esta tarea, complete los siguientes pasos.  
  
1.  **Solo en el caso de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)]**: abra el **Panel de control** > **Programas y características** y desinstale Microsoft [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)][!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)].  
  
2.  Actualice el motor de base de datos a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    1.  Abra el Asistente para la instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    2.  En el panel izquierdo, haga clic en **Instalación**.  
  
    3.  En el panel derecho, haga clic en **actualizar desde SQL Server 2005, SQL Server 2008, SQL Server 2008 R2 o SQL Server 2012**.  
  
    4.  Finalice el asistente.  
  
3.  **Para [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] sólo**: una vez completada la actualización, agregue el **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** característica.  
  
    1.  Abra el Asistente para la instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    2.  En el panel izquierdo, haga clic en **Instalación**.  
  
    3.  En el panel derecho, haga clic en **Nueva instalación independiente de SQL Server o agregar características a una instalación existente**.  
  
    4.  En el **tipo de instalación** página del asistente, seleccione el **agregar características a una instancia existente** opción y elija la instancia donde está instalada la base de datos MDS.  
  
    5.  En el **selección de características** página, en **características compartidas**, seleccione **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]**.  
  
    6.  Finalice el asistente.  
  
4.  Actualice el esquema de la base de datos de MDS.  
  
    1.  Abra el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] verzi [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
        > [!IMPORTANT]  
        >  Para actualizar el esquema de base de datos de MDS, debe haber iniciado sesión con la cuenta de administrador que se especificó cuando se creó la base de datos de MDS. En la base de datos de MDS, en mdm.tblUser, el usuario tiene el valor de **Id.** establecido en **1**. Para obtener información acerca de cómo cambiar este usuario, consulte [cambiar la cuenta de administrador del sistema &#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md).  
  
    2.  En el panel izquierdo, haga clic en **Configuración de base de datos**.  
  
    3.  En el panel derecho, haga clic en **Seleccionar base de datos** e indique la información de la instancia de base de datos.  
  
    4.  Haga clic en **Actualizar base de datos** para iniciar el **Asistente para actualizar base de datos**. Para más información, vea [Asistente para actualizar base de datos &#40;Administrador de configuración de Master Data Services&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md).  
  
    5.  Haga clic en **Aplicar**.  
  
5.  Una vez completada la actualización, cree una aplicación web de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    1.  Abra el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] verzi [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
    2.  En el panel izquierdo, haga clic en **Configuración web**.  
  
    3.  En el panel derecho, en la lista de **Sitio web** , seleccione una de las opciones siguientes:  
  
        -   **Sitio web predeterminado**y, después, haga clic en **Crear aplicación**.  
  
        -   **Crear nuevo sitio**. Se creará automáticamente una aplicación web cuando se cree el sitio web.  
  
        > [!IMPORTANT]  
        >  La aplicación web de MDS existente de una versión anterior de SQL Server ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) se puede seleccionar en la versión de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] del Administrador de configuración de Master Data Services. No debe seleccionar la aplicación web existente y en su lugar debe crear una aplicación web de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para MDS. De lo contrario, al intentar asociar la aplicación web a la base de datos actualizada de MDS recibirá un error que indica que no se puede tener acceso a la página solicitada porque los datos de configuración relacionados para la página no son válidos.  
        >   
        >  Si desea utilizar el mismo nombre (alias) para la aplicación web de MDS que la aplicación web existente ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]), debe eliminar primero la aplicación web y el grupo de aplicaciones asociado de IIS y crear después una aplicación web con el mismo nombre mediante la versión de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] del Administrador de configuración de Master Data Services. Para obtener más información sobre cómo quitar una aplicación web y grupos de aplicaciones de IIS, vea [Quitar una aplicación (IIS)](http://go.microsoft.com/fwlink/?LinkId=323537) y [Quitar un grupo de aplicaciones (IIS)](http://go.microsoft.com/fwlink/?LinkId=323538).  
  
6.  Asocie ahora la nueva aplicación web a la base de datos de MDS actualizada.  
  
    1.  En la sección **Asociar aplicación a base de datos** , haga clic en **Seleccionar**.  
  
    2.  Seleccione la base de datos de MDS.  
  
    3.  Haga clic en **Aplicar**.  
  
##  <a name="twocomputer"></a> Actualización en un escenario de dos equipos  
 Este escenario conlleva la actualización de un sistema en el que SQL Server está instalado en dos equipos: uno con [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] y otro con SQL Server 2008 R2 o SQL Server 2012.  
  
 Si está instalado [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], continúe usando [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], respectivamente, para hospedar la base de datos MDS en un equipo. Sin embargo, debe actualizar el esquema de la base de datos de MDS y, posteriormente, usar la aplicación web [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para tener acceso a la base de datos de MDS. La aplicación web de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] ya no puede tener acceso a la base de datos de MDS.  
  
-   En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], los archivos se instalan de forma predeterminada en *unidad*:\Archivos de programa\Microsoft SQL Server\120\Master Data Services.  
  
-   En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], los archivos se instalan de forma predeterminada en *unidad*:\Archivos de programa\Microsoft SQL Server\110\Master Data Services.  
  
-   En [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], los archivos se instalan de forma predeterminada en *unidad*:\Archivos de programa\Microsoft SQL Server\Master Data Services.  
  
 Para realizar esta tarea, complete los siguientes pasos.  
  
1.  Instale [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] y cualquier otra característica que desee.  
  
    1.  Abra el Asistente para la instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    2.  En el panel izquierdo, haga clic en **Instalación**.  
  
    3.  En el panel derecho, haga clic en **Nueva instalación independiente de SQL Server o agregar características a una instalación existente**.  
  
    4.  En la página de **Selección de características** , seleccione **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** y cualquier otra característica que desee instalar.  
  
    5.  Finalice el asistente.  
  
2.  Una vez completada la instalación, actualice el esquema de la base de datos de MDS.  
  
    1.  Abra el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] verzi [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
        > [!IMPORTANT]  
        >  Para actualizar el esquema de base de datos de MDS, debe haber iniciado sesión con la cuenta de administrador que se especificó cuando se creó la base de datos de MDS. En la base de datos de MDS, en mdm.tblUser, el usuario tiene el valor de **Id.** establecido en **1**. Para obtener información acerca de cómo cambiar este usuario, consulte [cambiar la cuenta de administrador del sistema &#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md).  
  
    2.  En el panel izquierdo, haga clic en **Configuración de base de datos**.  
  
    3.  En el panel derecho, haga clic en **Seleccionar base de datos** e indique la información de su [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] instancia en el otro equipo, la base de datos si [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] está instalado en el otro equipo.  
  
    4.  Haga clic en **Actualizar base de datos** para iniciar el **Asistente para actualizar base de datos**. Para más información, vea [Asistente para actualizar base de datos &#40;Administrador de configuración de Master Data Services&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md).  
  
3.  Una vez completada la actualización, cree una aplicación web de SQL Server 2014.  
  
    1.  Abra el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] verzi [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
    2.  En el panel izquierdo, haga clic en **Configuración web**.  
  
    3.  En el panel derecho, en la lista de **Sitio web** , seleccione una de las opciones siguientes:  
  
        -   **Sitio web predeterminado**y, después, haga clic en **Crear aplicación**.  
  
        -   **Crear nuevo sitio**. Se creará automáticamente una aplicación web cuando se cree el sitio web.  
  
        > [!IMPORTANT]  
        >  La aplicación web de MDS existente de una versión anterior de SQL Server ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) se puede seleccionar en la versión de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] del Administrador de configuración de Master Data Services. No debe seleccionar la aplicación web existente y en su lugar debe crear una aplicación web de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para MDS. De lo contrario, al intentar asociar la aplicación web a la base de datos actualizada de MDS recibirá un error que indica que no se puede tener acceso a la página solicitada porque los datos de configuración relacionados para la página no son válidos.  
        >   
        >  Si desea utilizar el mismo nombre (alias) para la aplicación web de MDS que la aplicación web existente ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]), debe eliminar primero la aplicación web y el grupo de aplicaciones asociado de IIS y crear después una aplicación web con el mismo nombre mediante la versión de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] del Administrador de configuración de Master Data Services. Para obtener más información sobre cómo quitar una aplicación web y grupos de aplicaciones de IIS, vea [Quitar una aplicación (IIS)](http://go.microsoft.com/fwlink/?LinkId=323537) y [Quitar un grupo de aplicaciones (IIS)](http://go.microsoft.com/fwlink/?LinkId=323538).  
  
4.  Asocie ahora la aplicación web a una base de datos de MDS actualizada.  
  
    1.  En la sección **Asociar aplicación a base de datos** , haga clic en **Seleccionar**.  
  
    2.  Seleccione la base de datos de MDS.  
  
    3.  Haga clic en **Aplicar**.  
  
##  <a name="restore"></a> Actualización con restauración de una base de datos desde la copia de seguridad  
 En este escenario, [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] está instalado junto con SQL Server 2008 R2 o SQL Server 2012 en el mismo equipo o en dos equipos diferentes. También se realizó una copia de seguridad de una base de datos en una versión anterior a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] CTP, antes de la actualización, y hay que restaurar la base de datos.  
  
-   En [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], los archivos se instalan de forma predeterminada en *unidad*:\Archivos de programa\Microsoft SQL Server\120\Master Data Services.  
  
-   En [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], los archivos se instalan de forma predeterminada en *unidad*:\Archivos de programa\Microsoft SQL Server\110\Master Data Services.  
  
-   En [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], los archivos se instalan de forma predeterminada en *unidad*:\Archivos de programa\Microsoft SQL Server\Master Data Services.  
  
 Para realizar esta tarea, complete los siguientes pasos.  
  
1.  Instale [!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)] y cualquier otra característica que desee.  
  
    1.  Abra el Asistente para la instalación de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    2.  En el panel izquierdo, haga clic en **Instalación**.  
  
    3.  En el panel derecho, haga clic en **Nueva instalación independiente de SQL Server o agregar características a una instalación existente**.  
  
    4.  En la página de **Selección de características** , seleccione **[!INCLUDE[ssMDSshort](../../includes/ssmdsshort-md.md)]** y cualquier otra característica que desee instalar.  
  
    5.  Finalice el asistente.  
  
2.  Restaure la base de datos de la que se realizó la copia de seguridad.  
  
3.  Una vez completada la instalación, actualice el esquema de la base de datos de MDS.  
  
    1.  Abra el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] verzi [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
        > [!IMPORTANT]  
        >  Para actualizar el esquema de base de datos de MDS, debe haber iniciado sesión con la cuenta de administrador que se especificó cuando se creó la base de datos de MDS. En la base de datos de MDS, en mdm.tblUser, el usuario tiene el valor de **Id.** establecido en **1**. Para obtener información acerca de cómo cambiar este usuario, consulte [cambiar la cuenta de administrador del sistema &#40;Master Data Services&#41;](../../master-data-services/change-the-system-administrator-account-master-data-services.md).  
  
    2.  En el panel izquierdo, haga clic en **Configuración de base de datos**.  
  
    3.  En el panel derecho, haga clic en **Seleccionar base de datos** e indique la información de su [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] instancia de base de datos.  
  
    4.  Haga clic en **Actualizar base de datos** para iniciar el **Asistente para actualizar base de datos**. Para más información, vea [Asistente para actualizar base de datos &#40;Administrador de configuración de Master Data Services&#41;](../../master-data-services/upgrade-database-wizard-master-data-services-configuration-manager.md).  
  
4.  Una vez completada la actualización, cree una aplicación web de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)].  
  
    1.  Abra el [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] verzi [!INCLUDE[ssMDScfgmgr](../../includes/ssmdscfgmgr-md.md)].  
  
    2.  En el panel izquierdo, haga clic en **Configuración web**.  
  
    3.  En el panel derecho, en la lista de **Sitio web** , seleccione una de las opciones siguientes:  
  
        -   **Sitio web predeterminado**y, después, haga clic en **Crear aplicación**.  
  
        -   **Crear nuevo sitio**. Se creará automáticamente una aplicación web cuando se cree el sitio web.  
  
        > [!IMPORTANT]  
        >  La aplicación web de MDS existente de una versión anterior de SQL Server ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]) se puede seleccionar en la versión de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] del Administrador de configuración de Master Data Services. No debe seleccionar la aplicación web existente y en su lugar debe crear una aplicación web de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] para MDS. De lo contrario, al intentar asociar la aplicación web a la base de datos actualizada de MDS recibirá un error que indica que no se puede tener acceso a la página solicitada porque los datos de configuración relacionados para la página no son válidos.  
        >   
        >  Si desea utilizar el mismo nombre (alias) para la aplicación web de MDS que la aplicación web existente ([!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)]), debe eliminar primero la aplicación web y el grupo de aplicaciones asociado de IIS y crear después una aplicación web con el mismo nombre mediante la versión de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] del Administrador de configuración de Master Data Services. Para obtener más información sobre cómo quitar una aplicación web y grupos de aplicaciones de IIS, vea [Quitar una aplicación (IIS)](http://go.microsoft.com/fwlink/?LinkId=323537) y [Quitar un grupo de aplicaciones (IIS)](http://go.microsoft.com/fwlink/?LinkId=323538).  
  
5.  Asocie ahora la nueva aplicación web a la base de datos de MDS actualizada.  
  
    1.  En la sección **Asociar aplicación a base de datos** , haga clic en **Seleccionar**.  
  
    2.  Seleccione la base de datos de MDS.  
  
    3.  Haga clic en **Aplicar**.  
  
## <a name="troubleshooting"></a>Solucionar problemas  
 **Problema:** al abrir el [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] [!INCLUDE[ssMDSmdm](../../includes/ssmdsmdm-md.md)] se muestra la aplicación web, un mensaje de error "versión de cliente no es compatible con la versión de la base de datos".  
  
 **Solución:** este problema se produce cuando un [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] aplicación web de Master Data Manager intenta tener acceso a una base de datos que se ha actualizado a [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Master Data Services. Debe utilizar una aplicación web de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] en su lugar.  
  
 Este problema puede producirse también si no se ha detenido y reiniciado el **Grupo de aplicaciones de MDS** en IIS al actualizar el esquema de la base de datos de MDS. Reinicie el **Grupo de aplicaciones de MDS** para corregir el problema.  
  
## <a name="see-also"></a>Vea también  
 [Instalar Master Data Services](../../master-data-services/install-windows/install-master-data-services.md)  
  
  
