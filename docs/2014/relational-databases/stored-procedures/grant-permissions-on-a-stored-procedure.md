---
title: Conceder permisos para un procedimiento almacenado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], permissions
ms.assetid: a7d15816-a788-4099-ad91-dc4b26618299
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 47b8e4b87ab3150ae7bf67d3c3a2f9c5e0732294
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/26/2020
ms.locfileid: "63015592"
---
# <a name="grant-permissions-on-a-stored-procedure"></a>Conceder permisos para un procedimiento almacenado
  En este tema se describe cómo conceder permisos para un procedimiento almacenado en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)]. Se pueden conceder permisos a un usuario, un rol de base de datos o un rol de aplicación existentes en la base de datos.  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para conceder permisos para un procedimiento almacenado, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitaciones y restricciones  
  
-   No se puede usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para conceder permisos para procedimientos del sistema o funciones del sistema. En su lugar, use [GRANT (permisos de objeto de Transact-SQL)](/sql/t-sql/statements/grant-object-permissions-transact-sql) .  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permisos  
 El otorgante del permiso (o la entidad de seguridad especificada con la opción AS) debe tener el permiso con GRANT OPTION, o un permiso superior que implique el permiso que se va a conceder. Requiere el permiso ALTER en el esquema al que pertenece el procedimiento o el permiso CONTROL en el procedimiento. Para obtener más información, vea [Permisos de objeto GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-object-permissions-transact-sql).  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-grant-permissions-on-a-stored-procedure"></a>Para conceder permisos para un procedimiento almacenado  
  
1.  En el Explorador de objetos, conéctese a una instancia de [!INCLUDE[ssDE](../../../includes/ssde-md.md)] y expándala.  
  
2.  Expanda **Bases de datos**, expanda la base de datos a la que pertenece el procedimiento y, a continuación, expanda **Programación**.  
  
3.  Expanda **Procedimientos almacenados**, haga clic con el botón derecho en el procedimiento en el que quiera conceder permisos y, luego, haga clic en **Propiedades**.  
  
4.  En **Propiedades del procedimiento almacenado**, seleccione la página **Permisos** .  
  
5.  Para conceder permisos a un usuario, un rol de base de datos o un rol de aplicación, haga clic en **Buscar**.  
  
6.  En **Seleccionar usuarios o roles**, haga clic en **Tipos de objeto** para agregar o borrar los usuarios y los roles que desee.  
  
7.  Haga clic en **Examinar** para mostrar la lista de usuarios o de roles. Seleccione los usuarios o los roles a los que deben concederse los permisos.  
  
8.  En la cuadrícula **Permisos explícitos** , seleccione los permisos que desea conceder al rol o al usuario especificados. Para obtener una descripción de los permisos, vea [Permisos &#40;motor de base de datos&#41;](../security/permissions-database-engine.md).  
  
 Al seleccionar **Conceder** , se indica que se concederá el permiso especificado al receptor. Al seleccionar **Grant With** , se indica que el receptor también podrá conceder el permiso especificado a otras entidades de seguridad.  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-grant-permissions-on-a-stored-procedure"></a>Para conceder permisos para un procedimiento almacenado  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se concede el permiso `EXECUTE` para el procedimiento almacenado `HumanResources.uspUpdateEmployeeHireInfo` a un rol de aplicación denominado `Recruiting11`.  
  
```sql  
USE AdventureWorks2012;   
GRANT EXECUTE ON OBJECT::HumanResources.uspUpdateEmployeeHireInfo  
    TO Recruiting11;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [sys.fn_builtin_permissions &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-builtin-permissions-transact-sql)   
 [Permisos de objeto GRANT &#40;Transact-SQL&#41;](/sql/t-sql/statements/grant-object-permissions-transact-sql)   
 [Crear un procedimiento almacenado](../stored-procedures/create-a-stored-procedure.md)   
 [Modificar un procedimiento almacenado](modify-a-stored-procedure.md)   
 [Eliminar un procedimiento almacenado](../stored-procedures/delete-a-stored-procedure.md)   
 [Cambiar el nombre de un procedimiento almacenado](rename-a-stored-procedure.md)  
  
  
