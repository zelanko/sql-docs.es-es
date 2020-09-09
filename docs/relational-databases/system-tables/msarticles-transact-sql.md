---
description: MSarticles (Transact-SQL)
title: MSarticles (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSarticles
- MSarticles_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSarticles system table
ms.assetid: 1acd79a5-b3e2-4161-9592-7acc2a41ba38
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 3123834712540681748ab39edbfa6ee39d78ea14
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89545728"
---
# <a name="msarticles-transact-sql"></a>MSarticles (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabla **MSarticles** contiene una fila por cada artículo replicado por un publicador. Esta tabla se almacena en la base de datos de distribución.  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|IDENTIFICADOR del publicador.|  
|**publisher_db**|**sysname**|Nombre de la base de datos del publicador.|  
|**publication_id**|**int**|Id. de la publicación.|  
|**artículo**|**sysname**|Nombre del artículo.|  
|**article_id**|**int**|Id. del artículo.|  
|**destination_object**|**sysname**|Nombre de la tabla creada en el suscriptor.|  
|**source_owner**|**sysname**|Nombre del esquema de la tabla de origen en el publicador.|  
|**source_object**|**sysname**|Nombre del objeto de origen del que se va a agregar el artículo.|  
|**description**|**nvarchar(255)**|Descripción del artículo.|  
|**destination_owner**|**sysname**|Nombre del esquema de la tabla creada en el suscriptor.|  
  
## <a name="see-also"></a>Consulte también  
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
