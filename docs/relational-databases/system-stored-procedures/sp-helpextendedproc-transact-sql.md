---
title: sp_helpextendedproc (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_helpextendedproc
- sp_helpextendedproc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpextendedproc
ms.assetid: 7e1f017e-c898-4225-b375-6a73ef9aac7b
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: cefcddf931e563c5ba5b2d632bdcf7d7f3c7edbb
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sphelpextendedproc-transact-sql"></a>sp_helpextendedproc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Indica los procedimientos almacenados extendidos definidos actualmente y el nombre de la biblioteca de vínculos dinámicos (DLL) a la que pertenece el procedimiento (o la función).  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] En su lugar, use la [integración con CLR](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) .  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpextendedproc [ [@funcname = ] 'procedure' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@funcname =**] **'***procedimiento***'**  
 Es el nombre del procedimiento almacenado extendido cuya información se va a presentar. *procedimiento* es **sysname**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Nombre**|**sysname**|Nombre del procedimiento almacenado extendido.|  
|**archivo DLL**|**nvarchar(255)**|Nombre de la DLL.|  
  
## <a name="remarks"></a>Comentarios  
 Cuando *procedimiento* se especifica, **sp_helpextendedproc** informes en las clases de procedimiento almacenado extendido. Si no se proporciona este parámetro, **sp_helpextendedproc** pertenece devuelve todos los extendidos, nombres de procedimientos almacenados y los nombres de archivo DLL para que cada procedimiento almacenado extendido.  
  
## <a name="permissions"></a>Permissions  
 Permiso para ejecutar **sp_helpextendedproc** se concede a **público**.  
  
## <a name="examples"></a>Ejemplos  
  
### <a name="a-reporting-help-on-all-extended-stored-procedures"></a>A. Presentar ayuda acerca de todos los procedimientos almacenados extendidos  
 El ejemplo siguiente informa de todos los procedimientos almacenados extendidos.  
  
```  
USE master;  
GO  
EXEC sp_helpextendedproc;  
GO  
```  
  
### <a name="b-reporting-help-on-a-single-extended-stored-procedure"></a>B. Presentar ayuda acerca de un solo procedimiento almacenado extendido  
 En el ejemplo siguiente se notifica en el `xp_cmdshell` el procedimiento almacenado extendido.  
  
```  
USE master;  
GO  
EXEC sp_helpextendedproc xp_cmdshell;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_addextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_dropextendedproc &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
