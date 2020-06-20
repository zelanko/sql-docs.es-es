---
title: Establezca la conexión SQL Server para el servicio Agente SQL Server (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, connections
- connections [SQL Server], SQL Server Agent service
ms.assetid: 28b6178b-0a9e-4f2c-8562-7a62d2d2a285
author: stevestein
ms.author: sstein
ms.openlocfilehash: 686e7026495c827101b279ee779db0e30852bb49
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85067590"
---
# <a name="set-the-sql-server-connection-for-the-sql-server-agent-service-sql-server-management-studio"></a>Set the SQL Server Connection for the SQL Server Agent Service (SQL Server Management Studio)
  En este tema se describe cómo establecer la conexión entre el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y el [!INCLUDE[ssDE](../../includes/ssde-md.md)] en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. El servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede conectarse a una instancia local de SQL Server mediante Autenticación de Windows.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para establecer la conexión de SQL Server para el Agente SQL Server, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitaciones y restricciones  
  
-   El Explorador de objetos solo muestra el nodo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si se tiene permiso para usarlo.  
  
-   A partir de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no admite la autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Esta opción solo está disponible al administrar una versión anterior de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Para realizar sus funciones, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe configurarse de modo que use las credenciales de una cuenta que sea miembro del rol fijo de servidor **sysadmin** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La cuenta debe tener los siguientes permisos de Windows:  
  
-   Iniciar sesión como servicio (SeServiceLogonRight)  
  
-   Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)  
  
-   Omitir la comprobación transversal (SeChangeNotifyPrivilege)  
  
-   Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaPrivilege)  
  
 Para obtener más información acerca de los permisos de Windows necesarios para la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta de servicio del agente, consulte [seleccionar una cuenta para el servicio de Agente SQL Server](select-an-account-for-the-sql-server-agent-service.md) y [configurar los permisos y las cuentas de servicio de Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-set-the-sql-server-connection"></a>Para establecer la conexión a SQL Server  
  
1.  En el **Explorador de objetos**, haga clic en el signo más para expandir el servidor que desea configurar con una conexión con el servicio del Agente SQL Server.  
  
2.  Haga clic con el botón derecho en **Agente SQL Server** y seleccione **propiedades**.  
  
3.  En el cuadro de diálogo **Propiedades de Agente SQL Server**, en **Seleccionar una página**, haga clic en **Conexión**.  
  
4.  En **Conexión de SQL Server**, seleccione **Usar autenticación de Windows** para que el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se conecte a una instancia del [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssDE](../../includes/ssde-md.md)] mediante la autenticación de [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows. Las conexiones a las bases de datos de [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] y versiones posteriores requieren la autenticación de Windows.  
  
  
