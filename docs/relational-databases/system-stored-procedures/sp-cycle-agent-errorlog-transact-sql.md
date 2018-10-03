---
title: sp_cycle_agent_errorlog (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_cycle_agent_errorlog
- sp_cycle_agent_errorlog_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_cycle_agent_errorlog
ms.assetid: 8aa96182-60b7-4d7b-b2a7-ccce70378c6e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dfb1f3ef9dc8bdac81ed7c3a3a490ca91f73ff23
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47779243"
---
# <a name="spcycleagenterrorlog-transact-sql"></a>sp_cycle_agent_errorlog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cierra el archivo de registro de errores actual del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y continúa el ciclo de números de extensión de registro de errores del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como ocurre al reiniciar el servidor. El nuevo registro de errores del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contiene una línea que indica que se ha creado el registro nuevo.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_cycle_agent_errorlog  
```  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 Cada vez que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] el agente se inicia, actual [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se cambia el nombre de registro de errores del agente a **SQLAgent.1**; **SQLAgent.1** se convierte en **SQLAgent.2**, **SQLAgent.2** se convierte en **SQLAgent.3**, y así sucesivamente. **sp_cycle_agent_errorlog** permite ciclo de archivos de registro de errores sin tener que detener e iniciar el servidor.  
  
 Este procedimiento almacenado se debe ejecutar desde la **msdb** base de datos.  
  
## <a name="permissions"></a>Permisos  
 Permisos de ejecución de **sp_cycle_agent_errorlog** están restringidos a los miembros de la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se realiza el ciclo del registro de errores del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_cycle_agent_errorlog ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_cycle_errorlog &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-cycle-errorlog-transact-sql.md)  
  
  
