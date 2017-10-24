---
title: SET FMTONLY (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- FMTONLY_TSQL
- FMTONLY
- SET FMTONLY
- SET_FMTONLY_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- metadata [SQL Server], only metadata returned
- SET FMTONLY statement
- FMTONLY option
ms.assetid: 02a1d9ac-2e58-433c-9a07-2c5a4a2214e1
caps.latest.revision: 48
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 1cf925ce8ec9095acec90a34ed7d08f04826c2c1
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="set-fmtonly-transact-sql"></a>SET FMTONLY (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all_md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  Devuelve solo metadatos al cliente. Se puede usar para probar el formato de la respuesta sin ejecutar realmente la consulta.  
  
> [!NOTE]  
>  No utilice esta característica. Esta característica se ha reemplazado por [sp_describe_first_result_set &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-describe-first-result-set-transact-sql.md), [sp_describe_undeclared_parameters &#40; Transact-SQL &#41; ](../../relational-databases/system-stored-procedures/sp-describe-undeclared-parameters-transact-sql.md), [sys.dm_exec_describe_first_result_set &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-transact-sql.md), y [sys.dm_exec_describe_first_result_set_for_object &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-describe-first-result-set-for-object-transact-sql.md).  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
SET FMTONLY { ON | OFF }   
```  
  
## <a name="remarks"></a>Comentarios  
 Cuando se establece SET FMTONLY en ON, no se procesa ni se envía al cliente ninguna fila como resultado de una solicitud.  
  
 La opción SET FMTONLY se establece en tiempo de ejecución, no en tiempo de análisis.  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer al rol public.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-view-the-column-header-information-for-a-query-without-actually-running-the-query"></a>R: ver la información de encabezado de columna para una consulta sin ejecutar realmente la consulta.  
 En el ejemplo siguiente se cambia el valor de `SET FMTONLY` a `ON` y se ejecuta una instrucción `SELECT`. La opción hace que la instrucción solo devuelva la información de las columnas, sin ninguna fila de datos.  
  
```  
USE AdventureWorks2012;  
GO  
SET FMTONLY ON;  
GO  
SELECT *   
FROM HumanResources.Employee;  
GO  
SET FMTONLY OFF;  
GO  
```  
  
## <a name="examples-includesssdwfullincludessssdwfull-mdmd-and-includesspdwincludessspdw-mdmd"></a>Ejemplos: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] y[!INCLUDE[ssPDW](../../includes/sspdw-md.md)]  
  
### <a name="b-view-the-column-header-information-for-a-query-without-actually-running-the-query"></a>B. Ver la información de encabezado de columna para una consulta sin ejecutar realmente la consulta.  
 En el ejemplo siguiente se muestra cómo devolver únicamente la información de encabezado (metadatos) de columna de una consulta. El lote comienza con FMTONLY establecida en OFF y cambia FMTONLY en ON antes de la instrucción SELECT. Esto hace que la instrucción SELECT devolver sólo los encabezados de columna; se devuelve ninguna fila de datos.  
  
```  
-- Uses AdventureWorks  
  
BEGIN  
    SET FMTONLY OFF;  
    SET DATEFORMAT mdy;  
    SET FMTONLY ON;  
    SELECT * FROM dbo.DimCustomer;  
    SET FMTONLY OFF;  
END  
  
```  
  
## <a name="see-also"></a>Vea también  
 [Instrucciones SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  


