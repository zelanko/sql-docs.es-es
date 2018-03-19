---
title: CONTEXT_INFO  (Transact-SQL) | Microsoft Docs
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
- CONTEXT_INFO_TSQL
- CONTEXT_INFO
dev_langs:
- TSQL
helpviewer_keywords:
- CONTEXT_INFO function
- Multiple Active Result Sets
- context information [SQL Server]
- MARS [SQL Server]
- session context information [SQL Server]
ms.assetid: 571320f5-7228-4b0e-9d01-ab732d2d1eab
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: a647bc7ced2188a45183200f08400f5507f7b328
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="contextinfo--transact-sql"></a>CONTEXT_INFO  (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve el valor **context_info** establecido para la sesión o lote actual mediante la instrucción [SET CONTEXT_INFO](../../t-sql/statements/set-context-info-transact-sql.md).
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
CONTEXT_INFO()  
```  
  
## <a name="return-value"></a>Valor devuelto
El valor de **context_info**.
  
Si **context_info** no se ha establecido:
-   En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve NULL.  
-   En [!INCLUDE[ssSDS](../../includes/sssds-md.md)] devuelve un GUID único específico de sesión.  
  
## <a name="remarks"></a>Notas  
Los conjuntos de resultados activos múltiples (MARS) permiten a las aplicaciones ejecutar varios lotes o solicitudes al mismo tiempo en la misma conexión. Cuando uno de los lotes de una conexión MARS ejecuta SET CONTEXT_INFO, la función CONTEXT_INFO devuelve el nuevo valor de contexto cuando se ejecuta en el mismo lote que la instrucción SET. La función CONTEXT_INFO ejecutada en uno o varios de los demás lotes de la conexión no devuelve el nuevo valor a menos que se hayan iniciado después de haber finalizado el lote que ejecutó la instrucción SET.
  
## <a name="permissions"></a>Permisos  
No requiere permisos especiales. La información de contexto también se almacena en las vistas del sistema **sys.dm_exec_requests**, **sys.dm_exec_sessions** y **sys.sysprocesses**, pero para consultar estas vistas directamente se requieren los permisos SELECT y VIEW SERVER STATE.
  
## <a name="examples"></a>Ejemplos  
En este ejemplo se establece el valor de **context_info** en `0x1256698456` y, después, se usa la función `CONTEXT_INFO` para recuperarlo.
  
```sql
SET CONTEXT_INFO 0x1256698456;  
GO  
SELECT CONTEXT_INFO();  
GO  
```  
  
## <a name="see-also"></a>Vea también
[SET CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)
  
  
