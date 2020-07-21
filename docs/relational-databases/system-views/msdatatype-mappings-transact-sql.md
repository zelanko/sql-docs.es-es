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
ms.openlocfilehash: 16da7db2dcf42ebfa00d634814f27839a3988a71
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/02/2020
ms.locfileid: "85889196"
---
# <a name="msdatatype_mappings-transact-sql"></a>MSdatatype_mappings (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  La vista **MSdatatype_mappings** se asigna SQL Server tipos de datos a tipos de datos utilizados por sistemas de administración de bases de datos (DBMS) que no son de SQL Server. Esta tabla se almacena en la base de datos **msdb** .  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|**dbms_name**|**nvarchar(128)**|Es el nombre del DBMS. A continuación se muestran los valores posibles y sus descripciones.<br /><br /> **MSSQLSERVER**: el destino es una base de datos de SQL Server.<br />**Oracle**: el destino es una base de datos de Oracle.<br />**DB2**: el destino es una base de datos de IBM DB2.<br />**Sybase**: el destino es una base de datos de Sybase.|  
|**sql_type**|**nvarchar(128)**|Es el tipo de datos de SQL Server.|  
|**dest_type**|**nvarchar(128)**|Es el nombre del tipo de datos que no es de SQL Server.|  
|**dest_prec**|**bigint**|Es la precisión del tipo de datos que no es de SQL Server.|  
|**dest_create_params**|**int**|Exclusivamente para uso interno.|  
|**dest_nullable**|**bit**|Especifica si el tipo de datos que no es de SQL Server admite un valor NULL.|  
  
## <a name="see-also"></a>Consulte también  
 [Replicación de base de datos heterogénea](../../relational-databases/replication/non-sql/heterogeneous-database-replication.md)   
 [Especificar asignaciones de tipos de datos para un publicador de Oracle](../../relational-databases/replication/publish/specify-data-type-mappings-for-an-oracle-publisher.md)   
 [Tablas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-tables/replication-tables-transact-sql.md)   
 [Vistas de replicación &#40;Transact-SQL&#41;](../../relational-databases/system-views/replication-views-transact-sql.md)  
  
  
