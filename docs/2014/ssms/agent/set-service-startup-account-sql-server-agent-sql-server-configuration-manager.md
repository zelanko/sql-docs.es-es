---
title: Establecer la cuenta de inicio del servicio Agente SQL Server (Administrador de configuración de SQL Server) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Agent, service accounts
- startup accounts [SQL Server]
- service startup accounts [SQL Server Agent]
ms.assetid: 46ffe818-ebb5-43a0-840b-923f219a2472
caps.latest.revision: 42
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 6d2fb2581a2f2f5b7d851323290665af2c23b8ac
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2018
ms.locfileid: "36198803"
---
# <a name="set-the-service-startup-account-for-sql-server-agent-sql-server-configuration-manager"></a>Set the Service Startup Account for SQL Server Agent (SQL Server Configuration Manager)
  La cuenta de inicio del servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] define la cuenta de Windows en la que se ejecuta el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , así como sus permisos de red. En este tema se describe cómo establecer la cuenta del servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] con el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] utilizando [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   [Para establecer la cuenta de inicio de servicio para el Agente SQL Server utilizando SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ya no necesita que la cuenta de inicio del servicio sea miembro del grupo Administradores de [!INCLUDE[msCoName](../../includes/msconame-md.md)] . Sin embargo, la cuenta de inicio de servicio para el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe ser miembro del rol fijo de servidor sysadmin de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La cuenta también debe ser miembro del rol TargetServersRole de la base de datos msdb en el servidor maestro si se usa el procesamiento de trabajos multiservidor.  
  
-   El Explorador de objetos solo muestra el nodo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si se tiene permiso para usarlo.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Para realizar sus funciones, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente debe estar configurado para usar las credenciales de una cuenta que sea miembro de la `sysadmin` rol fijo de servidor en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La cuenta debe tener los siguientes permisos de Windows:  
  
-   Iniciar sesión como servicio (SeServiceLogonRight)  
  
-   Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)  
  
-   Omitir la comprobación transversal (SeChangeNotifyPrivilege)  
  
-   Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaPrivilege)  
  
 Para obtener más información acerca de los permisos de Windows necesarios para la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta de servicio del agente, consulte [seleccionar una cuenta para el servicio del Agente SQL Server](select-an-account-for-the-sql-server-agent-service.md) y [configurar cuentas de servicio de Windows y Permisos](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-set-the-service-startup-account-for-sql-server-agent"></a>Para establecer la cuenta de inicio de servicio para el Agente SQL Server  
  
1.  En **Servidores registrados**, haga clic en el signo más para expandir **Motor de base de datos**.  
  
2.  Haga clic en el signo más para expandir la carpeta **Grupos de servidores locales** .  
  
3.  Haga clic con el botón derecho en la instancia de servidor donde desea instalar la cuenta de inicio de servicio y seleccione **Administrador de configuración de SQL Server**.  
  
4.  En el cuadro de diálogo **Control de cuentas de usuario** , haga clic en **Sí**.  
  
5.  En el Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , en el panel de la consola, seleccione **Servicios de SQL Server**.  
  
6.  En el panel de detalles, haga clic con el botón derecho en *Agente SQL Server***(nombre_de_servidor)*, donde *nombre_de_servidor* es el nombre de la instancia del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuya cuenta de inicio de servicio desea cambiar y, luego, seleccione **Propiedades**.  
  
7.  En el cuadro de diálogo **Agente SQL Server***(nombre_de_servidor)* **Propiedades**, en la pestaña **Iniciar sesión**, seleccione una de las opciones siguientes en **Iniciar sesión como**:  
  
    -   **Cuenta integrada**: seleccione esta opción si los trabajos solo necesitan recursos del servidor local. Para información sobre cómo elegir un tipo de cuenta integrada de Windows, consulte [Seleccionar una cuenta para el servicio del Agente SQL Server](http://msdn.microsoft.com/library/ms191543.aspx).  
  
        > [!IMPORTANT]  
        >  El servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no es compatible con la cuenta del **Servicio local** en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
    -   **Esta cuenta**: seleccione esta opción si los trabajos necesitan recursos de la red, incluidos recursos de aplicaciones; por ejemplo, si desea reenviar eventos a otros registros de aplicación Windows o si desea notificar a operadores mediante mensajes de correo electrónico o buscapersonas.  
  
         Si selecciona esta opción:  
  
        1.  En el cuadro **Nombre de cuenta** , escriba la cuenta que se utilizará para ejecutar el Agente SQL Server. Como alternativa, haga clic en **Examinar** para abrir el cuadro de diálogo **Seleccionar usuarios o grupos** y seleccione la cuenta que desea utilizar.  
  
        2.  En el cuadro **Contraseña** , escriba la contraseña para la cuenta. Vuelva a escribir la contraseña en el cuadro **Confirmar contraseña** .  
  
8.  Haga clic en **Aceptar**.  
  
9. En Administrador de configuración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , haga clic en el botón **Cerrar** .  
  
  