---
title: IHcolumns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHcolumns_TSQL
- IHcolumns
dev_langs:
- TSQL
helpviewer_keywords:
- IHcolumns system table
ms.assetid: 5bb027e5-5279-487b-9c33-5f402987253c
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: c1870e1d826fef593f5458004d424a02185028e2
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890317"
---
# <a name="ihcolumns-transact-sql"></a>IHcolumns (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabla del sistema **IHcolumns** contiene una fila por cada columna publicada. Esta tabla se utiliza para definir cómo se van a representar cuando se publiquen los tipos de datos de columna de un publicador que no es de SQL Server, proceso que esencialmente consiste en asignar tipos de datos entre un sistema de administración de bases de datos (DBMS) que no es de SQL Server y SQL Server. Esta tabla se almacena en la base de datos de distribución.  
  
## <a name="definition"></a>Definición  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**column_id**|**int**|Identifica una columna publicada.|  
|**publishercolumn_id**|**int**|Asocia una columna publicada a los metadatos de columna almacenados en la tabla del sistema [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) .|  
|**name**|**sysname**|Especifica el nombre de la columna.|  
|**article_id**|**int**|Identifica el artículo al que pertenece la columna.|  
|**column_ordinal**|**int**|Identifica la columna por orden.|  
|**mapped_type**|**tinyint**|Tipo de datos de columna de la columna de destino en el suscriptor.|  
|**mapped_length**|**bigint**|Longitud de la columna en el suscriptor.|  
|**mapped_prec**|**int**|Precisión de la columna en el suscriptor.|  
|**mapped_scale**|**int**|Escala de la columna en el suscriptor.|  
|**mapped_nullable**|**bit**|Indica si la columna en el suscriptor acepta valores NULL, donde **1** significa que se aceptan valores NULL.|  
  
## <a name="see-also"></a>Consulte también  
 [Replicación de base de datos heterogénea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_articlecolumn &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sysarticlecolumns &#40;vista del sistema&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [sysarticlecolumns &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
