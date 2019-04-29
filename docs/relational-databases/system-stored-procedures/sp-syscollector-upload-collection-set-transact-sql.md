---
title: sp_syscollector_upload_collection_set (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_upload_collection_set
- sp_syscollector_upload_collection_set_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_upload_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: eed9232c-2b0a-4b6a-8ba0-76b7c99f48dc
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: d246e2817c34449ab6d4dd5d3def62feba92b196
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63001306"
---
# <a name="spsyscollectoruploadcollectionset-transact-sql"></a>sp_syscollector_upload_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Inicia una carga de datos de conjuntos de recopilación si el conjunto de recopilación está habilitado.  
  
> [!IMPORTANT]  
>  Este procedimiento almacenado solo se puede utilizar para conjuntos de recopilación configurados para la recopilación y carga de datos en modo de almacenamiento en caché.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_syscollector_upload_collection_set [[ @collection_set_id = ] collection_set_id ]  
          , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>Argumentos  
`[ @collection_set_id = ] collection_set_id` Es el identificador local único del conjunto de recopilación. *collection_set_id* es **int** y debe tener un valor si *nombre* es NULL.  
  
`[ @name = ] 'name'` Es el nombre del conjunto de recopilación. *nombre* es **sysname** y debe tener un valor si *collection_set_id* es NULL.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 Cualquier *collection_set_id* o *nombre* debe tener un valor; no puede ser NULL.  
  
 Este procedimiento se puede usar para iniciar una carga a petición para un conjunto de recopilación en ejecución. Solo se puede utilizar para conjuntos de recopilación configurados para la recopilación y carga de datos en modo de almacenamiento en caché. Esto permite al usuario obtener datos para analizarlos sin tener que esperar a una carga programada.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer a la **dc_operator** (con permiso EXECUTE) rol fijo de base de datos para ejecutar este procedimiento.  
  
## <a name="example"></a>Ejemplo  
 Hace una carga a petición de un conjunto de recopilación denominado `Simple Collection Set`.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_upload_collection_set @name = 'Simple Collection Set' ;  
```  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Recopilación de datos](../../relational-databases/data-collection/data-collection.md)  
  
  
