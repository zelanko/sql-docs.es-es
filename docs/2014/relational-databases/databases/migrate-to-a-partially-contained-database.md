---
title: Migración a una base de datos parcialmente independiente | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- contained database, migrating to
ms.assetid: 90faac38-f79e-496d-b589-e8b2fe01c562
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7cf0720e920c11270ff2ca6c3c016fc853c2749c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/02/2018
ms.locfileid: "48176455"
---
# <a name="migrate-to-a-partially-contained-database"></a>Migrate to a Partially Contained Database
  En este tema se describe cómo preparar el cambio al modelo de base de datos parcialmente independiente y, a continuación, se proporcionan los pasos de migración.  
  
 **En este tema:**  
  
-   [Preparar la migración de una base de datos](#prepare)  
  
-   [Habilitar bases de datos independientes](#enable)  
  
-   [Convertir una base de datos en parcialmente independiente](#convert)  
  
-   [Migrar usuarios a usuarios de base de datos independiente](#users)  
  
##  <a name="prepare"></a> Preparar la migración de una base de datos  
 Revise los siguientes aspectos cuando vaya a migrar una base de datos al modelo de base de datos parcialmente independiente.  
  
-   Debe entender el modelo de base de datos parcialmente independiente. Para más información, consulte [Contained Databases](contained-databases.md).  
  
-   Debe conocer los riesgos que son exclusivos de las bases de datos parcialmente independientes. Para más información, vea [Security Best Practices with Contained Databases](security-best-practices-with-contained-databases.md).  
  
-   Las bases de datos independientes no admiten la replicación, la captura de datos modificados ni el seguimiento de cambios. Asegúrese de que la base de datos no utiliza estas características.  
  
-   Revise la lista de características de base de datos que se modifican en las bases de datos parcialmente independientes. Para obtener más información, vea [Características modificadas &#40;base de datos independiente&#41;](modified-features-contained-database.md).  
  
-   Consulte [sys.dm_db_uncontained_entities &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql) para encontrar objetos o características sin contención en la base de datos. Para obtener más información, vea:  
  
-   Supervise el XEvent **database_uncontained_usage** para ver cuándo se usan características sin contención.  
  
##  <a name="enable"></a> Habilitar bases de datos independientes  
 Las bases de datos independientes deben estar habilitadas en la instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]para poder crear bases de datos independientes.  
  
### <a name="enabling-contained-databases-using-transact-sql"></a>Habilitar las bases de datos independientes mediante Transact-SQL  
 En el siguiente ejemplo se habilitan las bases de datos independientes en la instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
```tsql  
sp_configure 'contained database authentication', 1;  
GO  
RECONFIGURE ;  
GO  
```  
  
#### <a name="enabling-contained-databases-using-management-studio"></a>Habilitar las bases de datos independientes mediante Management Studio  
 En el siguiente ejemplo se habilitan las bases de datos independientes en la instancia de [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)].  
  
1.  En el Explorador de objetos, haga clic con el botón derecho en el nombre del servidor y, después, haga clic en **Propiedades**.  
  
2.  En la página **Avanzadas** , en la sección **Contención** , establezca la opción **Habilitar bases de datos independientes** en **Verdadero**.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="convert"></a> Convertir una base de datos en parcialmente independiente  
 Una base de datos se convierte en base de datos independiente cambiando la **CONTAINMENT** opción.  
  
### <a name="converting-a-database-to-partially-contained-using-transact-sql"></a>Convertir una base de datos en parcialmente independiente mediante Transact-SQL  
 En el siguiente ejemplo se convierte en parcialmente independiente una base de datos denominada `Accounting` .  
  
```tsql  
USE [master]  
GO  
ALTER DATABASE [Accounting] SET CONTAINMENT = PARTIAL  
GO  
```  
  
### <a name="converting-a-database-to-partially-contained-using-management-studio"></a>Convertir una base de datos en parcialmente independiente mediante Management Studio  
 En el siguiente ejemplo se convierte una base de datos en una base de datos parcialmente independiente.  
  
1.  En el Explorador de objetos, expanda **Bases de datos**, haga clic con el botón derecho en la base de datos que quiera convertir y, después, haga clic en **Propiedades**.  
  
2.  En la página **Opciones** , cambie la opción **Tipo de contención** a **Parcial**.  
  
3.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
##  <a name="users"></a> Migrar usuarios a usuarios de base de datos independiente  
 En el siguiente ejemplo, se realiza la migración de todos los usuarios basados en inicio de sesión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a usuarios de base de datos independiente con contraseñas. En el ejemplo se excluyen los inicios de sesión que no están habilitados. El ejemplo se debe ejecutar en la base de datos independiente.  
  
```tsql  
DECLARE @username sysname ;  
DECLARE user_cursor CURSOR  
    FOR   
        SELECT dp.name   
        FROM sys.database_principals AS dp  
        JOIN sys.server_principals AS sp   
        ON dp.sid = sp.sid  
        WHERE dp.authentication_type = 1 AND sp.is_disabled = 0;  
OPEN user_cursor  
FETCH NEXT FROM user_cursor INTO @username  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
        EXECUTE sp_migrate_user_to_contained   
        @username = @username,  
        @rename = N'keep_name',  
        @disablelogin = N'disable_login';  
    FETCH NEXT FROM user_cursor INTO @username  
    END  
CLOSE user_cursor ;  
DEALLOCATE user_cursor ;  
```  
  
## <a name="see-also"></a>Vea también  
 [Contained Databases](contained-databases.md)   
 [sp_migrate_user_to_contained &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-migrate-user-to-contained-transact-sql)   
 [sys.dm_db_uncontained_entities &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-uncontained-entities-transact-sql)  
  
  
