---
title: Sys.dm_xe_database_sessions (base de datos de SQL Azure) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/06/2017
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: dmv's
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 33ea5179-16bb-4abd-96cc-9bc696e80987
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: e06a13a3c12048b9f4005fc34fdfa3f2f3e9dd7b
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sysdmxedatabasesessions-azure-sql-database"></a>Sys.dm_xe_database_sessions (base de datos de SQL Azure)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Devuelve información sobre los eventos de la sesión. Los eventos son puntos de ejecución discretos. Los predicados se pueden aplicar a los eventos para que no se activen si el evento no contiene la información necesaria.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 y las versiones posteriores.|  
  
|Nombre de columna|Tipo de datos|Description|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary (8)**|La dirección de memoria de la sesión de eventos. No admite valores NULL.|  
|event_name|**nvarchar(60)**|Nombre del evento al que se enlaza una acción. No admite valores NULL.|  
|event_package_guid|**uniqueidentifier**|El GUID del paquete que contiene el evento. No admite valores NULL.|  
|event_predicate|**nvarchar(2048)**|Representación XML del árbol de predicado que se aplica al evento. Acepta valores NULL.|  
  
## <a name="permissions"></a>Permissions  
 Requiere el permiso VIEW DATABASE STATE.  
  
### <a name="relationship-cardinalities"></a>Cardinalidades de relación  
A partir de 2015-07-13, 'sys.dm_xe_objects' es una de estas DMV XEvents que no contienen '_Base de datos' en su nombre. No un error de escritura o un error en la columna de la derecha de la tabla siguiente. El nombre es el mismo en Microsoft SQL Server y base de datos de SQL Azure. GeneMi.  
  
|De|En|Relación|  
|--------|------|----------------|  
|sys.dm_xe_database_session_events.event_session_address|sys.dm_xe_database_sessions.address|Varios a uno|  
|Sys.dm_xe_database_session_events.event_package_guid, sys.dm_xe_database_session_events.event_name|sys.dm_xe_objects.name, sys.dm_xe_objects.package_guid|Varios a uno|  
  
## <a name="see-also"></a>Vea también  
[Eventos extendidos en base de datos de SQL Azure](http://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/)  
[Eventos extendidos](../../relational-databases/extended-events/extended-events.md)  
  
 
