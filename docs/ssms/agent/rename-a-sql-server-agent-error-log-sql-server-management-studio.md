---
title: Cambiar el nombre del registro de errores del Agente SQL Server (SQL Server Management Studio) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- logs [SQL Server], SQL Server Agent
- renaming SQL Server Agent error log
- SQL Server Agent, errors
- errors [SQL Server Agent]
ms.assetid: dee2b199-48af-44cb-9177-d029a5edb169
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: a6da7992bd9767f4a5b05c307c85af694b074729
ms.lasthandoff: 04/11/2017

---
# <a name="rename-a-sql-server-agent-error-log-sql-server-management-studio"></a>Cambiar el nombre del registro de errores del Agente SQL Server (SQL Server Management Studio)
En este tema se describe el modo de cambiar el nombre del archivo en el que se escriben los errores del Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)].  
  
**En este tema**  
  
-   **Antes de empezar:**  
  
    [Limitaciones y restricciones](#Restrictions)  
  
    [Seguridad](#Security)  
  
-   [Para cambiar el nombre de un registro de errores del Agente SQL Server utilizando SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de comenzar  
  
### <a name="Restrictions"></a>Limitaciones y restricciones  
  
-   El Explorador de objetos solo muestra el nodo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] si se tiene permiso para usarlo.  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] no escribirá nada en el archivo de registro nuevo hasta que se reinicie el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
### <a name="Security"></a>Seguridad  
  
#### <a name="Permissions"></a>Permissions  
Para realizar sus funciones, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] debe configurarse de modo que use las credenciales de una cuenta que sea miembro del rol fijo de servidor **sysadmin** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. La cuenta debe tener los siguientes permisos de Windows:  
  
-   Iniciar sesión como servicio (SeServiceLogonRight)  
  
-   Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)  
  
-   Omitir la comprobación transversal (SeChangeNotifyPrivilege)  
  
-   Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaPrivilege)  
  
Para más información sobre los permisos de Windows necesarios para la cuenta de servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , consulte [Seleccionar una cuenta para el servicio del Agente SQL Server](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) y [Configurar cuentas de servicio de Windows](http://msdn.microsoft.com/en-us/309b9dac-0b3a-4617-85ef-c4519ce9d014).  
  
## <a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-rename-a-sql-server-agent-error-log"></a>Para cambiar el nombre del registro de errores del Agente SQL Server  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor que contiene el registro de errores del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] cuyo nombre desea cambiar.  
  
2.  Haga clic en el signo más para expandir **Agente SQL Server**.  
  
3.  Haga clic con el botón derecho en la carpeta **Registros de errores** y seleccione **Configurar**.  
  
4.  En el cuadro de diálogo **Configurar registros de errores del Agente SQL Server** , en el cuadro **Archivo de registro de errores** , escriba la nueva ruta de acceso y nombre de archivo para el registro de errores. Como alternativa, haga clic en los puntos suspensivos **(...)** para abrir el cuadro de diálogo **Especificar ubicación de registro de errores de agente** .  
  
5.  Cuando termine, haga clic en **Aceptar**.  
  

