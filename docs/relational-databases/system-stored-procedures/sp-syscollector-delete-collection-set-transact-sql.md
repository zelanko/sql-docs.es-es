---
title: sp_syscollector_delete_collection_set (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_delete_collection_set_TSQL
- sp_syscollector_delete_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_delete_collecton_set
ms.assetid: 29c63a74-4db4-4068-bd57-9fb519b0c598
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 9adfe94e791f8c0b0bb38305c538bd72918a71e1
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85892913"
---
# <a name="sp_syscollector_delete_collection_set-transact-sql"></a>sp_syscollector_delete_collection_set (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Elimina un conjunto de recopilación definido por el usuario y todos los elementos de recopilación.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_syscollector_delete_collection_set [[ @collection_set_id = ] collection_set_id OUTPUT ]  
    , [[ @name = ] 'name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @collection_set_id =] *collection_set_id*  
 Es el identificador único del conjunto de recopilación. *collection_set_id* es de **tipo int** y debe tener un valor si *el nombre* es NULL.  
  
 [ @name =] '*nombre*'  
 Es el nombre del conjunto de recopilación. *Name* es de **tipo sysname** y debe tener un valor si *collection_set_id* es NULL.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="remarks"></a>Comentarios  
 sp_syscollector_delete_collection_set se debe ejecutar en el contexto de la base de datos del sistema msdb.  
  
 *Collection_set_id* o *Name* deben tener un valor, ambos no pueden ser null. Para obtener estos valores, consulte la vista del sistema syscollector_collection_set.  
  
 No se pueden eliminar los conjuntos de recopilación definidos por el sistema.  
  
## <a name="permissions"></a>Permisos  
 Debe pertenecer al rol fijo de base de datos dc_admin (con permiso EXECUTE) para ejecutar este procedimiento.  
  
## <a name="examples"></a>Ejemplos  
 En el ejemplo siguiente se elimina un conjunto de recopilación definido por el usuario que especifica el *collection_set_id*.  
  
```  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_delete_collection_set  
    @collection_set_id = 4;  
```  
  
## <a name="see-also"></a>Consulte también  
 [Procedimientos almacenados del recopilador de datos &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [Recopilación de datos](../../relational-databases/data-collection/data-collection.md)   
 [syscollector_collection_sets &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)  
  
  
