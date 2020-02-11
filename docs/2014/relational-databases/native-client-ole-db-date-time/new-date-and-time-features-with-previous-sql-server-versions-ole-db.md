---
title: Nuevas características de fecha y hora con versiones anteriores de SQL Server (OLE DB) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- date/time [OLE DB], enhanced behavior with earlier SQL Server versions
ms.assetid: 96976bac-018c-47cc-b1b2-fa9605eb55e5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bc810ced25733ce77d80c7bec38b03e3aaf3753a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 02/08/2020
ms.locfileid: "63233079"
---
# <a name="new-date-and-time-features-with-previous-sql-server-versions-ole-db"></a>Nuevas características de fecha y hora con versiones de SQL Server anteriores (OLE DB)
  En este tema se describe el comportamiento esperado cuando una aplicación cliente que usa las características mejoradas de fecha y hora se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] comunica con [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]una versión de anterior a, y cuando un cliente [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] compilado con una versión [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] de Native Client anterior a envía comandos a un servidor que admite características mejoradas de fecha y hora.  
  
## <a name="down-level-client-behavior"></a>Comportamiento del cliente de nivel inferior  
 Las aplicaciones cliente que usan una versión [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de Native Client anterior [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] a ven los nuevos tipos de fecha y `nvarchar` hora como columnas. El contenido de las columnas son representaciones de literales. Para obtener más información, vea la sección "formatos de datos: cadenas y literales" de [compatibilidad con tipos de datos para obtener OLE DB mejoras de fecha y hora](data-type-support-for-ole-db-date-and-time-improvements.md). El tamaño de columna es la longitud máxima del literal para la precisión especificada para la columna.  
  
 Las API de catálogo devolverán metadatos coherentes con el código del tipo de datos de nivel inferior que se devuelve al cliente (por ejemplo, `nvarchar`) y la representación asociada de nivel inferior (por ejemplo, el formato de literal adecuado). Sin embargo, el nombre del tipo de datos devuelto será el nombre del tipo real de [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)].  
  
 Cuando una aplicación cliente de nivel inferior se ejecuta en [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] un servidor (o posterior) en el que se han realizado cambios de esquema en los tipos de fecha y hora, el comportamiento esperado es el siguiente:  
  
|Tipo de cliente OLE DB|Tipo de SQL Server 2005|SQL Server tipo 2008 (o posterior)|Conversión del resultado (servidor a cliente)|Conversión de parámetros (cliente a servidor)|  
|------------------------|--------------------------|---------------------------------------|--------------------------------------------|-----------------------------------------------|  
|DBTYPE_DBDATE|Datetime|Date|Aceptar|Aceptar|  
|DBTYPE_DBTIMESTAMP|||Los campos de hora se establecen en cero.|Se producirá un error en IRowsetChange debido al truncamiento de la cadena si el campo de hora es distinto de cero.|  
|DBTYPE_DBTIME||Time(0)|Aceptar|Aceptar|  
|DBTYPE_DBTIMESTAMP|||Los campos de fecha se establecen en la fecha actual.|Se producirá un error en IRowsetChange debido al truncamiento de la cadena si las fracciones de segundo son distintas de cero.<br /><br /> Se omite la fecha.|  
|DBTYPE_DBTIME||Time(7)|Error: literal de hora no válido.|Aceptar|  
|DBTYPE_DBTIMESTAMP|||Error: literal de hora no válido.|Aceptar|  
|DBTYPE_DBTIMESTAMP||Datetime2 (3)|Aceptar|Aceptar|  
|DBTYPE_DBTIMESTAMP||Datetime2 (7)|Aceptar|Aceptar|  
|DBTYPE_DBDATE|Smalldatetime|Date|Aceptar|Aceptar|  
|DBTYPE_DBTIMESTAMP|||Los campos de hora se establecen en cero.|Se producirá un error en IRowsetChange debido al truncamiento de la cadena si el campo de hora es distinto de cero.|  
|DBTYPE_DBTIME||Time(0)|Aceptar|Aceptar|  
|DBTYPE_DBTIMESTAMP|||Los campos de fecha se establecen en la fecha actual.|Se producirá un error en IRowsetChange debido al truncamiento de la cadena si las fracciones de segundo son distintas de cero.<br /><br /> Se omite la fecha.|  
|DBTYPE_DBTIMESTAMP||Datetime2(0)|Aceptar|Aceptar|  
  
 OK significa que si ha funcionado con [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], también debería funcionar con [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] o posterior.  
  
 Solo se han considerado los siguientes cambios de esquema:  
  
-   Usar un nuevo tipo donde de forma lógica una aplicación requiere un único valor de fecha u hora. Sin embargo, se ha forzado a la aplicación a usar `datetime` o `smalldatetime` porque no había disponibles tipos de fecha y hora independientes.  
  
-   Usar un nuevo tipo para obtener más precisión o exactitud en fracciones de segundo.  
  
-   Cambio a `datetime2` porque se trata del tipo de datos preferido para la fecha y hora.  
  
 Las aplicaciones que utilizan metadatos de servidor obtenidos a través de ICommandWithParameters:: GetParameterInfo o conjuntos de filas de esquema para establecer la información de tipo de parámetro mediante ICommandWithParameters:: SetParameterInfo producirán errores durante las conversiones de cliente donde la cadena la representación de un tipo de origen es mayor que la representación de cadena del tipo de destino. Por ejemplo, si un enlace de cliente utiliza DBTYPE_DBTIMESTAMP y la columna Server es Date [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , Native Client convertirá el valor a "YYYY-dd-mm HH: mm: SS. fff", pero los metadatos del servidor `nvarchar(10)`se devolverán como. El desbordamiento resultante produce DBSTATUS_E_CATCONVERTVALUE. Se producen problemas similares con las conversiones de datos de IRowsetChange, ya que los metadatos del conjunto de filas se establecen a partir de los metadatos del conjunto de resultados.  
  
### <a name="parameter-and-rowset-metadata"></a>Parámetros y metadatos de conjuntos de filas  
 En esta sección se describen los metadatos de los parámetros, las columnas de resultados y los conjuntos de filas de esquema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para los clientes que [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]se compilan con una versión de Native Client anterior a.  
  
#### <a name="icommandwithparametersgetparameterinfo"></a>ICommandWithParameters::GetParameterInfo  
 La estructura DBPARAMINFO devuelve la siguiente información a través del parámetro *prgParamInfo* :  
  
|Tipo de parámetro|wType|ulParamSize|bPrecision|bScale|  
|--------------------|-----------|-----------------|----------------|------------|  
|date|DBTYPE_WSTR|10|~0|~0|  
|time|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19, 21.. 27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26, 28.. 34|~0|~0|  
  
 Observe que algunos de estos intervalos de valores no son continuos; por ejemplo, en el intervalo 8,10..16 falta el 9. Esto se debe a la adición de un separador decimal cuando la precisión fraccionaria es mayor que cero.  
  
#### <a name="icolumnsrowsetgetcolumnsrowset"></a>IColumnsRowset::GetColumnsRowset  
 Se devuelven las siguientes columnas:  
  
|Tipo de columna|DBCOLUMN_TYPE|DBCOLUMN_COLUMNSIZE|DBCOLUMN_PRECISION|DBCOLUMN_SCALE, DBCOLUMN_DATETIMEPRECISION|  
|-----------------|--------------------|--------------------------|-------------------------|--------------------------------------------------|  
|date|DBTYPE_WSTR|10|NULL|NULL|  
|time|DBTYPE_WSTR|8, 10..16|NULL|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19, 21.. 27|NULL|NULL|  
|datetimeoffset|DBTYPE_WSTR|26, 28.. 34|NULL|NULL|  
  
#### <a name="columnsinfogetcolumninfo"></a>ColumnsInfo::GetColumnInfo  
 La estructura DBCOLUMNINFO devuelve la siguiente información:  
  
|Tipo de parámetro|wType|ulColumnSize|bPrecision|bScale|  
|--------------------|-----------|------------------|----------------|------------|  
|date|DBTYPE_WSTR|10|~0|~0|  
|time(1..7)|DBTYPE_WSTR|8, 10..16|~0|~0|  
|smalldatetime|DBTYPE_DBTIMESTAMP|16|16|0|  
|datetime|DBTYPE_DBTIMESTAMP|16|23|3|  
|datetime2|DBTYPE_WSTR|19, 21.. 27|~0|~0|  
|datetimeoffset|DBTYPE_WSTR|26, 28.. 34|~0|~0|  
  
### <a name="schema-rowsets"></a>Conjuntos de filas de esquema  
 En esta sección se describen los metadatos para los parámetros, columnas de resultados y conjuntos de filas de esquema de los nuevos tipos de datos. Esta información es útil si tiene un proveedor de cliente desarrollado con herramientas anteriores a [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client.  
  
#### <a name="columns-rowset"></a>Conjunto de filas COLUMNS  
 Para los tipos de fecha y hora se devuelven los siguientes valores de columna:  
  
|Tipo de columna|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|DATETIME_PRECISION|  
|-----------------|----------------|--------------------------------|------------------------------|-------------------------|  
|date|DBTYPE_WSTR|10|20|NULL|  
|time|DBTYPE_WSTR|8, 10..16|16, 20.. 32|NULL|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|0|  
|datetime|DBTYPE_DBTIMESTAMP|NULL|NULL|3|  
|datetime2|DBTYPE_WSTR|19, 21.. 27|38, 42.. 54|NULL|  
|datetimeoffset|DBTYPE_WSTR|26, 28.. 34|52, 56.. 68|NULL|  
  
#### <a name="procedure_parameters-rowset"></a>Conjunto de filas PROCEDURE_PARAMETERS  
 Para los tipos de fecha y hora se devuelven los siguientes valores de columna:  
  
|Tipo de columna|DATA_TYPE|CHARACTER_MAXIMUM_LENGTH|CHARACTER_OCTET_LENGTH|TYPE_NAME<br /><br /> LOCAL_TYPE_NAME|  
|-----------------|----------------|--------------------------------|------------------------------|--------------------------------------|  
|date|DBTYPE_WSTR|10|20|date|  
|time|DBTYPE_WSTR|8, 10..16|16, 20.. 32|time|  
|smalldatetime|DBTYPE_DBTIMESTAMP|NULL|NULL|smalldatetime|  
|datetime|DBTYPE_DBTIMESTAMP|NULL|NULL|datetime|  
|datetime2|DBTYPE_WSTR|19, 21.. 27|38, 42.. 54|datetime2|  
|datetimeoffset|DBTYPE_WSTR|26, 28.. 34|52, 56.. 68|datetimeoffset|  
  
#### <a name="provider_types-rowset"></a>Conjunto de filas PROVIDER_TYPES  
 Para los tipos de fecha y hora se devuelven las siguientes filas:  
  
|Tipo -><br /><br /> Columna|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|--------------------------|----------|----------|-------------------|--------------|---------------|--------------------|  
|TYPE_NAME|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|DATA_TYPE|DBTYPE_WSTR|DBTYPE_WSTR|DBTYPE_DBTIMESTAMP|DBTYPE_DBTIMESTAMP|DBTYPE_WSTR|DBTYPE_WSTR|  
|COLUMN_SIZE|10|16|16|23|27|34|  
|LITERAL_PREFIX|'|'|'|'|'|'|  
|LITERAL_SUFFIX|'|'|'|'|'|'|  
|CREATE_PARAMS|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_NULLABLE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|VARIANT_TRUE|  
|CASE_SENSITIVE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|DB_SEARCHABLE|  
|UNSIGNED_ATTRIBUTE|NULL|NULL|NULL|NULL|NULL|NULL|  
|FIXED_PREC_SCALE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|AUTO_UNIQUE_VALUE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|LOCAL_TYPE_NAME|date|time|smalldatetime|datetime|datetime2|datetimeoffset|  
|MINIMUM_SCALE|NULL|NULL|NULL|NULL|NULL|NULL|  
|MAXIMUM_SCALE|NULL|NULL|NULL|NULL|NULL|NULL|  
|GUID|NULL|NULL|NULL|NULL|NULL|NULL|  
|TYPELIB|NULL|NULL|NULL|NULL|NULL|NULL|  
|VERSION|NULL|NULL|NULL|NULL|NULL|NULL|  
|IS_LONG|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
|BEST_MATCH|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_TRUE|VARIANT_FALSE|VARIANT_FALSE|  
|IS_FIXEDLENGTH|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|VARIANT_FALSE|  
  
## <a name="down-level-server-behavior"></a>Comportamiento de un servidor de nivel inferior  
 Cuando se conecta a un servidor de una versión anterior [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]a, cualquier intento de usar los nuevos nombres de tipo de servidor (por ejemplo, con ICommandWithParameters:: SetParameterInfo o ITableDefinition:: CreateTable) dará como resultado DB_E_BADTYPENAME.  
  
 Si los nuevos tipos se enlazan en parámetros o resultados sin usar un nombre de tipo y el nuevo tipo se usa para especificar implícitamente el tipo de servidor, o no hay ninguna conversión válida del tipo de servidor al tipo de cliente, se devuelve DB_E_ERRORSOCCURRED, y DBBINDSTATUS_UNSUPPORTED_CONVERSION se establece como estado de enlace para el descriptor de acceso que se usó en Execute.  
  
 Si hay una conversión de cliente compatible del tipo de búfer al tipo de servidor para la versión del servidor en la conexión, pueden usarse todos los tipos de búfer del cliente. En este contexto, *tipo de servidor* significa el tipo especificado por ICommandWithParameters:: SetParameterInfo, o implícito por el tipo de búfer si no se ha llamado a ICommandWithParameters:: SetParameterInfo. Esto significa que DBTYPE_DBTIME2 y DBTYPE_DBTIMESTAMPOFFSET pueden usarse con servidores de nivel inferior, o cuando DataTypeCompatibility=80, si la conversión del cliente a un tipo de servidor compatible se realiza correctamente. Es evidente que si el tipo de servidor es incorrecto, el servidor todavía podría notificar un error si no puede realizar una conversión implícita al tipo de servidor real.  
  
## <a name="ssprop_init_datatypecompatibility-behavior"></a>Comportamiento de SSPROP_INIT_DATATYPECOMPATIBILITY  
 Cuando SSPROP_INIT_DATATYPECOMPATIBILITY se establece en SSPROPVAL_DATATYPECOMPATIBILITY_SQL2000, los nuevos tipos de fecha y hora y los metadatos asociados aparecen en los clientes tal y como aparecen en los clientes de nivel inferior, tal y como se describe en [cambios de copia masiva para tipos de fecha y hora mejorados &#40;OLE DB y ODBC&#41;](../native-client-odbc-date-time/bulk-copy-changes-for-enhanced-date-and-time-types-ole-db-and-odbc.md).  
  
## <a name="comparability-for-irowsetfind"></a>Comparaciones en IRowsetFind  
 Se permiten todos los operadores de comparación para los nuevos tipos de fecha y hora, debido a que aparecen como tipos de cadena en lugar de tipos de fecha y hora.  
  
## <a name="see-also"></a>Consulte también  
 [Mejoras de fecha y hora &#40;OLE DB&#41;](date-and-time-improvements-ole-db.md)  
  
  
