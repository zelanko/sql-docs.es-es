---
title: Sys.sysreferences (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: system-compatibility-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sys.sysreferences
- sys.sysreferences_TSQL
- sysreferences
- sysreferences_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sysreferences compatibility view
- sysreferences system table
ms.assetid: 81276f13-202e-4e74-962d-46eb98c98d2e
caps.latest.revision: 38
author: rothja
ms.author: jroth
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: b7468ff348e06cfabcf93da4e2ba939fe655bdc3
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39557135"
---
# <a name="syssysreferences-transact-sql"></a>sys.sysreferences (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  Contiene asignaciones de definiciones de restricciones FOREIGN KEY a las columnas a las que se hace referencia en la base de datos.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssnoteCompView](../../includes/ssnotecompview-md.md)]  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**constid**|**int**|Id. de la restricción FOREIGN KEY.|  
|**fkeyid**|**int**|Id. de la tabla que hace referencia.|  
|**rkeyid**|**int**|Id. de la tabla a la que se hace referencia.|  
|**rkeyindid**|**smallint**|Id. del índice exclusivo de la tabla a la que se hace referencia que abarca las columnas de clave con referencia.|  
|**keycnt**|**smallint**|Número de columnas de la clave.|  
|**forkeys**|**varbinary(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**refkeys**|**varbinary(32)**|[!INCLUDE[ssInternalOnly](../../includes/ssinternalonly-md.md)]|  
|**fkeydbid**|**smallint**|Reservado.|  
|**rkeydbid**|**smallint**|Reservado.|  
|**fkey1**|**smallint**|Id. de la columna que hace referencia.|  
|**fkey2**|**smallint**|Id. de la columna que hace referencia.|  
|**fkey3**|**smallint**|Id. de la columna que hace referencia.|  
|**fkey4**|**smallint**|Id. de la columna que hace referencia.|  
|**fkey5**|**smallint**|Id. de la columna que hace referencia.|  
|**fkey6**|**smallint**|Id. de la columna que hace referencia.|  
|**fkey7**|**smallint**|Id. de la columna que hace referencia.|  
|**fkey8**|**smallint**|Id. de la columna que hace referencia.|  
|**fkey9**|**smallint**|Id. de la columna que hace referencia.|  
|**fkey10**|**smallint**|Id. de la columna que hace referencia.|  
|**fkey11**|**smallint**|Id. de la columna que hace referencia.|  
|**fkey12**|**smallint**|Id. de la columna que hace referencia.|  
|**fkey13**|**smallint**|Id. de la columna que hace referencia.|  
|**fkey14**|**smallint**|Id. de la columna que hace referencia.|  
|**fkey15**|**smallint**|Id. de la columna que hace referencia.|  
|**fkey16**|**smallint**|Id. de la columna que hace referencia.|  
|**rkey1**|**smallint**|Id. de columna de la columna que se hace referencia.|  
|**rkey2**|**smallint**|Id. de columna de la columna que se hace referencia.|  
|**rkey3**|**smallint**|Id. de columna de la columna que se hace referencia.|  
|**rkey4**|**smallint**|Id. de columna de la columna que se hace referencia.|  
|**rkey5**|**smallint**|Id. de columna de la columna que se hace referencia.|  
|**rkey6**|**smallint**|Id. de columna de la columna que se hace referencia.|  
|**rkey7**|**smallint**|Id. de columna de la columna que se hace referencia.|  
|**rkey8**|**smallint**|Id. de columna de la columna que se hace referencia.|  
|**rkey9**|**smallint**|Id. de columna de la columna que se hace referencia.|  
|**rkey10**|**smallint**|Id. de columna de la columna que se hace referencia.|  
|**rkey11**|**smallint**|Id. de columna de la columna que se hace referencia.|  
|**rkey12**|**smallint**|Id. de columna de la columna que se hace referencia.|  
|**rkey13**|**smallint**|Id. de columna de la columna que se hace referencia.|  
|**rkey14**|**smallint**|Id. de columna de la columna que se hace referencia.|  
|**rkey15**|**smallint**|Id. de columna de la columna que se hace referencia.|  
|**rkey16**|**smallint**|Id. de columna de la columna que se hace referencia.|  
  
## <a name="see-also"></a>Vea también  
 [Asignar tablas del sistema a vistas del sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/mapping-system-tables-to-system-views-transact-sql.md)   
 [Vistas de compatibilidad &#40;Transact-SQL&#41;](~/relational-databases/system-compatibility-views/system-compatibility-views-transact-sql.md)  
  
  
