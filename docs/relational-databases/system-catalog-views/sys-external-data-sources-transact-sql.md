---
title: Sys. external_data_sources (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 1016db6e-9950-4ae2-a004-bd4171e27359
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: bbec44831d7025fd53cafe0248eb1f69b79bf14d
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/05/2020
ms.locfileid: "82828169"
---
# <a name="sysexternal_data_sources-transact-sql"></a>sys.external_data_sources (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Contiene una fila para cada origen de datos externo en la base de datos actual para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , [!INCLUDE[ssSDS](../../includes/sssds-md.md)] y [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] .  
  
 Contiene una fila por cada origen de datos externo en el servidor para [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] .  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|data_source_id|**int**|IDENTIFICADOR de objeto del origen de datos externo.||  
|name|**sysname**|Nombre del origen de datos externo.||  
|ubicación|**nvarchar(4000)**|La cadena de conexión, que incluye el protocolo, la dirección IP y el puerto para el origen de datos externo.||  
|type_desc|**nvarchar(255)**|Tipo de origen de datos que se muestra como una cadena.|HADOOP, RDBMS, SHARD_MAP_MANAGER, RemoteDataArchiveTypeExtDataSource|  
|tipo|**tinyint**|Tipo de origen de datos que se muestra como un número.|0-HADOOP<br /><br /> 1: RDBMS<br /><br /> 2-SHARD_MAP_MANAGER<br /><br /> 3-RemoteDataArchiveTypeExtDataSource|  
|resource_manager_location|**nvarchar(4000)**|Para el tipo HADOOP, la dirección IP y el puerto del administrador de recursos de Hadoop. Se usa para enviar un trabajo en un origen de datos de Hadoop.<br /><br /> NULL para otros tipos de orígenes de datos externos.||  
|credential_id|**int**|IDENTIFICADOR de objeto de la credencial con ámbito de base de datos utilizada para conectarse al origen de datos externo.||  
|database_name|**sysname**|Para el tipo RDBMS, el nombre de la base de datos remota. En tipo, SHARD_MAP_MANAGER, el nombre de la base de datos del administrador de mapa de particiones. NULL para otros tipos de orígenes de datos externos.||  
|shard_map_name|**sysname**|Para el tipo SHARD_MAP_MANAGER, el nombre del mapa de particiones. NULL para otros tipos de orígenes de datos externos.||  
  
## <a name="permissions"></a>Permisos  
 La visibilidad de los metadatos en las vistas de catálogo se limita a los elementos protegibles y que son propiedad de un usuario o sobre los que el usuario tiene algún permiso.  Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
 [Sys. external_file_formats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)   
 [Sys. external_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)   
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
  
