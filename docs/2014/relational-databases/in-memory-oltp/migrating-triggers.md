---
title: Migración de desencadenadores | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: ad5385c5-5a50-40ca-a319-97d5606b8511
author: rothja
ms.author: jroth
ms.openlocfilehash: d2dea44e08e58717f1dfe1c90af20d7fc4558b97
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/18/2020
ms.locfileid: "85026094"
---
# <a name="migrating-triggers"></a>Migrar desencadenadores
  En este tema se describen los desencadenadores DDL y DML, y las tablas optimizadas para memoria.  
  
 Los desencadenadores LOGON son desencadenadores definidos para activarse en eventos LOGON. Los desencadenadores LOGON no afectan a las tablas optimizadas para memoria.  
  
## <a name="ddl-triggers"></a>Desencadenadores DDL  
 Los desencadenadores DDL son desencadenadores definidos para activarse cuando se ejecuta una instrucción CREATE, ALTER, DROP, GRANT, DENY, REVOKE o UPDATE STATISTICS en la base de datos o el servidor en el que se define.  
  
 No se pueden crear tablas optimizadas para memoria si la base de datos o el servidor tiene uno o varios desencadenadores DDL definidos en CREATE_TABLE o en cualquier grupo de eventos que lo incluyan. No se puede quitar una tabla optimizada para memoria si la base de datos o el servidor tiene uno o varios desencadenadores DDL definidos en DROP_TABLE o en cualquier grupo de eventos que lo incluyan.  
  
 No se pueden crear procedimientos almacenados compilados de forma nativa si hay uno o más desencadenadores DDL en CREATE_PROCEDURE, DROP_PROCEDURE o cualquier grupo de eventos que incluya los eventos.  
  
## <a name="dml-triggers"></a>Desencadenadores DML  
 No se puede definir desencadenadores DML en tablas optimizadas para memoria. Sin embargo, OLTP en memoria permite conseguir un efecto similar a los desencadenadores DML si se utilizan explícitamente procedimientos almacenados para insertar, actualizar o eliminar datos. Si el sistema contiene consultas ad hoc, conviértalas para que utilicen estos procedimientos almacenados en su lugar para simular el efecto de los desencadenadores DML.  
  
 Según el evento de desencadenador (FOR/AFTER o INSTEAD OF), puede incluir el contenido del desencadenador en el procedimiento almacenado adecuado que realiza la operación INSERT, UPDATE o DELETE en esa tabla. Por ejemplo, al migrar un desencadenador AFTER INSERT, puede modificar el procedimiento almacenado que realiza la operación de inserción si incluye el contenido del desencadenador después de la instrucción INSERT adecuada.  
  
 Puede utilizar un procedimiento almacenado interpretado o un procedimiento almacenado compilado de forma nativa. La mayoría de las construcciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] de un procedimiento almacenado interpretado pueden ejecutarse en una tabla optimizada para memoria. Sin embargo, en los procedimientos almacenados compilados de forma nativa solo se admite un subconjunto de construcciones de [!INCLUDE[tsql](../../includes/tsql-md.md)] . Para obtener información acerca de la compatibilidad de [!INCLUDE[tsql](../../includes/tsql-md.md)] en tablas optimizadas para memoria, vea [Accessing Memory-Optimized Tables Using Interpreted Transact-SQL](accessing-memory-optimized-tables-using-interpreted-transact-sql.md). Para obtener información acerca de la compatibilidad de [!INCLUDE[tsql](../../includes/tsql-md.md)] en procedimientos almacenados compilados de forma nativa, vea [Transact-SQL Constructs Not Supported by In-Memory OLTP](transact-sql-constructs-not-supported-by-in-memory-oltp.md).  
  
 A continuación se muestra un ejemplo simple de simulación del comportamiento de un desencadenador DML en una tabla optimizada para memoria.  
  
 La base de datos contiene los siguientes objetos, incluidos en scripts como instrucciones CREATE TABLE, CREATE TRIGGER y CREATE PROCEDURE:  
  
```sql  
CREATE TABLE OrderDetails  
(  
   OrderId int not null primary key,  
   ProductId int not null,  
   SalePrice money not null,  
   Quantity int not null,  
   Total money not null,  
   IsDeleted bit not null DEFAULT (0)  
)  
GO  
  
CREATE TRIGGER tr_order_details_insteadof_insert  
ON OrderDetails  
INSTEAD OF INSERT AS  
BEGIN  
   DECLARE @pid int, @qty_buy int, @qty_remain int  
   SELECT @pid = ProductId, @qty_buy = Quantity FROM inserted  
   SELECT @qty_remain = Quantity FROM Inventory WHERE ProductId = @pid  
   IF (@qty_remain <= @qty_buy)  
      THROW 51000, N'Insufficient inventory!', 1  
   ELSE  
   BEGIN  
      INSERT INTO dbo.OrderDetails (OrderId, ProductId, SalePrice, Quantity, Total)   
      SELECT OrderId, ProductId, SalePrice, Quantity, Total FROM inserted  
      UPDATE Inventory SET Quantity = Quantity - @qty_buy WHERE ProductId = @pid  
   END  
END  
GO  
  
CREATE TRIGGER tr_order_details_after_update  
ON OrderDetails  
AFTER UPDATE AS  
BEGIN  
   INSERT INTO UpdateNotifications (OrderId, UpdateTime) SELECT OrderId, GETDATE() FROM inserted     
END  
GO  
  
CREATE PROCEDURE sp_insert_order_details   
   @OrderId int, @ProductId int, @SalePrice money, @Quantity int, @total money  
AS BEGIN  
   INSERT INTO dbo.OrderDetails (OrderId, ProductId, SalePrice, Quantity, Total)  
   VALUES (@OrderId, @ProductId, @SalePrice, @Quantity, @total)  
END  
GO  
  
CREATE PROCEDURE sp_update_order_details_by_id  
   @OrderId int, @ProductId int, @SalePrice money, @Quantity int, @Total money  
AS BEGIN  
   UPDATE dbo.OrderDetails   
   SET ProductId = @ProductId, SalePrice = @SalePrice, Quantity = @Quantity, Total = @total  
   WHERE OrderId = @OrderId  
END  
GO  
```  
  
 Los objetos siguientes son funcionalmente equivalentes al estado previo a la migración:  
  
```sql  
CREATE TABLE OrderDetails  
(  
   OrderId int not null PRIMARY KEY NONCLUSTERED HASH WITH (BUCKET_COUNT = 1048576),  
   ProductId int not null,  
   SalePrice money not null,  
   Quantity int not null,  
   Total money not null,  
   IsDeleted bit not null DEFAULT (0)  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
GO  
  
CREATE TABLE Inventory  
(  
   ProductId int not null PRIMARY KEY NONCLUSTERED,  
   Quantity int not null  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
GO  
  
CREATE TABLE UpdateNotifications  
(  
   OrderId int not null,  
   UpdateTime datetime2 not null  
   CONSTRAINT pk_updateNotifications PRIMARY KEY NONCLUSTERED (OrderId, UpdateTime)  
) WITH (MEMORY_OPTIMIZED = ON, DURABILITY = SCHEMA_AND_DATA)  
GO  
  
CREATE PROCEDURE sp_insert_order_details   
   @OrderId int, @ProductId int, @SalePrice money, @Quantity int, @total money  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'English')  
   DECLARE @qty_remain int  
   SELECT @qty_remain = Quantity FROM dbo.Inventory WHERE ProductId = @ProductId  
   IF (@qty_remain <= @Quantity)  
      THROW 51000, N'Insufficient inventory!', 1  
   ELSE  
   BEGIN  
      INSERT INTO dbo.OrderDetails (OrderId, ProductId, SalePrice, Quantity, Total)   
      VALUES (@OrderId, @ProductId, @SalePrice, @Quantity, @total)  
      UPDATE dbo.Inventory SET Quantity = Quantity - @Quantity WHERE ProductId = @ProductId  
   END  
END  
GO  
  
CREATE PROCEDURE sp_update_order_details_by_id  
   @OrderId int, @ProductId int, @SalePrice money, @Quantity int, @Total money  
WITH NATIVE_COMPILATION, SCHEMABINDING, EXECUTE AS OWNER  
AS BEGIN ATOMIC WITH (TRANSACTION ISOLATION LEVEL = SNAPSHOT, LANGUAGE = N'English')  
   UPDATE dbo.OrderDetails   
   SET ProductId = @ProductId, SalePrice = @SalePrice, Quantity = @Quantity, Total = @total  
   WHERE OrderId = @OrderId  
   INSERT INTO dbo.UpdateNotifications (OrderId, UpdateTime) VALUES (@OrderId, GETDATE())  
END  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Migrar a OLTP en memoria](migrating-to-in-memory-oltp.md)  
  
  
