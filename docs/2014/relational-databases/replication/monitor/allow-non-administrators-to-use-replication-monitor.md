---
title: Permitir el uso del Monitor de replicación a los usuarios que no son administradores | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor, non-administrators access
ms.assetid: 1cf21d9e-831d-41a1-a5a0-83ff6d22fa86
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9e8f03d12d3ac1695d4f6d000c8eab89a42004fd
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/25/2020
ms.locfileid: "62667393"
---
# <a name="allow-non-administrators-to-use-replication-monitor"></a>Permitir el uso del Monitor de replicación a los usuarios que no son administradores
  En este tema se describe cómo permitir a los usuarios que no son administradores que usen el Monitor de replicación en [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../../includes/tsql-md.md)]. El Monitor de replicación solamente pueden utilizarlo usuarios que son miembros de los siguientes roles:  
  
-   El rol fijo de servidor **sysadmin** .  
  
     Estos usuarios pueden supervisar la replicación y tener control total sobre los cambios en las propiedades de la replicación, como programaciones del agente, perfiles del agente, etc.  
  
-   El `replmonitor` rol de base de datos en la base de datos de distribución.  
  
     Estos usuarios pueden supervisar la replicación, pero no pueden cambiar ninguna de las propiedades de la replicación.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Seguridad](#Security)  
  
-   **Para permitir el uso del Monitor de replicación a los usuarios que no son administradores, mediante:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 Para permitir el uso del monitor de replicación a los usuarios que no son administradores, un miembro del rol fijo de servidor **sysadmin** debe agregar el usuario a la base de datos `replmonitor` de distribución y asignar ese usuario al rol.  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-allow-non-administrators-to-use-replication-monitor"></a>Para permitir el uso del Monitor de replicación a los usuarios que no son administradores  
  
1.  En [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], conéctese al distribuidor y, a continuación, expanda el nodo de servidor.  
  
2.  Expanda **Bases de datos**, expanda **Bases de datos del sistema**y, a continuación, expanda la base de datos de distribución (denominada, de forma predeterminada, **distribución** ).  
  
3.  Expanda **Seguridad**, haga clic con el botón secundario en **Usuarios**y, a continuación, haga clic en **Nuevo usuario**.  
  
4.  Escriba un nombre de usuario e inicie la sesión del usuario.  
  
5.  Seleccione un esquema predeterminado de `replmonitor`.  
  
6.  Active la `replmonitor` casilla de la cuadrícula **pertenencia al rol** de la base de datos.  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-add-a-user-to-the-replmonitor-fixed-database-role"></a>Para agregar un usuario al rol fijo de base de datos replmonitor  
  
1.  En cualquier base de datos de distribución, ejecute [sp_helpuser &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpuser-transact-sql). Si el usuario no aparece en `UserName` el conjunto de resultados, se debe conceder al usuario acceso a la base de datos de distribución mediante la instrucción [Create User &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-user-transact-sql) .  
  
2.  En el distribuidor de la base de datos de distribución, ejecute [sp_helprolemember &#40;&#41;de Transact-SQL ](/sql/relational-databases/system-stored-procedures/sp-helprolemember-transact-sql), especificando un valor de `replmonitor` para el **@rolename** parámetro. Si el usuario aparece en `MemberName` el conjunto de resultados, el usuario ya pertenece a este rol.  
  
3.  Si el usuario no pertenece al `replmonitor` rol, ejecute [sp_addrolemember &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql) en el distribuidor de la base de datos de distribución. Especifique un valor de `replmonitor` para **@rolename** y el nombre del usuario de la base de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] datos o el inicio de **@membername**sesión de Windows que se va a agregar para.  
  
#### <a name="to-remove-a-user-from-the-replmonitor-fixed-database-role"></a>Para quitar un usuario desde el rol fijo de base de datos replmonitor  
  
1.  Para comprobar que el usuario `replmonitor` pertenece al rol, ejecute [sp_helprolemember &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-helprolemember-transact-sql) en el distribuidor de la base de datos de distribución y especifique un `replmonitor` valor **@rolename**de para. Si el usuario no aparece en `MemberName` en el conjunto de resultados, el usuario no pertenece actualmente a este rol.  
  
2.  Si el usuario pertenece al `replmonitor` rol, ejecute [sp_droprolemember &#40;&#41;de Transact-SQL](/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql) en la base de datos de distribución del distribuidor. Especifique un valor de `replmonitor` para **@rolename** y el nombre del usuario de la base de datos o el inicio de **@membername**sesión de Windows que se va a quitar para.  
  
  
