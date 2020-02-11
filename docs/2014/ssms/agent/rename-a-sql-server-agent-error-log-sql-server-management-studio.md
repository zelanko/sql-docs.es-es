---
title: Cambiar el nombre del registro de errores del Agente SQL Server (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], SQL Server Agent
- renaming SQL Server Agent error log
- SQL Server Agent, errors
- errors [SQL Server Agent]
ms.assetid: dee2b199-48af-44cb-9177-d029a5edb169
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b3405f69ce36b4b46cdb519d281ab910d7220887
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62649931"
---
# <a name="rename-a-sql-server-agent-error-log-sql-server-management-studio"></a>Rename a SQL Server Agent Error Log (SQL Server Management Studio)
  En este tema se describe cómo cambiar el nombre del [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] archivo donde se escriben [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] los errores [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]del agente en mediante.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   [Para cambiar el nombre de un registro de errores de Agente SQL Server mediante SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   El Explorador de objetos solo muestra el nodo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si se tiene permiso para usarlo.  
  
-   
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no escribirá nada en el archivo de registro nuevo hasta que se reinicie el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Para realizar sus funciones, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe configurarse de modo que use las credenciales de una cuenta que sea miembro del rol fijo de servidor **sysadmin** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La cuenta debe tener los siguientes permisos de Windows:  
  
-   Iniciar sesión como servicio (SeServiceLogonRight)  
  
-   Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)  
  
-   Omitir la comprobación transversal (SeChangeNotifyPrivilege)  
  
-   Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaPrivilege)  
  
 Para obtener más información acerca de los permisos de Windows [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] necesarios para la cuenta de servicio del agente, consulte [seleccionar una cuenta para el servicio de Agente SQL Server](select-an-account-for-the-sql-server-agent-service.md) y [configurar los permisos y las cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-rename-a-sql-server-agent-error-log"></a>Para cambiar el nombre del registro de errores del Agente SQL Server  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor que contiene el registro de errores del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuyo nombre desea cambiar.  
  
2.  Haga clic en el signo más para expandir **Agente SQL Server**.  
  
3.  Haga clic con el botón derecho en la carpeta **Registros de errores** y seleccione **Configurar**.  
  
4.  En el cuadro de diálogo **Configurar registros de errores del Agente SQL Server** , en el cuadro **Archivo de registro de errores** , escriba la nueva ruta de acceso y nombre de archivo para el registro de errores. Como alternativa, haga clic en los puntos suspensivos **(...)** para abrir el cuadro de diálogo **Especificar ubicación de registro de errores de agente** .  
  
5.  Cuando termine, haga clic en **Aceptar**.  
  
  
