---
title: Cambiar la contraseña de las cuentas utilizadas por SQL Server (Administrador de configuración de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- expired password [SQL Server], SQL Server Agent
- passwords [SQL Server], SQL Server Agent service
- passwords [SQL Server], changing
- expired password [SQL Server], Database Engine
- passwords [SQL Server], SQL Server service
- Database Engine [SQL Server], passwords
- changing passwords used by SQL Server
- modifying passwords
ms.assetid: 5b6dcc03-6cae-45d3-acef-6f85ca6d615f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 865c23dc88571e0c9ee317eca280286a6c37118f
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "62810440"
---
# <a name="change-the-password-of-the-accounts-used-by-sql-server-sql-server-configuration-manager"></a>Cambiar la contraseña de las cuentas que usa SQL Server (Administración de configuración de SQL Server)
  En este tema se describe cómo cambiar la contraseña de las cuentas utilizadas por el [!INCLUDE[ssDE](../../includes/ssde-md.md)] y el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante el Administrador de configuración de SQL Server. El [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecutan en un equipo como un servicio mediante el uso de credenciales suministradas inicialmente durante la instalación. Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta con una cuenta de dominio y se cambia la contraseña de esa cuenta, la contraseña utilizada por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe actualizarse. Si la contraseña no se actualiza, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede perder el acceso a algunos recursos del dominio y si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se detiene, el servicio no se reiniciará hasta que la contraseña se actualice.  
  
 Para cambiar las contraseñas de autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , vea [Contraseña expirada](../password-expired.md).  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es la herramienta diseñada y autorizada para cambiar la configuración de los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El cambio de un servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la aplicación Administrador de control de servicios de Windows (**services.msc**) no siempre cambia todos los valores necesarios y puede impedir que el servicio funcione correctamente. Sin embargo, en un entorno en clúster, después de cambiar la contraseña en el nodo activo mediante el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , debe cambiar la contraseña en el nodo pasivo con el Administrador de control de servicios.  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Para cambiar la contraseña que utiliza un servicio debe ser el administrador del equipo.  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> Usar el Administrador de configuración de SQL Server  
  
#### <a name="to-change-the-password-used-by-the-sql-server-database-engine-service"></a>Para cambiar la contraseña utilizada por el servicio SQL Server (motor de base de datos)  
  
1.  Haga clic en el botón **Inicio** , seleccione **Todos los programas**, seleccione [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], seleccione **Herramientas de configuración**y, a continuación, haga clic en **Administrador de configuración de SQL Server**.  
  
    > [!NOTE]  
    >  Como el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es un complemento del programa [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console y no un programa independiente, el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no aparece como aplicación en las versiones más recientes de Windows.  
    >   
    >  -   **Windows 10**:  
    >          Para abrir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, en la **Página de inicio**, escriba SQLServerManager12. msc ( [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]para). Para versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , reemplace el 12 por un número inferior. Al hacer clic en SQLServerManager12.msc, se abre el Administrador de configuración. Para anclar el Configuration Manager a la página de inicio o a la barra de tareas, haga clic con el botón secundario en SQLServerManager12. msc y, a continuación, haga clic en **abrir ubicación de archivo**. En el explorador de archivos de Windows, haga clic con el botón secundario en SQLServerManager12. msc y, a continuación, haga clic en **anclar a Inicio** o **anclar a la barra de tareas**.  
    > -   **Windows 8**:  
    >          Para abrir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, en el acceso a **Buscar** , **en aplicaciones**, **Escriba\<SQLServerManager version>. msc** como `SQLServerManager12.msc`y, a continuación, presione **entrar**.  
  
2.  En Administrador de configuración de SQL Server, haga clic en **Servicios de SQL Server**.  
  
3.  En el panel de detalles, haga clic con el botón derecho en **(** \<nombreDeInstancia> **)** de SQL Server y, luego, haga clic en **Propiedades**.  
  
4.  En el cuadro de diálogo **Propiedades de (** \<nombreDeInstancia> **) de SQL Server**, en la pestaña Iniciar sesión, en la cuenta que aparece en el cuadro **Nombre de cuenta**, escriba la nueva contraseña en los cuadros **Contraseña** y **Confirmar contraseña**. Luego, haga clic en **Aceptar**.  
  
     La contraseña surte efecto inmediatamente, sin necesidad de reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
#### <a name="to-change-the-password-used-by-the-sql-server-agent-service"></a>Para cambiar la contraseña que utiliza el servicio del Agente SQL Server  
  
1.  Haga clic en el botón **Inicio** , seleccione **Todos los programas**, seleccione [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], seleccione **Herramientas de configuración**y, a continuación, haga clic en **Administrador de configuración de SQL Server**.  
  
2.  En Administrador de configuración de SQL Server, haga clic en **Servicios de SQL Server**.  
  
3.  En el panel de detalles, haga clic con el botón derecho en **Agente SQL Server (** \<nombreDeInstancia> **)** y, luego, haga clic en **Propiedades**.  
  
4.  En el cuadro de diálogo **Propiedades de (** \<nombreDeInstancia> **) de Agente SQL Server**, en la pestaña Iniciar sesión, en la cuenta que aparece en el cuadro **Nombre de cuenta**, escriba la nueva contraseña en los cuadros **Contraseña** y **Confirmar contraseña**. Luego, haga clic en **Aceptar**.  
  
     En una instancia independiente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la contraseña surte efecto inmediatamente, sin necesidad de reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En una instancia en clúster, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podría cambiar el recurso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a sin conexión y requerir un reinicio.  
  
## <a name="see-also"></a>Consulte también  
 [Temas de procedimientos de administración de servicios &#40;Administrador de configuración de SQL Server&#41;](../managing-services-how-to-topics-sql-server-configuration-manager.md)  
  
  
