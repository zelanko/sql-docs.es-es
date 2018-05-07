---
title: '@@ROWCOUNT (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 08/29/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.service: ''
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- '@@ROWCOUNT_TSQL'
- '@@ROWCOUNT'
dev_langs:
- TSQL
helpviewer_keywords:
- '@@ROWCOUNT function'
- number of rows affected by statement
- row affected by statements [SQL Server]
- statements [SQL Server], last statement
- counting rows
ms.assetid: 97a47998-81d9-4331-a244-9eb8b6fe4a56
caps.latest.revision: 40
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 78ffb0d32bb5f87b31f3dd24fa51dfcbeb36889d
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="x40x40rowcount-transact-sql"></a>&#x40;&#x40;ROWCOUNT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve el número de filas afectadas por la última instrucción. Si el número de filas superior a dos mil millones, use [ROWCOUNT_BIG](../../t-sql/functions/rowcount-big-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
@@ROWCOUNT  
```  
  
## <a name="return-types"></a>Tipos devueltos  
 **int**  
  
## <a name="remarks"></a>Notas  
 Las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] pueden establecer el valor de @@ROWCOUNT de las siguientes maneras:  
  
-   Establecer @@ROWCOUNT en el número de filas afectadas o leídas. Las filas pueden o no enviarse al cliente.  
  
-   Conservar @@ROWCOUNT de la anterior ejecución de una instrucción.  
  
-   Restablecer @@ROWCOUNT en 0 y no devolver el valor al cliente.  
  
 Las instrucciones que realizan una asignación simple siempre establecen el valor @@ROWCOUNT en 1. No se envían filas al cliente. Estos son algunos ejemplos de estas instrucciones: SET @*local_variable*, RETURN, READTEXT y SELECT sin instrucciones de consulta, como por ejemplo, SELECT GETDATE() o SELECT **'***Texto genérico***'**.  
  
 Las instrucciones que realizan una asignación en una consulta o usan RETURN en una consulta establecen el valor @@ROWCOUNT en el número de filas afectadas o leídas por la consulta, como por ejemplo: SELECT @*local_variable* = c1 FROM t1.  
  
 Las instrucciones de lenguaje de manipulación de datos (DML) establecen el valor de @@ROWCOUNT en el número de filas afectadas por la consulta y devuelven ese valor al cliente. Las instrucciones DML pueden no enviar ninguna fila al cliente.  
  
 DECLARE CURSOR y FETCH establecen el valor de @@ROWCOUNT en 1.  
  
 Las instrucciones EXECUTE conservan el valor anterior de @@ROWCOUNT.  
  
 Las instrucciones como USE, SET \<opción>, DEALLOCATE CURSOR, CLOSE CURSOR, BEGIN TRANSACTION o COMMIT TRANSACTION restablecen el valor de ROWCOUNT en 0.  
  
 Los procedimientos almacenados compilados de forma nativa mantienen el @@ROWCOUNT anterior. Las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] dentro de procedimientos almacenados compilados de forma nativa no establecen @@ROWCOUNT. Para más información, vea [Procedimientos almacenados compilados de forma nativa](../../relational-databases/in-memory-oltp/natively-compiled-stored-procedures.md).  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se ejecuta una instrucción `UPDATE` y se utiliza `@@ROWCOUNT` para detectar si ha cambiado alguna fila.  
  
```  
USE AdventureWorks2012;  
GO  
UPDATE HumanResources.Employee   
SET JobTitle = N'Executive'  
WHERE NationalIDNumber = 123456789  
IF @@ROWCOUNT = 0  
PRINT 'Warning: No rows were updated';  
GO  
```  
  
## <a name="see-also"></a>Ver también  
 [Funciones del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-functions/system-functions-for-transact-sql.md)   
 [SET ROWCOUNT &#40;Transact-SQL&#41;](../../t-sql/statements/set-rowcount-transact-sql.md)  
  
  
