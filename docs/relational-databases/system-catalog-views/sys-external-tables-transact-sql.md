---
title: sys.external_tables (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: fac4720c-b679-4ab2-864b-ff7810a9b559
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 4c261068e68503ff01429c3b215261dffcb48053
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/03/2018
---
# <a name="sysexternaltables-transact-sql"></a>sys.external_tables (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-all-md](../../includes/tsql-appliesto-ss2016-all-md.md)]

  Contiene una fila por cada tabla externa en la base de datos actual.  
  
|Nombre de la columna|Tipo de datos|Description|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|\<hereda columnas >||Para obtener una lista de columnas que hereda esta vista, consulte [sys.objects &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md).||  
|max_column_id_used|**int**|Id. de columna máximo utilizado alguna vez para esta tabla.||  
|uses_ansi_nulls|**bit**|La tabla se creó con la opción de base de datos SET ANSI_NULLS establecida en ON.||  
|data_source_id|**int**|Identificador de objeto de origen de datos externo.||  
|file_format_id|**int**|Para las tablas externas a través de un origen de datos externo de HADOOP, es el identificador de objeto para el formato de archivo externo.||  
|ubicación|**nvarchar(4000)**|Para las tablas externas a través de un origen de datos externo de HADOOP, se trata de la ruta de acceso de los datos externos en HDFS.||  
|reject_type|**tinyint**|Para las tablas externas a través de un origen de datos externo de HADOOP, esta es la manera en que se cuentan las filas rechazados al consultar datos externos.|VALOR: el número de filas rechazados.<br /><br /> PORCENTAJE: el porcentaje de filas rechazados.|  
|reject_value|**float**|Para las tablas externas a través de un origen de datos externo de HADOOP:<br /><br /> Para *reject_type =* valor, se trata del número de rechazos de fila para permitir antes de cancelar la consulta.<br /><br /> Para *reject_type* = porcentaje, éste es el porcentaje de rechazos de fila para permitir antes de cancelar la consulta.||  
|reject_sample_value|**int**|Para *reject_type* = porcentaje, este es el número de filas que se va a cargar, ya sea correcta o incorrectamente, antes de calcular el porcentaje de filas rechazados.|NULL si reject_type = valor.|  
|distribution_type|**int**|Para las tablas externas a través de un origen de datos externo SHARD_MAP_MANAGER, es la distribución de datos de las filas de las tablas base subyacentes.|0 – Sharded<br /><br /> 1 – replicado<br /><br /> 2 – Round robin|  
|distribution_desc|**nvarchar(120)**|Para las tablas externas a través de un origen de datos externo SHARD_MAP_MANAGER, este es el tipo de distribución que se muestra como una cadena.||  
|sharding_column_id|**int**|Para las tablas externas a través de un origen de datos externo de SHARD_MAP_MANAGER y una distribución particionada, es el identificador de columna de la columna que contiene los valores de clave de particionamiento.||  
|remote_schema_name|**sysname**|Para las tablas externas a través de un origen de datos externo SHARD_MAP_MANAGER, éste es el esquema donde se encuentra la tabla base en las bases de datos remotos (si difiere del esquema donde se define la tabla externa).||  
|remote_object_name|**sysname**|Para las tablas externas a través de un origen de datos externo SHARD_MAP_MANAGER, este es el nombre de la tabla base en las bases de datos remotos (si es diferente del nombre de la tabla externa).||  
  
## <a name="permissions"></a>Permissions  
 La visibilidad de los metadatos en las vistas de catálogo se limita a los elementos protegibles y que son propiedad de un usuario o sobre los que el usuario tiene algún permiso. Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [sys.external_file_formats &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-file-formats-transact-sql.md)   
 [sys.external_data_sources &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)   
 [CREATE EXTERNAL TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-table-transact-sql.md)  
  
  
