---
description: Crear desencadenadores anidados
title: Creación de desencadenadores anidados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- recursive DML triggers [SQL Server]
- DML triggers, nested
- triggers [SQL Server], nested
- direct recursion [SQL Server]
- triggers [SQL Server], recursive
- DML triggers, recursive
- RECURSIVE_TRIGGERS option
- indirect recursion [SQL Server]
- nested DML triggers
ms.assetid: cd522dda-b4ab-41b8-82b0-02445bdba7af
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 2709846194c14dc08653efa761edd6660620872a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88485386"
---
# <a name="create-nested-triggers"></a>Crear desencadenadores anidados
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  Los desencadenadores DML y DDL están anidados cuando un desencadenador realiza una acción que inicia otro desencadenador. Estas acciones pueden iniciar otros desencadenadores y así sucesivamente. Los desencadenadores DML y DDL se pueden anidar hasta un máximo de 32 niveles. Puede controlar si los desencadenadores AFTER se pueden anidar en la opción de configuración del servidor **nested triggers** . Los desencadenadores INSTEAD OF (solo los desencadenadores DML pueden ser desencadenadores INSTEAD OF) se pueden anidar independientemente de esta configuración.  
  
> [!NOTE]  
>  Una referencia a código administrado desde un desencadenador [!INCLUDE[tsql](../../includes/tsql-md.md)] se considera como un nivel en lo que respecta al límite de anidamiento de 32 niveles. Los métodos invocados desde el código administrado no cuentan para este límite.  
  
 Si se admiten desencadenadores anidados y un desencadenador de la cadena inicia un bucle infinito, se superará el nivel de anidamiento y se terminará el desencadenador.  
  
 Puede utilizar desencadenadores anidados para realizar funciones de mantenimiento, tales como almacenar una copia de seguridad de las filas que han sido afectadas por un desencadenador anterior. Por ejemplo, puede crear un desencadenador en `PurchaseOrderDetail` que guarde una copia de seguridad de las filas de `PurchaseOrderDetail` que haya eliminado el desencadenador `delcascadetrig` . Con el desencadenador `delcascadetrig` activado, la eliminación del valor `PurchaseOrderID` 1965 de `PurchaseOrderHeader` elimina las filas correspondientes de `PurchaseOrderDetail`. Para guardar los datos, puede crear un desencadenador DELETE en `PurchaseOrderDetail` que guarde los datos eliminados en una nueva tabla, `del_save`. Por ejemplo:  
  
```  
CREATE TRIGGER Purchasing.savedel  
   ON Purchasing.PurchaseOrderDetail  
FOR DELETE  
AS  
   INSERT del_save;  
   SELECT * FROM deleted;  
```  
  
 No se recomienda utilizar desencadenadores anidados en una secuencia que dependa del orden. Utilice desencadenadores diferentes para realizar modificaciones de datos en cascada.  
  
> [!NOTE]  
>  Dado que los desencadenadores se ejecutan dentro de una transacción, un error en cualquier nivel de un conjunto de desencadenadores anidados anula toda la transacción y provoca que se reviertan todas las modificaciones de datos. Incluya instrucciones PRINT en los desencadenadores para poder determinar dónde se produjo el error.  
  
## <a name="recursive-triggers"></a>Desencadenadores recursivos  
 Un desencadenador AFTER no se llama a sí mismo de forma recursiva a menos que se active la opción RECURSIVE_TRIGGERS de la base de datos.  
  
 Hay dos tipos de recursividad:  
  
-   Recursión directa  
  
     Esta recursividad se produce cuando un desencadenador se activa y realiza una acción que provoca que el mismo desencadenador se vuelva a activar. Por ejemplo, una aplicación actualiza la tabla **T3**y esto provoca la activación del desencadenador **Trig3** . **Trig3** vuelve a actualizar la tabla **T3** , lo que provoca una nueva activación del mismo desencadenador **Trig3** .  
  
     También se puede producir la repetición directa cuando se llama de nuevo al mismo desencadenador, pero después de que se llame a un desencadenador de un tipo diferente (AFTER o INSTEAD OF). Es decir, la repetición directa de un desencadenador INSTEAD OF puede producirse cuando se llama al mismo desencadenador INSTEAD OF por segunda vez, incluso cuando se llaman a uno o varios desencadenadores AFTER en medio. Del mismo modo, la repetición directa de un desencadenador AFTER puede producirse cuando se llama al mismo desencadenador AFTER por segunda vez, incluso cuando se llaman a uno o varios desencadenadores INSTEAD OF en medio. Por ejemplo, una aplicación actualiza la tabla **T4**. Esta actualización hace que se active el desencadenador INSTEAD OF **Trig4** . **Trig4** actualiza la tabla **T5**. Esta actualización hace que se active el desencadenador AFTER **Trig5** . **Trig5** actualiza la tabla **T4**y esta actualización hace que se active de nuevo el desencadenador INSTEAD OF **Trig4** . Esta cadena de eventos se considera una repetición directa de **Trig4**.  
  
-   Recursión indirecta  
  
     Esta repetición se produce cuando se activa un desencadenador y realiza una acción que provoca la activación de otro desencadenador del mismo tipo (AFTER o INSTEAD OF). Este segundo desencadenador realiza una acción que provoca una nueva activación del desencadenador original. Es decir, la repetición indirecta se puede producir cuando se llama a un desencadenador INSTEAD OF por segunda vez, pero no hasta que se llama a otro desencadenador INSTEAD OF en medio. Del mismo modo, la repetición indirecta se puede producir cuando se llama a un desencadenador AFTER por segunda vez, pero no hasta que se llama a otro desencadenador AFTER en medio. Por ejemplo, una aplicación actualiza la tabla **T1**. Esta actualización hace que se active el desencadenador AFTER **Trig1** . **Trig1** actualiza la tabla **T2**y esta actualización hace que se active el desencadenador AFTER **Trig2** . A su vez,**Trig2** actualiza la tabla **T1** , lo que provoca que se vuelva a activar el desencadenador AFTER **Trig1** .  
  
 La repetición directa de los desencadenadores AFTER solo se impide si la opción RECURSIVE_TRIGGERS de la base de datos se establece en OFF. Para deshabilitar la repetición indirecta de los desencadenadores AFTER, también debe establecer la opción **nested triggers** del servidor en **0**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se muestra la utilización de desencadenadores recursivos para solucionar una relación con referencia a sí misma (también denominada clausura transitiva). Por ejemplo, la tabla `emp_mgr` define los elementos siguientes:  
  
-   Un empleado (`emp`) de una empresa.  
  
-   El director de cada empleado (`mgr`).  
  
-   El número total de empleados en la estructura de la organización que dependen de cada empleado (`NoOfReports`).  
  
 Un desencadenador UPDATE recursivo puede servir para mantener actualizada la columna `NoOfReports` a medida que se insertan nuevos registros de empleado. El desencadenador INSERT actualiza la columna `NoOfReports` del registro de directores, que actualiza de modo recursivo la columna `NoOfReports` de otros registros superiores de la jerarquía de administración.  
  
```  
USE AdventureWorks2012;  
GO  
-- Turn recursive triggers ON in the database.  
ALTER DATABASE AdventureWorks2012  
   SET RECURSIVE_TRIGGERS ON;  
GO  
CREATE TABLE dbo.emp_mgr (  
   emp char(30) PRIMARY KEY,  
    mgr char(30) NULL FOREIGN KEY REFERENCES emp_mgr(emp),  
    NoOfReports int DEFAULT 0  
);  
GO  
CREATE TRIGGER dbo.emp_mgrins ON dbo.emp_mgr  
FOR INSERT  
AS  
DECLARE @e char(30), @m char(30);  
DECLARE c1 CURSOR FOR  
   SELECT emp_mgr.emp  
   FROM   emp_mgr, inserted  
   WHERE emp_mgr.emp = inserted.mgr;  
  
OPEN c1;  
FETCH NEXT FROM c1 INTO @e;  
WHILE @@fetch_status = 0  
BEGIN  
   UPDATE dbo.emp_mgr  
   SET emp_mgr.NoOfReports = emp_mgr.NoOfReports + 1 -- Add 1 for newly  
   WHERE emp_mgr.emp = @e ;                           -- added employee.  
  
   FETCH NEXT FROM c1 INTO @e;  
END  
CLOSE c1;  
DEALLOCATE c1;  
GO  
-- This recursive UPDATE trigger works assuming:  
--   1. Only singleton updates on emp_mgr.  
--   2. No inserts in the middle of the org tree.  
CREATE TRIGGER dbo.emp_mgrupd ON dbo.emp_mgr FOR UPDATE  
AS  
IF UPDATE (mgr)  
BEGIN  
   UPDATE dbo.emp_mgr  
   SET emp_mgr.NoOfReports = emp_mgr.NoOfReports + 1 -- Increment mgr's  
   FROM inserted                            -- (no. of reports) by  
   WHERE emp_mgr.emp = inserted.mgr;         -- 1 for the new report.  
  
   UPDATE dbo.emp_mgr  
   SET emp_mgr.NoOfReports = emp_mgr.NoOfReports - 1 -- Decrement mgr's  
   FROM deleted                             -- (no. of reports) by 1  
   WHERE emp_mgr.emp = deleted.mgr;          -- for the new report.  
END  
GO  
-- Insert some test data rows.  
INSERT dbo.emp_mgr(emp, mgr) VALUES  
    ('Harry', NULL)  
    ,('Alice', 'Harry')  
    ,('Paul', 'Alice')  
    ,('Joe', 'Alice')  
    ,('Dave', 'Joe');  
GO  
SELECT emp,mgr,NoOfReports  
FROM dbo.emp_mgr;  
GO  
-- Change Dave's manager from Joe to Harry  
UPDATE dbo.emp_mgr SET mgr = 'Harry'  
WHERE emp = 'Dave';  
GO  
SELECT emp,mgr,NoOfReports FROM emp_mgr;  
  
GO  
```  
  
 Resultados antes de la actualización.  
  
```  
emp                            mgr                           NoOfReports  
------------------------------ ----------------------------- -----------  
Alice                          Harry                          2  
Dave                           Joe                            0  
Harry                          NULL                           1  
Joe                            Alice                          1  
Paul                           Alice                          0  
```  
  
 Resultados tras la actualización.  
  
```  
emp                            mgr                           NoOfReports  
------------------------------ ----------------------------- -----------  
Alice                          Harry                          2  
Dave                           Harry                          0  
Harry                          NULL                           2  
Joe                            Alice                          0  
Paul                           Alice                          0  
```  
  
 **Para establecer la opción nested triggers**  
  
-   [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)  
  
 **Para establecer la opción de base de datos RECURSIVE_TRIGGERS**  
  
-   [Opciones de ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)  
  
## <a name="see-also"></a>Consulte también  
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [Establecer la opción de configuración del servidor Desencadenadores anidados](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md)  
  
  
