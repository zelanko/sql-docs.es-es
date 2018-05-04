---
title: Sys.external_data_sources (Transact-SQL) | Documentos de Microsoft
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 1016db6e-9950-4ae2-a004-bd4171e27359
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 1380dcaa90a42f011b4029f4577b018b234f2795
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sysexternaldatasources-transact-sql"></a>Sys.external_data_sources (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Contiene una fila por cada origen de datos externo en la base de datos actual para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)], y [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
 Contiene una fila por cada origen de datos externo en el servidor para [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|data_source_id|**int**|Identificador de objeto de origen de datos externo.||  
|name|**sysname**|Nombre del origen de datos externo.||  
|ubicación|**nvarchar(4000)**|La cadena de conexión, que incluye el protocolo, dirección IP y puerto para el origen de datos externo.||  
|type_desc|**nvarchar(255)**|Tipo que se muestra como una cadena de origen de datos.|HADOOP, RDBMS, SHARD_MAP_MANAGER, RemoteDataArchiveTypeExtDataSource|  
|Tipo|**tinyint**|Tipo de origen de datos aparece como un número.|0 - HADOOP<br /><br /> 1 - RDBMS<br /><br /> 2 - SHARD_MAP_MANAGER<br /><br /> 3 - RemoteDataArchiveTypeExtDataSource|  
|resource_manager_location|**nvarchar(4000)**|Para, escriba HADOOP, la dirección IP y puerto ubicación del Administrador de recursos de Hadoop. Esto se usa para enviar un trabajo en un origen de datos de Hadoop.<br /><br /> NULL para otros tipos de orígenes de datos externos.||  
|credential_id|**int**|El identificador de objeto de la base de datos con ámbito de credenciales usadas para conectarse al origen de datos externo.||  
|database_name|**sysname**|Para tipo de RDBMS, el nombre de la base de datos remota. Para tipo, SHARD_MAP_MANAGER, el nombre de la base de datos de administrador de asignación de particiones. NULL para otros tipos de orígenes de datos externos.||  
|shard_map_name|**sysname**|Para tipo SHARD_MAP_MANAGER, el nombre de la asignación de particiones. NULL para otros tipos de orígenes de datos externos.||  
  
## <a name="permissions"></a>Permissions  
 La visibilidad de los metadatos en las vistas de catálogo se limita a los elementos protegibles y que son propiedad de un usuario o sobre los que el usuario tiene algún permiso. Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [Sys.external_file_formats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)   
 [Sys.external_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)   
 [CREATE EXTERNAL DATA SOURCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-data-source-transact-sql.md)  
  
  
