---
title: CURSOR_STATUS (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 07/24/2017
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
- CURSOR_STATUS
- CURSOR_STATUS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- status information [SQL Server], cursors
- CURSOR_STATUS function
- cursors [SQL Server], status information
ms.assetid: 3a4a840e-04f8-43bd-aada-35d78c3cb6b0
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 59a2cd382855f47d7cb37a3bc00bc723dde8f6df
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="cursorstatus-transact-sql"></a>CURSOR_STATUS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Una función escalar que permite a quien llama en un procedimiento almacenado determinar si el procedimiento ha devuelto un cursor y un conjunto de resultados para un parámetro dado.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
CURSOR_STATUS   
     (  
          { 'local' , 'cursor_name' }   
          | { 'global' , 'cursor_name' }   
          | { 'variable' , 'cursor_variable' }   
     )  
```  
  
## <a name="arguments"></a>Argumentos  
'local'  
Especifica una constante que indica que el origen del cursor es un nombre de cursor local.
  
'*cursor_name*'  
Es el nombre del cursor. Un nombre de cursor debe ajustarse a las reglas para los identificadores.
  
'global'  
Especifica una constante que indica que el origen del cursor es un nombre de cursor global.
  
'variable'  
Especifica una constante que indica que el origen del cursor es una variable local.
  
'*cursor_variable*'  
Es el nombre de la variable de cursor. Una variable de cursor debe definirse mediante el tipo de datos **cursor**.
  
## <a name="return-types"></a>Tipos de valores devueltos
**smallint**
  
|Valor devuelto|Nombre de cursor|Variable de cursor|  
|---|---|---|
|1|El conjunto de resultados del cursor tiene al menos una fila.<br /><br /> Para los cursores INSENSITIVE y de conjunto de claves, el conjunto de resultados tiene al menos una fila.<br /><br /> Para los cursores dinámicos, el conjunto de resultados puede tener cero, una o más filas.|El cursor asignado a esta variable está abierto.<br /><br /> Para los cursores INSENSITIVE y de conjunto de claves, el conjunto de resultados tiene al menos una fila.<br /><br /> Para los cursores dinámicos, el conjunto de resultados puede tener cero, una o más filas.|  
|0|El conjunto de resultados del cursor está vacío.*|El cursor asignado a esta variable está abierto, pero el conjunto de resultados está definitivamente vacío.*|  
|-1|El cursor está cerrado.|El cursor asignado a esta variable está cerrado.|  
|-2|No aplicable.|Puede ser:<br /><br /> El procedimiento llamado anteriormente no ha asignado ningún cursor a esta variable OUTPUT.<br /><br /> El procedimiento llamado anteriormente asignó un cursor a esta variable OUTPUT, pero se encontraba en un estado cerrado al terminar el procedimiento. Por tanto, se cancela la asignación del cursor y no se devuelve al procedimiento que hace la llamada.<br /><br /> No hay ningún cursor asignado a una variable declarada de cursor.|  
|-3|No existe ningún cursor con el nombre indicado.|No existe una variable de cursor con el nombre indicado o, si existe, no tiene todavía ningún cursor asignado.|  
  
*Los cursores dinámicos no devuelven nunca este resultado.
  
## <a name="examples"></a>Ejemplos  
En el ejemplo siguiente, se usa la función `CURSOR_STATUS` para mostrar el estado de un cursor antes y después de abrirlo y cerrarlo.
  
```sql
CREATE TABLE #TMP  
(  
   ii int  
)  
GO  
  
INSERT INTO #TMP(ii) VALUES(1)  
INSERT INTO #TMP(ii) VALUES(2)  
INSERT INTO #TMP(ii) VALUES(3)  
  
GO  
  
--Create a cursor.  
DECLARE cur CURSOR  
FOR SELECT * FROM #TMP  
  
--Display the status of the cursor before and after opening  
--closing the cursor.  
  
SELECT CURSOR_STATUS('global','cur') AS 'After declare'  
OPEN cur  
SELECT CURSOR_STATUS('global','cur') AS 'After Open'  
CLOSE cur  
SELECT CURSOR_STATUS('global','cur') AS 'After Close'  
  
--Remove the cursor.  
DEALLOCATE cur  
  
--Drop the table.  
DROP TABLE #TMP  
  
```  
  
[!INCLUDE[ssResult](../../includes/ssresult-md.md)]
  
```
After declare
---------------
-1  
  
After Open
----------
1  
  
After Close
-----------
-1
```  
  
## <a name="see-also"></a>Vea también
[Funciones del cursor &#40;Transact-SQL&#41;](../../t-sql/functions/cursor-functions-transact-sql.md)  
[Tipos de datos &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)
  
  
