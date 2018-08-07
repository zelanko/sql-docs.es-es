---
title: BEGIN...END (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- BEGIN
- BEGIN_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- enclosing statements [SQL Server]
- BEGIN statement
- control-of-flow language [SQL Server], BEGIN...END statement
- BEGIN...END keyword
- grouping statements, BEGIN...END statement
- executing Transact-SQL statements together [SQL Server]
- statements [SQL Server], grouping
ms.assetid: fc2c7f76-f1f9-4f91-beef-bc8ef0da2feb
caps.latest.revision: 30
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: 819600311853e5dbd995e287302234c3dcd446e9
ms.sourcegitcommit: e02c28b0b59531bb2e4f361d7f4950b21904fb74
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 08/02/2018
ms.locfileid: "39451209"
---
# <a name="beginend-transact-sql"></a>BEGIN...END (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Incluye una serie de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] de forma que se pueda ejecutar un grupo de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)]. BEGIN y END son palabras clave del lenguaje de control de flujo.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
BEGIN  
    { sql_statement | statement_block }   
END  
```  
  
## <a name="arguments"></a>Argumentos  
 { *sql_statement* | *statement_block* }  
 Se trata de cualquier instrucción o grupo de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] definidas con un bloque de instrucciones.  
  
## <a name="remarks"></a>Notas  
 Los bloques BEGIN...END pueden anidarse.  
  
 Aunque todas las instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] son válidas en un bloque BEGIN...END, ciertas instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] no deben agruparse en el mismo proceso por lotes o bloque de instrucciones.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo, `BEGIN` y `END` definen un conjunto de instrucciones [!INCLUDE[tsql](../../includes/tsql-md.md)] que se ejecutan juntas. Si el bloqueo `BEGIN...END` no se incluye, ambas instrucciones `ROLLBACK TRANSACTION` se ejecutarán y se devolverán ambos mensajes `PRINT`.  
  
```  
USE AdventureWorks2012;  
GO  
BEGIN TRANSACTION;  
GO  
IF @@TRANCOUNT = 0  
BEGIN  
    SELECT FirstName, MiddleName   
    FROM Person.Person WHERE LastName = 'Adams';  
    ROLLBACK TRANSACTION;  
    PRINT N'Rolling back the transaction two times would cause an error.';  
END;  
ROLLBACK TRANSACTION;  
PRINT N'Rolled back the transaction.';  
GO  
/*  
Rolled back the transaction.  
*/  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
 En el siguiente ejemplo, `BEGIN` y `END` definen un conjunto de instrucciones [!INCLUDE[DWsql](../../includes/dwsql-md.md)] que se ejecutan juntas. Si no se incluye el bloque `BEGIN...END`, en el ejemplo siguiente se estará en un bucle continuo.  
  
```  
-- Uses AdventureWorks  
  
DECLARE @Iteration Integer = 0  
WHILE @Iteration <10  
BEGIN  
    SELECT FirstName, MiddleName   
    FROM dbo.DimCustomer WHERE LastName = 'Adams';  
SET @Iteration += 1  
END;  
  
```  
  
## <a name="see-also"></a>Ver también  
 [ALTER TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/alter-trigger-transact-sql.md)   
 [Lenguaje de control de flujo &#40;Transact-SQL&#41;](~/t-sql/language-elements/control-of-flow.md)   
 [CREATE TRIGGER &#40;Transact-SQL&#41;](../../t-sql/statements/create-trigger-transact-sql.md)   
 [END &#40;BEGIN...END&#41; &#40;Transact-SQL&#41;](../../t-sql/language-elements/end-begin-end-transact-sql.md)  
  
  


