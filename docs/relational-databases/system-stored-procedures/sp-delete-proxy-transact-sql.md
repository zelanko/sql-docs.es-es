---
description: sp_delete_proxy (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: ccc9d7639bbe7f929a28b249e6767d0d703a0068
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89529245"
---
# <a name="sp_delete_proxy-transact-sql"></a>sp_delete_proxy (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Quita el proxy especificado.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_delete_proxy [ @proxy_id = ] id , [ @proxy_name = ] 'proxy_name'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @proxy_id = ] id` Número de identificación del proxy que se va a quitar. La *proxy_id* es de **tipo int**y su valor predeterminado es NULL.  
  
`[ @proxy_name = ] 'proxy_name'` Nombre del proxy que se va a quitar. La *proxy_name* es de **tipo sysname y su**valor predeterminado es NULL.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 None  
  
## <a name="remarks"></a>Observaciones  
 Se debe especificar ** \@ proxy_name** o ** \@ proxy_id** . Si se especifican los dos argumentos, deben hacer referencia al mismo proxy; de lo contrario, el procedimiento almacenado genera un error.  
  
 Si un paso de trabajo hace referencia al proxy especificado, este último no se podrá eliminar y el procedimiento almacenado generará un error.  
  
## <a name="permissions"></a>Permisos  
 De forma predeterminada, solo los miembros del rol fijo de servidor **sysadmin** pueden ejecutar **sp_delete_proxy**.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se elimina el proxy `Catalog application proxy`.  
  
```  
USE msdb ;  
GO  
  
EXEC dbo.sp_delete_proxy  
    @proxy_name = N'Catalog application proxy' ;  
GO  
```  
  
## <a name="see-also"></a>Consulte también  
 [sp_add_proxy &#40;&#41;de Transact-SQL ](../../relational-databases/system-stored-procedures/sp-add-proxy-transact-sql.md)  
  
  
