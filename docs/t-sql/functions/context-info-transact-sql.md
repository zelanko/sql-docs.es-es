---
title: CONTEXT_INFO  (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/24/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.suite: sql
ms.technology: t-sql
ms.tgt_pltfrm: ''
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
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7f3d572bee6b06ef8cb1573759ec12e68f9e6ec9
ms.sourcegitcommit: 05e18a1e80e61d9ffe28b14fb070728b67b98c7d
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 07/04/2018
ms.locfileid: "37792196"
---
# <a name="contextinfo--transact-sql"></a>CONTEXT_INFO  (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

Esta función devuelve el valor **context_info** establecido para la sesión o lote actual, o derivada del uso de la instrucción [SET CONTEXT_INFO](../../t-sql/statements/set-context-info-transact-sql.md).
  
![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxis  
  
```sql
CONTEXT_INFO()  
```  
  
## <a name="return-value"></a>Valor devuelto
El valor **context_info**.
  
Si **context_info** no se ha establecido:
-   En [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] devuelve NULL.  
-   En [!INCLUDE[ssSDS](../../includes/sssds-md.md)] devuelve un GUID único específico de sesión.  
  
## <a name="remarks"></a>Notas  
La característica de conjuntos de resultados activos múltiples (MARS) permite a las aplicaciones ejecutar varios lotes o solicitudes al mismo tiempo en la misma conexión. Cuando uno de los lotes de una conexión MARS ejecuta SET CONTEXT_INFO, la función `CONTEXT_INFO` devuelve el nuevo valor de contexto cuando la función `CONTEXT_INFO` se ejecuta en el mismo lote que la instrucción SET. Si la función `CONTEXT_INFO` se ejecuta en uno o más de los otros lotes de conexión, `CONTEXT_FUNCTION` no devuelve el nuevo valor a menos que esos lotes hayan comenzado después de completar el lote que ejecutó la instrucción SET.
  
## <a name="permissions"></a>Permisos  
No requiere permisos especiales. Las siguientes vistas del sistema almacenan la información de contexto, pero la consulta directa de estas vistas requiere los permisos SELECT y VIEW SERVER STATE:
- **sys.dm_exec_requests**
- **sys.dm_exec_sessions**
- **sys.sysprocesses**
  
## <a name="examples"></a>Ejemplos  
En este ejemplo sencillo se establece el valor de **context_info** en `0x1256698456` y, después, se usa la función `CONTEXT_INFO` para recuperarlo.
  
```sql
SET CONTEXT_INFO 0x1256698456;  
GO  
SELECT CONTEXT_INFO();  
GO  
```  
  
## <a name="see-also"></a>Vea también
[SET CONTEXT_INFO &#40;Transact-SQL&#41;](../../t-sql/statements/set-context-info-transact-sql.md)
  
  
