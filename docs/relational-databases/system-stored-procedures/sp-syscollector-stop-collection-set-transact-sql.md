---
title: sp_syscollector_stop_collection_set (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_syscollector_stop_collection_set_TSQL
- sp_syscollector_stop_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_stop_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: 4668cfb7-462f-40d0-948c-8f740a792a4d
caps.latest.revision: 16
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 12bd5d11de99a8ca14f7fc36dea59186a02623ec
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="spsyscollectorstopcollectionset-transact-sql"></a>sp_syscollector_stop_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Detiene un conjunto de recopilación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_syscollector_stop_collection_set   
    [ [ @collection_set_id = ] collection_set_id ]  
    , [ [ @name = ] 'name' ]  
    , [ [ @stop_collection_job = ] stop_collection_job ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @collection_set_id =] *collection_set_id*  
 Es el identificador único local del conjunto de recopilaciones. *collection_set_id* es **int** con un valor predeterminado es NULL. *collection_set_id* debe tener un valor si *nombre* es NULL.  
  
 [ @name =] '*nombre*'  
 Es el nombre del conjunto de recopilación. *nombre* es **sysname** con un valor predeterminado es NULL. *nombre* debe tener un valor si *collection_set_id* es NULL.  
  
 [ @stop_collection_job =] *stop_collection_job*  
 Especifica que el trabajo de recopilación del conjunto de recopilación debe detenerse si está en ejecución. *stop_collection_job* es **bits** con un valor predeterminado es 1.  
  
 *stop_collection_job* se aplica solo a conjuntos de recopilación con almacenamiento en caché de modo de recopilación. Para obtener más información, consulte [sp_syscollector_create_collection_set &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md).  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 sp_syscollector_create_collection_set se debe ejecutar en el contexto de la base de datos del sistema msdb.  
  
## <a name="permissions"></a>Permissions  
 Requiere la pertenencia al rol fijo de base de datos dc_operator (con permiso EXECUTE) para ejecutar este procedimiento.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se detiene un conjunto de recopilación mediante su identificador.  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_stop_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>Vea también  
 [Recopilación de datos](../../relational-databases/data-collection/data-collection.md)   
 [Procedimientos almacenados del recopilador de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)  
  
  
