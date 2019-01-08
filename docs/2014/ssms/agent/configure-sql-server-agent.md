---
title: Configurar el Agente SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent, configuring
- accounts [SQL Server], SQL Server Agent
- SQL Server Agent, permissions
- security [SQL Server], SQL Server Agent
ms.assetid: 2e361a62-9e92-4fcd-80d7-d6960f127900
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 0e7c8cb2230a7b6923514f0928b844f72c216d58
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52796127"
---
# <a name="configure-sql-server-agent"></a>Configurar el Agente SQL Server
  En este tema se describe cómo especificar algunas opciones de configuración para el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durante la instalación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El conjunto completo de opciones de configuración del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] solo está disponible dentro de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], Objetos de administración de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (SMO) o los procedimientos almacenados del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   [Para configurar el Agente SQL Server](#SSMSProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Haga clic en el **Agente SQL Server** en el Explorador de objetos de [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para administrar trabajos, operadores, alertas y el servicio del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . No obstante, el Explorador de objetos solo muestra el nodo del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] si tiene permiso para utilizarlo.  
  
-   El reinicio automático no debe habilitarse para el servicio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o el servicio Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en las instancias de clúster de conmutación por error.  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Para realizar sus funciones, el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] debe configurarse de modo que use las credenciales de una cuenta que sea miembro del rol fijo de servidor **sysadmin** en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. La cuenta debe tener los siguientes permisos de Windows:  
  
-   Iniciar sesión como servicio (SeServiceLogonRight)  
  
-   Reemplazar un token de nivel de proceso (SeAssignPrimaryTokenPrivilege)  
  
-   Omitir la comprobación transversal (SeChangeNotifyPrivilege)  
  
-   Ajustar las cuotas de memoria de un proceso (SeIncreaseQuotaPrivilege)  
  
 Para obtener más información sobre los permisos de Windows necesarios para la [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cuenta de servicio del agente, consulte [seleccionar una cuenta para el servicio Agente SQL Server](select-an-account-for-the-sql-server-agent-service.md) y [configurar cuentas de servicio de Windows y Permisos](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md).  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-configure-sql-server-agent"></a>Para configurar el Agente SQL Server  
  
1.  Haga clic en el botón **Inicio** y después, en el menú **Inicio**  , haga clic en **Panel de control**.  
  
2.  En el Panel de control, haga clic en **Sistema y seguridad**, haga clic en **Herramientas administrativas**y seleccione **Directiva de seguridad local**.  
  
3.  En Directiva de seguridad local, haga clic en las comillas angulares para expandir la carpeta **Directivas locales** y, a continuación, haga clic en la carpeta **Asignación de derechos de usuario** .  
  
4.  Haga clic con el botón derecho en un permiso que desee configurar para su uso con [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y seleccione **Propiedades**.  
  
5.  En el cuadro de diálogo de propiedades del permiso, compruebe que se muestra la cuenta con la que se ejecuta el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Si no aparece, haga clic en **Agregar usuario o grupo**, escriba la cuenta bajo la que se ejecuta el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el cuadro de diálogo **Seleccionar usuarios, equipos, cuentas de servicio o grupos** y, a continuación, haga clic en **Aceptar**.  
  
6.  Repita el proceso para cada permiso que desee agregar para el Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Cuando termine, haga clic en **Aceptar**.  
  
  
