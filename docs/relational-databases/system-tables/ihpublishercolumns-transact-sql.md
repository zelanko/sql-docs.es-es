---
title: IHpublishercolumns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublishercolumns
- IHpublishercolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumns system table
ms.assetid: a5347750-224c-40d9-ae12-57e7213b7db9
author: stevestein
ms.author: sstein
ms.openlocfilehash: a5e2f64294652586a87fcd25fda3c29517dc295d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990270"
---
# <a name="ihpublishercolumns-transact-sql"></a>IHpublishercolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **IHpublishercolumns** tabla del sistema representa los metadatos almacenados en el publicador. Esta tabla contiene una fila por cada columna replicada desde publicadores que no son: SQL Server utilizando el distribuidor actual. Información de tipo de datos **IHpublishercolumns** es específico para el sistema de administración de base de datos que no son de SQL Server (DBMS) desde el que se publican los datos. Esta tabla se almacena en la base de datos de distribución.  
  
## <a name="definition"></a>Definición  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|Identifica una columna publicada.|  
|**table_id**|**int**|Identifica la tabla de origen de [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md) al que pertenece la columna.|  
|**publisher_id**|**smallint**|Identifica el no publicador de SQL Server desde el que se publica la columna.|  
|**name**|**sysname**|El nombre de la columna publicada.|  
|**column_ordinal**|**int**|Identifica la columna por orden.|  
|**type**|**varchar(255)**|El tipo de datos de la columna de origen del publicador.|  
|**length**|**bigint**|La longitud de la columna de origen del publicador.|  
|**Prec**|**int**|La precisión de la columna de origen del publicador.|  
|**scale**|**int**|La escala de la columna de origen del publicador.|  
|**IsNullable**|**bit**|Indica si la columna acepta valores NULL, donde **1** significa que se aceptan valores NULL.|  
|**iscaptured**|**bit**|Indica si hay un desencadenador en la columna. Puede haberlo aunque la columna no esté publicada en un artículo. Un valor de **1** significa que el desencadenador existe en la columna.|  
  
## <a name="see-also"></a>Vea también  
 [Replicación de bases de datos heterogéneas](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sysarticlecolumns &#40;vista del sistema&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [sysarticlecolumns &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
