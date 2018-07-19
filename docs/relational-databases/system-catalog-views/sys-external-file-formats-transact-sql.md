---
title: Sys.external_file_formats (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: a89efb2c-0a3a-4b64-9284-6e93263e29ac
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: f834434e2e03bad82df9221b1d66db6f4f1e300a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2018
ms.locfileid: "38059132"
---
# <a name="sysexternalfileformats-transact-sql"></a>Sys.external_file_formats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2016-xxxx-asdw-pdw-md.md)]

  Contiene una fila para cada formato de archivo externo en la base de datos actual para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], [!INCLUDE[ssSDS](../../includes/sssds-md.md)], y [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].  
  
 Contiene una fila para cada formato de archivo externo en el servidor para [!INCLUDE[ssPDW](../../includes/sspdw-md.md)].  
  
|Nombre de la columna|Tipo de datos|Descripción|Intervalo|  
|-----------------|---------------|-----------------|-----------|  
|file_format_id|**int**|Id. de objeto para el formato de archivo externo.||  
|NAME|**sysname**|Nombre del formato de archivo. en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] y [!INCLUDE[ssSDW](../../includes/sssdw-md.md)], debe ser único para la base de datos. En [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], debe ser único para el servidor.||  
|format_type|**tinyint**|El tipo de formato de archivo.|DELIMITEDTEXT, RCFILE, ORC, PARQUET|  
|field_terminator|**nvarchar (10)**|Para obtener más format_type = DELIMITEDTEXT, esto es el terminador de campo.||  
|string_delimiter|**nvarchar (10)**|Para obtener más format_type = DELIMITEDTEXT, es el delimitador de cadena.||  
|date_format|**nvarchar(50)**|Para obtener más format_type = DELIMITEDTEXT, esto es el formato de hora y fecha definido por el usuario.||  
|use_type_default|**bit**|Para format_type = texto DELIMITADO, especifica cómo controlar los valores que faltan cuando PolyBase está importando datos desde archivos de texto HDFS a [!INCLUDE[ssSDW](../../includes/sssdw-md.md)].|0: almacenar los valores que faltan, como la cadena 'NULL'.<br /><br /> 1: almacenar los valores que faltan, como el valor predeterminado de columna.|  
|serde_method|**nvarchar(255)**|Para obtener más format_type = RCFILE, este es el método de serialización y deserialización.||  
|row_terminator|**nvarchar (10)**|Para obtener más format_type = DELIMITEDTEXT, se trata de la cadena de caracteres que finaliza cada fila en el archivo externo de Hadoop.|Siempre '\n'.|  
|codificación|**nvarchar (10)**|Para obtener más format_type = DELIMITEDTEXT, este es el método de codificación para el archivo externo de Hadoop.|Siempre 'UTF8'.|  
|data_compression|**nvarchar(255)**|El método de compresión de datos para los datos externos.|Para obtener más format_type = DELIMITEDTEXT:<br /><br /> -'org.apache.hadoop.io.compress.DefaultCodec'<br />-'org.apache.hadoop.io.compress.GzipCodec'<br /><br /> Para obtener más format_type = RCFILE:<br /><br /> -'org.apache.hadoop.io.compress.DefaultCodec'<br /><br /> Para obtener más format_type = ORC:<br /><br /> -'org.apache.hadoop.io.compress.DefaultCodec'<br />-   'org.apache.hadoop.io.compress.SnappyCodec'<br /><br /> Para obtener más format_type = PARQUET:<br /><br /> -'org.apache.hadoop.io.compress.GzipCodec'<br />-   'org.apache.hadoop.io.compress.SnappyCodec'|  
  
## <a name="permissions"></a>Permisos  
 La visibilidad de los metadatos en las vistas de catálogo se limita a los elementos protegibles y que son propiedad de un usuario o sobre los que el usuario tiene algún permiso. Para obtener más información, consulte [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md).  
  
## <a name="see-also"></a>Vea también  
 [sys.external_data_sources &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-data-sources-transact-sql.md)   
 [Sys.external_tables &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-external-tables-transact-sql.md)   
 [CREATE EXTERNAL FILE FORMAT &#40;Transact-SQL&#41;](../../t-sql/statements/create-external-file-format-transact-sql.md)  
  
  
