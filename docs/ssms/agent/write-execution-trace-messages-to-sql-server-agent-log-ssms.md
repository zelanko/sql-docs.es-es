---
title: Escritura de mensajes de seguimiento de ejecución en el registro de errores del Agente SQL Server
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- logs [SQL Server], SQL Server Agent
- writing trace messages
- traces [SQL Server], SQL Server Agent logs
- SQL Server Agent, errors
- errors [SQL Server Agent]
ms.assetid: 90e3731e-6fae-43db-833e-9accecdd1c03
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: b83953fd675d61a49f83609a145b08c569e8c72c
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "75243971"
---
# <a name="write-execution-trace-messages-to-the-sql-server-agent-error-log"></a>Escritura de mensajes de seguimiento de ejecución en el registro de errores del Agente SQL Server
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

En este tema se describe cómo configurar el Agente [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para que incluya mensajes de seguimiento de ejecución en su registro de errores en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>Limitaciones y restricciones  
  
-   El Explorador de objetos solo muestra el nodo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si se tiene permiso para usarlo.  
  
-   Dado que esta opción puede hacer que el tamaño del registro de errores sea muy grande, solo se incluyen los mensajes de seguimiento de ejecución en los registros de errores del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuando se investiga un problema específico del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
### <a name="security"></a><a name="Security"></a>Seguridad  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permisos  
Para realizar sus funciones, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe configurarse de modo que use las credenciales de una cuenta que sea miembro del rol fijo de servidor **sysadmin** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La cuenta debe tener los siguientes permisos de Windows:  
  
-   Iniciar sesión como servicio (SeServiceLogonRight)  
  
-   Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)  
  
-   Omitir la comprobación transversal (SeChangeNotifyPrivilege)  
  
-   Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaPrivilege)  
  
Para más información sobre los permisos de Windows necesarios para la cuenta de servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [Seleccionar una cuenta para el servicio del Agente SQL Server](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) y [Configurar cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
## <a name="SSMSProcedure"></a>  
#### <a name="to-write-execution-trace-messages-to-the-sql-server-agent-error-log"></a>Para escribir mensajes de seguimiento de ejecución en el registro de errores del Agente SQL Server  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor que contiene el registro de errores del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el que desea escribir mensajes de seguimiento de ejecución.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server** y seleccione **Propiedades**.  
  
3.  En el cuadro de diálogo **Propiedades de Agente SQL Server -** _nombre\_servidor_, en **Registro de errores** de la página **General**, active la casilla **Incluir mensajes de seguimiento de ejecución**.  
  
4.  Haga clic en **OK**.  
  
