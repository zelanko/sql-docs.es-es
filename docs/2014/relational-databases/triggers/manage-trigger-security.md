---
title: Administración de la seguridad de los desencadenadores | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- triggers [SQL Server], security
ms.assetid: e94720a8-a3a2-4364-b0a3-bbe86e3ce4d5
author: rothja
ms.author: jroth
ms.openlocfilehash: fdc176dcad50c3bf28f058c3724a01267975bfc5
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85014315"
---
# <a name="manage-trigger-security"></a>Administrar la seguridad de los desencadenadores
  De forma predeterminada, los desencadenadores DML y DDL se ejecutan en el contexto del usuario que llama al desencadenador. El autor de la llamada a un desencadenador es el usuario que ejecuta la instrucción que hace que el desencadenador se ejecute. Por ejemplo, si el usuario **Mary** ejecuta una instrucción DELETE que hace que el desencadenador DML **DML_trigMary** se ejecute, el código incluido en **DML_trigMary** se ejecutará en el contexto de los privilegios de usuario de **Mary**. Este comportamiento predeterminado podría ser utilizado por usuarios que deseen introducir código dañino en la base de datos o la instancia de servidor. Por ejemplo, el usuario `JohnDoe`crea el siguiente desencadenador DDL:  
  
 `CREATE TRIGGER DDL_trigJohnDoe`  
  
 `ON DATABASE`  
  
 `FOR ALTER_TABLE`  
  
 `AS`  
  
 `GRANT CONTROL SERVER TO JohnDoe ;`  
  
 `GO`  
  
 Este desencadenador significa que cuando un usuario con permiso para ejecutar una instrucción `GRANT CONTROL SERVER` , por ejemplo, un miembro del rol fijo de servidor **sysadmin** , ejecute una instrucción `ALTER TABLE` , `JohnDoe` obtendrá el permiso `CONTROL SERVER` . En otras palabras, aunque `JohnDoe` no puede otorgarse el permiso `CONTROL SERVER` a sí mismo, ha habilitado el código de desencadenador que le otorga permiso para ejecutar instrucciones con privilegios aumentados. Tanto el desencadenador DML como el DLL están sujetos a este tipo de amenaza de seguridad.  
  
## <a name="trigger-security-best-practices"></a>Prácticas recomendadas de seguridad de los desencadenadores  
 Para evitar que se ejecute código de desencadenador con privilegios aumentados, puede adoptar las siguientes medidas:  
  
-   Tenga en cuenta los desencadenadores DML y DDL que se encuentran en la base de datos y en la instancia del servidor al consultar la vistas de catálogo [sys.triggers](/sql/relational-databases/system-catalog-views/sys-triggers-transact-sql) y [sys.server_triggers](/sql/relational-databases/system-catalog-views/sys-server-triggers-transact-sql) . La consulta siguiente devuelve todos los desencadenadores DML y DLL de base de datos para la base de datos actual, además de todos los desencadenadores DDL de servidor para la instancia de servidor:  
  
    ```  
    SELECT type, name, parent_class_desc FROM sys.triggers  
    UNION  
    SELECT type, name, parent_class_desc FROM sys.server_triggers ;  
    ```  
  
-   Utilice [DISABLE TRIGGER](/sql/t-sql/statements/disable-trigger-transact-sql) para deshabilitar desencadenadores que podrían dañar la integridad de la base de datos o el servidor si se ejecutan con privilegios aumentados. La siguiente instrucción deshabilita todos los desencadenadores DDL de base de datos para la base de datos actual:  
  
    ```  
    DISABLE TRIGGER ALL ON DATABASE  
    ```  
  
     Esta instrucción deshabilita todos los desencadenadores DDL en la instancia de servidor:  
  
    ```  
    DISABLE TRIGGER ALL ON ALL SERVER  
    ```  
  
     Esta instrucción deshabilita todos los desencadenadores DML en la base de datos actual:  
  
    ```  
    DECLARE @schema_name sysname, @trigger_name sysname, @object_name sysname ;  
    DECLARE @sql nvarchar(max) ;  
    DECLARE trig_cur CURSOR FORWARD_ONLY READ_ONLY FOR  
        SELECT SCHEMA_NAME(schema_id) AS schema_name,  
            name AS trigger_name,  
            OBJECT_NAME(parent_object_id) as object_name  
        FROM sys.objects WHERE type in ('TR', 'TA') ;  
  
    OPEN trig_cur ;  
    FETCH NEXT FROM trig_cur INTO @schema_name, @trigger_name, @object_name ;  
  
    WHILE @@FETCH_STATUS = 0  
    BEGIN  
        SELECT @sql = 'DISABLE TRIGGER ' + QUOTENAME(@schema_name) + '.'  
            + QUOTENAME(@trigger_name) +  
            ' ON ' + QUOTENAME(@schema_name) + '.'   
            + QUOTENAME(@object_name) + ' ; ' ;  
        EXEC (@sql) ;  
        FETCH NEXT FROM trig_cur INTO @schema_name, @trigger_name, @object_name ;  
    END  
    GO  
  
    -- Verify triggers are disabled. Should return an empty result set.  
    SELECT * FROM sys.triggers WHERE is_disabled = 0 ;  
    GO  
  
    CLOSE trig_cur ;  
    DEALLOCATE trig_cur;  
    ```  
  
## <a name="see-also"></a>Consulte también  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)   
 [Desencadenadores DML](../triggers/dml-triggers.md)   
 [Desencadenadores DDL](../triggers/ddl-triggers.md)  
  
  
