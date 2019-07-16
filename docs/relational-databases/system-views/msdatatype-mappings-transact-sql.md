---
title: MSdatatype_mappings (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: replication
ms.topic: language-reference
f1_keywords:
- MSdatatype_mappings
- MSdatatype_mappings_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- MSdatatype_mappings view
ms.assetid: 13cdabb3-6e07-4e8d-ae80-4235022ccc7f
author: stevestein
ms.author: sstein
ms.openlocfilehash: ee1a0cc83b55fc265ae2bb490fd9d5e11fd73f22
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68129622"
---
# <a name="msdatatypemappings-transact-sql"></a>MSdatatype_mappings (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  El **MSdatatype_mappings** vista asigna los tipos de datos de SQL Server a tipos de datos usados por sistemas de administración de base de datos (DBMS) de que no son de SQL Server. Esta tabla se almacena en el **msdb** base de datos.  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**dbms_name**|**nvarchar(128)**|Es el nombre del DBMS. A continuación se muestran los valores posibles y sus descripciones.<br /><br /> **MSSQLSERVER**: El destino es una base de datos de SQL Server.<br />**ORACLE**: El destino es una base de datos de Oracle.<br />**DB2**: El destino es una base de datos IBM DB2.<br />**SYBASE**: El destino es una base de datos Sybase.|  
|**sql_type**|**nvarchar(128)**|Es el tipo de datos de SQL Server.|  
|**dest_type**|**nvarchar(128)**|Es el nombre del tipo de datos que no son de SQL Server.|  
|**dest_prec**|**bigint**|Es la precisión del tipo de datos que no son de SQL Server.|  
|**dest_create_params**|**int**|Exclusivamente para uso interno.|  
|**dest_nullable**|**bit**|Indica si el tipo de datos que no son de SQL Server admite un valor NULL.|  
  
## <a name="see-also"></a>Vea también  
 [Replicación de bases de datos heterogéneas](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Especificar asignaciones de tipo de datos para un publicador de Oracle](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Las tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
