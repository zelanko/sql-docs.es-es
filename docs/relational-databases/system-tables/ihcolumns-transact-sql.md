---
title: IHcolumns (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
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
- IHcolumns_TSQL
- IHcolumns
dev_langs:
- TSQL
helpviewer_keywords:
- IHcolumns system table
ms.assetid: 5bb027e5-5279-487b-9c33-5f402987253c
caps.latest.revision: 23
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: d713dbd76921955aab6066b51d163a17ca7cba9a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="ihcolumns-transact-sql"></a>IHcolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **IHcolumns** tabla del sistema contiene una fila por cada columna publicada. Esta tabla se utiliza para definir cómo se representarán los tipos de datos de columna de la no publicador de SQL Server cuando se publica, que básicamente asigna tipos de datos entre un sistemas de administración de bases de datos (DBMS) de ajeno a SQL Server y SQL Server. Esta tabla se almacena en la base de datos de distribución.  
  
## <a name="definition"></a>Definición  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**column_id**|**int**|Identifica una columna publicada.|  
|**publishercolumn_id**|**int**|Asocia una columna publicada a metadatos de columna almacenados en la [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) tabla del sistema.|  
|**Nombre**|**sysname**|Especifica el nombre de la columna.|  
|**article_id**|**int**|Identifica el artículo al que pertenece la columna.|  
|**column_ordinal**|**int**|Identifica la columna por orden.|  
|**mapped_type**|**tinyint**|Tipo de datos de columna de la columna de destino en el suscriptor.|  
|**mapped_length**|**bigint**|Longitud de la columna en el suscriptor.|  
|**mapped_prec**|**int**|Precisión de la columna en el suscriptor.|  
|**mapped_scale**|**int**|Escala de la columna en el suscriptor.|  
|**mapped_nullable**|**bit**|Indica si la columna en el suscriptor acepta valores NULL, donde **1** significa que se aceptan valores NULL.|  
  
## <a name="see-also"></a>Vea también  
 [Replicación de bases de datos heterogéneas](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sysarticlecolumns &#40;vista del sistema&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [sysarticlecolumns &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
