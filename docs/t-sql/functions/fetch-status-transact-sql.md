---
title: '@@FETCH_STATUS (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- '@@FETCH_STATUS'
- '@@FETCH_STATUS_TSQL'
dev_langs:
- TSQL
helpviewer_keywords:
- FETCH statement
- status information [SQL Server], FETCH
- '@@FETCH_STATUS function'
ms.assetid: 93659193-e4ff-4dfb-9043-0c4114921b91
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: d07892e1a47025107205f590d6a41aebebbb571a
ms.sourcegitcommit: 58158eda0aa0d7f87f9d958ae349a14c0ba8a209
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 03/30/2020
ms.locfileid: "68071565"
---
# <a name="x40x40fetch_status-transact-sql"></a>&#x40;&#x40;FETCH_STATUS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Esta función devuelve el estado de la última instrucción FETCH del cursor emitida contra cualquier cursor abierto actualmente por la conexión.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
@@FETCH_STATUS  
```  
  
## <a name="return-type"></a>Tipo de valor devuelto  
 **integer**  
  
## <a name="return-value"></a>Valor devuelto  
  
|Valor devuelto|Descripción|  
|------------------|-----------------|  
|&nbsp;0|La instrucción FETCH se ejecutó correctamente.|  
|-1|La instrucción FETCH no se ejecutó correctamente o la fila estaba más allá del conjunto de resultados.|  
|-2|Falta la fila capturada.|
|-9|El cursor no está realizando ninguna operación de búsqueda.|  
  
## <a name="remarks"></a>Observaciones  
Como `@@FETCH_STATUS` es global para todos los cursores de una conexión, úselo con cuidado. Después de ejecutar una instrucción FETCH, la prueba de `@@FETCH_STATUS` se debe realizar antes de que se ejecute otra instrucción FETCH sobre otro cursor. `@@FETCH_STATUS` no está definido antes de producirse las capturas en la conexión.  
  
Por ejemplo, supongamos que un usuario ejecuta una instrucción FETCH sobre un cursor y a continuación llama a un procedimiento almacenado que abre y procesa los resultados de otro cursor. Cuando devuelve el control desde el procedimiento almacenado llamado, `@@FETCH_STATUS` refleja la última instrucción FETCH ejecutada dentro de ese procedimiento almacenado, no la ejecutada antes de llamar al procedimiento almacenado.  
  
Para recuperar el último estado capturado de un cursor específico, realice una consulta en la columna **fetch_status** de la función de administración dinámica **sys.dm_exec_cursors**.  
  
## <a name="examples"></a>Ejemplos  
En este ejemplo se usa `@@FETCH_STATUS` para controlar las actividades del cursor en un bucle `WHILE`.  
  
```  
DECLARE Employee_Cursor CURSOR FOR  
SELECT BusinessEntityID, JobTitle  
FROM AdventureWorks2012.HumanResources.Employee;  
OPEN Employee_Cursor;  
FETCH NEXT FROM Employee_Cursor;  
WHILE @@FETCH_STATUS = 0  
   BEGIN  
      FETCH NEXT FROM Employee_Cursor;  
   END;  
CLOSE Employee_Cursor;  
DEALLOCATE Employee_Cursor;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [Funciones del cursor &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-functions-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)  
  
  
