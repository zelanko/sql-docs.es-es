---
title: Establecer un alias de SQL Server para el servicio Agente SQL Server (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- aliases [SQL Server], creating
- SQL Server Agent, aliases
ms.assetid: 02d6295d-ab52-44f0-8f1b-f3910a507d8f
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: b9f91ec957665975fd956e36a5af3c4261fb47af
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84929199"
---
# <a name="set-a-sql-server-alias-for-the-sql-server-agent-service-sql-server-management-studio"></a>Set a SQL Server Alias for the SQL Server Agent Service (SQL Server Management Studio)
  En este tema se describe cómo establecer un [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] alias para [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] que el agente lo use para conectarse a [!INCLUDE[ssDE](../includes/ssde-md.md)] mediante [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] . De manera predeterminada, el servicio del Agente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] se conecta a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a través de canalizaciones con nombre, mediante nombres de servidores dinámicos que no requieren ninguna configuración adicional del cliente. Solo es necesario configurar un alias de conexión de servidor si no se utiliza el transporte de red predeterminado o si se va a conectar a una instancia de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] a la escucha en una canalización con nombre alternativa.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   [Para establecer un alias de SQL Server para el servicio del Agente SQL Server utilizando SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitaciones y restricciones  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no funcionará correctamente si no se selecciona un alias que haga referencia a la instancia local de [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
-   El Explorador de objetos solo muestra el nodo del Agente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] si se tiene permiso para usarlo.  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Para realizar sus funciones, el Agente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] debe configurarse de modo que use las credenciales de una cuenta que sea miembro del rol fijo de servidor **sysadmin** en [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. La cuenta debe tener los siguientes permisos de Windows:  
  
-   Iniciar sesión como servicio (SeServiceLogonRight)  
  
-   Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)  
  
-   Omitir la comprobación transversal (SeChangeNotifyPrivilege)  
  
-   Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaPrivilege)  
  
 Para obtener más información acerca de los permisos de Windows necesarios para la [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] cuenta de servicio del agente, consulte [seleccionar una cuenta para el servicio de Agente SQL Server](../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) y [configurar los permisos y las cuentas de servicio de Windows](configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-set-a-sql-server-alias-for-the-sql-server-agent-service"></a>Para establecer un alias de SQL Server para servicio del Agente SQL Server  
  
1.  En el **Explorador de objetos**, conéctese a una instancia de [!INCLUDE[ssDEnoversion](../includes/ssdenoversion-md.md)] y expándala.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server**y, luego, haga clic en **Propiedades**.  
  
3.  En el cuadro de diálogo **propiedades de Agente SQL Server**_Server_name_ , en **seleccionar una página**, seleccione **conexión**y  
  
4.  En el cuadro de **Servidor de host local del alias** , escriba el alias de servidor al que debe conectarse el Agente [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
5.  Haga clic en **OK**.  
  
  
