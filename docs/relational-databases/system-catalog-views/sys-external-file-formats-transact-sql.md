---
description: Sys. external_file_formats (Transact-SQL)
title: Sys. external_file_formats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a89efb2c-0a3a-4b64-9284-6e93263e29ac
author: CarlRabeler
ms.author: carlrab
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 327e43fe36762ae2118c3c737bc0beb28260b8d7
ms.sourcegitcommit: 5da46e16b2c9710414fe36af9670461fb07555dc
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 09/01/2020
ms.locfileid: "89283796"
---
# <a name="sysexternal_file_formats-transact-sql"></a>Sys. external_file_formats (Transact-SQL)
[!INCLUDE [sqlserver2016-asdbmi-asa-pdw](../../includes/applies-to-version/sqlserver2016-asdbmi-asa-pdw.md)]

  Contiene una fila para cada formato de archivo externo en la base de datos actual para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , [!INCLUDE[ssSDS](../../includes/sssds-md.md)] y [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] .  
  
 Contiene una fila para cada formato de archivo externo en el servidor para [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] .  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|file_format_id|**int**|IDENTIFICADOR de objeto para el formato de archivo externo.||  
|name|**sysname**|Nombre del formato de archivo. en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] , es único para la base de datos. En [!INCLUDE[ssPDW](../../includes/sspdw-md.md)] , es único para el servidor de.||  
|format_type|**tinyint**|Tipo de formato de archivo.|DELIMITEDTEXT, RCFILE, ORC, PARQUET|  
|field_terminator|**nvarchar(10**|Por format_type = DELIMITEDTEXT, este es el terminador de campo.||  
|string_delimiter|**nvarchar(10**|Por format_type = DELIMITEDTEXT, este es el delimitador de cadena.||  
|date_format|**nvarchar(50)**|Por format_type = DELIMITEDTEXT, este es el formato de fecha y hora definido por el usuario.||  
|use_type_default|**bit**|En format_type = texto delimitado, especifica cómo controlar los valores que faltan cuando polybase está importando datos de archivos de texto HDFS en [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] .|0: almacena los valores que faltan como la cadena "NULL".<br /><br /> 1-almacenar los valores que faltan como valor predeterminado de la columna.|  
|serde_method|**nvarchar(255)**|Por format_type = RCFILE, este es el método de serialización y deserialización.||  
|row_terminator|**nvarchar(10**|Por format_type = DELIMITEDTEXT, esta es la cadena de caracteres que finaliza cada fila del archivo de Hadoop externo.|Siempre es "\n".|  
|encoding|**nvarchar(10**|Por format_type = DELIMITEDTEXT, este es el método de codificación del archivo de Hadoop externo.|Siempre es ' UTF8 '.|  
|data_compression|**nvarchar(255)**|Método de compresión de datos para los datos externos.|Por format_type = DELIMITEDTEXT:<br /><br /> -' org. apache. Hadoop. IO. compress. DefaultCodec '<br />-' org. apache. Hadoop. IO. compress. GzipCodec '<br /><br /> Por format_type = RCFILE:<br /><br /> -' org. apache. Hadoop. IO. compress. DefaultCodec '<br /><br /> Por format_type = ORC:<br /><br /> -' org. apache. Hadoop. IO. compress. DefaultCodec '<br />-' org. apache. Hadoop. IO. compress. SnappyCodec '<br /><br /> Por format_type = PARQUET:<br /><br /> -' org. apache. Hadoop. IO. compress. GzipCodec '<br />-' org. apache. Hadoop. IO. compress. SnappyCodec '|  
  
## <a name="permissions"></a>Permisos  
 La visibilidad de los metadatos en las vistas de catálogo se limita a los elementos protegibles y que son propiedad de un usuario o sobre los que el usuario tiene algún permiso. Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
 [Sys. external_data_sources &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)   
 [Sys. external_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)  
  
  
