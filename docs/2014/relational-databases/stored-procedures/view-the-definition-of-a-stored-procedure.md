---
title: Ver la definición de un procedimiento almacenado | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.technology: stored-procedures
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [SQL Server], viewing
- definition of stored procedure
- viewing stored procedures
- displaying stored procedures
ms.assetid: 93318587-a0c5-4788-946f-3b5dc8372ea9
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 333d4d9f0ab9feb5d5b5c4d0aa48fd584cef3143
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62856511"
---
# <a name="view-the-definition-of-a-stored-procedure"></a>Ver la definición de un procedimiento almacenado
    
##  <a name="Top"></a> Puede ver la definición de un procedimiento almacenado en [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] mediante las opciones de menú del Explorador de objetos o en el Editor de consultas mediante [!INCLUDE[tsql](../../includes/tsql-md.md)]. En este tema se describe cómo ver la definición del procedimiento en el Explorador de objetos y utilizar un procedimiento almacenado del sistema, una función del sistema y una vista de catálogo de objetos en el Editor de consultas.  
  
-   **Antes de empezar:**  [Seguridad](#Security)  
  
-   **Para ver la definición de un procedimiento con:**  [SQL Server Management Studio](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Procedimiento almacenado del sistema: `sp_helptext`  
 Debe pertenecer al rol **public** . Las definiciones de los objetos del sistema están visibles públicamente. La definición de objetos de usuario está visible para el propietario del objeto o para los receptores que dispongan de uno de los siguientes permisos: ALTER, CONTROL, TAKE OWNERSHIP o VIEW DEFINITION.  
  
 Función del sistema: `OBJECT_DEFINITION`  
 Las definiciones de los objetos del sistema están visibles públicamente. La definición de objetos de usuario está visible para el propietario del objeto o para los receptores que dispongan de uno de los siguientes permisos: ALTER, CONTROL, TAKE OWNERSHIP o VIEW DEFINITION. Estos permisos corresponden implícitamente a los miembros de los roles fijos de base de datos **db_owner**, **db_ddladmin**y **db_securityadmin** .  
  
 Vista de catálogo de objetos: `sys.sql_modules`  
 La visibilidad de los metadatos en las vistas de catálogo se limita a los elementos protegibles y que son propiedad de un usuario o sobre los que el usuario tiene algún permiso. Para obtener más información, consulte [Metadata Visibility Configuration](../security/metadata-visibility-configuration.md).  
  
##  <a name="Procedures"></a> Ver la definición de un procedimiento almacenado  
 Puede usar cualquiera de los siguientes medios:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
 **Para ver la definición de un procedimiento en el Explorador de objetos**  
  
1.  En el Explorador de objetos, conéctese a una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y expándala.  
  
2.  Expanda **Bases de datos**, expanda la base de datos a la que pertenece el procedimiento y, a continuación, expanda **Programación**.  
  
3.  Expanda **Procedimientos almacenados**, haga clic con el botón derecho en el procedimiento y luego en **Incluir procedimiento almacenado como**. A continuación, haga clic en uno de los siguientes: **Create To**, **Alter To** o **Drop and Create To**.  
  
4.  Seleccione **Nueva ventana del Editor de consultas**. Se mostrará la definición del procedimiento.  
  
###  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para ver la definición de un procedimiento en el Editor de consultas**  
  
 Procedimiento almacenado del sistema: `sp_helptext`  
 1.  En el Explorador de objetos, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de herramientas, haga clic en **Nueva consulta**.  
  
3.  En la ventana de consulta, escriba la siguiente instrucción que usa el procedimiento almacenado del sistema `sp_helptext`. Cambie el nombre de la base de datos y el nombre del procedimiento almacenado de forma que hagan referencia a la base de datos y al procedimiento almacenado que desee.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    EXEC sp_helptext N'AdventureWorks2012.dbo.uspLogError';  
    ```  
  
 Función del sistema: `OBJECT_DEFINITION`  
 1.  En el Explorador de objetos, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de herramientas, haga clic en **Nueva consulta**.  
  
3.  En la ventana de consulta, escriba las siguientes instrucciones que usan la función del sistema `OBJECT_DEFINITION`. Cambie el nombre de la base de datos y el nombre del procedimiento almacenado de forma que hagan referencia a la base de datos y al procedimiento almacenado que desee.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT OBJECT_DEFINITION (OBJECT_ID(N'AdventureWorks2012.dbo.uspLogError'));  
    ```  
  
 Vista de catálogo de objetos: `sys.sql_modules`  
 1.  En el Explorador de objetos, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)].  
  
2.  En la barra de herramientas, haga clic en **Nueva consulta**.  
  
3.  En la ventana de consulta, escriba las siguientes instrucciones que usan la vista de catálogo `sys.sql_modules`. Cambie el nombre de la base de datos y el nombre del procedimiento almacenado de forma que hagan referencia a la base de datos y al procedimiento almacenado que desee.  
  
    ```  
    USE AdventureWorks2012;  
    GO  
    SELECT definition  
    FROM sys.sql_modules  
    WHERE object_id = (OBJECT_ID(N'AdventureWorks2012.dbo.uspLogError'));  
    ```  
  
## <a name="see-also"></a>Consulte también  
 [Crear un procedimiento almacenado](create-a-stored-procedure.md)   
 [Modificar un procedimiento almacenado](modify-a-stored-procedure.md)   
 [Eliminar un procedimiento almacenado](delete-a-stored-procedure.md)   
 [Cambiar el nombre de un procedimiento almacenado](rename-a-stored-procedure.md)   
 [OBJECT_DEFINITION &#40;Transact-SQL&#41;](/sql/t-sql/functions/object-definition-transact-sql)   
 [sys.sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)   
 [sp_helptext &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helptext-transact-sql)   
 [OBJECT_ID &#40;Transact-SQL&#41;](/sql/t-sql/functions/object-id-transact-sql)  
  
  
