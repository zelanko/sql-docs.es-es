---
title: Ejecutar funciones definidas por el usuario | Microsoft Docs
ms.custom: 
ms.date: 10/24/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- dbe-udf
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- invoking user-defined functions
- user-defined functions [SQL Server], executing
ms.assetid: 0de7744d-9b73-463f-ae80-e31a020004b5
caps.latest.revision: 35
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 08287922d15adabd1128da2edbb1caa65bc3f85f
ms.contentlocale: es-es
ms.lasthandoff: 06/22/2017

---
# <a name="execute-user-defined-functions"></a>Ejecutar funciones definidas por el usuario
  Ejecutar una función definida por el usuario mediante Transact-SQL.
  

> **Nota:** Visite  [Funciones definidas por el usuario](https://msdn.microsoft.com/library/ms191007.aspx) y [Create Function (Transact SQL)](https://msdn.microsoft.com/library/ms186755.aspx) para obtener más información acerca de las funciones definidas por el usuario. 
  
 
##  <a name="BeforeYouBegin"></a> Antes de empezar  
  
###  <a name="Restrictions"></a> Limitaciones y restricciones  
 En Transact-SQL, los parámetros se pueden proporcionar mediante *value* o @*parameter_name*=*value.* Un parámetro no forma parte de una transacción; por tanto, si se cambia un parámetro en una transacción que se revierte posteriormente, el valor del parámetro no vuelve a su valor anterior. El valor devuelto al procedimiento llamante es siempre el valor del parámetro en el momento en que finaliza el módulo llamado.  
  
###  <a name="Security"></a> Seguridad  
  
 No se requieren permisos para ejecutar la instrucción [EXECUTE](https://msdn.microsoft.com/library/ms188332.aspx) , pero **se requieren** permisos para los elementos protegibles a los que se hace referencia en la cadena EXECUTE. Por ejemplo, si la cadena contiene una instrucción [INSERT](https://msdn.microsoft.com/library/ms174335.aspx) , el autor de la llamada de la instrucción EXECUTE debe tener el permiso INSERT en la tabla de destino. Los permisos se comprueban cuando se encuentra la instrucción EXECUTE, incluso si la instrucción EXECUTE está incluida en un módulo. Para obtener más información, vea [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md).  
  
##  <a name="TsqlProcedure"></a> Usar Transact-SQL  
  
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
  
  
  

