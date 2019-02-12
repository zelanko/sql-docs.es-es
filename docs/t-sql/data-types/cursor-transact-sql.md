---
title: cursor (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/23/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- cursor data type
ms.assetid: fbea16ef-f2cc-4734-9149-ec2598fd3cca
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 1849a138410485a26be32e6a15603d5aa1a56de8
ms.sourcegitcommit: dfb1e6deaa4919a0f4e654af57252cfb09613dd5
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 02/11/2019
ms.locfileid: "56024026"
---
# <a name="cursor-transact-sql"></a>cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Un tipo de datos para las variables o para los parámetros de resultado de los procedimientos almacenados que contiene una referencia a un cursor.
  
## <a name="remarks"></a>Notas  
Las operaciones a las que pueden hacer referencia las variables y los parámetros que tienen un tipo de datos **cursor** son:
-   Las instrucciones DECLARE *@local_variable* y SET *@local_variable*.  
-   Las instrucciones del cursor OPEN, FETCH, CLOSE y DEALLOCATE.  
-   Los parámetros de resultado de procedimientos almacenados.  
-   La función CURSOR_STATUS.  
-   Los procedimientos almacenados del sistema **sp_cursor_list**, **sp_describe_cursor**, **sp_describe_cursor_tables** y **sp_describe_cursor_columns**.  
  
La columna de salida **cursor_name** de **sp_cursor_list** y **sp_describe_cursor** devuelve el nombre de la variable de cursor.
  
Cualquier variable creada con el tipo de datos **cursor** acepta valores NULL.
  
El tipo de datos **cursor** no se puede usar para una columna en una instrucción CREATE TABLE.
  
## <a name="see-also"></a>Vea también
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CURSOR_STATUS &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-status-transact-sql.md)  
[Conversiones de tipos de datos &#40;motor de base de datos&#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE CURSOR &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)
  
  
