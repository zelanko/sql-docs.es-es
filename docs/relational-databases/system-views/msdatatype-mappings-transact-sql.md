---
title: MSdatatype_mappings (Transact-SQL) | Documentos de Microsoft
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: language-reference
applies_to:
- SQL Server
f1_keywords:
- MSdatatype_mappings
- MSdatatype_mappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdatatype_mappings view
ms.assetid: 13cdabb3-6e07-4e8d-ae80-4235022ccc7f
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f0acbcbf2c70b08b44e0147989fb1f9dcd3e2301
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="msdatatypemappings-transact-sql"></a>MSdatatype_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSdatatype_mappings** vista asigna los tipos de datos de SQL Server a tipos de datos utilizados por sistemas de administración de bases de datos no es de SQL Server (DBMS). Esta tabla se almacena en la **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|**dbms_name**|**nvarchar(128)**|Es el nombre del DBMS. A continuación se muestran los valores posibles y sus descripciones.<br /><br /> **MSSQLSERVER**: el destino es una base de datos de SQL Server.<br />**ORACLE**: el destino es una base de datos de Oracle.<br />**DB2**: el destino es una base de datos de IBM DB2.<br />**SYBASE**: el destino es una base de datos de Sybase.|  
|**sql_type**|**nvarchar(128)**|Es el tipo de datos de SQL Server.|  
|**dest_type**|**nvarchar(128)**|Es el nombre del tipo de datos no es de SQL Server.|  
|**dest_prec**|**bigint**|Es la precisión del tipo de datos no es de SQL Server.|  
|**dest_create_params**|**int**|Exclusivamente para uso interno.|  
|**dest_nullable**|**bit**|Indica si el tipo de datos no es de SQL Server admite un valor NULL.|  
  
## <a name="see-also"></a>Vea también  
 [Replicación de bases de datos heterogéneas](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Especificar asignaciones de tipo de datos para un publicador de Oracle](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Tablas de replicación &#40; Transact-SQL &#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
