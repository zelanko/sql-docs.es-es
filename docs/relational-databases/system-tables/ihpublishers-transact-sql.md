---
title: IHpublishers (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- IHpublishers
- IHpublishers_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- IHpublishers system table
ms.assetid: 77007246-f10b-4b87-8edf-7afc3c2096af
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: d2e2b5037854cdd533f48549c5b4c4694907fd5e
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85890246"
---
# <a name="ihpublishers-transact-sql"></a>IHpublishers (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La tabla del sistema **IHpublishers** contiene una fila por cada publicador que no sea de SQL Server mediante el distribuidor actual. Esta tabla se almacena en la base de datos de distribución.  
  
## <a name="definition"></a>Definición  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**publisher_id**|**smallint**|Identifica un publicador que no es de SQL Server.|  
|**proveedor**|**sysname**|Nombre del proveedor de la base de datos que no es de SQL Server.|  
|**publisher_guid**|**uniqueidentifier**|GUID que identifica al publicador que no es de SQL Server.|  
|**flush_request_time**|**datetime**|Indica la fecha y hora en que se produjo el último cambio en los metadatos del artículo que requirió que el Agente de registro del LOG actualizara su caché de metadatos.|  
|**version**|**sysname**|Cadena de texto que caracteriza a la versión del publicador que no es de SQL Server.|  
  
## <a name="see-also"></a>Consulte también  
 [Replicación de base de datos heterogénea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)   
 [sp_adddistpublisher &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql.md)   
 [sp_changedistpublisher &#40;&#41;de Transact-SQL](../../relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql.md)   
 [sp_helpdistpublisher &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-helpdistpublisher-transact-sql.md)  
  
  
