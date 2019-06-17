---
title: sp_cycle_errorlog (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cycle_errorlog_TSQL
- sp_cycle_errorlog
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cycle_errorlog
ms.assetid: 61a12cbf-78a3-4052-8604-3b29d07573fd
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 565cc98059c056dbb4fc73f3e0734229754aad93
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "62724200"
---
# <a name="spcycleerrorlog-transact-sql"></a>sp_cycle_errorlog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cierra el archivo del registro de errores actual y continúa el ciclo de números de extensión de registro de errores, como ocurre al reiniciar el servidor. El nuevo registro de errores contiene información de versión y de copyright, y una línea que indica que se ha creado un nuevo registro.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_cycle_errorlog  
```  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 Cada vez que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] está iniciado, el registro de errores actual cambia a **errorlog.1**; **errorlog.1** se convierte en **errorlog.2**, **errorlog.2** se convierte en **errorlog.3**, y así sucesivamente. **sp_cycle_errorlog** permite ciclo de archivos de registro de errores sin tener que detener e iniciar el servidor.  
  
## <a name="permissions"></a>Permisos  
 Permisos de ejecución de **sp_cycle_errorlog** están restringidos a los miembros de la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se recorre el registro de errores de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
EXEC sp_cycle_errorlog ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_cycle_agent_errorlog &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cycle-agent-errorlog-transact-sql.md)  
  
  
