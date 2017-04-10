---
title: "Evitar el inicio autom&#225;tico de una instancia de SQL Server (Administrador de configuraci&#243;n de SQL Server) | Microsoft Docs"
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
  - "inicio automático de SQL Server"
  - "SQL Server, detener"
  - "SQL Server, inicio automático"
  - "cancelar el inicio automático"
  - "detener SQL Server"
  - "evitar el inicio automático [SQL Server]"
ms.assetid: 782663cf-f3d7-4cc6-b621-21e4550f0322
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# Evitar el inicio autom&#225;tico de una instancia de SQL Server (Administrador de configuraci&#243;n de SQL Server)
  En este tema se describe cómo evitar que una instancia de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se inicie automáticamente en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante el Administrador de configuración de SQL Server. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se suele configurar para iniciarse automáticamente. Puede cambiar esta configuración estableciendo en manual el modo de inicio de la instancia.  
  
##  <a name="SSMSProcedure"></a> Usar el Administrador de configuración de SQL Server  
  
#### Para evitar el inicio automático de una instancia de SQL Server  
  
1.  En el menú **Inicio** , elija **Todos los programas**, [!INCLUDE[ssCurrentUI](../../includes/sscurrentui-md.md)], **Herramientas de configuración**y, por último, **Administrador de configuración de SQL Server**.  
  
    > [!NOTE]  
    >  Como el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] es un complemento del programa [!INCLUDE[msCoName](../../includes/msconame-md.md)] Management Console y no un programa independiente, el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no aparece como aplicación en las versiones más recientes de Windows.  
    >   
    >  -   **Windows 10**:  
    >          Para abrir el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], escriba SQLServerManager13.msc (para [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]) en la **página de inicio**. Para versiones anteriores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , reemplace el 13 por un número inferior. Al hacer clic en SQLServerManager13.msc, se abre el Administrador de configuración. Para anclar el Administrador de configuración a la página de inicio o a la barra de tareas, haga clic con el botón derecho en SQLServerManager13.msc y, después, haga clic en **Abrir ubicación del archivo**. En el Explorador de archivos de Windows, haga clic con el botón derecho en SQLServerManager13.msc y, después, haga clic en **Anclar a Inicio** o **Anclar a la barra de tareas**.  
    > -   **Windows 8**:  
    >          Para abrir el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], escriba **SQLServerManager\<versión>.msc** por ejemplo, **SQLServerManager13.msc**, en el acceso a **Buscar** de **Aplicaciones** y, después, presione **Entrar**.  
  
2.  En el Administrador de configuración de SQL Server, expanda **Servicios**y haga clic en **SQL Server**.  
  
3.  En el panel de detalles, haga clic con el botón derecho en **MSSQLServer** y, después, haga clic en **Propiedades**.  
  
4.  En el cuadro de diálogo **SQL Server \<***NombreDeInstancia***> Propiedades**, en el cuadro **Propiedades**, defina el valor de **Modo de inicio** en **Manual**.  
  
5.  Haga clic en **Aceptar** para cerrar el cuadro de diálogo **SQL Server \<***NombreDeInstancia***> Propiedades** y, luego, cierre el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## Vea también  
 [Iniciar, detener, pausar, reanudar y reiniciar el motor de base de datos, Agente SQL Server o el Servicio SQL Server Browser](../../database-engine/configure-windows/start, stop, pause, resume, restart sql server services.md)  
  
  