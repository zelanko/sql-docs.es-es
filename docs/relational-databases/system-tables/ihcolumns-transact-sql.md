---
title: IHcolumns (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- replication
ms.topic: language-reference
f1_keywords:
- IHcolumns_TSQL
- IHcolumns
dev_langs:
- TSQL
helpviewer_keywords:
- IHcolumns system table
ms.assetid: 5bb027e5-5279-487b-9c33-5f402987253c
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 26725530cec4fcc05ff977537d4b6ac2d46cd0c5
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47718433"
---
# <a name="ihcolumns-transact-sql"></a>IHcolumns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **IHcolumns** tabla del sistema contiene una fila por cada columna publicada. Esta tabla se utiliza para definir cómo se representarán los tipos de datos de columna desde la que no sea publicador de SQL Server cuando se publica, básicamente, se asignan los tipos de datos entre un sistema de administración de base de datos (DBMS) de que no son de SQL Server y SQL Server. Esta tabla se almacena en la base de datos de distribución.  
  
## <a name="definition"></a>Definición  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**column_id**|**int**|Identifica una columna publicada.|  
|**publishercolumn_id**|**int**|Asocia una columna publicada a metadatos de columna almacenados en el [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) tabla del sistema.|  
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
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_articlecolumn &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-articlecolumn-transact-sql.md)   
 [sysarticlecolumns &#40;vista del sistema&#41; &#40;Transact-SQL&#41;](../../relational-databases/system-views/sysarticlecolumns-system-view-transact-sql.md)   
 [sysarticlecolumns &#40;Transact-SQL&#41;](../../relational-databases/system-tables/sysarticlecolumns-transact-sql.md)  
  
  
