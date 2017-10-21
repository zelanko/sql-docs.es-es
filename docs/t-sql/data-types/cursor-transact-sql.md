---
title: cursor (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 7/23/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
helpviewer_keywords:
- cursor data type
ms.assetid: fbea16ef-f2cc-4734-9149-ec2598fd3cca
caps.latest.revision: 22
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 4b0b96a3bc147f51102fa10f2dff96b7f1761759
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="cursor-transact-sql"></a>cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Un tipo de datos para las variables o para los parámetros de resultado de los procedimientos almacenados que contiene una referencia a un cursor.
  
## <a name="remarks"></a>Comentarios  
Las operaciones que pueden hacer referencia a las variables y parámetros que tengan un **cursor** son de tipo de datos:
-   DECLARE  *@local_variable*  y establezca  *@local_variable*  instrucciones.  
-   Las instrucciones del cursor OPEN, FETCH, CLOSE y DEALLOCATE.  
-   Los parámetros de resultado de procedimientos almacenados.  
-   La función CURSOR_STATUS.  
-   El **sp_cursor_list**, **sp_describe_cursor**, **sp_describe_cursor_tables**, y **sp_describe_cursor_columns** almacenados del sistema procedimientos.  
  
El **cursor_name** columna de salida de **sp_cursor_list** y **sp_describe_cursor** devuelve el nombre de la variable de cursor.
  
Las variables creadas con el **cursor** tipo de datos admiten valores NULL.
  
El **cursor** no se puede usar el tipo de datos para una columna en una instrucción CREATE TABLE.
  
## <a name="see-also"></a>Vea también
[CAST y CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md)  
[CURSOR_STATUS &#40; Transact-SQL &#41;](../../t-sql/functions/cursor-status-transact-sql.md)  
[Conversiones de tipos de datos &#40; motor de base de datos &#41;](../../t-sql/data-types/data-type-conversion-database-engine.md)  
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)  
[DECLARE CURSOR &#40; Transact-SQL &#41;](../../t-sql/language-elements/declare-cursor-transact-sql.md)  
[DECLARE @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/declare-local-variable-transact-sql.md)  
[SET @local_variable &#40;Transact-SQL&#41;](../../t-sql/language-elements/set-local-variable-transact-sql.md)
  
  

