---
title: Configurar un usuario para crear y administrar trabajos del Agente SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, user configuration
- jobs [SQL Server Agent], user configuration
- SQLAgentUserRole database role
- proxy accounts [SQL Server Agent]
ms.assetid: 67897e3e-b7d0-43dd-a2e2-2840ec4dd1ef
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a62f6c2e1ef86a6fcd5e532b2ef413d8142698e6
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/03/2018
ms.locfileid: "52796147"
---
# <a name="configure-a-user-to-create-and-manage-sql-server-agent-jobs"></a>Configurar un usuario para crear y administrar trabajos del Agente SQL Server
  En este tema se describe cómo configurar un usuario para que cree o ejecute trabajos del Agente [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   **Antes de empezar:**  [Seguridad](#Security)  
  
-   **Para configurar un usuario para crear y administrar trabajos del Agente SQL Server, utilizando:**  [SQL Server Management Studio](#SSMS)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
 Para configurar un usuario para crear o ejecutar [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] trabajos del agente, primero debe agregar un rol msdb o inicio de sesión de SQL Server existente a uno de los siguientes [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente fijas de base de datos en la base de datos msdb: SQLAgentUserRole, SQLAgentReaderRole o SQLAgentOperatorRole.  
  
 De forma predeterminada, los miembros de estos roles de la base de datos pueden crear sus propios pasos de trabajo que se ejecutan como ellos mismos. Si estos usuarios no administrativos desean ejecutar trabajos que ejecuten otros tipos de pasos de trabajo (por ejemplo, paquetes [!INCLUDE[ssIS](../../includes/ssis-md.md)] ), necesitarán tener acceso a una cuenta de proxy. Todos los miembros del rol fijo de servidor sysadmin tienen permiso para crear, modificar o eliminar cuentas de proxy. Para más información sobre los permisos asociados con estos roles fijos de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , consulte [Roles fijos de base de datos del Agente SQL Server](sql-server-agent-fixed-database-roles.md).  
  
####  <a name="Permissions"></a> Permissions  
 Para obtener información detallada, vea [Implementar la seguridad del Agente SQL Server](implement-sql-server-agent-security.md).  
  
##  <a name="SSMS"></a> Usar SQL Server Management Studio  
 **Para agregar un inicio de sesión de SQL o un rol msdb a un rol fijo de base de datos del Agente SQL Server**  
  
1.  En el **Explorador de objetos**, expanda un servidor.  
  
2.  Expanda **Seguridad**y, a continuación, **Inicios de sesión**.  
  
3.  Haga clic con el botón derecho en el inicio de sesión que desee agregar a un rol fijo de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y seleccione **Propiedades**.  
  
4.  En el **User Mapping** página de la **propiedades de inicio de sesión** cuadro de diálogo, seleccione la fila que contiene `msdb`.  
  
5.  En **Miembros del rol de base de datos para: msdb**, active el rol fijo de base de datos del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] adecuado.  
  
 **Para configurar una cuenta de proxy para crear y administrar pasos de trabajo del Agente SQL Server**  
  
1.  En el **Explorador de objetos**, expanda un servidor.  
  
2.  Expanda **Agente SQL Server**.  
  
3.  Haga clic con el botón derecho en **Servidores proxy** y seleccione **Nuevo proxy**.  
  
4.  En la página **General** del cuadro de diálogo **Nueva cuenta de proxy** , especifique el nombre del proxy, el nombre de credencial y la descripción del nuevo proxy. Tenga en cuenta que debe crear una credencial antes de crear un proxy del Agente SQL Server. Para obtener más información acerca de cómo crear una credencial, vea [crear una credencial](../../relational-databases/security/authentication-access/create-a-credential.md) y [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql).  
  
5.  Seleccione los subsistemas correspondientes para este proxy.  
  
6.  En la página **Entidades de seguridad** , agregue o quite inicios de sesión o roles para conceder o quitar el acceso a la cuenta de proxy.  
  
## <a name="see-also"></a>Vea también  
 [Implementar la seguridad del Agente SQL Server](implement-sql-server-agent-security.md)  
  
  
