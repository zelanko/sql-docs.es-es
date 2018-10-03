---
title: Permitir el uso del Monitor de replicación a los usuarios que no son administradores | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- Replication Monitor, non-administrators access
ms.assetid: 1cf21d9e-831d-41a1-a5a0-83ff6d22fa86
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e0c880bbb7c21ec7d0a766f8bdf0876d4962d10b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219855"
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
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permissions  
 Para permitir que los usuarios utilizar el Monitor de replicación, un miembro de la **sysadmin** debe agregar el usuario a la base de datos de distribución y asignar ese usuario al rol fijo de servidor el `replmonitor` rol.  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-allow-non-administrators-to-use-replication-monitor"></a>Para permitir el uso del Monitor de replicación a los usuarios que no son administradores  
  
1.  En [!INCLUDE[ssManStudioFull](../../../includes/ssmanstudiofull-md.md)], conéctese al distribuidor y, a continuación, expanda el nodo de servidor.  
  
2.  Expanda **Bases de datos**, expanda **Bases de datos del sistema**y, a continuación, expanda la base de datos de distribución (denominada, de forma predeterminada, **distribución** ).  
  
3.  Expanda **Seguridad**, haga clic con el botón secundario en **Usuarios**y, a continuación, haga clic en **Nuevo usuario**.  
  
4.  Escriba un nombre de usuario e inicie la sesión del usuario.  
  
5.  Seleccione un esquema predeterminado de `replmonitor`.  
  
6.  Seleccione el `replmonitor` casilla de verificación en la **pertenencia al rol de base de datos** cuadrícula.  
  
7.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-add-a-user-to-the-replmonitor-fixed-database-role"></a>Para agregar un usuario al rol fijo de base de datos replmonitor  
  
1.  En cualquier base de datos de distribución, ejecute [sp_helpuser &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpuser-transact-sql). Si el usuario no aparece en `UserName` en el conjunto de resultados, el usuario debe tener acceso a la base de datos de distribución mediante el [CREATE USER &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-user-transact-sql) instrucción.  
  
2.  En el distribuidor en la base de datos de distribución, ejecute [sp_helprolemember &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helprolemember-transact-sql), especificando un valor de `replmonitor` para el **@rolename** parámetro. Si el usuario aparece en `MemberName` en el conjunto de resultados, el usuario ya pertenece a este rol.  
  
3.  Si el usuario no pertenece a la `replmonitor` rol, ejecute [sp_addrolemember &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-addrolemember-transact-sql) en el distribuidor de la base de datos de distribución. Especifique un valor de `replmonitor` para **@rolename** y el nombre del usuario de base de datos o el [!INCLUDE[msCoName](../../../includes/msconame-md.md)] inicio de sesión de Windows que se agrega para **@membername**.  
  
#### <a name="to-remove-a-user-from-the-replmonitor-fixed-database-role"></a>Para quitar un usuario desde el rol fijo de base de datos replmonitor  
  
1.  Para comprobar que el usuario pertenece a la `replmonitor` rol, ejecute [sp_helprolemember &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-helprolemember-transact-sql) en el distribuidor de la base de datos de distribución y especifique un valor de `replmonitor` para **@rolename**. Si el usuario no aparece en `MemberName` en el conjunto de resultados, el usuario no pertenece actualmente a este rol.  
  
2.  Si el usuario pertenece a la `replmonitor` rol, ejecute [sp_droprolemember &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sp-droprolemember-transact-sql) en el distribuidor de la base de datos de distribución. Especifique un valor de `replmonitor` para **@rolename** y el nombre de usuario de la base de datos o el inicio de sesión de Windows que se quita de **@membername**.  
  
  
