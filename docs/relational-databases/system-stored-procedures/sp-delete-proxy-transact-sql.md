---
title: sp_delete_proxy (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_delete_proxy
- sp_delete_proxy_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_delete_proxy
- DROP PROXY statement
ms.assetid: 44a1db13-b7f2-4dab-a1b5-b8dafb41737c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1db08d96a36112d686ab34db0b7989e910a01960
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47844063"
---
# <a name="spdeleteproxy-transact-sql"></a>sp_delete_proxy (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Quita el proxy especificado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_delete_proxy [ @proxy_id = ] id , [ @proxy_name = ] 'proxy_name'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ **@proxy_id**=] *Id.*  
 Número de identificación del proxy que se va a quitar. El *proxy_id* es **int**, su valor predeterminado es null.  
  
 [ **@proxy_name**=] **'***proxy_name***'**  
 Nombre del proxy que se va a quitar. El *proxy_name* es **sysname**, su valor predeterminado es null.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Comentarios  
 Cualquier **@proxy_name** o **@proxy_id** debe especificarse. Si se especifican los dos argumentos, deben hacer referencia al mismo proxy; de lo contrario, el procedimiento almacenado genera un error.  
  
 Si un paso de trabajo hace referencia al proxy especificado, este último no se podrá eliminar y el procedimiento almacenado generará un error.  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, solo los miembros de la **sysadmin** rol fijo de servidor puede ejecutar **sp_delete_proxy**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se elimina el proxy `Catalog application proxy`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_proxy  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>Vea también  
 [sp_add_proxy &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)  
  
  
