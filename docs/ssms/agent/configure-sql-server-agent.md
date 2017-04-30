---
title: Configurar el Agente SQL Server | Microsoft Docs
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
- SQL Server Agent, configuring
- accounts [SQL Server], SQL Server Agent
- SQL Server Agent, permissions
- security [SQL Server], SQL Server Agent
ms.assetid: 2e361a62-9e92-4fcd-80d7-d6960f127900
caps.latest.revision: 5
author: stevestein
ms.author: sstein
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e433dd732e153213da84aa9a1444f9255cc5a4d5
ms.lasthandoff: 04/11/2017

---
# <a name="configure-sql-server-agent"></a>Configurar el Agente SQL Server
En este tema se describe cómo especificar algunas opciones de configuración para el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. El conjunto completo de opciones de configuración del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] solo está disponible dentro de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)], Objetos de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] (SMO) o los procedimientos almacenados del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] .  
  
**En este tema**  
  
-   **Antes de empezar:**  
  
    [Limitaciones y restricciones](#Restrictions)  
  
    [Seguridad](#Security)  
  
-   [Para configurar el Agente SQL Server](#SSMSProcedure)  
  
## <a name="BeforeYouBegin"></a>Antes de comenzar  
  
### <a name="Restrictions"></a>Limitaciones y restricciones  
  
-   Haga clic en el **Agente SQL Server** en el Explorador de objetos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)] para administrar trabajos, operadores, alertas y el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] . No obstante, el Explorador de objetos solo muestra el nodo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] si tiene permiso para utilizarlo.  
  
-   El reinicio automático no debe habilitarse para el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] o el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] en las instancias de clúster de conmutación por error.  
  
### <a name="Security"></a>Seguridad  
  
#### <a name="Permissions"></a>Permissions  
Para realizar sus funciones, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] debe configurarse de modo que use las credenciales de una cuenta que sea miembro del rol fijo de servidor **sysadmin** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)]. La cuenta debe tener los siguientes permisos de Windows:  
  
-   Iniciar sesión como servicio (SeServiceLogonRight)  
  
-   Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)  
  
-   Omitir la comprobación transversal (SeChangeNotifyPrivilege)  
  
-   Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaPrivilege)  
  
Para más información sobre los permisos de Windows necesarios para la cuenta de servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] , consulte [Seleccionar una cuenta para el servicio del Agente SQL Server](../../ssms/agent/select-an-account-for-the-sql-server-agent-service.md) y [Configurar cuentas de servicio de Windows](http://msdn.microsoft.com/en-us/309b9dac-0b3a-4617-85ef-c4519ce9d014).  
  
## <a name="SSMSProcedure"></a>Usar SQL Server Management Studio  
  
#### <a name="to-configure-sql-server-agent"></a>Para configurar el Agente SQL Server  
  
1.  Haga clic en el botón **Inicio** y después, en el menú **Inicio**  , haga clic en **Panel de control**.  
  
2.  En el Panel de control, haga clic en **Sistema y seguridad**, haga clic en **Herramientas administrativas**y seleccione **Directiva de seguridad local**.  
  
3.  En Directiva de seguridad local, haga clic en las comillas angulares para expandir la carpeta **Directivas locales** y, a continuación, haga clic en la carpeta **Asignación de derechos de usuario** .  
  
4.  Haga clic con el botón derecho en un permiso que desee configurar para su uso con [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] y seleccione **Propiedades**.  
  
5.  En el cuadro de diálogo de propiedades del permiso, compruebe que se muestra la cuenta con la que se ejecuta el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] . Si no aparece, haga clic en **Agregar usuario o grupo**, escriba la cuenta bajo la que se ejecuta el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] en el cuadro de diálogo **Seleccionar usuarios, equipos, cuentas de servicio o grupos** y, a continuación, haga clic en **Aceptar**.  
  
6.  Repita el proceso para cada permiso que desee agregar para el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] . Cuando termine, haga clic en **Aceptar**.  
  

