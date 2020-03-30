---
title: Ejecutar funciones definidas por el usuario | Microsoft Docs
ms.custom: ''
ms.date: 10/24/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- invoking user-defined functions
- user-defined functions [SQL Server], executing
ms.assetid: 0de7744d-9b73-463f-ae80-e31a020004b5
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: b028b6ab4da678444427682a635f679acce576ab
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68123582"
---
# <a name="execute-user-defined-functions"></a>Ejecutar funciones definidas por el usuario
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]
  Ejecutar una función definida por el usuario mediante Transact-SQL.
  

> **Nota:** Visite  [Funciones definidas por el usuario](user-defined-functions.md) y [Create Function (Transact SQL)](../../t-sql/statements/create-function-transact-sql.md) para obtener más información acerca de las funciones definidas por el usuario. 
  
 
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="limitations-and-restrictions"></a><a name="Restrictions"></a> Limitaciones y restricciones  
 En Transact-SQL, los parámetros se pueden proporcionar mediante *value* o @*parameter_name*=*value.* Un parámetro no forma parte de una transacción; por tanto, si se cambia un parámetro en una transacción que se revierte posteriormente, el valor del parámetro no vuelve a su valor anterior. El valor devuelto al procedimiento llamante es siempre el valor del parámetro en el momento en que finaliza el módulo llamado.  
  
###  <a name="security"></a><a name="Security"></a> Seguridad  
  
 No se requieren permisos para ejecutar la instrucción [EXECUTE](../../t-sql/language-elements/execute-transact-sql.md) , pero **se requieren** permisos para los elementos protegibles a los que se hace referencia en la cadena EXECUTE. Por ejemplo, si la cadena contiene una instrucción [INSERT](../../t-sql/statements/insert-transact-sql.md) , el autor de la llamada de la instrucción EXECUTE debe tener el permiso INSERT en la tabla de destino. Los permisos se comprueban cuando se encuentra la instrucción EXECUTE, incluso si la instrucción EXECUTE está incluida en un módulo. Para obtener más información, vea [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md).  
  
##  <a name="using-transact-sql"></a><a name="TsqlProcedure"></a> Usar Transact-SQL  
  
### <a name="example"></a>Ejemplo 
  
En este ejemplo se usa la función escalar `ufnGetSalesOrderStatusText` que está disponible en la mayoría de las ediciones de `AdventureWorks`.  El propósito de la función es devolver un valor de texto para el estado de las ventas de un entero dado.  Varíe el ejemplo pasando enteros del 1 al 7 para el parámetro **\@Status** .
  
~~~tsql
USE [AdventureWorks2016CTP3]
GO  

-- Declare a variable to return the results of the function. 
DECLARE @ret nvarchar(15);   

-- Execute the function while passing a value to the @status parameter
EXEC @ret = dbo.ufnGetSalesOrderStatusText 
    @Status = 5; 

-- View the returned value.  The Execute and Select statements must be executed at the same time.  
SELECT N'Order Status: ' + @ret; 

-- Result:
-- Order Status: Shipped
~~~
  
  
  
