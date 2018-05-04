---
title: sp_syscollector_delete_execution_log_tree (Transact-SQL) | Documentos de Microsoft
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
- sp_syscollector_delete_execution_log_tree_TSQL
- sp_syscollector_delete_execution_log_tree
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_delete_execution_log_tree
- data collector [SQL Server], stored procedures
ms.assetid: 0a9a7c5b-c3cc-40ca-b524-e948a8cce4e4
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: fb66c3d92789637c27b50e0180dd314cfa907e81
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="spsyscollectordeleteexecutionlogtree-transact-sql"></a>sp_syscollector_delete_execution_log_tree (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Elimina todas las entradas de registro para la ejecución de un conjunto de recopilación. También elimina las entradas de registro en las tablas [!INCLUDE[ssIS](../../includes/ssis-md.md)] para dicha ejecución.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_syscollector_delete_execution_log_tree[ @log_id = ] log_id  
          , [ @from_collection_set = ] from_collection_set  
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@log_id =** ] *log_id*  
 Es el identificador único del registro del conjunto de recopilación. *log_id* es **int**.  
  
 [  **@from_collection_set =** ] *from_collection_set*  
 Es el identificador del conjunto de recopilación. *from_collection_set* es **bits = 1**.  
  
## <a name="return-code-values"></a>Valores de código de retorno  
 **0** (correcto) o **1** (error)  
  
## <a name="permissions"></a>Permissions  
 Debe pertenecer a la **dc_operator** (con permiso EXECUTE) rol fijo de base de datos para ejecutar este procedimiento.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenados del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
