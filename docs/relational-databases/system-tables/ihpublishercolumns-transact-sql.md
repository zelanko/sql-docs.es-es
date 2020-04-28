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
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "67990270"
---
# <a name="ihpublishercolumns-transact-sql"></a>IHpublishercolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  La tabla del sistema **IHpublishercolumns** representa los metadatos almacenados en el publicador. Esta tabla contiene una fila por cada columna replicada desde publicadores que no son de SQL Server mediante el distribuidor actual. La información del tipo de datos en **IHpublishercolumns** es específica del sistema de administración de bases de datos (DBMS) no SQL Server desde el que se publican los datos. Esta tabla se almacena en la base de datos de distribución.  
  
## <a name="definition"></a>Definición  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|Identifica una columna publicada.|  
|**table_id**|**int**|Identifica la tabla de origen de [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md) a la que pertenece la columna.|  
|**publisher_id**|**smallint**|Identifica el publicador que no es de SQL Server desde el que se publica la columna.|  
|**name**|**sysname**|El nombre de la columna publicada.|  
|**column_ordinal**|**int**|Identifica la columna por orden.|  
|**type**|**VARCHAR(255**|El tipo de datos de la columna de origen del publicador.|  
|**length**|**bigint**|La longitud de la columna de origen del publicador.|  
|**prec**|**int**|La precisión de la columna de origen del publicador.|  
|**scale**|**int**|La escala de la columna de origen del publicador.|  
|**IsNullable**|**bit**|Indica si la columna acepta valores NULL, donde **1** significa que se aceptan valores NULL.|  
|**iscaptured**|**bit**|Indica si hay un desencadenador en la columna. Puede haberlo aunque la columna no esté publicada en un artículo. Un valor de **1** significa que el desencadenador existe en la columna.|  
  
## <a name="see-also"></a>Consulte también  
 [Replicación de base de datos heterogénea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sysarticlecolumns &#40;vista del sistema&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [sysarticlecolumns &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
