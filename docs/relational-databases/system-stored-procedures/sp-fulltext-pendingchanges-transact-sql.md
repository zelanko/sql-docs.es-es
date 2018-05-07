---
title: sp_fulltext_pendingchanges (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_fulltext_pendingchanges_TSQL
- sp_fulltext_pendingchanges
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_pendingchanges
ms.assetid: fee042fe-4781-4a33-a01b-d98fb5629f1b
caps.latest.revision: 15
author: douglaslMS
ms.author: douglasl
manager: craigg
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: 4a6defefbc225d2f8301977d5826c74597eefb2c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/04/2018
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
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**Key**|*|Valor de clave de texto completo de la tabla especificada.|  
|**DocId**|**bigint**|Una columna de identificador de documento interno (DocId) que se corresponde con el valor de clave.|  
|**Estado**|**int**|0 = La fila se eliminará del índice de texto completo.<br /><br /> 1 = La fila contendrá un índice de texto completo.<br /><br /> 2 = La fila está actualizada.<br /><br /> -1 = La fila se encuentra en un estado transicional (de lote, pero no confirmado) o un estado de error.|  
|**DocState**|**tinyint**|Es un volcado de la columna de estado de la asignación del identificador de documento interno (DocId).|  
  
 <sup>* El tipo de datos para la clave es igual que el tipo de datos de la columna de clave de texto completo en la tabla base.</sup>  
  
## <a name="permissions"></a>Permissions  
 Requiere la pertenencia al rol fijo de servidor **sysadmin** .  
  
## <a name="remarks"></a>Comentarios  
 Si no hay cambios que procesar, se devuelve un conjunto de filas vacío.  
  
 Las consultas de búsqueda de texto completo no devuelven filas con un **estado** el valor 0. Esto se debe a que la fila se ha eliminado de la tabla base y está esperando a ser eliminada del índice de texto completo.  
  
 Para averiguar cuántos cambios siguen pendientes para una tabla específica, utilice la propiedad **TableFullTextPendingChanges** de la función OBJECTPROPERTYEX.  
  
## <a name="see-also"></a>Vea también  
 [Procedimientos almacenan de búsqueda de texto completo y la búsqueda semántica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)   
 [OBJECTPROPERTYEX &#40;Transact-SQL&#41;](../../t-sql/functions/objectpropertyex-transact-sql.md)  
  
  
