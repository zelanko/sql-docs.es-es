---
title: Configuración de ejemplo de copia masiva
description: Describe las tablas usadas en los ejemplos de copia masiva y proporciona scripts SQL para crear las tablas en la base de datos AdventureWorks.
ms.date: 09/30/2019
dev_langs:
- sql
ms.assetid: d4dde6ac-b8b6-4593-965a-635c8fb2dadb
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: rothja
ms.author: jroth
ms.reviewer: v-kaywon
ms.openlocfilehash: 4b156f3f9deeb6f74393631555c0fc8ad0e9acf2
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/29/2020
ms.locfileid: "78897046"
---
# <a name="bulk-copy-example-setup"></a>Configuración de ejemplo de copia masiva

[!INCLUDE[Driver_ADONET_Download](../../../includes/driver_adonet_download.md)]

La clase <xref:Microsoft.Data.SqlClient.SqlBulkCopy> puede usarse para escribir datos solo en tablas de SQL Server. Los ejemplos de código que se muestran en este tema usan la base de datos de ejemplo de SQL Server, **AdventureWorks**. Para evitar modificar los ejemplos de código de las tablas existentes escriba los datos en tablas que tendrá que crear en primer lugar.  
  
Las tablas **BulkCopyDemoMatchingColumns** y **BulkCopyDemoDifferentColumns** se basan en la tabla **AdventureWorks** **Production.Products**. En los ejemplos de código que usan estas tablas, los datos se agregan desde la tabla **Production.Products** a una de estas tablas de muestra. La tabla **BulkCopyDemoDifferentColumns** se usa cuando el ejemplo muestra cómo asignar columnas de los datos de origen a la tabla de destino; **BulkCopyDemoMatchingColumns** se usa para la mayoría de los demás ejemplos.  
  
Algunos de los ejemplos de código muestran cómo usar una clase <xref:Microsoft.Data.SqlClient.SqlBulkCopy> para escribir en varias tablas. En estos ejemplos, se usan las tablas **BulkCopyDemoOrderHeader** y **BulkCopyDemoOrderDetail** como tablas de destino. Estas tablas se basan en las tablas **Sales.SalesOrderHeader** y **Sales.SalesOrderDetail** de **AdventureWorks**.  
  
> [!NOTE]
>  Los ejemplos de código **SqlBulkCopy** se proporcionan para mostrar la sintaxis para usar **SqlBulkCopy** únicamente. Si las tablas de origen y destino se encuentran en la misma instancia de SQL Server, es más fácil y rápido usar una instrucción `INSERT … SELECT` de Transact-SQL para copiar los datos.  
  
## <a name="table-setup"></a>Configuración de tabla  
Para crear las tablas necesarias para que los ejemplos de código se ejecuten correctamente, debe ejecutar las siguientes instrucciones de Transact-SQL en una base de datos de SQL Server.  
  
```sql
USE AdventureWorks  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoMatchingColumns]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoMatchingColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoMatchingColumns]([ProductID] [int] IDENTITY(1,1) NOT NULL,  
    [Name] [nvarchar](50) NOT NULL,  
    [ProductNumber] [nvarchar](25) NOT NULL,  
 CONSTRAINT [PK_ProductID] PRIMARY KEY CLUSTERED  
(  
    [ProductID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoDifferentColumns]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoDifferentColumns]  
  
CREATE TABLE [dbo].[BulkCopyDemoDifferentColumns]([ProdID] [int] IDENTITY(1,1) NOT NULL,  
    [ProdNum] [nvarchar](25) NOT NULL,  
    [ProdName] [nvarchar](50) NOT NULL,  
 CONSTRAINT [PK_ProdID] PRIMARY KEY CLUSTERED  
(  
    [ProdID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderHeader]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderHeader]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderHeader]([SalesOrderID] [int] IDENTITY(1,1) NOT NULL,  
    [OrderDate] [datetime] NOT NULL,  
    [AccountNumber] [nvarchar](15) NULL,  
 CONSTRAINT [PK_SalesOrderID] PRIMARY KEY CLUSTERED  
(  
    [SalesOrderID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
  
IF EXISTS (SELECT * FROM dbo.sysobjects   
 WHERE id = object_id(N'[dbo].[BulkCopyDemoOrderDetail]')  
 AND OBJECTPROPERTY(id, N'IsUserTable') = 1)  
    DROP TABLE [dbo].[BulkCopyDemoOrderDetail]  
  
CREATE TABLE [dbo].[BulkCopyDemoOrderDetail]([SalesOrderID] [int] NOT NULL,  
    [SalesOrderDetailID] [int] NOT NULL,  
    [OrderQty] [smallint] NOT NULL,  
    [ProductID] [int] NOT NULL,  
    [UnitPrice] [money] NOT NULL,  
 CONSTRAINT [PK_LineNumber] PRIMARY KEY CLUSTERED  
(  
    [SalesOrderID] ASC,  
    [SalesOrderDetailID] ASC  
) ON [PRIMARY]) ON [PRIMARY]  
```  
  
## <a name="next-steps"></a>Pasos siguientes
- [Operaciones de copia masiva en SQL Server](bulk-copy-operations-sql-server.md)
