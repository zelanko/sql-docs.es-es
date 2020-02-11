---
title: Ver las dependencias de un procedimiento almacenado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], dependencies
- displaying stored procedure dependencies
- viewing stored procedure dependencies
ms.assetid: 6ae0a369-1bc7-4ae4-be89-2b483697cd1f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 14f380f510070da1b8fa77f7f5440640ce37452b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62856500"
---
# <a name="view-the-dependencies-of-a-stored-procedure"></a>Ver las dependencias de un procedimiento almacenado
    
##  
  <a name="Top"></a> En este tema se describe cómo ver las dependencias de procedimiento almacenado en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   **Antes de empezar:**  [seguridad](#Security)  
  
-   **Para ver las dependencias de un procedimiento con:**  [SQL Server Management Studio](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Función del sistema: `sys.dm_sql_referencing_entities`  
 Requiere el permiso CONTROL en la entidad a la que se hace referencia y el permiso SELECT en sys.dm_sql_referencing_entities. Cuando la entidad a la que se hace referencia es una función de partición, se requiere el permiso CONTROL en la base de datos. De forma predeterminada, se concede el permiso SELECT a public.  
  
 Función del sistema: `sys.dm_sql_referenced_entities`  
 Requiere el permiso SELECT en sys.dm_sql_referenced_entities y el permiso VIEW DEFINITION en la entidad de referencia. De forma predeterminada, se concede el permiso SELECT a public. Requiere el permiso VIEW DEFINITION en la base de datos o el permiso ALTER DATABASE DDL TRIGGER en la base de datos si la entidad de referencia es un desencadenador DDL de base de datos. Requiere el permiso VIEW ANY DEFINITION en el servidor si la entidad de referencia es un desencadenador DDL de servidor.  
  
 Vista de catálogo de objetos: `sys.sql_expression_dependencies`  
 Necesita el permiso VIEW DEFINITION en la base de datos y el permiso SELECT en sys.sql_expression_dependencies para la base de datos. De forma predeterminada, solo se permite el permiso SELECT a los miembros del rol fijo de base de datos db_owner. Si se conceden los permisos SELECT y VIEW DEFINITION a otro usuario, el receptor puede ver todas las dependencias de la base de datos.  
  
##  <a name="Procedures"></a>Cómo ver las dependencias de un procedimiento almacenado  
 Puede usar cualquiera de los siguientes medios:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
 **Para ver las dependencias de un procedimiento en Explorador de objetos**  
  
1.  En el Explorador de objetos, conéctese a una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y expándala.  
  
2.  Expanda **Bases de datos**, expanda la base de datos a la que pertenece el procedimiento y, a continuación, expanda **Programación**.  
  
3.  Expanda **Procedimientos almacenados**, haga clic con el botón derecho en el procedimiento y, luego, haga clic en **Ver dependencias**.  
  
4.  Examine la lista de objetos que dependen del procedimiento.  
  
5.  Examine la lista de objetos de los cuales depende el procedimiento.  
  
6.  Haga clic en **OK**.  
  
###  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para ver las dependencias de un procedimiento en el editor de consultas**  
  
 Función del sistema: `sys.dm_sql_referencing_entities`  
 Esta función se usa para mostrar los objetos que dependen de un procedimiento.  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] y expándala.  
  
2.  Expanda **Bases de datos**, expanda la base de datos a la que pertenece el procedimiento.  
  
3.  En el menú **Archivo** , haga clic en **Nueva consulta** .  
  
4.  Copie y pegue los ejemplos siguientes en el editor de consultas. El primer ejemplo crea el procedimiento `uspVendorAllInfo` , que devuelve los nombres de todos los proveedores en la base de datos [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] , los productos que suministran, su solvencia y su disponibilidad.  
  
     [!code-sql[ProcedureDDL#CreateProc8](../../snippets/tsql/SQL14/tsql/procedureddl/transact-sql/createproc.sql#createproc8)]  
  
5.  Después de crear el procedimiento, el segundo ejemplo usa la función sys.dm_sql_referencing_entities para mostrar los objetos que dependen del procedimiento.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT referencing_schema_name, referencing_entity_name, referencing_id, referencing_class_desc, is_caller_dependent  
    FROM sys.dm_sql_referencing_entities ('Purchasing.uspVendorAllInfo', 'OBJECT');   
    GO  
  
    ```  
  
 Función del sistema: `sys.dm_sql_referenced_entities`  
 Esta función se usa para mostrar los objetos de los que depende un procedimiento.  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] y expándala.  
  
2.  Expanda **Bases de datos**, expanda la base de datos a la que pertenece el procedimiento.  
  
3.  En el menú **Archivo** , haga clic en **Nueva consulta** .  
  
4.  Copie y pegue los ejemplos siguientes en el editor de consultas. El primer ejemplo crea el procedimiento `uspVendorAllInfo` , que devuelve los nombres de todos los proveedores en la base de datos [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] , los productos que suministran, su solvencia y su disponibilidad.  
  
     [!code-sql[ProcedureDDL#CreateProc8](../../snippets/tsql/SQL14/tsql/procedureddl/transact-sql/createproc.sql#createproc8)]  
  
5.  Después de crear el procedimiento, el segundo ejemplo usa la función sys.dm_sql_referenced_entities para mostrar los objetos de los que depende el procedimiento.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT referenced_schema_name, referenced_entity_name,  
    referenced_minor_name,referenced_minor_id, referenced_class_desc,  
    is_caller_dependent, is_ambiguous  
    FROM sys.dm_sql_referencing_entities ('Purchasing.uspVendorAllInfo', 'OBJECT');  
    GO  
    ```  
  
 Vista de catálogo de objetos: `sys.sql_expression_dependencies`  
 Esta vista se puede usar para mostrar los objetos de los que depende un procedimiento o que dependen de un procedimiento.  
  
 Mostrar los objetos que dependen de un procedimiento.  
 1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] y expándala.  
  
2.  Expanda **Bases de datos**, expanda la base de datos a la que pertenece el procedimiento.  
  
3.  En el menú **Archivo** , haga clic en **Nueva consulta** .  
  
4.  Copie y pegue los ejemplos siguientes en el editor de consultas. El primer ejemplo crea el procedimiento `uspVendorAllInfo` , que devuelve los nombres de todos los proveedores en la base de datos [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] , los productos que suministran, su solvencia y su disponibilidad.  
  
     [!code-sql[ProcedureDDL#CreateProc8](../../snippets/tsql/SQL14/tsql/procedureddl/transact-sql/createproc.sql#createproc8)]  
  
5.  Después de crear el procedimiento, el segundo ejemplo usa la vista sys.sql_expression_dependencies para mostrar los objetos que dependen del procedimiento.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT OBJECT_SCHEMA_NAME ( referencing_id ) AS referencing_schema_name,  
        OBJECT_NAME(referencing_id) AS referencing_entity_name,   
        o.type_desc AS referencing_desciption,   
        COALESCE(COL_NAME(referencing_id, referencing_minor_id), '(n/a)') AS referencing_minor_id,   
        referencing_class_desc, referenced_class_desc,  
        referenced_server_name, referenced_database_name, referenced_schema_name,  
        referenced_entity_name,   
        COALESCE(COL_NAME(referenced_id, referenced_minor_id), '(n/a)') AS referenced_column_name,  
        is_caller_dependent, is_ambiguous  
    FROM sys.sql_expression_dependencies AS sed  
    INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
    WHERE referenced_id = OBJECT_ID(N'Purchasing.uspVendorAllInfo')  
    GO  
    ```  
  
 Mostrar los objetos de los que depende un procedimiento.  
 1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] y expándala.  
  
2.  Expanda **Bases de datos**, expanda la base de datos a la que pertenece el procedimiento.  
  
3.  En el menú **Archivo** , haga clic en **Nueva consulta** .  
  
4.  Copie y pegue los ejemplos siguientes en el editor de consultas. El primer ejemplo crea el procedimiento `uspVendorAllInfo` , que devuelve los nombres de todos los proveedores en la base de datos [!INCLUDE[ssSampleDBCoFull](../../includes/sssampledbcofull-md.md)] , los productos que suministran, su solvencia y su disponibilidad.  
  
     [!code-sql[ProcedureDDL#CreateProc8](../../snippets/tsql/SQL14/tsql/procedureddl/transact-sql/createproc.sql#createproc8)]  
  
5.  Después de crear el procedimiento, el segundo ejemplo usa la vista sys.sql_expression_dependencies para mostrar los objetos de los que depende el procedimiento.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT OBJECT_NAME(referencing_id) AS referencing_entity_name,   
        o.type_desc AS referencing_desciption,   
        COALESCE(COL_NAME(referencing_id, referencing_minor_id), '(n/a)') AS referencing_minor_id,   
        referencing_class_desc, referenced_class_desc,  
        referenced_server_name, referenced_database_name, referenced_schema_name,  
        referenced_entity_name,   
        COALESCE(COL_NAME(referenced_id, referenced_minor_id), '(n/a)') AS referenced_column_name,  
        is_caller_dependent, is_ambiguous  
    FROM sys.sql_expression_dependencies AS sed  
    INNER JOIN sys.objects AS o ON sed.referencing_id = o.object_id  
    WHERE referencing_id = OBJECT_ID(N'Purchasing.uspVendorAllInfo')  
    GO  
    ```  
  
## <a name="see-also"></a>Consulte también  
 [Cambiar el nombre de un procedimiento almacenado](rename-a-stored-procedure.md)   
 [Sys. dm_sql_referencing_entities &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql)   
 [Sys. dm_sql_referenced_entities &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql)   
 [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql)  
  
  
