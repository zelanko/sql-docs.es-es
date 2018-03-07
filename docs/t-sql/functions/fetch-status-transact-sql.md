---
title: '@@FETCH_STATUS (Transact-SQL) | Documentos de Microsoft'
ms.custom: 
ms.date: 09/18/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Active
ms.openlocfilehash: 9bc4027eb6be9d79599cb06f7935bd2d052bb2a2
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
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
|-9|El cursor no está realizando una operación de búsqueda.|  
  
## <a name="remarks"></a>Comentarios  
 Dado que @@FETCH_STATUS es global para todos los cursores de una conexión, utilice @@FETCH_STATUS cuidadosamente. Después de ejecuta una instrucción FETCH, la comprobación de @@FETCH_STATUS deben tener lugar antes de que se ejecuta otra instrucción FETCH sobre otro cursor. El valor de @@FETCH_STATUS no está definido antes de producirse las capturas en la conexión.  
  
 Por ejemplo, supongamos que un usuario ejecuta una instrucción FETCH sobre un cursor y a continuación llama a un procedimiento almacenado que abre y procesa los resultados de otro cursor. Cuando el control se devuelve desde el procedimiento almacenado llamado, @@FETCH_STATUS refleja la última captura ejecutada en el procedimiento almacenado, no la instrucción de captura que se ejecuta antes de que se llama al procedimiento almacenado.  
  
 Para recuperar el último estado de un cursor específico, consulte la **fetch_status** columna de la **sys.dm_exec_cursors** función de administración dinámica.  
  
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
  
## <a name="see-also"></a>Vea también  
 [Funciones del cursor &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-functions-transact-sql.md)   
 [FETCH &#40; Transact-SQL &#41;](../../t-sql/language-elements/fetch-transact-sql.md)  
  
  
