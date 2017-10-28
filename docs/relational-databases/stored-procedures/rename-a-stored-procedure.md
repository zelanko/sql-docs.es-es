---
title: Cambio de nombre de un procedimiento almacenado | Microsoft Docs
ms.custom: 
ms.date: 07/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-stored-Procs
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- stored procedures [SQL Server], renaming
- renaming stored procedures
ms.assetid: 5d2e4c68-7e0b-4405-8919-f5b203e46770
caps.latest.revision: 23
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: HT
ms.sourcegitcommit: 47182ebd082dfae0963d761e54c4045be927d627
ms.openlocfilehash: 1d0ddb568fd162f4be42234607b5b8484cb89f60
ms.contentlocale: es-es
ms.lasthandoff: 07/31/2017

---
# <a name="rename-a-stored-procedure"></a>Cambiar el nombre de un procedimiento almacenado
  En este tema se describe cómo cambiar el nombre de un procedimiento almacenado [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Seguridad](#Security)  
  
-   **Para cambiar el nombre de un procedimiento almacenado, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Los nombres de los procedimientos se deben ajustar a las reglas para los [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
-   Cambiar el nombre de un procedimiento almacenado retiene `object_id` y todos los permisos asignados de forma específica al procedimiento. Al quitar y volver a crear el objeto se crea un nuevo `object_id` y se quita cualquier permiso asignado de forma específica al procedimiento.

-   Al cambiar el nombre de un procedimiento almacenado no se cambia el nombre del objeto correspondiente en la columna de definición de la vista de catálogo **sys.sql_modules**. Para ello, debe quitar el procedimiento almacenado y volver a crearlo con su nuevo nombre.  

-   El hecho de cambiar el nombre o la definición de un procedimiento puede provocar errores en los objetos dependientes si no se actualizan para reflejar los cambios realizados en el procedimiento. Para obtener más información, vea [Ver las dependencias de un procedimiento almacenado](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 CREATE PROCEDURE  
 Necesita el permiso CREATE PROCEDURE en la base de datos y el permiso ALTER en el esquema en el que se va a crear el procedimiento o la pertenencia al rol fijo de base de datos **db_ddladmin** .  
  
 ALTER PROCEDURE  
 Necesita el permiso ALTER en el procedimiento o la pertenencia al rol fijo de base de datos **db_ddladmin** .  
  
##  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
  
#### <a name="to-rename-a-stored-procedure"></a>Para cambiar el nombre de un procedimiento almacenado  
  
1.  En el Explorador de objetos, conéctese a una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y expándala.  
2.  Expanda **Bases de datos**, expanda la base de datos a la que pertenece el procedimiento y, a continuación, expanda **Programación**.  
3.  [Cómo ver las dependencias de un procedimiento almacenado (SQL Server Management Studio)](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md).  
4.  Expanda **Procedimientos almacenados**, haga clic con el botón derecho en el procedimiento cuyo nombre quiere cambiar y, después, haga clic en **Cambiar nombre**.  
5.  Modifique el nombre del procedimiento.  
6.  Modifique el nombre del procedimiento al que se hace referencia en cualquier objeto dependiente o script.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-rename-a-stored-procedure"></a>Para cambiar el nombre de un procedimiento almacenado  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se muestra cómo cambiar el nombre de un procedimiento quitando el procedimiento y volviendo a crearlo con otro nombre. En el primer ejemplo se crea el procedimiento almacenado `'HumanResources.uspGetAllEmployeesTest`. En el segundo ejemplo se cambia el nombre del procedimiento almacenado a `HumanResources.uspEveryEmployeeTest`.  
  
```sql  
--Create the stored procedure.  
USE AdventureWorks2012;  
GO  

CREATE PROCEDURE HumanResources.uspGetAllEmployeesTest  
AS  
    SET NOCOUNT ON;  
    SELECT LastName, FirstName, Department  
    FROM HumanResources.vEmployeeDepartmentHistory;  
GO  
  
--Rename the stored procedure.  
EXEC sp_rename 'HumanResources.uspGetAllEmployeesTest', 'HumanResources.uspEveryEmployeeTest'; 
```  
  
## <a name="see-also"></a>Vea también  
 [ALTER PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-procedure-transact-sql.md)   
 [CREATE PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/create-procedure-transact-sql.md)   
 [Crear un procedimiento almacenado](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [Modificar un procedimiento almacenado](../../relational-databases/stored-procedures/modify-a-stored-procedure.md)   
 [Eliminar un procedimiento almacenado](../../relational-databases/stored-procedures/delete-a-stored-procedure.md)   
 [Ver la definición de un procedimiento almacenado](../../relational-databases/stored-procedures/view-the-definition-of-a-stored-procedure.md)   
 [Ver las dependencias de un procedimiento almacenado](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)  
  
  

