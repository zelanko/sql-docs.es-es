---
title: sp_cycle_agent_errorlog (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_cycle_agent_errorlog
- sp_cycle_agent_errorlog_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_cycle_agent_errorlog
ms.assetid: 8aa96182-60b7-4d7b-b2a7-ccce70378c6e
caps.latest.revision: "16"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 59c6136224bc639c4609dd149ade598b3ef80940
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/17/2017
---
# <a name="spcycleagenterrorlog-transact-sql"></a>sp_cycle_agent_errorlog (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cierra el archivo de registro de errores actual del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y continúa el ciclo de números de extensión de registro de errores del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como ocurre al reiniciar el servidor. El nuevo registro de errores del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contiene una línea que indica que se ha creado el registro nuevo.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a través de la [versión actual](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_cycle_agent_errorlog  
```  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Ninguno  
  
## <a name="remarks"></a>Comentarios  
 Cada vez que [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] agente se inicia, actual [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] registro de errores del agente cambia a **SQLAgent.1**; **SQLAgent.1** se convierte en **SQLAgent.2**, **SQLAgent.2** se convierte en **SQLAgent.3**, y así sucesivamente. **sp_cycle_agent_errorlog** permite ciclo los archivos de registro de errores sin tener que detener e iniciar el servidor.  
  
 Este procedimiento almacenado se debe ejecutar desde la **msdb** base de datos.  
  
## <a name="permissions"></a>Permissions  
 Permisos de ejecución para **sp_cycle_agent_errorlog** están restringidos a los miembros de la **sysadmin** rol fijo de servidor.  
  
## <a name="examples"></a>Ejemplos  
 En el siguiente ejemplo se realiza el ciclo del registro de errores del Agente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_cycle_agent_errorlog ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_cycle_errorlog &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-cycle-errorlog-transact-sql.md)  
  
  
