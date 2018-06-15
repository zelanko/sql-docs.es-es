---
title: Establecer la cuenta de inicio del servicio del Agente SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-agent
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, service accounts
- startup accounts [SQL Server]
- service startup accounts [SQL Server Agent]
ms.assetid: 46ffe818-ebb5-43a0-840b-923f219a2472
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: = azuresqldb-mi-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 358b9406a7f2235d710b7da4146205e62cca0c30
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33046562"
---
# <a name="set-the-service-startup-account-for-sql-server-agent-sql-server-configuration-manager"></a>Set the Service Startup Account for SQL Server Agent (SQL Server Configuration Manager)
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]

> [!IMPORTANT]  
> En [Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance), la mayoría de las características de agente SQL Server son compatibles actualmente, aunque no todas. Vea [Diferencias de T-SQL en Instancia administrada de Azure SQL Database](https://docs.microsoft.com/azure/sql-database/sql-database-managed-instance-transact-sql-information#sql-server-agent) para obtener más información.

La cuenta de inicio del servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] define la cuenta de Windows en la que se ejecuta el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , así como sus permisos de red. En este tema se describe cómo establecer la cuenta del servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] con el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent_md.md)] utilizando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)].  
  
**En este tema**  
  
-   **Antes de empezar:**  
  
    [Limitaciones y restricciones](#Restrictions)  
  
    [Seguridad](#Security)  
  
-   [Para establecer la cuenta de inicio de servicio para el Agente SQL Server utilizando SQL Server Management Studio](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de empezar  
  
### <a name="Restrictions"></a>Limitaciones y restricciones  
  
-   En [!INCLUDE[ssVersion2005](../../includes/ssversion2005_md.md)], el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] ya no necesita que la cuenta de inicio del servicio sea miembro del grupo Administradores de [!INCLUDE[msCoName](../../includes/msconame_md.md)] . Sin embargo, la cuenta de inicio de servicio para el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] debe ser miembro del rol fijo de servidor sysadmin de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. La cuenta también debe ser miembro del rol TargetServersRole de la base de datos msdb en el servidor maestro si se usa el procesamiento de trabajos multiservidor.  
  
-   El Explorador de objetos solo muestra el nodo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] si se tiene permiso para usarlo.  
  
### <a name="Security"></a>Seguridad  
  
#### <a name="Permissions"></a>Permissions  
Para realizar sus funciones, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] debe configurarse de modo que use las credenciales de una cuenta que sea miembro del rol fijo de servidor **sysadmin** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. La cuenta debe tener los siguientes permisos de Windows:  
  
-   Iniciar sesión como servicio (SeServiceLogonRight)  
  
-   Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)  
  
-   Omitir la comprobación transversal (SeChangeNotifyPrivilege)  
  
-   Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaPrivilege)  
  
Para más información sobre los permisos de Windows necesarios para la cuenta de servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , consulte [Seleccionar una cuenta para el servicio del Agente SQL Server](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) y [Configurar cuentas de servicio de Windows](http://msdn.microsoft.com/en-us/309b9dac-0b3a-4617-85ef-c4519ce9d014).  
  
## <a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-set-the-service-startup-account-for-sql-server-agent"></a>Para establecer la cuenta de inicio de servicio para el Agente SQL Server  
  
1.  En **Servidores registrados**, haga clic en el signo más para expandir **Motor de base de datos**.  
  
2.  Haga clic en el signo más para expandir la carpeta **Grupos de servidores locales** .  
  
3.  Haga clic con el botón derecho en la instancia de servidor donde desea instalar la cuenta de inicio de servicio y seleccione **Administrador de configuración de SQL Server**.  
  
4.  En el cuadro de diálogo **Control de cuentas de usuario** , haga clic en **Sí**.  
  
5.  En el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , en el panel de la consola, seleccione **Servicios de SQL Server**.  
  
6.  En el panel de detalles, haga clic con el botón derecho en *Agente SQL Server***(nombre_de_servidor)*, donde *nombre_de_servidor* es el nombre de la instancia del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] cuya cuenta de inicio de servicio desea cambiar y, luego, seleccione **Propiedades**.  
  
7.  En el cuadro de diálogo **Agente SQL Server***(nombre_de_servidor)* **Propiedades**, en la pestaña **Iniciar sesión**, seleccione una de las opciones siguientes en **Iniciar sesión como**:  
  
    -   **Cuenta integrada**: seleccione esta opción si los trabajos solo necesitan recursos del servidor local. Para información sobre cómo elegir un tipo de cuenta integrada de Windows, consulte [Seleccionar una cuenta para el servicio del Agente SQL Server](http://msdn.microsoft.com/library/ms191543.aspx).  
  
        > [!IMPORTANT]  
        > El servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] no es compatible con la cuenta del **Servicio local** en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)].  
  
    -   **Esta cuenta**: seleccione esta opción si los trabajos necesitan recursos de la red, incluidos recursos de aplicaciones; por ejemplo, si desea reenviar eventos a otros registros de aplicación Windows o si desea notificar a operadores mediante mensajes de correo electrónico o buscapersonas.  
  
        Si selecciona esta opción:  
  
        1.  En el cuadro **Nombre de cuenta** , escriba la cuenta que se utilizará para ejecutar el Agente SQL Server. Como alternativa, haga clic en **Examinar** para abrir el cuadro de diálogo **Seleccionar usuarios o grupos** y seleccione la cuenta que desea utilizar.  
  
        2.  En el cuadro **Contraseña** , escriba la contraseña para la cuenta. Vuelva a escribir la contraseña en el cuadro **Confirmar contraseña** .  
  
8.  Haga clic en **Aceptar**.  
  
9. En Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , haga clic en el botón **Cerrar** .  
  
