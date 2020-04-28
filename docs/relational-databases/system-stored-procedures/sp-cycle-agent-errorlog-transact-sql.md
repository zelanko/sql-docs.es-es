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
ms.openlocfilehash: c95cc2db84bdf059437a45e2719bbc63d6eb6829
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68108351"
---
# <a name="sp_cycle_agent_errorlog-transact-sql"></a>sp_cycle_agent_errorlog (Transact-SQL)
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
  
## <a name="remarks"></a>Observaciones  
 Cada vez [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que se inicia el agente, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se cambia el nombre del registro de errores actual del agente a **SQLAgent. 1**; **SQLAgent. 1** se convierte en **SQLAgent. 2**, **SQLAgent. 2** se convierte en **SQLAgent. 3**, etc. **sp_cycle_agent_errorlog** permite recorrer los archivos de registro de errores sin tener que detener e iniciar el servidor.  
  
 Este procedimiento almacenado se debe ejecutar desde la base de datos **msdb** .  
  
## <a name="permissions"></a>Permisos  
 Los permisos de ejecución para **sp_cycle_agent_errorlog** están restringidos a los miembros del rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se realiza el ciclo del registro de errores del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_cycle_agent_errorlog ;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [sp_cycle_errorlog &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-cycle-errorlog-transact-sql.md)  
  
  
