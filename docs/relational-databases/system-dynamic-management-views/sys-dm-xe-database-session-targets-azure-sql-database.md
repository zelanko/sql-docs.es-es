---
title: Sys.dm_xe_database_session_targets (Azure SQL Database) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: ''
ms.prod_service: sql-database
ms.reviewer: ''
ms.service: sql-database
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
ms.assetid: 7f353e2a-f8fc-4366-97e4-aa1c49eadaf4
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 8978a41b22beb36ccc31d1cfdc0a73eaf2da34ec
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38041023"
---
# <a name="sysdmxedatabasesessiontargets-azure-sql-database"></a>Sys.dm_xe_database_session_targets (Azure SQL Database)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

  Devuelve información sobre los destinos de la sesión.  
  
||  
|-|  
|**Se aplica a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] V12 y todas las versiones futuras.|  
  
|Nombre de columna|Tipo de datos|Descripción|  
|-----------------|---------------|-----------------|  
|event_session_address|**varbinary (8)**|La dirección de memoria de la sesión de eventos. Tiene una relación de varios a uno con sys.dm_xe_database_sessions.address. No admite valores NULL.|  
|target_name|**nvarchar(60)**|El nombre del destino dentro de una sesión. No admite valores NULL.|  
|target_package_guid|**uniqueidentifier**|GUID del paquete que contiene el destino. No admite valores NULL.|  
|execution_count|**bigint**|El número de veces que se ha ejecutado el destino para la sesión. No admite valores NULL.|  
|execution_duration_ms|**bigint**|El tiempo total, en milisegundos, que se ha estado ejecutando el destino. No admite valores NULL.|  
|target_data|**nvarchar(max)**|Datos que mantiene el destino como, por ejemplo, información de agregación de eventos. Acepta valores NULL.|  
  
## <a name="permissions"></a>Permisos  
 Requiere el permiso VIEW DATABASE STATE.  
  
### <a name="relationship-cardinalities"></a>Cardinalidades de relación  
  
|De|En|Relación|  
|----------|--------|------------------|  
|sys.dm_xe_database_session_targets.event_session_address|sys.dm_xe_database_sessions.address|Varios a uno|  
  
  
