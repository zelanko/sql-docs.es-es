---
title: IHpublishercolumns (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-tables
ms.reviewer: ''
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: ''
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- IHpublishercolumns
- IHpublishercolumns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishercolumns system table
ms.assetid: a5347750-224c-40d9-ae12-57e7213b7db9
caps.latest.revision: 24
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 06d0d772ee3def5c7b3823735793127bbe5cb26b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="ihpublishercolumns-transact-sql"></a>IHpublishercolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **IHpublishercolumns** tabla del sistema representa los metadatos almacenados en el publicador. Esta tabla contiene una fila por cada columna replicada desde no publicadores de SQL Server utilizando el distribuidor actual. Información de tipo de datos **IHpublishercolumns** es específica del sistema de administración de base de datos no es de SQL Server (DBMS) desde el que los datos se publican. Esta tabla se almacena en la base de datos de distribución.  
  
## <a name="definition"></a>Definición  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|Identifica una columna publicada.|  
|**table_id**|**int**|Identifica la tabla de origen de [IHpublishertables](../../relational-databases/system-tables/ihpublishertables-transact-sql.md) a la que pertenece la columna.|  
|**publisher_id**|**smallint**|Identifica el no - publicador de SQL Server desde el que se publica la columna.|  
|**Nombre**|**sysname**|El nombre de la columna publicada.|  
|**column_ordinal**|**int**|Identifica la columna por orden.|  
|**Tipo**|**varchar (255)**|El tipo de datos de la columna de origen del publicador.|  
|**length**|**bigint**|La longitud de la columna de origen del publicador.|  
|**Prec**|**int**|La precisión de la columna de origen del publicador.|  
|**escala**|**int**|La escala de la columna de origen del publicador.|  
|**IsNullable**|**bit**|Indica si la columna acepta valores NULL, donde **1** significa que se aceptan valores NULL.|  
|**iscaptured**|**bit**|Indica si hay un desencadenador en la columna. Puede haberlo aunque la columna no esté publicada en un artículo. Un valor de **1** significa que el desencadenador existe en la columna.|  
  
## <a name="see-also"></a>Vea también  
 [Replicación de bases de datos heterogéneas](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sysarticlecolumns &#40;vista del sistema&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [sysarticlecolumns &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
