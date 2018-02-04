---
title: sp_delete_targetserver (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_delete_targetserver
- sp_delete_targetserver_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_targetserver
ms.assetid: cc438701-ad91-419d-9f23-ebc4c548c700
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5f95d6489635c40a7ba478e4100cb672dc6938c2
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="spdeletetargetserver-transact-sql"></a>sp_delete_targetserver (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita el servidor especificado de la lista de servidores de destino disponibles.  
   
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_delete_targetserver [ @server_name = ] 'server'   
     [ , [ @clear_downloadlist = ] clear_downloadlist ]  
     [ , [ @post_defection = ] post_defection ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@server_name=** ] **'***server***'**  
 Es el nombre del servidor que se va a quitar como servidor de destino disponible. *servidor* es **nvarchar (30)**, no tiene ningún valor predeterminado.  
  
 [ **@clear_downloadlist=** ] *clear_downloadlist*  
 Especifica si se debe borrar la lista de descarga para el servidor de destino. *clear_downloadlist* es de tipo **bits**, su valor predeterminado es **1**. Cuando *clear_downloadlist* es **1**, el procedimiento borra la lista de descarga para el servidor antes de eliminar el servidor. Cuando *clear_downloadlist* es **0**, no se borra la lista de descarga.  
  
 [ **@post_defection=** ] *post_defection*  
 Especifica si se va a enviar una instrucción Dar de baja al servidor de destino. *post_defection* es de tipo **bits**, su valor predeterminado es 1. Cuando *post_defection* es **1**, el procedimiento envía una instrucción dar de baja al servidor de destino antes de eliminar el servidor. Cuando *post_defection* es **0**, el procedimiento no expone una instrucción dar de baja al servidor de destino.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 La forma normal de eliminar un servidor de destino es llamar a **sp_msx_defect** en el servidor de destino. Use **sp_delete_targetserver** sólo cuando es necesaria una baja manual.  
  
## <a name="permissions"></a>Permissions  
 Para ejecutar este procedimiento almacenado, deben concederse a los usuarios la **sysadmin** rol fijo de servidor.  
  
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
 [sp_help_targetserver &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-targetserver-transact-sql.md)   
 [sp_msx_defect &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-msx-defect-transact-sql.md)   
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
