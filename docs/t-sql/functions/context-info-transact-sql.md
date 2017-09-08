---
title: CONTEXT_INFO (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 07/24/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
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
caps.latest.revision: 19
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: dd261b2f7f1cc4234792bec66c3662d6d9b8dcd8
ms.contentlocale: es-es
ms.lasthandoff: 09/01/2017

---
# <a name="contextinfo--transact-sql"></a>CONTEXT_INFO (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Devuelve el **context_info** valor que se haya establecido para la sesión actual o el lote mediante la [SET CONTEXT_INFO](../../t-sql/statements/set-context-info-transact-sql.md) instrucción.
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
CONTEXT_INFO()  
```  
  
## <a name="return-value"></a>Valor devuelto
El valor de **context_info**.
  
Si **context_info** no se ha establecido:
-   En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve NULL.  
-   En [!INCLUDE[ssSDS](../../includes/sssds-md.md)] devuelve un GUID único de específicas de la sesión.  
  
## <a name="remarks"></a>Comentarios  
Los conjuntos de resultados activos múltiples (MARS) permiten a las aplicaciones ejecutar varios lotes o solicitudes al mismo tiempo en la misma conexión. Cuando uno de los lotes de una conexión MARS ejecuta SET CONTEXT_INFO, la función CONTEXT_INFO devuelve el nuevo valor de contexto cuando se ejecuta en el mismo lote que la instrucción SET. La función CONTEXT_INFO ejecutada en uno o varios de los demás lotes de la conexión no devuelve el nuevo valor a menos que se hayan iniciado después de haber finalizado el lote que ejecutó la instrucción SET.
  
## <a name="permissions"></a>Permissions  
No requiere permisos especiales. También se almacena la información de contexto en el **sys.dm_exec_requests**, **sys.dm_exec_sessions**, y **sys.sysprocesses** vistas del sistema, pero la consulta directa a las vistas requiere permisos SELECT y VIEW SERVER STATE.
  
## <a name="examples"></a>Ejemplos  
El ejemplo siguiente se establece la **context_info** valor `0x1256698456`y, a continuación, usa el `CONTEXT_INFO` función para recuperar el valor.
  
```sql
SET CONTEXT_INFO 0x1256698456;  
GO  
SELECT CONTEXT_INFO();  
GO  
```  
  
## <a name="see-also"></a>Vea también
[SET CONTEXT_INFO &#40; Transact-SQL &#41;](../../t-sql/statements/set-context-info-transact-sql.md)
  
  

