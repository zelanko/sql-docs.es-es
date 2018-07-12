---
title: Nuevas características fecha y hora con versiones anteriores SQL Server (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB], enhanced behavior with earlier SQL Server versions
ms.assetid: 96976bac-018c-47cc-b1b2-fa9605eb55e5
caps.latest.revision: 27
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bd1f9f48b1703719ce08ca2d1da4a5c9addaffc0
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37420191"
---
# <a name="new-date-and-time-features-with-previous-sql-server-versions-ole-db"></a>Nuevas características fecha y hora con versiones anteriores SQL Server (OLE DB)
  Este tema describe el comportamiento esperado cuando una aplicación cliente que utiliza características mejorada fecha y hora se comunica con una versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] anteriores a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]y cuando un cliente compilado con una versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client anterior a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] envía comandos a un servidor que admite características mejoradas de fecha y hora.  
  
## <a name="down-level-client-behavior"></a>Comportamiento del cliente de nivel inferior  
 Las aplicaciones cliente que usan una versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client anterior a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] ver los tipos de fecha y hora nueva como `nvarchar` columnas. El contenido de las columnas son representaciones de literales. Para obtener más información, vea la sección "Formatos de datos: cadenas y literales" de [compatibilidad con tipos de datos para OLE DB mejoras de fecha y hora](data-type-support-for-ole-db-date-and-time-improvements.md). El tamaño de columna es la longitud máxima del literal para la precisión especificada para la columna.  
  
 Las API de catálogo devolverán metadatos coherentes con el código del tipo de datos de nivel inferior que se devuelve al cliente (por ejemplo, `nvarchar`) y la representación asociada de nivel inferior (por ejemplo, el formato de literal adecuado). Sin embargo, el nombre del tipo de datos devuelto será el nombre del tipo real de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
 Cuando se ejecuta una aplicación de cliente de nivel inferior en un [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] (o posterior) en que los cambios de esquema a la fecha y hora se realizaron los tipos de servidor, el comportamiento esperado es como sigue:  
  
|Tipo de cliente OLE DB|Tipo de SQL Server 2005|Tipo SQL Server 2008 (o posterior)|Conversión del resultado (servidor a cliente)|Conversión de parámetros (cliente a servidor)|  
|------------------------|--------------------------|---------------------------------------|--------------------------------------------|-----------------------------------------------|  
|DBTYPE_DBDATE|DATETIME|date|Aceptar|Aceptar|  
|DBTYPE_DBTIMESTAMP|||Los campos de hora se establecen en cero.|Si el campo de hora es distinto de cero, se producirá un error de IRowsetChange debido al truncamiento de cadena.|  
|DBTYPE_DBTIME||Time(0)|Aceptar|Aceptar|  
|DBTYPE_DBTIMESTAMP|||Los campos de fecha se establecen en la fecha actual.|Si las fracciones de segundo son distintas de cero, se producirá un error de IRowsetChange debido al truncamiento de cadena.<br /><br /> Se omite la fecha.|  
|DBTYPE_DBTIME||Time(7)|Se produce un error: literal de hora no válido.|Aceptar|  
|DBTYPE_DBTIMESTAMP|||Se produce un error: literal de hora no válido.|Aceptar|  
|DBTYPE_DBTIMESTAMP||Datetime2(3)|Aceptar|Aceptar|  
|DBTYPE_DBTIMESTAMP||Datetime2 (7)|Aceptar|Aceptar|  
|DBTYPE_DBDATE|Smalldatetime|date|Aceptar|Aceptar|  
|DBTYPE_DBTIMESTAMP|||Los campos de hora se establecen en cero.|Si el campo de hora es distinto de cero, se producirá un error de IRowsetChange debido al truncamiento de cadena.|  
|DBTYPE_DBTIME||Time(0)|Aceptar|Aceptar|  
|DBTYPE_DBTIMESTAMP|||Los campos de fecha se establecen en la fecha actual.|Si las fracciones de segundo son distintas de cero, se producirá un error de IRowsetChange debido al truncamiento de cadena.<br /><br /> Se omite la fecha.|  
|DBTYPE_DBTIMESTAMP||Datetime2(0)|Aceptar|Aceptar|  
  
 OK significa que si ha funcionado con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], también debería funcionar con [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o posterior.  
  
 Solo se han considerado los siguientes cambios de esquema:  
  
-   Usar un nuevo tipo donde de forma lógica una aplicación requiere un único valor de fecha u hora. Sin embargo, se ha forzado a la aplicación a usar `datetime` o `smalldatetime` porque no había disponibles tipos de fecha y hora independientes.  
  
-   Usar un nuevo tipo para obtener más precisión o exactitud en fracciones de segundo.  
  
-   Cambio a `datetime2` porque se trata del tipo de datos preferido para la fecha y hora.  
  
 Se producirá un error de las aplicaciones que usan los metadatos del servidor obtenidos a través de conjuntos de filas de esquema o ICommandWithParameters:: GetParameterInfo para establecer la información de tipo de parámetro a través de ICommandWithParameters:: SetParameterInfo durante las conversiones de cliente donde la cadena representación de un tipo de origen es mayor que la representación de cadena del tipo de destino. Por ejemplo, si un enlace de cliente usa DBTYPE_DBTIMESTAMP y la columna del servidor es la fecha, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client convertirá el valor a "aaaa-mm-dd fff", pero los metadatos del servidor se devolverán como `nvarchar(10)`. El desbordamiento resultante produce DBSTATUS_E_CATCONVERTVALUE. Surgen problemas similares con las conversiones de datos por IRowsetChange, porque se ha establecido los metadatos del conjunto de filas de los metadatos del conjunto de resultados.  
  
### <a name="parameter-and-rowset-metadata"></a>Parámetros y metadatos de conjuntos de filas  
 Esta sección describen los metadatos de parámetros, las columnas de resultados y conjuntos de filas de esquema para los clientes que se compilan con una versión de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client anterior a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
#### <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 La estructura DBPARAMINFO devuelve la siguiente información a través de la *prgParamInfo* parámetro:  
  
|Tipo de parámetro|wType|ulParamSize|bPrecision|bScale|  
|--------------------|-----------|-----------------|----------------|------------|  
|Date|DBTYPE_WSTR|10|~0|~0|  
|time|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|~0|~0|  
  
 Observe que algunos de estos intervalos de valores no son continuos; por ejemplo, en el intervalo 8,10..16 falta el 9. Esto se debe a la adición de un separador decimal cuando la precisión fraccionaria es mayor que cero.  
  
#### <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 Se devuelven las siguientes columnas:  
  
|Tipo de columna|DBCOLUMN_TYPE|DBCOLUMN_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE, DBCOLUMN_DATETIMEPRECISION|  
|-----------------|--------------------|--------------------------|-------------------------|--------------------------------------------------|  
|Date|DBTYPE_WSTR|10|NULL|NULL|  
|time|DBTYPE_WSTR|8, 10..16|NULL|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|NULL|NULL|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|NULL|NULL|  
  
#### <a name="columnsinfogetcolumninfo"></a>ColumnsInfo::GetColumnInfo  
 La estructura DBCOLUMNINFO devuelve la siguiente información:  
  
|Tipo de parámetro|wType|ulColumnSize|bPrecision|bScale|  
|--------------------|-----------|------------------|----------------|------------|  
|Date|DBTYPE_WSTR|10|~0|~0|  
|time(1..7)|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|DATETIME|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19,21..27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|~0|~0|  
  
### <a name="schema-rowsets"></a>Conjuntos de filas de esquema  
 En esta sección se describen los metadatos para los parámetros, columnas de resultados y conjuntos de filas de esquema de los nuevos tipos de datos. Esta información es útil es tener un proveedor de cliente desarrollado con herramientas anteriores a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
#### <a name="columns-rowset"></a>Conjunto de filas COLUMNS  
 Para los tipos de fecha y hora se devuelven los siguientes valores de columna:  
  
|Tipo de columna|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|DATETIME_PRECISION|  
|-----------------|----------------|--------------------------------|------------------------------|-------------------------|  
|Date|DBTYPE_WSTR|10|20|NULL|  
|time|DBTYPE_WSTR|8, 10..16|16,20..32|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|0|  
|DATETIME|DBTYPE_DBTIMESTAMP|NULL|NULL|3|  
|datetime2|DBTYPE_WSTR|19,21..27|38,42..54|NULL|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|52, 56..68|NULL|  
  
#### <a name="procedureparameters-rowset"></a>Conjunto de filas PROCEDURE_PARAMETERS  
 Para los tipos de fecha y hora se devuelven los siguientes valores de columna:  
  
|Tipo de columna|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|TYPE_NAME<br /><br /> LOCAL_TYPE_NAME|  
|-----------------|----------------|--------------------------------|------------------------------|--------------------------------------|  
|Date|DBTYPE_WSTR|10|20|Date|  
|time|DBTYPE_WSTR|8, 10..16|16,20..32|time|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|smalldatetime|  
|DATETIME|DBTYPE_DBTIMESTAMP|NULL|NULL|DATETIME|  
|datetime2|DBTYPE_WSTR|19,21..27|38,42..54|datetime2|  
|datetimeoffset|DBTYPE_WSTR|26,28..34|52, 56..68|datetimeoffset|  
  
#### <a name="providertypes-rowset"></a>Conjunto de filas PROVIDER_TYPES  
 Para los tipos de fecha y hora se devuelven las siguientes filas:  
  
|Tipo -><br /><br /> columna|Date|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|Date|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|DATA_TYPE|DBTYPE_WSTR|DBTYPE_WSTR|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_WSTR|DBTYPE_WSTR|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|‘|‘|‘|‘|‘|‘|  
|LITERAL_SUFFIX|‘|‘|‘|‘|‘|‘|  
|CREATE_PARAMS|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_NULLABLE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
|CASE_SENSITIVE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FIXED_PREC_SCALE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|AUTO_UNIQUE_VALUE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|LOCAL_TYPE_NAME|Date|time|smalldatetime|DATETIME|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|NULL|NULL|NULL|NULL|NULL|  
|MAXIMUM_SCALE|NULL|NULL|NULL|NULL|NULL|NULL|  
|GUID|NULL|NULL|NULL|NULL|NULL|NULL|  
|TYPELIB|NULL|NULL|NULL|NULL|NULL|NULL|  
|VERSION|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_LONG|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|BEST_MATCH|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_TRUE|VARIANT_FALSE|VARIANT_FALSE|  
|IS_FIXEDLENGTH|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
  
## <a name="down-level-server-behavior"></a>Comportamiento de un servidor de nivel inferior  
 Cuando se conecta a un servidor de una versión anterior a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], cualquier intento de usar los nuevos nombres de tipo de servidor (por ejemplo, con ICommandWithParameters:: SetParameterInfo o ITableDefinition:: CreateTable) dará lugar a DB_E_BADTYPENAME.  
  
 Si los nuevos tipos se enlazan en parámetros o resultados sin usar un nombre de tipo y el nuevo tipo se usa para especificar implícitamente el tipo de servidor, o no hay ninguna conversión válida del tipo de servidor al tipo de cliente, se devuelve DB_E_ERRORSOCCURRED, y DBBINDSTATUS_UNSUPPORTED_CONVERSION se establece como estado de enlace para el descriptor de acceso que se usó en Execute.  
  
 Si hay una conversión de cliente compatible del tipo de búfer al tipo de servidor para la versión del servidor en la conexión, pueden usarse todos los tipos de búfer del cliente. En este contexto, *tipo de servidor* significa que el tipo especificado por ICommandWithParameters:: SetParameterInfo, o implícita en el tipo de búfer si no se ha llamado ICommandWithParameters:: SetParameterInfo. Esto significa que DBTYPE_DBTIME2 y DBTYPE_DBTIMESTAMPOFFSET pueden usarse con servidores de nivel inferior, o cuando DataTypeCompatibility=80, si la conversión del cliente a un tipo de servidor compatible se realiza correctamente. Es evidente que si el tipo de servidor es incorrecto, el servidor todavía podría notificar un error si no puede realizar una conversión implícita al tipo de servidor real.  
  
## <a name="sspropinitdatatypecompatibility-behavior"></a>Comportamiento de SSPROP_INIT_DATATYPECOMPATIBILITY  
 Cuando SSPROP_INIT_DATATYPECOMPATIBILITY se establece en SSPROPVAL_DATATYPECOMPATIBILITY_SQL2000, los tipos de fecha y hora nuevas y los metadatos asociados aparecen en los clientes en que aparecen para los clientes de nivel inferior, como se describe en [cambios de copia masiva Mejorado de tipos de fecha y hora &#40;de OLE DB y ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
## <a name="comparability-for-irowsetfind"></a>Comparaciones en IRowsetFind  
 Se permiten todos los operadores de comparación para los nuevos tipos de fecha y hora, debido a que aparecen como tipos de cadena en lugar de tipos de fecha y hora.  
  
## <a name="see-also"></a>Vea también  
 [Mejoras de fecha y hora &#40;OLE DB&#41;](date-and-time-improvements-ole-db.md)  
  
  
