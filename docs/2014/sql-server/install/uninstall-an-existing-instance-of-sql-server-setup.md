---
title: Desinstalar una instancia existente de SQL Server (programa de instalación) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- removing instances of SQL Server
- uninstalling instances of SQL Server
- removing SQL Server
- instances of SQL Server, uninstalling
- uninstalling SQL Server
ms.assetid: 3c64b29d-61d7-4b86-961c-0de62261c6a1
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 484ef7dead58a6e8ae35639cdc6218d5c8223bd9
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62990188"
---
# <a name="uninstall-an-existing-instance-of-sql-server-setup"></a>Desinstalar una instancia existente de SQL Server (programa de instalación)
  En este artículo se describe cómo desinstalar una instancia independiente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Siguiendo los pasos de este tema, también prepara el sistema para reinstalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]  
>  Para desinstalar una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe ser administrador local con permiso para iniciar sesión como servicio.  
  
> [!NOTE]  
>  Para desinstalar un clúster de conmutación por error de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , utilice la funcionalidad Eliminar nodo proporcionada por el programa de instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para quitar cada nodo individualmente. Para obtener más información, vea [Agregar o quitar nodos en un clúster de conmutación por error de SQL Server &#40;programa de instalación&#41;](../failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
 Tenga en cuenta la siguiente información importante antes de desinstalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Antes de quitar componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de un equipo que tenga la cantidad de memoria física mínima requerida, debe asegurarse de que el tamaño del archivo de paginación es suficiente. El valor del tamaño del archivo de paginación debe ser el doble de la cantidad de memoria física. Una cantidad insuficiente de memoria virtual puede dar como resultado una eliminación incompleta de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Si tiene varias instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser se desinstala automáticamente cuando se desinstale la última instancia de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
     Si desea desinstalar todos los componentes de [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)], deberá desinstalar el componente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Browser manualmente desde **Programas y características** del **Panel de control**.  
  
### <a name="before-you-uninstall"></a>Antes de la desinstalación  
  
1.  **Haga una copia de seguridad de los datos.** Aunque este paso no sea obligatorio, podría tener bases de datos que desee guardar en su estado presente. También es posible que desee guardar cambios realizados en las bases de datos del sistema. Si se da alguna de estas situaciones, asegúrese de realizar una copia de seguridad de los datos antes de desinstalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. También puede guardar una copia de todos los datos y archivos de registro en una carpeta distinta a la carpeta MSSQL. La carpeta MSSQL se elimina durante la desinstalación.  
  
     Entre los archivos que debe guardar se incluyen los siguientes archivos de base de datos:  
  
    -   Master.mdf  
  
    -   Mastlog.ldf  
  
    -   Model.mdf  
  
    -   Modellog.ldf  
  
    -   Msdbdata.mdf  
  
    -   Msdblog.ldf  
  
    -   Mssqlsystemresource.mdf  
  
    -   Mssqlsustemresource.ldf  
  
    -   Tempdb.mdf  
  
    -   Templog.ldf  
  
    -   `ReportServer[$InstanceName]`(Esta es la [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] base de datos predeterminada).  
  
    -   ReportServer[$InstanceName]TempDB (Es la base de datos temporal predeterminada de [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] ).  
  
2.  **Elimine los grupos de seguridad locales.** Antes de desinstalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], elimine los grupos de seguridad locales correspondientes a los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
3.  **Detenga todos los **  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **servicios de .** Se recomienda detener todos los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] antes de desinstalar los componentes de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Las conexiones activas pueden evitar que la desinstalación se realice correctamente.  
  
4.  **Utilice una cuenta que tenga los permisos adecuados.** Inicie sesión en el servidor mediante la cuenta de servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o con una cuenta que tenga permisos equivalentes. Por ejemplo, puede iniciar sesión en el servidor mediante una cuenta miembro del grupo de administradores locales.  
  
### <a name="to-uninstall-an-instance-of-ssnoversion"></a>To Uninstall an Instance of [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
1.  Para comenzar el proceso de desinstalación, vaya al **Panel de control** y, a continuación, a **Programas y características**.  
  
2.  Haga clic ** [!INCLUDE[msCoName](../../includes/msconame-md.md)] ** con el botón derecho y seleccione **desinstalar**. A continuación, haga clic en **Quitar**. De esta forma se inicia el Asistente para la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
     Se ejecutan las Reglas auxiliares del programa de instalación para comprobar la configuración del equipo. Para continuar, haga clic en **Siguiente**.  
  
3.  En la página Seleccionar instancia, use la lista desplegable para especificar la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que desea quitar, o especifique la opción para quitar solo las características compartidas y las herramientas de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para continuar, haga clic en **Siguiente**.  
  
4.  En la página Seleccionar características, especifique las características que desea quitar de la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]especificada.  
  
     Se ejecutan las reglas de eliminación para comprobar que la operación se puede completar correctamente.  
  
5.  En la página **Listo para eliminar** , revise la lista de componentes y características que se van a desinstalar. Haga clic en **Quitar** para iniciar la desinstalación.  
  
6.  Inmediatamente después de desinstalar la última instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , los demás programas asociados con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] seguirán estando visibles en la lista de programas de **Programas y características**. Sin embargo, si cierra **Programas y características**, la próxima vez que abra **Programas y características**se actualizará la lista de programas y solo mostrará los programas que siguen estando instalados.  
  
### <a name="if-the-uninstallation-fails"></a>Si se produce un error en la desinstalación  
  
1.  Si el proceso de desinstalación no se completa correctamente, intente corregir el problema que provocó el error de desinstalación. Los siguientes artículos pueden ayudarle a entender la causa del error de desinstalación:  
  
    -   [Cómo identificar problemas de instalación de SQL Server 2008 en los archivos de registro de instalación](https://support.microsoft.com/kb/955396/en-us)  
  
    -   [Ver y leer los archivos de registro de instalación de SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
2.  Si no puede solucionar la causa del error de desinstalación, puede ponerse en contacto con el servicio de soporte técnico de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . En algunos casos, como en la eliminación accidental de archivos importantes, puede ser necesario reinstalar el sistema operativo antes de reinstalar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el equipo.  
  
## <a name="see-also"></a>Consulte también  
 [Ver y leer los archivos de registro de instalación de SQL Server](../../database-engine/install-windows/view-and-read-sql-server-setup-log-files.md)  
  
  
