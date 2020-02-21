---
title: Fecha y hora y conjuntos de filas de esquema | Microsoft Docs
description: Fecha y hora y conjuntos de filas de esquema
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB], schema rowsets
author: pmasl
ms.author: pelopes
ms.openlocfilehash: 19524bbd935335cc0568dc499f95a794580df476
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 01/31/2020
ms.locfileid: "68015692"
---
# <a name="metadata---date-and-time-and-schema-rowsets"></a>Metadatos: fecha y hora y conjuntos de filas de esquema
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  En este tema se proporciona información sobre los conjuntos de filas COLUMNS y PROCEDURE_PARAMETERS. Esta información está relacionada con las mejoras realizadas en la fecha y la hora de OLE DB introducidas en [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)].  
  
## <a name="columns-rowset"></a>Conjunto de filas COLUMNS  
 Para los tipos de fecha y hora se devuelven los siguientes valores de columna:  
  
|Tipo de columna|DATA_TYPE|COLUMN_FLAGS, DBCOLUMFLAGS_SS_ISVARIABLESCALE|DATETIME_PRECISION|  
|-----------------|----------------|------------------------------------------------------|-------------------------|  
|date|DBTYPE_DBDATE|Desactivar|0|  
|time|DBTYPE_DBTIME2|Set|0..7|  
|smalldatetime|DBTYPE_DBTIMESTAMP|Desactivar|0|  
|datetime|DBTYPE_DBTIMESTAMP|Desactivar|3|  
|datetime2|DBTYPE_DBTIMESTAMP|Set|0..7|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|Set|0..7|  
  
 En COLUMN_FLAGS, DBCOLUMNFLAGS_ISFIXEDLENGTH es siempre TRUE para los tipos de fecha y hora, y las marcas siguientes son siempre FALSE:  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER  
  
-   DBCOLUMNFLAGS_MAYDEFER  
  
 Se pueden establecer las marcas restantes (DBCOLUMNFLAGS_ISNULLABLE, DBCOLUMNFLAGS_MAYBENULL, DBCOLUMNFLAGS_WRITE y DBCOLUMNFLAGS_WRITEUNKNOWN), dependiendo de cómo se defina la columna.  
  
 Se proporciona una nueva marca en COLUMN_FLAGS, DBCOLUMNFLAGS_SS_ISVARIABLESCALE, para permitir que una aplicación determine el tipo de servidor de columnas, donde DATA_TYPE es DBTYPE_DBTIMESTAMP. DATETIME_PRECISION también se debe utilizar para identificar el tipo de servidor.  
  
 DBCOLUMNFLAGS_SS_ISVARIABLESCALE es solo válido cuando se conecta a un servidor [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] o posteriores. DBCOLUMNFLAGS_SS_ISFIXEDSCALE no está definido cuando se conecta a servidores de nivel inferior.  
  
## <a name="procedure_parameters-rowset"></a>Conjunto de filas PROCEDURE_PARAMETERS  
 DATA_TYPE contiene los mismos valores que el conjunto de filas de esquema COLUMNS y TYPE_NAME contiene el tipo de servidor.  
  
 Se ha agregado una nueva columna, SS_DATETIME_PRECISION, para devolver la precisión del tipo como en la columna DATETIME_PRECISION, similar al conjunto de filas COLUMNS.  
  
## <a name="provider_types-rowset"></a>Conjunto de filas PROVIDER_TYPES  
 Para los tipos de fecha y hora se devuelven las siguientes filas:  
  
|Tipo -><br /><br /> Columna|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|DATA_TYPE|DBTYPE_DBDATE|DBTYPE_DBTIME2|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMPOFFSET|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|'|'|'|'|'|'|  
|LITERAL_SUFFIX|'|'|'|'|'|'|  
|CREATE_PARAMS|NULL|scale|NULL|NULL|scale|scale|  
|IS_NULLABLE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
|CASE_SENSITIVE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FIXED_PREC_SCALE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|AUTO_UNIQUE_VALUE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|LOCAL_TYPE_NAME|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|0|NULL|NULL|0|0|  
|MAXIMUM_SCALE|NULL|7|NULL|NULL|7|7|  
|GUID|NULL|NULL|NULL|NULL|NULL|NULL|  
|TYPELIB|NULL|NULL|NULL|NULL|NULL|NULL|  
|VERSION|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_LONG|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|BEST_MATCH|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE a menos que se dé uno de los siguientes casos:<br /><br /> Es un cliente conectado a un servidor de nivel inferior.<br /><br /> La propiedad de conexión de compatibilidad de tipo de datos especifica un nivel de compatibilidad igual a 80.|VARIANT_TRUE a menos que se dé uno de los siguientes casos:<br /><br /> Es un cliente conectado a un servidor de nivel inferior.<br /><br /> La propiedad de conexión de compatibilidad de tipo de datos especifica un nivel de compatibilidad igual a 80.|VARIANT_TRUE|  
|IS_FIXEDLENGTH|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
  
 OLE DB solo define MINIMUM_SCALE y MAXIMUM_SCALE para tipos numéricos y decimales, por lo que el uso que hace el controlador OLE DB para SQL Server de estas columnas para time, datetime2 y datetimeoffset no es estándar.  
  
## <a name="see-also"></a>Consulte también  
 [Metadatos &#40;OLE DB&#41;](../../oledb/ole-db-date-time/metadata-parameter-and-rowset.md)  
  
  
