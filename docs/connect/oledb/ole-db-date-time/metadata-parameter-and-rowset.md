---
title: Parámetros y metadatos del conjunto de filas | Microsoft Docs
description: Parámetros y metadatos de conjuntos de filas
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-date-time
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- metadata [OLE DB]
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: dfc4ffcb718cc9e11e760505baedce17507e1b90
ms.sourcegitcommit: 50838d7e767c61dd0b5e677b6833dd5c139552f2
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 07/18/2018
ms.locfileid: "39107357"
---
# <a name="metadata---parameter-and-rowset"></a>Metadatos: Parámetro y conjunto de filas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  En este artículo, se proporciona información sobre los siguientes tipos y miembros de tipo relacionados con las mejoras de fecha y hora de OLE DB.  
  
-   Estructura DBBINDING  
  
-   **ICommandWithParameters::GetParameterInfo**  
  
-   **ICommandWithParameters::SetParameterInfo**  
  
-   **IColumnsRowset::GetColumnsRowset**  
  
-   **IColumnsInfo::GetColumnInfo**  
  
## <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 La siguiente información se devuelve en la estructura DBPARAMINFO mediante *prgParamInfo*:  
  
|Tipo de parámetro|*wType*|*ulParamSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBPARAMFLAGS_SS_ISVARIABLESCALE|  
|--------------------|-------------|-------------------|------------------|--------------|-----------------------------------------------------|  
|Date|DBTYPE_DBDATE|6|10|0|Desactivar|  
|time|DBTYPE_DBTIME2|10|8, 10..16|0..7|Establecer|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Desactivar|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|Desactivar|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|Establecer|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|Establecer|  
  
 Observe que en algunos casos los intervalos de valores no son continuos. Esto se debe a la adición de un separador decimal cuando la precisión fraccionaria es mayor que cero.  
  
 DBPARAMFLAGS_SS_ISVARIABLESCALE solo es válido cuando se conecta a un servidor [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] (o posteriores). DBPARAMFLAGS_SS_ISVARIABLESCALE no se establece nunca cuando se conecta a servidores de nivel inferior.  
  
## <a name="icommandwithparameterssetparameterinfo-and-implied-parameter-types"></a>ICommandWithParameters::SetParameterInfo y tipos de parámetro implícitos  
 La información que se proporciona en la estructura DBPARAMBINDINFO debe cumplir lo siguiente:  
  
|*pwszDataSourceType*<br /><br /> (depende del proveedor)|*pwszDataSourceType*<br /><br /> (OLE DB genérico)|*ulParamSize*|*bScale*|  
|----------------------------------------------------|-------------------------------------------------|-------------------|--------------|  
||DBTYPE_DATE|6|Omitido|  
|Date|DBTYPE_DBDATE|6|Omitido|  
||DBTYPE_DBTIME|10|Omitido|  
|time|DBTYPE_DBTIME2|10|0..7|  
|smalldatetime||16|Omitido|  
|DATETIME||16|Omitido|  
|datetime2 o DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|16|0..7|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|0..7|  
  
 El *bPrecision* parámetro se omite.  
  
 No se tiene en cuenta "DBPARAMFLAGS_SS_ISVARIABLESCALE" al enviar los datos al servidor. Las aplicaciones pueden exigir el uso de tipos heredados de flujo TDS mediante los nombres de tipo específico del proveedor "**datetime**" y "**smalldatetime**". Cuando se conecta a los servidores de [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] (o posteriores), se usará el formato "**datetime2**" y, si es necesario, se producirá una conversión implícita de servidor cuando el nombre de tipo sea "**datetime2**" o "DBTYPE_DBTIMESTAMP". *bScale* se omite si los nombres de tipo específico del proveedor "**datetime**"o"**smalldatetime**" se usan. En caso contrario, las aplicaciones deben asegurarse de que *bScale* se ha establecido correctamente. Las aplicaciones actualizadas de MDAC y controlador de OLE DB para SQL Server desde [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] que usan "DBTYPE_DBTIMESTAMP" se producirá un error si no se establece *bScale* correctamente. Cuando esté conectado a las instancias de servidor anteriores a [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)], un valor *bScale* que no sea 0 o 3 con "DBTYPE_DBTIMESTAMP" es un error y se devolverá E_FAIL.  
  
 Cuando no se llama a ICommandWithParameters:: SetParameterInfo, el proveedor implica el tipo de servidor en el tipo de enlace como se especifica en IAccessor:: CreateAccessor como sigue:  
  
|Tipo de enlace|*pwszDataSourceType*<br /><br /> (depende del proveedor)|  
|------------------|----------------------------------------------------|  
|DBTYPE_DATE|datetime2(0)|  
|DBTYPE_DBDATE|Date|  
|DBTYPE_DBTIME|time(0)|  
|DBTYPE_DBTIME2|time(7)|  
|DBTYPE_DBTIMESTAMP|datetime2(7)|  
|DBTYPE_DBTIMESTAMPOFFSET|datetimeoffset(7)|  
  
## <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 **IColumnsRowset:: GetColumnsRowset** devuelve las columnas siguientes:  
  
|Tipo de columna|DBCOLUMN_TYPE|DBCOLUM_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE, DBCOLUMN_DATETIMEPRECISION|DBCOLUMN_FLAGS, DBCOLUMNFLAGS_SS_ISVARIABLESCALE|  
|-----------------|--------------------|-------------------------|-------------------------|--------------------------------------------------|---------------------------------------------------------|  
|Date|DBTYPE_DBDATE|6|10|0|Desactivar|  
|time|DBTYPE_DBTIME2|10|8, 10..16|0..7|Establecer|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Desactivar|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|Desactivar|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|Establecer|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|Establecer|  
  
 DBCOLUMN_FLAGS, DBCOLUMNFLAGS_ISFIXEDLENGTH es siempre TRUE para los tipos de fecha y hora, y las marcas siguientes son siempre FALSE:  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER  
  
-   DBCOLUMNFLAGS_MAYDEFER  
  
 Se pueden establecer las marcas restantes (DBCOLUMNFLAGS_ISNULLABLE, DBCOLUMNFLAGS_MAYBENULL, DBCOLUMNFLAGS_WRITE y DBCOLUMNFLAGS_WRITEUNKNOWN), dependiendo de cómo se defina la columna y la consulta real.  
  
 Se proporciona una nueva marca DBCOLUMNFLAGS_SS_ISVARIABLESCALE en DBCOLUMN_FLAGS para permitir que una aplicación determine el tipo de servidor de columnas, donde DBCOLUMN_TYPE es DBTYPE_DBTIMESTAMP. DBCOLUMN_SCALE o DBCOLUMN_DATETIMEPRECISION también se debe usar para identificar el tipo de servidor.  
  
 DBCOLUMNFLAGS_SS_ISVARIABLESCALE solo es válido cuando se conecta a un servidor [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] (o posteriores). DBCOLUMNFLAGS_SS_ISVARIABLESCALE no está definido cuando se conecta a servidores de nivel inferior.  
  
## <a name="icolumnsinfogetcolumninfo"></a>IColumnsInfo::GetColumnInfo  
 La estructura DBCOLUMNINFO devuelve la información siguiente:  
  
|Tipo de parámetro|*wType*|*ulColumnSize*|*bPrecision*|*bScale*|*dwFlags*<br /><br /> DBPARAMFLAGS_SS_ISVARIABLESCALE|  
|--------------------|-------------|--------------------|------------------|--------------|-----------------------------------------------------|  
|Date|DBTYPE_DBDATE|6|10|0|Desactivar|  
|time(1..7)|DBTYPE_DBTIME2|10|8, 10..16|0..7|Establecer|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|Desactivar|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|Desactivar|  
|datetime2|DBTYPE_DBTIMESTAMP|16|19, 21..27|0..7|Establecer|  
|datetimeoffset|DBTYPE_DBTIMESTAMPOFFSET|20|26, 28..34|0..7|Establecer|  
  
 En *dwFlags*, DBCOLUMNFLAGS_ISFIXEDLENGTH siempre es TRUE para los tipos de fecha y hora, y las marcas siguientes son siempre FALSE:  
  
-   DBCOLUMNFLAGS_CACHEDEFERRED  
  
-   DBCOLUMNFLAGS_ISBOOKMARK  
  
-   DBCOLUMNFLAGS_ISCHAPTER  
  
-   DBCOLUMNFLAGS_ISLONG  
  
-   DBCOLUMNFLAGS_ISROWID  
  
-   DBCOLUMNFLAGS_ISROWVER, MAYDEFER  
  
 Se pueden establecer las marcas restantes (DBCOLUMNFLAGS_ISNULLABLE, DBCOLUMNFLAGS_MAYBENULL, DBCOLUMNFLAGS_WRITE y DBCOLUMNFLAGS_WRITEUNKNOWN).  
  
 Se proporciona una nueva marca DBCOLUMNFLAGS_SS_ISVARIABLESCALE en *dwFlags* para permitir que una aplicación determine el tipo de servidor de columnas, donde *wType* es DBTYPE_DBTIMESTAMP. *bScale* también tiene que usarse para identificar el tipo de servidor.  
  
## <a name="see-also"></a>Ver también  
 [Compatibilidad con tipos de datos para mejoras de fecha y hora de OLE DB](../../oledb/ole-db-date-time/data-type-support-for-ole-db-date-and-time-improvements.md)  
  
  
