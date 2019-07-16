---
title: CHANGE_TRACKING_IS_COLUMN_IN_MASK (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- CHANGE_TRACKING_IS_COLUMN_IN_MASK_TSQL
- CHANGE_TRACKING_IS_COLUMN_IN_MASK
dev_langs:
- TSQL
helpviewer_keywords:
- change tracking [SQL Server], CHANGE_TRACKING_IS_COLUMN_IN_MASK
- CHANGE_TRACKING_IS_COLUMN_IN_MASK
ms.assetid: 649b370b-da54-4915-919d-1b597a39d505
author: rothja
ms.author: jroth
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: a6f7e9d8d9ab99ebe4a7c5749033eacf85b8feb5
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68042992"
---
# <a name="changetrackingiscolumninmask-transact-sql"></a>CHANGE_TRACKING_IS_COLUMN_IN_MASK (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Interpreta el valor SYS_CHANGE_COLUMNS devuelto por la función CHANGETABLE(CHANGES...). Esto permite a una aplicación determinar si la columna especificada está incluida en los valores devueltos para SYS_CHANGE_COLUMNS.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
CHANGE_TRACKING_IS_COLUMN_IN_MASK ( column_id , change_columns )  
```  
  
## <a name="arguments"></a>Argumentos  
 *column_id*  
 Es el Id. de la columna que se está comprobando. La columna de identificador puede obtenerse mediante el uso de la [COLUMNPROPERTY](../../t-sql/functions/columnproperty-transact-sql.md) función.  
  
 *change_columns*  
 Son los datos binarios de la columna SYS_CHANGE_COLUMNS de los [CHANGETABLE](../../relational-databases/system-functions/changetable-transact-sql.md) datos.  
  
## <a name="return-type"></a>Tipo devuelto  
 **bit**  
  
## <a name="return-values"></a>Valores devueltos  
 CHANGE_TRACKING_IS_COLUMN_IN_MASK devuelve los siguientes valores.  
  
|Valor devuelto|Descripción|  
|------------------|-----------------|  
|0|La columna especificada no está en el *change_columns* lista.|  
|1|La columna especificada está en el *change_columns* lista.|  
  
## <a name="remarks"></a>Comentarios  
 CHANGE_TRACKING_IS_COLUMN_IN_MASK no realiza ninguna comprobación para validar el *column_id* valor o que el *change_columns* parámetro se obtuvo de la tabla desde el que el  *column_id* obtuvo.  
  
## <a name="examples"></a>Ejemplos  
 El siguiente ejemplo determina si la columna `Salary` de la tabla `Employees` está actualizada. El `COLUMNPROPERTY` función devuelve el Id. de columna de la `Salary` columna. La variable local `@change_columns` debe establecerse en los resultados de una consulta con CHANGETABLE como origen de datos.  
  
```sql  
SET @SalaryChanged = CHANGE_TRACKING_IS_COLUMN_IN_MASK  
    (COLUMNPROPERTY(OBJECT_ID('Employees'), 'Salary', 'ColumnId')  
    ,@change_columns);  
```  
  
## <a name="see-also"></a>Vea también  
 [Funciones de seguimiento de cambios &#40;Transact-SQL&#41;](../../relational-databases/system-functions/change-tracking-functions-transact-sql.md)   
 [CHANGETABLE &#40;Transact-SQL&#41;](../../relational-databases/system-functions/changetable-transact-sql.md)   
 [Seguimiento de cambios de datos &#40;SQL Server&#41;](../../relational-databases/track-changes/track-data-changes-sql-server.md)  
  
  
