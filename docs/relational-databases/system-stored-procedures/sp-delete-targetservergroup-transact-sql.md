---
title: sp_delete_targetservergroup (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_targetservergroup_TSQL
- sp_delete_targetservergroup
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_targetservergroup
ms.assetid: d8dd838e-64aa-419f-9ccb-ff04908cf3e4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2d6f00cf5fcc0cad2c5b6874b7302d00655e7a76
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85862374"
---
# <a name="sp_delete_targetservergroup-transact-sql"></a>sp_delete_targetservergroup (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Elimina el grupo de servidores de destino especificado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_delete_targetservergroup [ @name = ] 'name'   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @name = ] 'name'`Nombre del grupo de servidores de destino que se va a quitar. *Name* es de **tipo sysname**y no tiene ningún valor predeterminado.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se quita el grupo de servidores de destino `Servers Processing Customer Orders`.  
  
```  
USE msdb ;  
GO  
  
EXEC sp_delete_targetservergroup  
    @name = N'Servers Processing Customer Orders';  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [sp_add_targetservergroup &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-add-targetservergroup-transact-sql.md)   
 [sp_help_targetservergroup &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-help-targetservergroup-transact-sql.md)   
 [sp_update_targetservergroup &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-update-targetservergroup-transact-sql.md)  
  
  
