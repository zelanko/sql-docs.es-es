---
title: "Cambiar la contrase&#241;a de las cuentas que usa SQL Server (Administraci&#243;n de configuraci&#243;n de SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "contraseña expirada [SQL Server], Agente SQL Server"
  - "contraseñas [SQL Server], servicio Agente SQL Server"
  - "contraseñas [SQL Server], cambiar"
  - "contraseña expirada [SQL Server], motor de base de datos"
  - "contraseñas [SQL Server], servicio SQL Server"
  - "Motor de base de datos [SQL Server], contraseñas"
  - "cambiar las contraseñas utilizadas por SQL Server"
  - "modificar contraseñas"
ms.assetid: 5b6dcc03-6cae-45d3-acef-6f85ca6d615f
caps.latest.revision: 22
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Cambiar la contrase&#241;a de las cuentas que usa SQL Server (Administraci&#243;n de configuraci&#243;n de SQL Server)
  En este tema se describe cómo cambiar la contraseña de las cuentas utilizadas por el [!INCLUDE[ssDE](../../includes/ssde-md.md)] y el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante el Administrador de configuración de SQL Server. El [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] y el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecutan en un equipo como un servicio mediante el uso de credenciales suministradas inicialmente durante la instalación. Si la instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se ejecuta con una cuenta de dominio y se cambia la contraseña de esa cuenta, la contraseña utilizada por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe actualizarse. Si la contraseña no se actualiza, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede perder el acceso a algunos recursos del dominio y si [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se detiene, el servicio no se reiniciará hasta que la contraseña se actualice.  
  
 Para cambiar las contraseñas de autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], vea [Contraseña expirada](../../ssms/f1-help/password-expired.md).  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es la herramienta diseñada y autorizada para cambiar la configuración de los servicios de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . El cambio de un servicio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mediante la aplicación Administrador de control de servicios de Windows (**services.msc**) no siempre cambia todos los valores necesarios y puede impedir que el servicio funcione correctamente. Sin embargo, en un entorno en clúster, después de cambiar la contraseña en el nodo activo mediante el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], debe cambiar la contraseña en el nodo pasivo con el Administrador de control de servicios.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Para cambiar la contraseña que utiliza un servicio debe ser el administrador del equipo.  
  
##  <a name="SSMSProcedure"></a> Usar el Administrador de configuración de SQL Server  
  
#### Para cambiar la contraseña utilizada por el servicio SQL Server (motor de base de datos)  
  
1.  Haga clic en el botón **Inicio** , seleccione **Todos los programas**, seleccione [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], seleccione **Herramientas de configuración**y, a continuación, haga clic en **Administrador de configuración de SQL Server**.  
  
    > [!NOTE]  
    >  Como el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es un complemento del programa [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console y no un programa independiente, el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no aparece como aplicación en las versiones más recientes de Windows.  
    >   
    >  -   **Windows 10**:  
    >          Para abrir el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], escriba SQLServerManager13.msc (para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) en la **página de inicio**. Para versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , reemplace el 13 por un número inferior. Al hacer clic en SQLServerManager13.msc, se abre el Administrador de configuración. Para anclar el Administrador de configuración a la página de inicio o a la barra de tareas, haga clic con el botón derecho en SQLServerManager13.msc y, después, haga clic en **Abrir ubicación del archivo**. En el Explorador de archivos de Windows, haga clic con el botón derecho en SQLServerManager13.msc y, después, haga clic en **Anclar a Inicio** o **Anclar a la barra de tareas**.  
    > -   **Windows 8**:  
    >          Para abrir el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], escriba **SQLServerManager\<versión>.msc** por ejemplo, **SQLServerManager13.msc**, en el acceso a **Buscar** de **Aplicaciones** y, después, pulse **Entrar**.  
  
2.  En Administrador de configuración de SQL Server, haga clic en **Servicios de SQL Server**.  
  
3.  En el panel de detalles, haga clic con el botón derecho en **SQL Server (**\<instancename>**)** y, luego, con el botón primario, en **Propiedades**.  
  
4.  En el cuadro de diálogo **Propiedades de SQL Server (**\<instancename>**) **, en la pestaña Iniciar sesión, para la cuenta que aparece en el cuadro **Nombre de cuenta**, escriba la nueva contraseña en los cuadros **Contraseña** y **Confirmar contraseña**. Luego, haga clic en **Aceptar**.  
  
     La contraseña surte efecto inmediatamente, sin necesidad de reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
#### Para cambiar la contraseña que utiliza el servicio del Agente SQL Server  
  
1.  Haga clic en el botón **Inicio** , seleccione **Todos los programas**, seleccione [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], seleccione **Herramientas de configuración**y, a continuación, haga clic en **Administrador de configuración de SQL Server**.  
  
2.  En Administrador de configuración de SQL Server, haga clic en **Servicios de SQL Server**.  
  
3.  En el panel de detalles, haga clic con el botón derecho en **Agente SQL Server (**\<instancename>**)** y, luego, con el botón primario, en **Propiedades**.  
  
4.  En el cuadro de diálogo **Propiedades de Agente SQL Server (**\<instancename>**)**, en la pestaña Iniciar sesión, para la cuenta que aparece en el cuadro **Nombre de cuenta**, escriba la nueva contraseña en los cuadros **Contraseña** y **Confirmar contraseña**. Luego, haga clic en **Aceptar**.  
  
     En una instancia independiente de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], la contraseña surte efecto inmediatamente, sin necesidad de reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. En una instancia en clúster, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podría cambiar el recurso de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a sin conexión y requerir un reinicio.  
  
## Vea también  
 [Temas de procedimientos de administración de servicios &#40;Administrador de configuración de SQL Server&#41;](../Topic/Managing%20Services%20How-to%20Topics%20\(SQL%20Server%20Configuration%20Manager\).md)  
  
  