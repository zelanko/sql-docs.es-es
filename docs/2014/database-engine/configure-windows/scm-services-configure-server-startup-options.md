---
title: Configurar opciones de inicio del servidor (Administrador de configuración de SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 01/07/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
helpviewer_keywords:
- parameters [SQL Server], startup options
- SQL Server, startup options
- single-user mode [SQL Server], starting in
- startup options [SQL Server]
- SQL Server services, setting startup options
ms.assetid: 7a94643c-6460-4baf-bb31-0cb99eaf970d
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: af822eb405fb66f5e91340d42fc79bef0d769fbf
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84935066"
---
# <a name="configure-server-startup-options-sql-server-configuration-manager"></a>Configurar opciones de inicio del servidor (Administrador de configuración de SQL Server)
  En este tema se describe cómo configurar las opciones de inicio que se utilizarán cada vez que el [!INCLUDE[ssDE](../../includes/ssde-md.md)] se inicie en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obtener una lista de opciones de inicio, vea [Opciones de inicio del servicio de motor de base de datos](database-engine-service-startup-options.md).  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
### <a name="limitations-and-restrictions"></a>Limitaciones y restricciones  
 El Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] escribe los parámetros de inicio en el Registro. Estos surten efecto en el siguiente inicio de [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
 En un clúster, se deben efectuar cambios en el servidor activo cuando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está en línea y surtirán efecto cuando el [!INCLUDE[ssDE](../../includes/ssde-md.md)] se reinicie. La actualización de las opciones de inicio del Registro del otro nodo se producirá tras la siguiente conmutación por error.  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 La configuración de opciones de inicio del servidor está restringida a los usuarios que pueden cambiar las entradas relacionadas del Registro. Esto incluye a los usuarios siguientes.  
  
-   Miembros del grupo local de administradores.  
  
-   La cuenta de dominio utilizada por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], si el [!INCLUDE[ssDE](../../includes/ssde-md.md)] está configurado para ejecutarse bajo una cuenta de dominio.  
  
##  <a name="using-sql-server-configuration-manager"></a><a name="SSMSProcedure"></a> Usar el Administrador de configuración de SQL Server  
  
#### <a name="to-configure-startup-options"></a>Para configurar las opciones de inicio  
  
1.  En el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , haga clic en **Servicios de SQL Server**.  
  
    > [!NOTE]  
    >  Como el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es un complemento del programa [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console y no un programa independiente, el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no aparece como aplicación en las versiones más recientes de Windows.  
    >   
    >  -   **Windows 10**:  
    >          Para abrir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, en la **Página de inicio**, escriba SQLServerManager12. msc (para [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ). Para versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , reemplace el 12 por un número inferior. Al hacer clic en SQLServerManager12.msc, se abre el Administrador de configuración. Para anclar el Configuration Manager a la página de inicio o a la barra de tareas, haga clic con el botón secundario en SQLServerManager12. msc y, a continuación, haga clic en **abrir ubicación de archivo**. En el explorador de archivos de Windows, haga clic con el botón secundario en SQLServerManager12. msc y, a continuación, haga clic en **anclar a Inicio** o **anclar a la barra de tareas**.  
    > -   **Windows 8**:  
    >          Para abrir [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Configuration Manager, en el acceso a **Buscar** , en **aplicaciones**, escriba **SQLServerManager \<version> . msc** como y, `SQLServerManager12.msc` a continuación, presione **entrar**.  
  
2.  En el panel derecho, haga clic con el botón derecho en **SQL Server (***<nombre_de_instancia>***)** y, luego, haga clic en **Propiedades**.  
  
3.  En la pestaña **Parámetros de inicio** , en el cuadro **Especifique un parámetro de inicio** , escriba el parámetro y, a continuación, haga clic en **Agregar**.  
  
     Por ejemplo, para iniciar en modo de usuario único, escriba `-m` en el cuadro **Especifique un parámetro de inicio** y, a continuación, haga clic en **Agregar**. (Al reiniciar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en modo de usuario único, detenga el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . De lo contrario, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] podría conectarse primero e impedir que se conecte como un segundo usuario).  
  
4.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
5.  Reinicie el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
    > [!WARNING]  
    >  Cuando haya terminado de usar el modo de usuario único, en el cuadro parámetros de inicio, seleccione el `-m` parámetro en el cuadro **parámetros existentes** y, a continuación, haga clic en **quitar**. Reinicie el [!INCLUDE[ssDE](../../includes/ssde-md.md)] para restaurar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] al modo típico multiusuario.  
  
## <a name="see-also"></a>Consulte también  
 [Iniciar SQL Server en modo de usuario único](start-sql-server-in-single-user-mode.md)   
 [Conectarse a SQL Server cuando los administradores del sistema están bloqueados](connect-to-sql-server-when-system-administrators-are-locked-out.md)   
 [Start, Stop, or Pause the SQL Server Agent Service](../../ssms/agent/start-stop-or-pause-the-sql-server-agent-service.md)  
  
  
