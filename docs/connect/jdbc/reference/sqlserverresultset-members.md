---
title: Los miembros de SQLServerResultSet | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 2a438d5d-2d6a-46a0-a2ae-f35fbae4a472
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cf318137b6d3f23a2161de97999df29b7f29ed8b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
ms.locfileid: "32852749"
---
# <a name="sqlserverresultset-members"></a>Miembros SQLServerResultSet
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Las siguientes tablas enumeran los miembros expuestos por el [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) clase.  
  
## <a name="constructors"></a>Constructores  
 Ninguno.  
  
## <a name="fields"></a>Campos  
  
|Nombre|Description|  
|----------|-----------------|  
|[CONCUR_SS_OPTIMISTIC_CC](../../../connect/jdbc/reference/concur-ss-optimistic-cc-field-sqlserverresultset.md)|Se utiliza para especificar un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de simultaneidad optimista con sin bloqueos de fila de lectura/escritura.|  
|[POR CONCUR_SS_OPTIMISTIC_CCVAL](../../../connect/jdbc/reference/concur-ss-optimistic-ccval-field-sqlserverresultset.md)|Se utiliza para especificar un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de simultaneidad optimista con sin bloqueos de fila de lectura/escritura.|  
|[CONCUR_SS_SCROLL_LOCKS](../../../connect/jdbc/reference/concur-ss-scroll-locks-field-sqlserverresultset.md)|Se utiliza para especificar un tipo de simultaneidad optimista de lectura y escritura de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] con bloqueos de fila.|  
|[TYPE_SS_DIRECT_FORWARD_ONLY](../../../connect/jdbc/reference/type-ss-direct-forward-only-field-sqlserverresultset.md)|Se utiliza para especificar un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de cursor de solo avance rápido, de sólo lectura.|  
|[TYPE_SS_SCROLL_DYNAMIC](../../../connect/jdbc/reference/type-ss-scroll-dynamic-field-sqlserverresultset.md)|Se utiliza para especificar un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de cursor dinámico.|  
|[TYPE_SS_SCROLL_KEYSET](../../../connect/jdbc/reference/type-ss-scroll-keyset-field-sqlserverresultset.md)|Se utiliza para especificar un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de cursor de conjunto de claves.|  
|[TYPE_SS_SCROLL_STATIC](../../../connect/jdbc/reference/type-ss-scroll-static-field-sqlserverresultset.md)|Se utiliza para especificar un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de cursor estático.|  
|[TYPE_SS_SERVER_CURSOR_FORWARD_ONLY](../../../connect/jdbc/reference/type-ss-server-cursor-forward-only-field-sqlserverresultset.md)|Se utiliza para especificar un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] tipo de cursor de solo avance rápido, de sólo lectura.|  
  
## <a name="inherited-fields"></a>Campos heredados  
  
|Clase heredada de:|Description|  
|---------------------------|-----------------|  
|java.sql.ResultSet|CLOSE_CURSORS_AT_COMMIT, CONCUR_READ_ONLY, CONCUR_UPDATABLE, FETCH_FORWARD, FETCH_REVERSE, FETCH_UNKNOWN, HOLD_CURSORS_OVER_COMMIT, TYPE_FORWARD_ONLY, TYPE_SCROLL_INSENSITIVE, TYPE_SCROLL_SENSITIVE|  
  
## <a name="methods"></a>Métodos  
  
|Nombre|Description|  
|----------|-----------------|  
|[Absoluta](../../../connect/jdbc/reference/absolute-method-sqlserverresultset.md)|Mueve el cursor a la fila especificada en este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[afterLast](../../../connect/jdbc/reference/afterlast-method-sqlserverresultset.md)|Mueve el cursor hasta después de la última fila de esta [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[beforeFirst](../../../connect/jdbc/reference/beforefirst-method-sqlserverresultset.md)|Mueve el cursor a antes de la primera fila de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[cancelRowUpdates](../../../connect/jdbc/reference/cancelrowupdates-method-sqlserverresultset.md)|Cancela las actualizaciones realizadas en la fila actual en este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverresultset.md)|Borra todas las advertencias emitidas en el objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[Cerrar](../../../connect/jdbc/reference/close-method-sqlserverresultset.md)|Esto libera [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) del objeto base de datos y recursos de JDBC inmediatamente en lugar de esperar para que esto suceda cuando se cierra automáticamente.|  
|[deleteRow](../../../connect/jdbc/reference/deleterow-method-sqlserverresultset.md)|Elimina la fila actual de este[SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto y de la base de datos subyacente.|  
|[Finalizar](../../../connect/jdbc/reference/finalize-method-sqlserverresultset.md)|Esto cierra explícitamente [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[findColumn](../../../connect/jdbc/reference/findcolumn-method-sqlserverresultset.md)|Recupera el índice de la primera columna de búsqueda de coincidencias para el nombre de columna especificado en este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[first](../../../connect/jdbc/reference/first-method-sqlserverresultset.md)|Mueve el cursor a la primera fila de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[getArray](../../../connect/jdbc/reference/getarray-method-sqlserverresultset.md)|Recupera el valor de la columna designada en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un objeto de matriz.|  
|[getAsciiStream](../../../connect/jdbc/reference/getasciistream-method-sqlserverresultset.md)|Recupera el valor de la columna designada en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como una secuencia de caracteres ASCII.|  
|[getBigDecimal](../../../connect/jdbc/reference/getbigdecimal-method-sqlserverresultset.md)|Recupera el valor del índice de columna designado en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como java.math.BigDecimal.|  
|[getBinaryStream](../../../connect/jdbc/reference/getbinarystream-method-sqlserverresultset.md)|Recupera el valor de la columna designada en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como una secuencia binaria de bytes no interpretados.|  
|[GetBlob](../../../connect/jdbc/reference/getblob-method-sqlserverresultset.md)|Recupera el valor de la columna designada en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un objeto Blob en el lenguaje de programación Java.|  
|[GetBoolean](../../../connect/jdbc/reference/getboolean-method-sqlserverresultset.md)|Recupera el valor de la columna designada en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un **booleano** en el lenguaje de programación Java.|  
|[GetByte](../../../connect/jdbc/reference/getbyte-method-sqlserverresultset.md)|Recupera el valor de la columna designada en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un **bytes** en el lenguaje de programación Java.|  
|[GetBytes](../../../connect/jdbc/reference/getbytes-method-sqlserverresultset.md)|Recupera el valor de la columna designada en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un **bytes** matriz en el lenguaje de programación Java.|  
|[getCharacterStream](../../../connect/jdbc/reference/getcharacterstream-method-sqlserverresultset.md)|Recupera el valor de la columna designada en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un objeto java.io.Reader.|  
|[getClob](../../../connect/jdbc/reference/getclob-method-sqlserverresultset.md)|Recupera el valor de la columna designada en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un objeto Clob en el lenguaje de programación Java.|  
|[getConcurrency](../../../connect/jdbc/reference/getconcurrency-method-sqlserverresultset.md)|Recupera el modo de simultaneidad de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[getCursorName](../../../connect/jdbc/reference/getcursorname-method-sqlserverresultset.md)|Recupera el nombre del cursor SQL utilizado por este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[getDate](../../../connect/jdbc/reference/getdate-method-sqlserverresultset.md)|Recupera el valor de la columna designada en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un objeto java.sql.Date en el lenguaje de programación Java.|  
|[getDateTimeOffset](../../../connect/jdbc/reference/getdatetimeoffset-sqlserverresultset.md)|Recupera el valor de la columna especificada como un[clase DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) objeto.|  
|[GetDouble](../../../connect/jdbc/reference/getdouble-method-sqlserverresultset.md)|Recupera el valor de la columna designada en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un **doble** en el lenguaje de programación Java.|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverresultset.md)|Recupera la dirección de la captura para este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverresultset.md)|Recupera el tamaño de captura para este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[GetFloat](../../../connect/jdbc/reference/getfloat-method-sqlserverresultset.md)|Recupera el valor de la columna designada en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un **float** en el lenguaje de programación Java.|  
|[getHoldability](../../../connect/jdbc/reference/getholdability-method-sqlserverresultset.md)|Recupera la capacidad de alojamiento de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[getInt](../../../connect/jdbc/reference/getint-method-sqlserverresultset.md)|Recupera el valor de la columna designada en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un **int** en el lenguaje de programación Java.|  
|[getLong](../../../connect/jdbc/reference/getlong-method-sqlserverresultset.md)|Recupera el valor de la columna designada en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un **largo** en el lenguaje de programación Java.|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverresultset.md)|Recupera el número, tipos y propiedades de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) columnas del objeto.|  
|[getNCharacterStream](../../../connect/jdbc/reference/getncharacterstream-method-sqlserverresultset.md)|Recupera el valor de la columna designada en la fila actual de la [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un objeto de lector.|  
|[getNClob](../../../connect/jdbc/reference/getnclob-method-sqlserverresultset.md)|Recupera el valor de la columna designada en la fila actual de la [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)objeto como un **NClob** objeto en el lenguaje de programación Java.|  
|[getNString](../../../connect/jdbc/reference/getnstring-method-sqlserverresultset.md)|Recupera el valor de la columna designada en la fila actual de la [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como una cadena en el Java lenguaje de programación.|  
|[GetObject](../../../connect/jdbc/reference/getobject-method-sqlserverresultset.md)|Obtiene el valor de la columna designada en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un objeto en el lenguaje de programación Java.|  
|[getRef](../../../connect/jdbc/reference/getref-method-sqlserverresultset.md)|Recupera el valor de la columna designada en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un objeto de referencia en el lenguaje de programación Java.|  
|[getRow](../../../connect/jdbc/reference/getrow-method-sqlserverresultset.md)|Recupera el número de fila actual.|  
|[getShort](../../../connect/jdbc/reference/getshort-method-sqlserverresultset.md)|Recupera el valor de la columna designada en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un **breve** en el lenguaje de programación Java.|  
|[getStatement](../../../connect/jdbc/reference/getstatement-method-sqlserverresultset.md)|Recupera el [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto que generó este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[GetString](../../../connect/jdbc/reference/getstring-method-sqlserverresultset.md)|Recupera el valor de la columna designada en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un **cadena** en el lenguaje de programación Java.|  
|[getSQLXML](../../../connect/jdbc/reference/getsqlxml-method-sqlserverresultset.md)|Recupera el valor de la columna designada en la fila actual de la [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un **SQLXML** objeto.|  
|[getTime](../../../connect/jdbc/reference/gettime-method-sqlserverresultset.md)|Recupera el valor de la columna designada en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un objeto java.sql.Time en el lenguaje de programación Java.|  
|[getTimestamp](../../../connect/jdbc/reference/gettimestamp-method-sqlserverresultset.md)|Recupera el valor de la columna designada en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un objeto java.sql.Timestamp en el lenguaje de programación Java.|  
|[GetType](../../../connect/jdbc/reference/gettype-method-sqlserverresultset.md)|Recupera el tipo de cursor de [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[getUnicodeStream](../../../connect/jdbc/reference/getunicodestream-method-sqlserverresultset.md)|Recupera el valor de la columna designada en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como una secuencia de caracteres Unicode.|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverresultset.md)|Recupera el valor de la columna designada en la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto como un objeto de dirección URL.|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverresultset.md)|Recupera la primera advertencia que notifican las llamadas en el objeto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[insertRow](../../../connect/jdbc/reference/insertrow-method-sqlserverresultset.md)|Inserta el contenido de la fila de inserción en esto [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto y en la base de datos.|  
|[isAfterLast](../../../connect/jdbc/reference/isafterlast-method-sqlserverresultset.md)|Recupera si el cursor está después de la última fila en esta [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[isBeforeFirst](../../../connect/jdbc/reference/isbeforefirst-method-sqlserverresultset.md)|Recupera si el cursor está antes de la primera fila en esta [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[IsClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverresultset.md)|Indica si este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto se ha cerrado.|  
|[isFirst](../../../connect/jdbc/reference/isfirst-method-sqlserverresultset.md)|Recupera si el cursor está en la primera fila de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[isLast](../../../connect/jdbc/reference/islast-method-sqlserverresultset.md)|Recupera si el cursor está en la última fila de esta [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[último](../../../connect/jdbc/reference/last-method-sqlserverresultset.md)|Mueve el cursor a la última fila en esta [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[moveToCurrentRow](../../../connect/jdbc/reference/movetocurrentrow-method-sqlserverresultset.md)|Mueve el cursor a la posición del cursor guardados, normalmente la fila actual.|  
|[moveToInsertRow](../../../connect/jdbc/reference/movetoinsertrow-method-sqlserverresultset.md)|Mueve el cursor a la fila de inserción.|  
|[Siguiente](../../../connect/jdbc/reference/next-method-sqlserverresultset.md)|Mueve el cursor una fila hacia abajo desde su posición actual.|  
|[anterior](../../../connect/jdbc/reference/previous-method-sqlserverresultset.md)|Mueve el cursor a la fila anterior en este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[refreshRow](../../../connect/jdbc/reference/refreshrow-method-sqlserverresultset.md)|Actualiza la fila actual con el valor más reciente en la base de datos.|  
|[relative](../../../connect/jdbc/reference/relative-method-sqlserverresultset.md)|Mueve el cursor a la cantidad dada de filas, con respecto a la fila actual, positivo o una dirección negativa.|  
|[RowDeleted](../../../connect/jdbc/reference/rowdeleted-method-sqlserverresultset.md)|Recupera si se ha eliminado una fila.|  
|[rowInserted](../../../connect/jdbc/reference/rowinserted-method-sqlserverresultset.md)|Recupera si la fila actual ha tenido una inserción.|  
|[RowUpdated](../../../connect/jdbc/reference/rowupdated-method-sqlserverresultset.md)|Recupera si se ha actualizado la fila actual.|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverresultset.md)|Ofrece una sugerencia sobre la dirección en la que las filas en esta [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) se procesará el objeto.|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverresultset.md)|Ofrece el controlador JDBC una sugerencia sobre el número de filas que se debe capturar desde la base de datos cuando se necesitan más filas para este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[updateArray](../../../connect/jdbc/reference/updatearray-method-sqlserverresultset.md)|Actualiza la columna designada con un objeto de matriz.|  
|[updateAsciiStream](../../../connect/jdbc/reference/updateasciistream-method-sqlserverresultset.md)|Actualiza la columna designada con un valor de flujo ASCII.|  
|[updateBigDecimal](../../../connect/jdbc/reference/updatebigdecimal-method-sqlserverresultset.md)|Actualiza la columna designada con un objeto BigDecimal.|  
|[updateBinaryStream](../../../connect/jdbc/reference/updatebinarystream-method-sqlserverresultset.md)|Actualiza la columna designada con un valor de flujo binario.|  
|[updateBlob](../../../connect/jdbc/reference/updateblob-method-sqlserverresultset.md)|Actualiza la columna designada con un valor java.sql.Blob.|  
|[updateBoolean](../../../connect/jdbc/reference/updateboolean-method-sqlserverresultset.md)|Actualiza la columna designada con un **booleano** valor.|  
|[updateByte](../../../connect/jdbc/reference/updatebyte-method-sqlserverresultset.md)|Actualiza la columna designada con un **bytes** valor.|  
|[updateBytes](../../../connect/jdbc/reference/updatebytes-method-sqlserverresultset.md)|Actualiza la columna designada con una matriz de **bytes** valores.|  
|[updateCharacterStream](../../../connect/jdbc/reference/updatecharacterstream-method-sqlserverresultset.md)|Actualiza la columna designada con un valor de flujo de caracteres.|  
|[updateClob](../../../connect/jdbc/reference/updateclob-method-sqlserverresultset.md)|Actualiza la columna designada con un valor java.sql.Clob.|  
|[updateDate](../../../connect/jdbc/reference/updatedate-method-sqlserverresultset.md)|Actualiza la columna designada con un valor de fecha.|  
|[updateDateTimeOffset](../../../connect/jdbc/reference/updatedatetimeoffset-sqlserverresultset.md)|Las actualizaciones de un [clase DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) columna.|  
|[updateDouble](../../../connect/jdbc/reference/updatedouble-method-sqlserverresultset.md)|Actualiza la columna designada con un **doble** valor.|  
|[updateFloat](../../../connect/jdbc/reference/updatefloat-method-sqlserverresultset.md)|Actualiza la columna designada con un **float** valor.|  
|[updateInt](../../../connect/jdbc/reference/updateint-method-sqlserverresultset.md)|Actualiza la columna designada con un **int** valor.|  
|[updateLong](../../../connect/jdbc/reference/updatelong-method-sqlserverresultset.md)|Actualiza la columna designada con un **largo** valor.|  
|[updateNCharacterStream](../../../connect/jdbc/reference/updatencharacterstream-method-sqlserverresultset.md)|Actualiza la columna designada con un valor de flujo de caracteres.|  
|[updateNClob](../../../connect/jdbc/reference/updatenclob-method-sqlserverresultset.md)|Actualiza la columna designada con el valor de objeto especificado.|  
|[updateNString](../../../connect/jdbc/reference/updatenstring-method-sqlserverresultset.md)|Actualiza la columna designada con un **cadena** valor.|  
|[updateNull](../../../connect/jdbc/reference/updatenull-method-sqlserverresultset.md)|Actualiza la columna designada con un valor NULL.|  
|[updateObject](../../../connect/jdbc/reference/updateobject-method-sqlserverresultset.md)|Actualiza la columna designada con un **objeto** valor.|  
|[updateRef](../../../connect/jdbc/reference/updateref-method-sqlserverresultset.md)|Actualiza la columna designada con un valor java.sql.Ref.|  
|[updateRow](../../../connect/jdbc/reference/updaterow-method-sqlserverresultset.md)|Actualiza la base de datos subyacente con el nuevo contenido de la fila actual de este [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[updateShort](../../../connect/jdbc/reference/updateshort-method-sqlserverresultset.md)|Actualiza la columna designada con un **corto** valor.|  
|[updateString](../../../connect/jdbc/reference/updatestring-method-sqlserverresultset.md)|Actualiza la columna designada con un **cadena** valor.|  
|[updateSQLXML](../../../connect/jdbc/reference/updatesqlxml-method-sqlserverresultset.md)|Actualiza la columna designada con un **SQLXML** valor.|  
|[updateTime](../../../connect/jdbc/reference/updatetime-method-sqlserverresultset.md)|Actualiza la columna designada con un valor de hora.|  
|[updateTimestamp](../../../connect/jdbc/reference/updatetimestamp-method-sqlserverresultset.md)|Actualiza la columna designada con un valor de marca de tiempo.|  
|[wasNull](../../../connect/jdbc/reference/wasnull-method-sqlserverresultset.md)|Comprueba si el último valor leído era un valor null.|  
  
## <a name="inherited-methods"></a>Métodos heredados  
  
|Clase heredada de:|Métodos|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>Vea también  
 [Clase SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md)  
  
  
