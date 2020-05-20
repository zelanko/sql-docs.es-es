---
title: sp_update_targetservergroup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_update_targetservergroup_TSQL
- sp_update_targetservergroup
dev_langs:
- TSQL
helpviewer_keywords:
- sp_update_targetservergroup
ms.assetid: 4ac65ed6-e07e-40e4-a282-13bfd92dfa41
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 46e14eb91dde8018abcc52fe618dd9ff688a15b3
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82809123"
---
# <a name="sp_update_targetservergroup-transact-sql"></a>sp_update_targetservergroup (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Cambia el nombre del grupo de servidores de destino especificado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_update_targetservergroup  
     [@name =] 'current_name' ,  
     [@new_name =] 'new_name'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @name = ] 'current_name'`Nombre del grupo de servidores de destino. *current_name* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
`[ @new_name = ] 'new_name'`Nuevo nombre del grupo de servidores de destino. *new_name* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="permissions"></a>Permisos  
 Para ejecutar este procedimiento almacenado, se debe conceder a los usuarios el rol fijo de servidor **sysadmin** .  
  
## <a name="remarks"></a>Comentarios  
 **sp_update_targetservergroup** se debe ejecutar desde la base de datos **msdb** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se cambia el nombre del grupo de servidores de destino `Servers Processing Customer Orders` a `Local Servers Processing Customer Orders`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_update_targetservergroup  
    @name = N'Servers Processing Customer Orders',  
    @new_name = N'Local Servers Processing Customer Orders' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [sp_add_targetservergroup &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql.md)   
 [sp_delete_targetservergroup &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-delete-targetservergroup-transact-sql.md)   
 [sp_help_targetservergroup &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-help-targetservergroup-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
