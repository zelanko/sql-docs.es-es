---
title: "Permitir el uso del Monitor de replicación a los usuarios que no son administradores | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: replication
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: Replication Monitor, non-administrators access
ms.assetid: 1cf21d9e-831d-41a1-a5a0-83ff6d22fa86
caps.latest.revision: "36"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6f4bca1cbe7dbf8b77a6cbf6855c5b874035e541
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="allow-non-administrators-to-use-replication-monitor"></a>Permitir el uso del Monitor de replicación a los usuarios que no son administradores
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] En este tema se describe cómo permitir a los usuarios que no son administradores que usen el Monitor de replicación en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. El Monitor de replicación solamente pueden utilizarlo usuarios que son miembros de los siguientes roles:  
  
-   El rol fijo de servidor **sysadmin** .  
  
     Estos usuarios pueden supervisar la replicación y tener control total sobre los cambios en las propiedades de la replicación, como programaciones del agente, perfiles del agente, etc.  
  
-   El rol de base de datos **replmonitor** en la base de datos de distribución.  
  
     Estos usuarios pueden supervisar la replicación, pero no pueden cambiar ninguna de las propiedades de la replicación.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para permitir el uso del Monitor de replicación a los usuarios que no son administradores, mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Para permitir el uso del Monitor de replicación a los usuarios que no son administradores, un miembro del rol fijo de servidor **sysadmin** debe agregar al usuario a la base de datos de distribución y asignar ese usuario al rol **replmonitor** .  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-allow-non-administrators-to-use-replication-monitor"></a>Para permitir el uso del Monitor de replicación a los usuarios que no son administradores  
  
1.  En [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], conéctese al distribuidor y, a continuación, expanda el nodo de servidor.  
  
2.  Expanda **Bases de datos**, expanda **Bases de datos del sistema**y, a continuación, expanda la base de datos de distribución (denominada, de forma predeterminada, **distribución** ).  
  
3.  Expanda **Seguridad**, haga clic con el botón secundario en **Usuarios**y, a continuación, haga clic en **Nuevo usuario**.  
  
4.  Escriba un nombre de usuario e inicie la sesión del usuario.  
  
5.  Seleccione un esquema predeterminado de **replmonitor**.  
  
6.  Active la casilla **replmonitor** en la cuadrícula **Pertenencia al rol de la base de datos** .  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-add-a-user-to-the-replmonitor-fixed-database-role"></a>Para agregar un usuario al rol fijo de base de datos replmonitor  
  
1.  En cualquier base de datos de distribución, ejecute [sp_helpuser &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helpuser-transact-sql.md). Si el usuario no aparece en **UserName** en el conjunto de resultados, se le debe conceder acceso a la base de datos de distribución mediante la instrucción [CREATE USER &#40;Transact-SQL&#41;](../../../t-sql/statements/create-user-transact-sql.md).  
  
2.  En la base de datos de distribución del distribuidor, ejecute [sp_helprolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md) y especifique el valor de **replmonitor** para el parámetro **@rolename**. Si el usuario aparece en **MemberName** en el conjunto de resultados, el usuario ya pertenece a este rol.  
  
3.  Si el usuario no pertenece al rol **replmonitor**, ejecute [sp_addrolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-addrolemember-transact-sql.md) en la base de datos de distribución del distribuidor. Especifique un valor de **replmonitor** para **@rolename** y el nombre del usuario de la base de datos o el inicio de sesión de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Windows que se agrega para **@membername**.  
  
#### <a name="to-remove-a-user-from-the-replmonitor-fixed-database-role"></a>Para quitar un usuario desde el rol fijo de base de datos replmonitor  
  
1.  Para comprobar que el usuario pertenece al rol **replmonitor**, ejecute [sp_helprolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-helprolemember-transact-sql.md) en la base de datos de distribución del distribuidor y especifique un valor de **replmonitor** para **@rolename**. Si el usuario no aparece en **MemberName** en el conjunto de resultados, el usuario no pertenece actualmente a este rol.  
  
2.  Si el usuario pertenece al rol **replmonitor**, ejecute [sp_droprolemember &#40;Transact-SQL&#41;](../../../relational-databases/system-stored-procedures/sp-droprolemember-transact-sql.md) en la base de datos de distribución del distribuidor. Especifique un valor de **replmonitor** para **@rolename** y el nombre del usuario de la base de datos o el inicio de sesión de Windows que se quita de **@membername**.  
  
  
