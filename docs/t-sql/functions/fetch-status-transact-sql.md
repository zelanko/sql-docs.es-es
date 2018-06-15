---
title: '@@FETCH_STATUS (Transact-SQL) | Microsoft Docs'
ms.custom: ''
ms.date: 09/18/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: t-sql|functions
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
caps.latest.revision: 39
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 46b6c72283ab0ead6aad871f3801fb3ed967f8f4
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "33055572"
---
# <a name="x40x40fetchstatus-transact-sql"></a>&#x40;&#x40;FETCH_STATUS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve el estado de la última instrucción FETCH del cursor emitida contra cualquier cursor abierto actualmente por la conexión.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
@@FETCH_STATUS  
```  
  
## <a name="return-type"></a>Tipo devuelto  
 **integer**  
  
## <a name="return-value"></a>Valor devuelto  
  
|Valor devuelto|Description|  
|------------------|-----------------|  
|0|La instrucción FETCH se ejecutó correctamente.|  
|-1|La instrucción FETCH no se ejecutó correctamente o la fila estaba más allá del conjunto de resultados.|  
|-2|Falta la fila capturada.|
|-9|El cursor no está realizando ninguna operación de búsqueda.|  
  
## <a name="remarks"></a>Notas  
 Como @@FETCH_STATUS es global para todos los cursores de una conexión, use @@FETCH_STATUS con cuidado. Después de ejecutar una instrucción FETCH, la prueba de @@FETCH_STATUS se debe realizar antes de que se ejecute otra instrucción FETCH sobre otro cursor. El valor de @@FETCH_STATUS no está definido antes de producirse las capturas en la conexión.  
  
 Por ejemplo, supongamos que un usuario ejecuta una instrucción FETCH sobre un cursor y a continuación llama a un procedimiento almacenado que abre y procesa los resultados de otro cursor. Cuando vuelve el control desde el procedimiento almacenado llamado, @@FETCH_STATUS reflejará la última instrucción FETCH ejecutada en el procedimiento almacenado, no la ejecutada antes de llamar al procedimiento.  
  
 Para recuperar el último estado capturado de un cursor específico, realice una consulta en la columna **fetch_status** de la función de administración dinámica **sys.dm_exec_cursors**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se usa `@@FETCH_STATUS` para controlar las actividades del cursor en un bucle `WHILE`.  
  
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
  
## <a name="see-also"></a>Ver también  
 [Funciones del cursor &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-functions-transact-sql.md)   
 [FETCH &#40;Transact-SQL&#41;](../../t-sql/language-elements/fetch-transact-sql.md)  
  
  
