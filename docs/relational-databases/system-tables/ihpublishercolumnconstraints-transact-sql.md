---
title: IHpublishercolumnconstraints (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-tables
ms.reviewer: 
ms.suite: sql
ms.technology: replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to: SQL Server
f1_keywords:
- IHpublishercolumnconstraints
- IHpublishercolumnconstraints_TSQL
dev_langs: TSQL
helpviewer_keywords: IHpublishercolumnconstraints system table
ms.assetid: d7a41da6-e067-430a-8da2-3f6745b8a4f3
caps.latest.revision: "26"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b9dd056bc97aeb438339303813d6661a02dcc63f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/21/2017
---
# <a name="ihpublishercolumnconstraints-transact-sql"></a>IHpublishercolumnconstraints (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **IHpublishercolumnconstraints** tabla del sistema asigna las columnas de una publicación no es de SQL Server en el [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) tabla del sistema a las restricciones en la [IHpublisherconstraints ](../../relational-databases/system-tables/ihpublisherconstraints-transact-sql.md) tabla del sistema. Esta tabla se almacena en la base de datos de distribución.  
  
## <a name="definition"></a>Definición  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**publishercolumn_id**|**int**|Identifica la columna de [IHpublishercolumns](../../relational-databases/system-tables/ihpublishercolumns-transact-sql.md) con una restricción asociada.|  
|**publisherconstraint_id**|**int**|Identifica una restricción de [IHpublisherconstraints](../../relational-databases/system-tables/ihpublisherconstraints-transact-sql.md) asociado a la columna.|  
|**indid**|**int**|Indica la posición de la columna en la tabla publicada.|  
  
## <a name="see-also"></a>Vea también  
 [Replicación de bases de datos heterogéneas](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Tablas de replicación &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
