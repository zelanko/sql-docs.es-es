---
title: sp_dropextendedproc (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 10/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dropextendedproc
- sp_dropextendedproc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dropextendedproc
ms.assetid: dd93af2c-1b7d-4e39-af23-2d21d270a381
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 645d9d6f1951c1e35bd8e72f764f46a209a77161
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82830156"
---
# <a name="sp_dropextendedproc-transact-sql"></a>sp_dropextendedproc (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita un procedimiento almacenado extendido.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]En su lugar, use la [integración con CLR](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) .  
  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
sp_dropextendedproc [ @functname = ] 'procedure'   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @functname = ] 'procedure'`Es el nombre del procedimiento almacenado extendido que se va a quitar. *procedure* es de tipo **nvarchar (** de-bajo) y no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Observaciones  
 Al ejecutar **sp_dropextendedproc** se quita el nombre del procedimiento almacenado extendido definido por el usuario de la vista de catálogo [Sys. Objects](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md) y se quita la entrada de la vista de catálogo [Sys. extended_procedures](../../relational-databases/system-catalog-views/sys-extended-procedures-transact-sql.md) . Este procedimiento almacenado solo se puede ejecutar en la base de datos **maestra** .  
  
**sp_dropextendedproc** no quita los procedimientos almacenados extendidos del sistema. En su lugar, el administrador del sistema debe denegar el permiso EXECUTe para el procedimiento almacenado extendido al rol **Public** .  
  
 no se puede ejecutar **sp_dropextendedproc** dentro de una transacción.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros del rol fijo de servidor **sysadmin** pueden ejecutar **sp_dropextendedproc**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se quita el procedimiento almacenado extendido `xp_hello`.  
  
> [!NOTE]  
>  Este procedimiento almacenado extendido debe existir; en caso contrario, aparecerá un mensaje de error.  
  
```  
USE master;  
GO  
EXEC sp_dropextendedproc 'xp_hello';  
```  
  
## <a name="see-also"></a>Consulte también  
 [sp_addextendedproc &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_helpextendedproc &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-helpextendedproc-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
