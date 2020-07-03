---
title: sp_delete_targetserver (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_targetserver
- sp_delete_targetserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_targetserver
ms.assetid: cc438701-ad91-419d-9f23-ebc4c548c700
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4489e34ec83bd3981e464e72cb8e72885fcc994f
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85862190"
---
# <a name="sp_delete_targetserver-transact-sql"></a>sp_delete_targetserver (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Quita el servidor especificado de la lista de servidores de destino disponibles.  
   
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_delete_targetserver [ @server_name = ] 'server'   
     [ , [ @clear_downloadlist = ] clear_downloadlist ]  
     [ , [ @post_defection = ] post_defection ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @server_name = ] 'server'`Nombre del servidor que se va a quitar como servidor de destino disponible. el *servidor* es de tipo **nvarchar (30)** y no tiene ningún valor predeterminado.  
  
`[ @clear_downloadlist = ] clear_downloadlist`Especifica si se va a borrar la lista de descarga del servidor de destino. *clear_downloadlist* es de tipo **bit**y su valor predeterminado es **1**. Cuando *clear_downloadlist* es **1**, el procedimiento borra la lista de descarga del servidor antes de eliminar el servidor. Cuando *clear_downloadlist* es **0**, la lista de descarga no se borra.  
  
`[ @post_defection = ] post_defection`Especifica si se va a publicar una instrucción de defecto en el servidor de destino. *post_defection* es de tipo **bit**y su valor predeterminado es 1. Cuando *post_defection* es **1**, el procedimiento expone una instrucción defect en el servidor de destino antes de eliminar el servidor. Cuando *post_defection* es **0**, el procedimiento no publica una instrucción de defecto en el servidor de destino.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Observaciones  
 La forma normal de eliminar un servidor de destino es llamar a **sp_msx_defect** en el servidor de destino. Utilice **sp_delete_targetserver** solo cuando sea necesaria una baja manual.  
  
## <a name="permissions"></a>Permisos  
 Para ejecutar este procedimiento almacenado, se debe conceder a los usuarios el rol fijo de servidor **sysadmin** .  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se quita el servidor `LONDON1` de los servidores de trabajo disponibles.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_targetserver  
  @server_name = N'LONDON1' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_help_targetserver &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-help-targetserver-transact-sql.md)   
 [sp_msx_defect &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-msx-defect-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
