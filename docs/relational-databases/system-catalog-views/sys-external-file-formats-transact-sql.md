---
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
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: eae119fe16b916f47f1acdcd2ebe15efd96e51e9
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "68048389"
---
# <a name="sysexternal_file_formats-transact-sql"></a>Sys. external_file_formats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contiene una fila para cada formato de archivo externo en la base de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]datos [!INCLUDE[ssSDS](../../includes/sssds-md.md)]actual para [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], y.  
  
 Contiene una fila para cada formato de archivo externo en el servidor [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]para.  
  
|Nombre de columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|file_format_id|**int**|IDENTIFICADOR de objeto para el formato de archivo externo.||  
|name|**sysname**|Nombre del formato de archivo. en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], es único para la base de datos. En [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], es único para el servidor de.||  
|format_type|**tinyint**|Tipo de formato de archivo.|DELIMITEDTEXT, RCFILE, ORC, PARQUET|  
|field_terminator|**nvarchar(10**|Por format_type = DELIMITEDTEXT, este es el terminador de campo.||  
|string_delimiter|**nvarchar(10**|Por format_type = DELIMITEDTEXT, este es el delimitador de cadena.||  
|date_format|**nvarchar(50)**|Por format_type = DELIMITEDTEXT, este es el formato de fecha y hora definido por el usuario.||  
|use_type_default|**bit**|En format_type = texto delimitado, especifica cómo controlar los valores que faltan cuando polybase está importando datos de archivos de [!INCLUDE[ssSDW](../../includes/sssdw-md.md)]texto HDFS en.|0: almacena los valores que faltan como la cadena "NULL".<br /><br /> 1-almacenar los valores que faltan como valor predeterminado de la columna.|  
|serde_method|**nvarchar(255)**|Por format_type = RCFILE, este es el método de serialización y deserialización.||  
|row_terminator|**nvarchar(10**|Por format_type = DELIMITEDTEXT, esta es la cadena de caracteres que finaliza cada fila del archivo de Hadoop externo.|Siempre es "\n".|  
|encoding|**nvarchar(10**|Por format_type = DELIMITEDTEXT, este es el método de codificación del archivo de Hadoop externo.|Siempre es ' UTF8 '.|  
|data_compression|**nvarchar(255)**|Método de compresión de datos para los datos externos.|Por format_type = DELIMITEDTEXT:<br /><br /> -' org. apache. Hadoop. IO. compress. DefaultCodec '<br />-' org. apache. Hadoop. IO. compress. GzipCodec '<br /><br /> Por format_type = RCFILE:<br /><br /> -' org. apache. Hadoop. IO. compress. DefaultCodec '<br /><br /> Por format_type = ORC:<br /><br /> -' org. apache. Hadoop. IO. compress. DefaultCodec '<br />-' org. apache. Hadoop. IO. compress. SnappyCodec '<br /><br /> Por format_type = PARQUET:<br /><br /> -' org. apache. Hadoop. IO. compress. GzipCodec '<br />-' org. apache. Hadoop. IO. compress. SnappyCodec '|  
  
## <a name="permissions"></a>Permisos  
 La visibilidad de los metadatos en las vistas de catálogo se limita a los elementos protegibles y que son propiedad de un usuario o sobre los que el usuario tiene algún permiso.  Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Consulte también  
 [Sys. external_data_sources &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)   
 [Sys. external_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)  
  
  
