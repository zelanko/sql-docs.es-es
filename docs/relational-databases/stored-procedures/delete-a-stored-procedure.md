---
title: "Eliminación de un procedimiento almacenado | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-stored-Procs
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- removing stored procedures
- stored procedures [SQL Server], deleting
- deleting stored procedures
ms.assetid: 232dbf4d-392a-406f-af3a-579518cd8e46
caps.latest.revision: "26"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 145ec25d4bcf4f100449960440eddfa2cff61e01
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/09/2017
---
# <a name="delete-a-stored-procedure"></a>Eliminar un procedimiento almacenado
    
##  <a name="Top"></a> En este tema se describe cómo eliminar un procedimiento almacenado [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
-   **Antes de empezar:**  [Limitaciones y restricciones](#Restrictions), [Seguridad](#Security)  
  
-   **Para eliminar un procedimiento con**  [SQL Server Management Studio](#SSMSProcedure), [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
 Eliminar un procedimiento puede hacer que los objetos y scripts dependientes produzcan un error cuando los objetos y scripts no se han actualizado para reflejar la eliminación del procedimiento. No obstante, si se crea un nuevo procedimiento con el mismo nombre y los mismos parámetros para reemplazar al que se eliminó, los objetos que hagan referencia a él antiguo se procesarán correctamente. Para obtener más información, vea [Ver las dependencias de un procedimiento almacenado](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md).  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Requiere el permiso ALTER en el esquema al que pertenece el procedimiento o el permiso CONTROL en el procedimiento.  
  
##  <a name="Procedures"></a> Cómo eliminar un procedimiento almacenado  
 Puede usar cualquiera de los siguientes medios:  
  
-   [SQL Server Management Studio](#SSMSProcedure)  
  
-   [Transact-SQL](#TsqlProcedure)  
  
###  <a name="SSMSProcedure"></a> Usar SQL Server Management Studio  
 **Para eliminar un procedimiento en el Explorador de objetos**  
  
1.  En el Explorador de objetos, conéctese a una instancia de [!INCLUDE[ssDE](../../includes/ssde-md.md)] y expándala.  
  
2.  Expanda **Bases de datos**, expanda la base de datos a la que pertenece el procedimiento y, a continuación, expanda **Programación**.  
  
3.  Expanda **Procedimientos almacenados**, haga clic con el botón derecho en el procedimiento que quiera eliminar y, luego, haga clic en **Eliminar**.  
  
4.  Para ver los objetos que dependen del procedimiento, haga clic en **Mostrar dependencias**.  
  
5.  Confirme que haya seleccionado el procedimiento correcto y haga clic en **Aceptar**.  
  
6.  Quite las referencias al procedimiento de cualquier objeto y script dependientes.  
  
###  <a name="TsqlProcedure"></a> Usar Transact-SQL  
 **Para eliminar un procedimiento en el Editor de consultas**  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../includes/ssde-md.md)] y expándala.  
  
2.  Expanda **Bases de datos**, expanda la base de datos a la que pertenece el procedimiento o bien, en la barra de herramientas, seleccione la base de datos en la lista de bases de datos disponibles.  
  
3.  En el menú Archivo, haga clic en **Nueva consulta**.  
  
4.  Obtenga el nombre del procedimiento almacenado para quitar en la base de datos actual. En el Explorador de objetos, expanda **Programación** y, a continuación, **Procedimientos almacenados**. Como alternativa, en el editor de consultas, ejecute la siguiente instrucción.  
  
    ```tsql  
    SELECT name AS procedure_name   
        ,SCHEMA_NAME(schema_id) AS schema_name  
        ,type_desc  
        ,create_date  
        ,modify_date  
    FROM sys.procedures;  
    ```  
  
5.  Copie y pegue el ejemplo siguiente en el editor de consultas e inserte un procedimiento almacenado para eliminarlo de la base de datos actual.  
  
    ```tsql  
    DROP PROCEDURE <stored procedure name>;  
    GO  
    ```  
  
6.  Quite las referencias al procedimiento de cualquier objeto y script dependientes.  
  
## <a name="see-also"></a>Vea también  
 [Crear un procedimiento almacenado](../../relational-databases/stored-procedures/create-a-stored-procedure.md)   
 [Modificar un procedimiento almacenado](../../relational-databases/stored-procedures/modify-a-stored-procedure.md)   
 [Cambiar el nombre de un procedimiento almacenado](../../relational-databases/stored-procedures/rename-a-stored-procedure.md)   
 [Ver la definición de un procedimiento almacenado](../../relational-databases/stored-procedures/view-the-definition-of-a-stored-procedure.md)   
 [Ver las dependencias de un procedimiento almacenado](../../relational-databases/stored-procedures/view-the-dependencies-of-a-stored-procedure.md)   
 [DROP PROCEDURE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-procedure-transact-sql.md)  
  
  
