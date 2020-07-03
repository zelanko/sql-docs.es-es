---
title: sp_helpextendedproc (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpextendedproc
- sp_helpextendedproc_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpextendedproc
ms.assetid: 7e1f017e-c898-4225-b375-6a73ef9aac7b
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: bf7e95f30eb4a6abdc61b47b5f64b20f0ed4b27a
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85881576"
---
# <a name="sp_helpextendedproc-transact-sql"></a>sp_helpextendedproc (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Indica los procedimientos almacenados extendidos definidos actualmente y el nombre de la biblioteca de vínculos dinámicos (DLL) a la que pertenece el procedimiento (o la función).  
  
> [!NOTE]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]En su lugar, use la [integración con CLR](../../relational-databases/clr-integration/common-language-runtime-integration-overview.md) .  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_helpextendedproc [ [@funcname = ] 'procedure' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @funcname = ] 'procedure'`Es el nombre del procedimiento almacenado extendido cuya información se va a presentar. *procedure* es de **tipo sysname y su**valor predeterminado es NULL.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 0 (correcto) o 1 (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**name**|**sysname**|Nombre del procedimiento almacenado extendido.|  
|**dll**|**nvarchar(255)**|Nombre de la DLL.|  
  
## <a name="remarks"></a>Comentarios  
 Cuando se especifica *procedure* , **sp_helpextendedproc** informes en el procedimiento almacenado extendido especificado. Cuando no se proporciona este parámetro, **sp_helpextendedproc** devuelve todos los nombres de procedimientos almacenados extendidos y los nombres de dll a los que pertenece cada procedimiento almacenado extendido.  
  
## <a name="permissions"></a>Permisos  
 El permiso para ejecutar **sp_helpextendedproc** se concede a **Public**.  
  
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
 En el siguiente ejemplo se informa del `xp_cmdshell` procedimiento almacenado extendido.  
  
```  
USE master;  
GO  
EXEC sp_helpextendedproc xp_cmdshell;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [sp_addextendedproc &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-addextendedproc-transact-sql.md)   
 [sp_dropextendedproc &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-dropextendedproc-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
