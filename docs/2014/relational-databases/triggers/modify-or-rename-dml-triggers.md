---
title: Modificación o cambio de nombre de desencadenadores DML | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- renaming triggers
- modifying triggers
- DML triggers, modifying
ms.assetid: c7317eec-c0e9-479e-a4a7-83b6b6c58d59
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 824ea1587955884f10a53579865d2029cc63eefc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "62473226"
---
# <a name="modify-or-rename-dml-triggers"></a>Modificar o cambiar el nombre de desencadenadores DML
  En este tema se describe cómo modificar o cambiar el nombre de un desencadenador DML en [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mediante [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o [!INCLUDE[tsql](../../includes/tsql-md.md)].  
  
 **En este tema**  
  
-   **Antes de empezar:**  
  
     [Limitaciones y restricciones](#Restrictions)  
  
     [Recomendaciones](#Recommendations)  
  
     [Seguridad](#Security)  
  
-   **Para modificar o cambiar el nombre de un desencadenador DML, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> Antes de comenzar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
  
-   Al cambiar el nombre de un desencadenador, el desencadenador debe estar en la base de datos actual y el nuevo nombre debe seguir las reglas para los [identificadores](../databases/database-identifiers.md).  
  
###  <a name="Recommendations"></a> Recomendaciones  
  
-   Se recomienda no usar el procedimiento almacenado [sp_rename](/sql/relational-databases/system-stored-procedures/sp-rename-transact-sql) para cambiar el nombre de un desencadenador. Al cambiar cualquier parte del nombre de un objeto se pueden interrumpir scripts y procedimientos almacenados. Al cambiar el nombre de un desencadenador no se cambia el nombre del objeto correspondiente en la columna de definición de la vista de catálogo [sys.sql_modules](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql) . En su lugar, se recomienda quitar y volver a crear el desencadenador.  
  
-   Si cambia el nombre de un objeto al que hace referencia un desencadenador DML, deberá modificar este último para que el texto refleje el nuevo nombre. Por tanto, antes de cambiar el nombre de un objeto, vea primero las dependencias del mismo para determinar si algún desencadenador va a verse afectado por el cambio propuesto.  
  
-   También es posible modificar un desencadenador DML para cifrar su definición.  
  
-   Para ver las dependencias de un desencadenador, puede usar [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] o la función y las vistas de catálogo siguientes:  
  
    -   [sys.sql_expression_dependencies &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-expression-dependencies-transact-sql)  
  
    -   [sys.dm_sql_referenced_entities &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-sql-referenced-entities-transact-sql)  
  
    -   [sys.dm_sql_referencing_entities &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-sql-referencing-entities-transact-sql)  
  
###  <a name="Security"></a> Seguridad  
  
####  <a name="Permissions"></a> Permisos  
 Para modificar un desencadenador DML se requiere el permiso ALTER en la tabla o vista en la que se define el desencadenador.  
  
##  <a name="SSMSProcedure"></a> Uso de SQL Server Management Studio  
  
#### <a name="to-modify-a-dml-trigger"></a>Para modificar un desencadenador DML  
  
1.  En el **Explorador de objetos**, conéctese a una instancia del [!INCLUDE[ssDE](../../../includes/ssde-md.md)] y expándala.  
  
2.  Expanda la base de datos que desee, expanda **Tablas**y, a continuación, expanda la tabla que contiene el desencadenador que desea modificar.  
  
3.  Expanda **Desencadenadores**, haga clic con el botón derecho en el desencadenador que quiera cambiar y, luego, haga clic en **Modificar**.  
  
4.  Modifique el desencadenador y, a continuación, haga clic en **Ejecutar**.  
  
#### <a name="to-rename-a-dml-trigger"></a>Para cambiar el nombre de un desencadenador DML  
  
1.  [Elimine el desencadenador](../triggers/dml-triggers.md) cuyo nombre desea cambiar.  
  
2.  [Vuelva a crear el desencadenador](../triggers/create-dml-triggers.md), especificando el nuevo nombre.  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
#### <a name="to-modify-a-trigger-using-alter-trigger"></a>Para modificar un desencadenador mediante ALTER TRIGGER  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue los ejemplos siguientes en la consulta. Ejecute el primer ejemplo para crear un desencadenador DML que muestre al cliente un mensaje definido por el usuario cuando un usuario intente agregar o cambiar los datos de la tabla `SalesPersonQuotaHistory` . Ejecute la instrucción [ALTER TRIGGER](/sql/t-sql/statements/alter-trigger-transact-sql) para modificar el desencadenador de manera que solo se active en las actividades `INSERT` . Este desencadenador es útil porque recuerda al usuario que actualiza o inserta filas en esta tabla que debe notificar también al departamento `Compensation` .  
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N'Sales.bonus_reminder', N'TR') IS NOT NULL  
    DROP TRIGGER Sales.bonus_reminder;  
GO  
CREATE TRIGGER Sales.bonus_reminder  
ON Sales.SalesPersonQuotaHistory  
WITH ENCRYPTION  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
  
```  
  
```sql  
USE AdventureWorks2012;  
GO  
ALTER TRIGGER Sales.bonus_reminder  
ON Sales.SalesPersonQuotaHistory  
AFTER INSERT  
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
  
```  
  
#### <a name="to-rename-a-trigger-using-drop-trigger-and-alter-trigger"></a>Para cambiar el nombre de un desencadenador mediante DROP TRIGGER y ALTER TRIGGER  
  
1.  Conéctese con el [!INCLUDE[ssDE](../../../includes/ssde-md.md)].  
  
2.  En la barra Estándar, haga clic en **Nueva consulta**.  
  
3.  Copie y pegue el siguiente ejemplo en la ventana de consulta y haga clic en **Ejecutar**. En este ejemplo se usan las instrucciones [DROP TRIGGER](/sql/t-sql/statements/drop-trigger-transact-sql) y [ALTER TRIGGER](/sql/t-sql/statements/alter-trigger-transact-sql) para cambiar el nombre del desencadenador `Sales.bonus_reminder` a `Sales.bonus_reminder_2`.  
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID(N'Sales.bonus_reminder', N'TR') IS NOT NULL  
    DROP TRIGGER Sales.bonus_reminder;  
GO  
CREATE TRIGGER Sales.bonus_reminder_2  
ON Sales.SalesPersonQuotaHistory  
WITH ENCRYPTION  
AFTER INSERT, UPDATE   
AS RAISERROR ('Notify Compensation', 16, 10);  
GO  
  
```  
  
## <a name="see-also"></a>Consulte también  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-trigger-transact-sql)   
 [DROP TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/drop-trigger-transact-sql)   
 [ENABLE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/enable-trigger-transact-sql)   
 [DISABLE TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/disable-trigger-transact-sql)   
 [EVENTDATA &#40;Transact-SQL&#41;](/sql/t-sql/functions/eventdata-transact-sql)   
 [sp_rename &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-rename-transact-sql)   
 [ALTER TRIGGER &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-trigger-transact-sql)   
 [Obtener información acerca de los desencadenadores DML](../triggers/get-information-about-dml-triggers.md)   
 [sp_help &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-transact-sql)   
 [sp_helptrigger &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helptrigger-transact-sql)   
 [sys.triggers &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-triggers-transact-sql)   
 [sys.trigger_events &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-trigger-events-transact-sql)   
 [sys.sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-sql-modules-transact-sql)   
 [sys.assembly_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-assembly-modules-transact-sql)   
 [sys.server_triggers &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-triggers-transact-sql)   
 [sys.server_trigger_events &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-trigger-events-transact-sql)   
 [sys.server_sql_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-sql-modules-transact-sql)   
 [sys.server_assembly_modules &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/sys-server-assembly-modules-transact-sql)  
  
  
