---
title: sp_getmergedeletetype (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- sp_getmergedeletetype
- sp_getmergedeletetype_TSQL
helpviewer_keywords:
- sp_getmergedeletetype
ms.assetid: 64450e4d-844d-4176-874e-f3845536f7d2
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3056c5c298fc1987e7c6f25e4a28220d3e033115
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 03/27/2019
ms.locfileid: "58535207"
---
# <a name="spgetmergedeletetype-transact-sql"></a>sp_getmergedeletetype (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Devuelve el tipo de eliminación de mezcla. Este procedimiento almacenado se ejecuta en el publicador de la base de datos de publicación o en el suscriptor de la base de datos de suscripción.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_getmergedeletetype [ @source_object = ] 'source_object', [ @rowguid =] 'rowguid', [ @delete_type=] delete_type OUTPUT  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @source_object = ] 'source_object'` Es el nombre del objeto de origen. *source_object* es **nvarchar (386)**, no tiene ningún valor predeterminado.  
  
`[ @rowguid = ] 'rowguid'` Es el identificador de fila del tipo de eliminación. *ROWGUID* es **uniqueidentifier**, no tiene ningún valor predeterminado.  
  
`[ @delete_type = ] delete_type OUTPUT` Es el código que indica el tipo de eliminación. *delete_type* es **int**, no tiene ningún valor predeterminado. *delete_type* también es un parámetro de salida, y puede tener uno de estos valores.  
  
|Valor|Descripción|  
|-----------|-----------------|  
|**1**|Eliminación por parte del usuario|  
|**5**|Eliminación parcial|  
|**6**|Eliminación por parte del sistema|  
  
## <a name="remarks"></a>Comentarios  
 **sp_getmergedeletetype** se utiliza en la replicación de mezcla.  
  
## <a name="permissions"></a>Permisos  
 Solo los miembros de la **sysadmin** rol fijo de servidor o el **db_owner** rol fijo de base de datos se puede ejecutar **sp_getmergedeletetype**.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
