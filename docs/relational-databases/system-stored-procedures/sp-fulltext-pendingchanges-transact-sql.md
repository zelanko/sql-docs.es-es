---
title: sp_fulltext_pendingchanges (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_pendingchanges_TSQL
- sp_fulltext_pendingchanges
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_pendingchanges
ms.assetid: fee042fe-4781-4a33-a01b-d98fb5629f1b
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: ef93287acb610e813f20f213e8fb6a325058116d
ms.sourcegitcommit: 5ed48c7dc6bed153079bc2b23a1e0506841310d1
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/21/2019
ms.locfileid: "65983025"
---
# <a name="spfulltextpendingchanges-transact-sql"></a>sp_fulltext_pendingchanges (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Devuelve cambios sin procesar, como eliminaciones, actualizaciones e inserciones pendientes, de una tabla especificada que utilice el seguimiento de cambios.  
  
 ![Icono de vínculo de tema](../../database-engine/configure-windows/media/topic-link.gif "Icono de vínculo de tema") [Convenciones de sintaxis de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
sp_fulltext_pendingchanges table_id  
```  
  
## <a name="arguments"></a>Argumentos  
 *table_id*  
 Id. de la tabla. Si la tabla no tiene un índice de texto completo o no se ha habilitado el seguimiento de cambios, se obtiene un error.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**Key**|*|Valor de clave de texto completo de la tabla especificada.|  
|**DocId**|**bigint**|Una columna de identificador de documento interno (DocId) que se corresponde con el valor de clave.|  
|**Estado**|**int**|0 = La fila se eliminará del índice de texto completo.<br /><br /> 1 = La fila contendrá un índice de texto completo.<br /><br /> 2 = La fila está actualizada.<br /><br /> -1 = La fila se encuentra en un estado transicional (de lote, pero no confirmado) o un estado de error.|  
|**DocState**|**tinyint**|Es un volcado de la columna de estado de la asignación del identificador de documento interno (DocId).|  
  
 <sup>* El tipo de datos de clave es igual que el tipo de datos de la columna de clave de texto completo en la tabla base.</sup>  
  
## <a name="permissions"></a>Permisos  
 Requiere la pertenencia al rol fijo de servidor **sysadmin** .  
  
## <a name="remarks"></a>Comentarios  
 Si no hay cambios que procesar, se devuelve un conjunto de filas vacío.  
  
 Las consultas de búsqueda de texto completo no devolverá las filas con un **estado** valor de 0. Esto se debe a que la fila se ha eliminado de la tabla base y está esperando a ser eliminada del índice de texto completo.  
  
 Para averiguar cuántos cambios siguen pendientes para una tabla específica, utilice la propiedad **TableFullTextPendingChanges** de la función OBJECTPROPERTYEX.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenan de búsqueda de texto completo y la búsqueda semántica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)   
 [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)  
  
  
