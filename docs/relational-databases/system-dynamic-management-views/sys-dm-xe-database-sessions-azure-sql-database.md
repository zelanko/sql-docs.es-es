---
description: sys.dm_xe_database_sessions (Azure SQL Database)
title: Sys. dm_xe_database_sessions (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
ms.assetid: 33ea5179-16bb-4abd-96cc-9bc696e80987
author: markingmyname
ms.author: maghan
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 4af2c0fafeae67291043d990c1bbaff175de9f5a
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546402"
---
# <a name="sysdm_xe_database_sessions-azure-sql-database"></a>sys.dm_xe_database_sessions (Azure SQL Database)
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  Devuelve información sobre los eventos de la sesión. Los eventos son puntos de ejecución discretos. Los predicados se pueden aplicar a los eventos para que no se activen si el evento no contiene la información necesaria.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 y a las versiones posteriores.|  
  
|Nombre de la columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary(8**|La dirección de memoria de la sesión de eventos. No admite valores NULL.|  
|event_name|**nvarchar(60)**|Nombre del evento al que se enlaza una acción. No admite valores NULL.|  
|event_package_guid|**uniqueidentifier**|El GUID del paquete que contiene el evento. No admite valores NULL.|  
|event_predicate|**nvarchar(2048)**|Representación XML del árbol de predicado que se aplica al evento. Acepta valores NULL.|  
  
## <a name="permissions"></a>Permisos  
 Necesita el permiso VIEW DATABASE STATE.  
  
### <a name="relationship-cardinalities"></a>Cardinalidades de relación  
A partir de 2015-07-13, ' sys. dm_xe_objects ' es una de estas DMV XEvents que no contiene ' _database ' en su nombre. No se trata de un error tipográfico o de la columna derecha de la tabla siguiente. El nombre es el mismo en Microsoft SQL Server y Azure SQL Database.  
  
|From|En|Relación|  
|--------|------|----------------|  
|Sys. dm_xe_database_session_events. event_session_address|Sys. dm_xe_database_sessions. Address|Varios a uno|  
|Sys. dm_xe_database_session_events. event_package_guid, sys. dm_xe_database_session_events. event_name|sys.dm_xe_objects.name, sys.dm_xe_objects.package_guid|Varios a uno|  
  
## <a name="see-also"></a>Consulte también  
[Eventos extendidos en Base de datos SQL de Azure](https://azure.microsoft.com/documentation/articles/sql-database-xevent-db-diff-from-svr/)  
[Eventos extendidos](../../relational-databases/extended-events/extended-events.md)  
  
 
