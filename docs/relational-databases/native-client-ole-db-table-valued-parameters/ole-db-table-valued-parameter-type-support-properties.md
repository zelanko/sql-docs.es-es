---
title: Compatibilidad con tipos de parámetros con valores de tabla de OLE DB (propiedades) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- table-valued parameters (OLE DB), API support (properties)
ms.assetid: b9c4e6ed-fe4f-4ef8-9bc8-784d80d44039
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017'
ms.openlocfilehash: b56c59bd6a12c01cb16101b42d7b5a51ea8ad4da
ms.sourcegitcommit: 4cd008a77f456b35204989bbdd31db352716bbe6
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/06/2018
ms.locfileid: "39556435"
---
# <a name="ole-db-table-valued-parameter-type-support-properties"></a>Compatibilidad con tipos de parámetros con valores de tabla de OLE DB (propiedades)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  En este tema se proporciona información sobre las propiedades de OLE DB y los conjuntos de propiedades asociados a los objetos de conjunto de filas de parámetro con valores de tabla.  
  
## <a name="properties"></a>Propiedades  
 A continuación, se muestra la lista de propiedades expuestas mediante el método IRowsetInfo::GetPropeties en los objetos de conjunto de filas de parámetro con valores de tabla. Observe que todas las propiedades de conjunto de filas de parámetro con valores de tabla son de solo lectura. Por lo tanto, intenta establecer cualquiera de las propiedades mediante IOpenRowset:: OpenRowset o ITableDefinitionWithConstraints::CreateTableWithConstraints métodos en sus valores no predeterminados se producirá un error y no se creará ningún objeto.  
  
 No se enumeran aquí las propiedades no implementadas en el objeto de conjunto de filas de parámetro con valores. Para obtener una lista completa de las propiedades, vea la documentación de OLE DB en Data Access Components para Windows.  
  
|Id. de propiedad|Valor|  
|-----------------|-----------|  
|DBPROP_ABORTPRESERVE|VARIANT_TRUE|  
|DBPROP_ACCESSORDER|DBPROPVAL_AO_RANDOM|  
|DBPROP_BLOCKINGSTORAGEOBJECTS|VARIANT_TRUE|  
|DBPROP_BOOKMARKS<br /><br /> DBPROP_LITERALBOOKMARKS|L/E: solo lectura<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Descripción: no se permiten marcadores en los objetos de conjunto de filas de parámetro con valores de tabla.|  
|DBPROP_BOOKMARKSKIPPED|VARIANT_FALSE|  
|DBPROP_BOOKMARKTYPE|DBPROPVAL_BMK_NUMERIC|  
|DBPROP_CANHOLDROWS|VARIANT_FALSE|  
|DBPROP_CHANGEINSERTEDROWS|VARIANT_TRUE|  
|DBPROP_COLUMNRESTRICT|VARIANT_FALSE|  
|DBPROP_COMMANDTIMEOUT|0|  
|DBPROP_COMMITPRESERVE|VARIANT_TRUE|  
|DBPROP_DEFERRED|VARIANT_FALSE|  
|DBPROP_DELAYSTORAGEOBJECTS|VARIANT_FALSE|  
|DBPROP_IAccessor<br /><br /> DBPROP_IColumnsInfo<br /><br /> DBPROP_IConvertType<br /><br /> DBPROP_IRowset<br /><br /> DBPROP_IRowsetInfo<br /><br /> DBPROP_IColumnsRowset|VARIANT_TRUE|  
|DBPROP_IConnectionPointContainer<br /><br /> DBPROP_IMultipleResults<br /><br /> DBPROP_IRowsetUpdate<br /><br /> DBPROP_IRowsetIdentity<br /><br /> DBPROP_IRowsetLocate<br /><br /> DBPROP_IRowsetScroll<br /><br /> DBPROP_IRowsetResynch|VARIANT_FALSE|  
|DBPROP_IRowsetChange|VARIANT_TRUE<br /><br /> Nota: El objeto de conjunto de filas de parámetro con valores de tabla admite las interfaces IRowsetChange.<br /><br /> Los conjuntos de filas creados utilizando DBPROP_IRowsetChange igual a VARIANT_TRUE exhiben los comportamientos de modo de actualización inmediatos.<br /><br /> Pero, si las columnas BLOB se enlazan como objetos ISequentialStream, se espera que el consumidor las mantenga mientras exista el objeto de conjunto de filas de parámetro con valores de tabla.|  
|DBPROP_ISupportErrorInfo|VARIANT_TRUE|  
|DBPROP_ISequentialStream|VARIANT_TRUE|  
|DBPROP_IMMOBILEROWS|VARIANT_TRUE|  
|DBPROP_LITERALIDENTITY|VARIANT_TRUE|  
|DBPROP_LOCKMODE|DBPROPVAL_LM_NONE|  
|DBPROP_MAXOPENROWS|0|  
|DBPROP_MAXPENDINGROWS|0|  
|DBPROP_MAXROWS|0|  
|DBPROP_NOTIFICATIONPHASES|0|  
|DBPROP_NOTIFYCOLUMNSET DBPROP_NOTIFYROWDELETE DBPROP_NOTIFYROWFIRSTCHANGE DBPROP_NOTIFYROWINSERT DBPROP_NOTIFYROWRESYNCH DBPROP_NOTIFYROWSETRELEASE DBPROP_NOTIFYROWSETFETCH-POSITIONCHANGE DBPROP_NOTIFYROWUNDOCHANGE DBPROP_NOTIFYROWUNDODELETE DBPROP_NOTIFYROWUNDOINSERT DBPROP_NOTIFYROWUPDATE|0|  
|DBPROP_OTHERINSERT DBPROP_OTHERUPDATEDELETE|VARIANT_FALSE|  
|DBPROP_OWNINSERT<br /><br /> DBPROP_OWNUPDATEDELETE|VARIANT_TRUE|  
|DBPROP_QUICKRESTART|VARIANT_TRUE|  
|DBPROP_REENTRANTEVENTS|VARIANT_FALSE|  
|DBPROP_REMOVEDELETED|VARIANT_TRUE|  
|DBPROP_RETURNPENDINGINSERTS|VARIANT_TRUE|  
|DBPROP_ROWRESTRICT|VARIANT_FALSE|  
|DBPROP_ROWTHREADMODEL|DBPROPVAL_RT_FREETHREAD|  
|DBPROP_SERVERCURSOR|VARIANT_FALSE|  
|DBPROP_SERVERDATAONINSERT|VARIANT_FALSE|  
|DBPROP_STRONGIDENTITY|VARIANT_TRUE|  
|DBPROP_TRANSACTEDOBJECT|VARIANT_FALSE|  
|DBPROP_UNIQUEROWS|VARIANT_FALSE|  
|DBPROP_UPDATABILITY|LAS PROPIEDADES DBPROPVAL_UP_CHANGE &AMP;#124; DBPROPVAL_UP_DELETE &AMP;#124; DBPROPVAL_UP_INSERT|  
  
## <a name="property-sets"></a>Conjuntos de propiedades  
 La propiedad siguiente establece los parámetros con valores de tabla admitidos.  
  
### <a name="dbpropsetsqlservercolumn"></a>DBPROPSET_SQLSERVERCOLUMN  
 Esta propiedad se utiliza por el consumidor en el proceso de creación de un objeto de conjunto de filas de parámetro con valores de tabla mediante el uso de ITableDefinitionWithConstraints::CreateTableWithConstraints para cada columna a través de la estructura DBCOLUMNDESC, si es necesario.  
  
|Id. de propiedad|Valor de la propiedad|  
|-----------------|--------------------|  
|SSPROP_COL_COMPUTED|L/E: de lectura/escritura<br /><br /> Valor predeterminado: VARIANT_FALSE<br /><br /> Tipo: VT_BOOL<br /><br /> Descripción: cuando se establece en VARIANT_TRUE, indica que la columna es calculada. VARIANT_FALSE indica que no es una columna calculada.|  
  
### <a name="dbpropsetsqlserverparameter"></a>DBPROPSET_SQLSERVERPARAMETER  
 Estas propiedades son leídas por el consumidor al detectar la información de tipo de parámetro con valores de tabla en las llamadas a ISSCommandWithParamters::GetParameterProperties y establecidas por el usuario al establecer las propiedades concretas sobre el parámetro con valores de tabla a través de isscommandwithparameters:: SetParameterProperties.  
  
 En la tabla siguiente se proporcionan descripciones detalladas de estas propiedades.  
  
|Id. de propiedad|Valor de la propiedad|  
|-----------------|--------------------|  
|SSPROP_PARAM_TYPE_TYPENAME|L/E: de lectura/escritura<br /><br /> Valor predeterminado: VT_EMPTY<br /><br /> Tipo: VT_BSTR<br /><br /> Descripción: los consumidores utilizan esta propiedad para obtener o establecer el nombre del tipo de parámetro con valores de tabla.<br /><br /> Esta propiedad se puede utilizar también con tipos definidos por el usuario CLR.<br /><br /> Esta propiedad se puede especificar opcionalmente para proporcionar un nombre de tipo de tabla para un parámetro con valores de tabla (en caso del comando de sintaxis de llamada ODBC). Esta propiedad es necesaria para las consultas SQL parametrizadas ad hoc.|  
|SSPROP_PARAM_TYPE_SCHEMANAME|L/E: de lectura/escritura<br /><br /> Valor predeterminado: VT_EMPTY<br /><br /> Tipo: VT_BSTR<br /><br /> Descripción: los consumidores utilizan esta propiedad para obtener o establecer el nombre de esquema del tipo de parámetro con valores de tabla.<br /><br /> Esta propiedad se puede utilizar también con tipos definidos por el usuario CLR.|  
|SSPROP_PARAM_TYPE_CATALOGNAME|L/E: de solo lectura<br /><br /> Valor predeterminado: VT_EMPTY<br /><br /> Tipo: VT_BSTR<br /><br /> Descripción: los consumidores utilizan esta propiedad para obtener el nombre de catálogo del tipo de parámetro con valores de tabla.<br /><br /> Esta propiedad se puede utilizar también con tipos definidos por el usuario CLR. Es un error establecer esta propiedad; los tipos de tabla definidos por el usuario deben estar en la misma base de datos que los parámetros con valores de tabla que los usan.|  
|SSPROP_PARAM_TABLE_DEFAULT_COLUMNS|L/E: de lectura/escritura<br /><br /> Valor predeterminado: VT_EMPTY<br /><br /> Tipo: VT_UI2 &#124; VT_ARRAY<br /><br /> Descripción: los consumidores usan esta propiedad para especificar qué conjunto de columnas del conjunto de filas será tratado como valores predeterminados. No se enviará ningún valor para esas columnas. Al capturar datos del objeto de conjunto de filas del consumidor, el proveedor no requiere un enlace para tales columnas.<br /><br /> Todos los elementos de la matriz deben ser ordinales de columnas del objeto de conjunto de filas. Los ordinales no válidos producirán errores durante la ejecución del comando.|  
|SSPROP_PARAM_TABLE_COLUMN_ORDER|L/E: de lectura/escritura<br /><br /> Valor predeterminado: VT_EMPTY<br /><br /> Tipo: VT_UI2 &#124; VT_ARRAY<br /><br /> Descripción: el consumidor utiliza esta propiedad para proporcionar una sugerencia al servidor que indica el orden de clasificación de los datos de columna. El proveedor no realiza ninguna validación y asume que el consumidor se ajusta a la especificación que se proporcionó. El servidor usa esta propiedad para realizar las optimizaciones.<br /><br /> La información de orden de las columnas para cada columna se representa mediante un par de elementos de la matriz. El primer elemento del par es el número de la columna. El segundo elemento del par será 1 para el orden ascendente o 2 para el orden descendente.|  
  
## <a name="see-also"></a>Vea también  
 [Compatibilidad con tipos de parámetros con valores de tabla de OLE DB](../../relational-databases/native-client-ole-db-table-valued-parameters/ole-db-table-valued-parameter-type-support.md)   
 [Usar parámetros con valores de tabla &#40;OLE DB&#41;](../../relational-databases/native-client-ole-db-how-to/use-table-valued-parameters-ole-db.md)  
  
  
