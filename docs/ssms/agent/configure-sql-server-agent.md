---
title: Configure SQL Server Agent
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, configuring
- accounts [SQL Server], SQL Server Agent
- SQL Server Agent, permissions
- security [SQL Server], SQL Server Agent
ms.assetid: 2e361a62-9e92-4fcd-80d7-d6960f127900
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 01/19/2017
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 50021dca6e570e7150ffb6a16ac030804ad3f4ea
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/01/2020
ms.locfileid: "85755289"
---
# <a name="configure-sql-server-agent"></a>Configure SQL Server Agent

[!INCLUDE [SQL Server SQL MI](../../includes/applies-to-version/sql-asdbmi.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características del Agente SQL Server son compatibles actualmente, aunque no todas. En la instancia administrada de SQL Database no se permite habilitar y deshabilitar el Agente SQL Server. El Agente SQL se ejecuta de forma continua. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database de SQL Server](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

En este tema se describe cómo especificar algunas opciones de configuración para el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El conjunto completo de opciones de configuración del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo está disponible dentro de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], Objetos de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SMO) o los procedimientos almacenados del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="before-you-begin"></a><a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="limitations-and-restrictions"></a><a name="Restrictions"></a>Limitaciones y restricciones  
  
-   Haga clic en el **Agente SQL Server** en el Explorador de objetos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para administrar trabajos, operadores, alertas y el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . No obstante, el Explorador de objetos solo muestra el nodo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si tiene permiso para utilizarlo.  
  
-   El reinicio automático no debe habilitarse para el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en las instancias de clúster de conmutación por error.  
  
### <a name="security"></a><a name="Security"></a>Seguridad  
  
#### <a name="permissions"></a><a name="Permissions"></a>Permisos  
Para realizar sus funciones, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe configurarse de modo que use las credenciales de una cuenta que sea miembro del rol fijo de servidor **sysadmin** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La cuenta debe tener los siguientes permisos de Windows:  
  
-   Iniciar sesión como servicio (SeServiceLogonRight)  
  
-   Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)  
  
-   Omitir la comprobación transversal (SeChangeNotifyPrivilege)  
  
-   Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaPrivilege)  
  
Para más información sobre los permisos de Windows necesarios para la cuenta de servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [Seleccionar una cuenta para el servicio del Agente SQL Server](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) y [Configurar cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
## <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-configure-sql-server-agent"></a>Para configurar el Agente SQL Server  
  
1.  Haga clic en el botón **Inicio** y después, en el menú **Inicio**  , haga clic en **Panel de control**.  
  
2.  En el Panel de control, haga clic en **Sistema y seguridad**, haga clic en **Herramientas administrativas**y seleccione **Directiva de seguridad local**.  
  
3.  En Directiva de seguridad local, haga clic en las comillas angulares para expandir la carpeta **Directivas locales** y, a continuación, haga clic en la carpeta **Asignación de derechos de usuario** .  
  
4.  Haga clic con el botón derecho en un permiso que desee configurar para su uso con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y seleccione **Propiedades**.  
  
5.  En el cuadro de diálogo de propiedades del permiso, compruebe que se muestra la cuenta con la que se ejecuta el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si no aparece, haga clic en **Agregar usuario o grupo**, escriba la cuenta bajo la que se ejecuta el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el cuadro de diálogo **Seleccionar usuarios, equipos, cuentas de servicio o grupos** y, a continuación, haga clic en **Aceptar**.  
  
6.  Repita el proceso para cada permiso que desee agregar para el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Cuando termine, haga clic en **Aceptar**.  
  
