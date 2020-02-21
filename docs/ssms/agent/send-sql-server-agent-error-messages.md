---
title: Send SQL Server Agent Error Messages
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- messages [SQL Server], SQL Server Agent
- sending messages
- SQL Server Agent, errors
- errors [SQL Server Agent]
ms.assetid: 2597d0d7-951a-48cf-989f-abb67b9fdb36
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 3aec88f017ffd9b405a68e15494f980322386690
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "75239190"
---
# <a name="send-sql-server-agent-error-messages"></a>Send SQL Server Agent Error Messages
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

En este tema se describe cómo configurar el Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que envíe sus mensajes de error mediante NET SEND en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] con [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="Restrictions"></a>Limitaciones y restricciones  
  
-   El Explorador de objetos solo muestra el nodo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si se tiene permiso para usarlo.  
  
-   Para recibir eventos mediante NET SEND, el servicio [!INCLUDE[msCoName](../../includes/msconame_md.md)] Windows Messenger debe estar en ejecución.  
  
### <a name="Security"></a>Seguridad  
  
#### <a name="Permissions"></a>Permisos  
Para realizar sus funciones, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe configurarse de modo que use las credenciales de una cuenta que sea miembro del rol fijo de servidor **sysadmin** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La cuenta debe tener los siguientes permisos de Windows:  
  
-   Iniciar sesión como servicio (SeServiceLogonRight)  
  
-   Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)  
  
-   Omitir la comprobación transversal (SeChangeNotifyPrivilege)  
  
-   Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaPrivilege)  
  
Para más información sobre los permisos de Windows necesarios para la cuenta de servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [Seleccionar una cuenta para el servicio del Agente SQL Server](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) y [Configurar cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
## <a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-send-sql-server-agent-error-messages"></a>Para enviar mensajes de error del Agente SQL Server  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor que contiene el registro de errores del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] desde el que desea enviar mensajes de error mediante NET SEND.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server** y seleccione **Propiedades**.  
  
3.  En el cuadro de diálogo **Propiedades de Agente SQL Server -** _nombre\_servidor_, en **Registro de errores** en la página **General**, escriba el nombre de usuario o del equipo al que quiere enviar mensajes de error en el cuadro **Destinatario de NET SEND**.  
  
4.  Haga clic en **OK**.  
  
