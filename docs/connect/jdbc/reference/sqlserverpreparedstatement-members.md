---
title: Miembros de SQLServerPreparedStatement | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 2363902f-d4c6-4cd4-a5fc-86079eb9e418
caps.latest.revision: 38
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 89955e45eacf8c4b9331276706bcbebbe6ab9948
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverpreparedstatement-members"></a>Miembros de SQLServerPreparedStatement
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Las siguientes tablas enumeran los miembros expuestos por el [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) clase.  
  
## <a name="constructors"></a>Constructores  
 Ninguno.  
  
## <a name="fields"></a>Campos  
 Ninguno.  
  
## <a name="inherited-fields"></a>Campos heredados  
  
|Clase heredada de:|Métodos|  
|---------------------------|-------------|  
|java.sql.Statement|CLOSE_ALL_RESULTS, CLOSE_CURRENT_RESULT, EXECUTE_FAILED, KEEP_CURRENT_RESULT, NO_GENERATED_KEYS, RETURN_GENERATED_KEYS, SUCCESS_NO_INFO|  
  
## <a name="methods"></a>Métodos  
  
|Nombre|Description|  
|----------|-----------------|  
|[addBatch](../../../connect/jdbc/reference/addbatch-method-sqlserverpreparedstatement.md)|Agrega un conjunto de parámetros al lote de comandos para este objeto de instrucción.|  
|[Cancelar](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Cancela la instrucción SQL que se esté ejecutando este objeto de instrucción.|  
|[clearBatch](../../../connect/jdbc/reference/clearbatch-method-sqlserverpreparedstatement.md)|Vacía la lista actual de comandos SQL para este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[clearParameters](../../../connect/jdbc/reference/clearparameters-method-sqlserverpreparedstatement.md)|Borra inmediatamente los valores de parámetro actuales.|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Borra todas las advertencias que se notifican en este objeto de instrucción.|  
|[Cerrar](../../../connect/jdbc/reference/close-method-sqlserverpreparedstatement.md)|Libera la base de datos y los recursos de JDBC de este objeto de instrucción inmediatamente en lugar de esperar a que se liberen automáticamente.|  
|[ejecutar](../../../connect/jdbc/reference/execute-method-sqlserverpreparedstatement.md)|Ejecuta la instrucción SQL en este objeto de instrucción, que puede ser cualquier tipo de instrucción SQL.|  
|[executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverpreparedstatement.md)|Envía un lote de comandos a la base de datos para que se ejecute. Si todos los comandos se ejecutan correctamente, devuelve una matriz de recuentos de actualizaciones.|  
|[executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverpreparedstatement.md)|Ejecuta la consulta SQL en este objeto de instrucción y devuelve el [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto generado por la consulta.|  
|[executeUpdate](../../../connect/jdbc/reference/executeupdate-method-sqlserverpreparedstatement.md)|Ejecuta la instrucción SQL en este objeto de instrucción, que debe ser un INSERT de SQL, la instrucción UPDATE, MERGE o DELETE; o una instrucción SQL que no devuelva nada, como una instrucción DDL.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera el [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto que generó este objeto de instrucción.|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera la dirección para capturar las filas de tablas de base de datos es el valor predeterminado para los conjuntos de resultados generado a partir de este objeto de instrucción.|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera el número de filas del conjunto de resultados que es el tamaño de captura predeterminado para el resultado del conjunto de objetos generados a partir de este objeto de instrucción.|  
|[getGeneratedKeys](../../../connect/jdbc/reference/getgeneratedkeys-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera cualquiera clave generada automáticamente que se crea como resultado de ejecutar este objeto de instrucción.|  
|[getMaxFieldSize](../../../connect/jdbc/reference/getmaxfieldsize-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera el número máximo de bytes que se pueden devolver para los caracteres y valores de columna binaria en un [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto generado por este objeto de instrucción.|  
|[getMaxRows](../../../connect/jdbc/reference/getmaxrows-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera el número máximo de filas que un [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto generado por este objeto de instrucción puede contener.|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverpreparedstatement.md)|Recupera un [clase SQLServerResultSetMetaData](../../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) objeto que contiene información acerca de las columnas de la [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto que se devolverá cuando se ejecuta este objeto de instrucción.|  
|[getMoreResults](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Se desplaza al próximo resultado de este objeto de instrucción.|  
|[getParameterMetaData](../../../connect/jdbc/reference/getparametermetadata-method-sqlserverpreparedstatement.md)|Recupera el número, tipos y propiedades de los parámetros para este objeto de instrucción.|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera la respuesta el modo de almacenamiento en búfer para esta [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[getQueryTimeout](../../../connect/jdbc/reference/getquerytimeout-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera el número de segundos que el [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] esperará a que se ejecute este objeto de instrucción.|  
|[getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera el resultado actual como un [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[getResultSetConcurrency](../../../connect/jdbc/reference/getresultsetconcurrency-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera el conjunto de resultados de simultaneidad para [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objetos que haya generado este objeto de instrucción.|  
|[getResultSetHoldability](../../../connect/jdbc/reference/getresultsetholdability-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera el conjunto de resultados capacidad de alojamiento para [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objetos que haya generado este objeto de instrucción.|  
|[getResultSetType](../../../connect/jdbc/reference/getresultsettype-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera el conjunto de resultados tipo para [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objetos que haya generado este objeto de instrucción.|  
|[getUpdateCount](../../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md),) recupera el resultado actual como un recuento de actualización.|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Recupera la primera advertencia que notifica las llamadas en este objeto de instrucción.|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Indica si se ha cerrado este objeto de instrucción.|  
|[isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Devuelve un valor que indica si una instrucción se puede agregar al grupo de instrucciones proporcionado por el usuario.|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverpreparedstatement.md)|Indica si este objeto de instrucción es un contenedor para la interfaz especificada.|  
|[setArray](../../../connect/jdbc/reference/setarray-method-sqlserverpreparedstatement.md)|Establece el número de parámetro designado para el objeto de matriz determinado.|  
|[setAsciiStream](../../../connect/jdbc/reference/setasciistream-method-sqlserverpreparedstatement.md)|Establece el número de parámetro designado para el objeto InputStream determinado.|  
|[setBigDecimal](../../../connect/jdbc/reference/setbigdecimal-method-sqlserverpreparedstatement.md)|Establece el número de parámetro designado para el objeto BigDecimal determinado.|  
|[setBinaryStream](../../../connect/jdbc/reference/setbinarystream-method-sqlserverpreparedstatement.md)|Establece el parámetro designado en el flujo de entrada especificado.|  
|[setBlob](../../../connect/jdbc/reference/setblob-method-sqlserverpreparedstatement.md)|Establece el parámetro designado en el objeto Blob especificado.|  
|[SetBoolean](../../../connect/jdbc/reference/setboolean-method-sqlserverpreparedstatement.md)|Establece el parámetro designado para especificado **booleano** valor.|  
|[setByte](../../../connect/jdbc/reference/setbyte-method-sqlserverpreparedstatement.md)|Establece el parámetro designado para especificado **bytes** valor.|  
|[setBytes](../../../connect/jdbc/reference/setbytes-method-sqlserverpreparedstatement.md)|Establece el parámetro designado en la matriz de bytes especificada.|  
|[setCharacterStream](../../../connect/jdbc/reference/setcharacterstream-method-sqlserverpreparedstatement.md)|Establece el parámetro designado para el objeto Reader especificado.|  
|[setClob](../../../connect/jdbc/reference/setclob-method-sqlserverpreparedstatement.md)|Establece el parámetro designado para el objeto Clob determinado.|  
|[setCursorName](../../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Establece el nombre de cursor de SQL para la cadena especificada, el cual utilizarán métodos ulteriores.|  
|[setDate](../../../connect/jdbc/reference/setdate-method-sqlserverpreparedstatement.md)|Establece el parámetro designado para el valor de fecha especificado.|  
|[setDateTimeOffset](../../../connect/jdbc/reference/setdatetimeoffset-method-sqlserverpreparedstatement.md)|Establece el valor de la columna especificada en el [clase DateTimeOffset](../../../connect/jdbc/reference/datetimeoffset-class.md) valor.|  
|[setDouble](../../../connect/jdbc/reference/setdouble-method-sqlserverpreparedstatement.md)|Establece el parámetro designado para especificado **doble** valor.|  
|[setEscapeProcessing](../../../connect/jdbc/reference/setescapeprocessing-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Establece el modo de procesamiento de escape.|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ofrece una sugerencia al controlador JDBC sobre la dirección en la que se deberían procesar las filas del conjunto de resultados.|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Ofrece una sugerencia al controlador JDBC sobre el número de filas que se deberían capturar en la base de datos cuando se necesitan más filas.|  
|[setFloat](../../../connect/jdbc/reference/setfloat-method-sqlserverpreparedstatement.md)|Establece el parámetro designado para especificado **float** valor.|  
|[setInt](../../../connect/jdbc/reference/setint-method-sqlserverpreparedstatement.md)|Establece el parámetro designado para especificado **int** valor.|  
|[setLong](../../../connect/jdbc/reference/setlong-method-sqlserverpreparedstatement.md)|Establece el parámetro designado para especificado **largo** valor.|  
|[setMaxFieldSize](../../../connect/jdbc/reference/setmaxfieldsize-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Establece el límite para el número máximo de bytes en un [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) columna almacena valores de caracteres o binarios para el número de bytes determinado.|  
|[setMaxRows](../../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Establece el límite para el número máximo de filas que cualquier [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto puede contener el número determinado.|  
|[setNCharacterStream](../../../connect/jdbc/reference/setncharacterstream-method-sqlserverpreparedstatement.md)|Establece el parámetro designado para el objeto Reader especificado.|  
|[setNClob](../../../connect/jdbc/reference/setnclob-method-sqlserverpreparedstatement.md)|Establece el parámetro designado para el objeto especificado.|  
|[setNull](../../../connect/jdbc/reference/setnull-method-sqlserverpreparedstatement.md)|Establece el parámetro designado en un valor NULL, según en tipo de parámetro que se va a establecer.|  
|[setNString](../../../connect/jdbc/reference/setnstring-method-int-java-lang-string.md)|Establece el parámetro designado para especificado **cadena** objeto.|  
|[setObject](../../../connect/jdbc/reference/setobject-method-sqlserverpreparedstatement.md)|Establece el valor del parámetro designado utilizando el objeto especificado.|  
|[setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Solicita que una instrucción se agrupe o no. De forma predeterminada, es agrupables cuando crea un objeto SQLServerPreparedStatement.|  
|[setQueryTimeout](../../../connect/jdbc/reference/setquerytimeout-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Establece el número de segundos que esperará el controlador para que un objeto de instrucción que se ejecute el número de segundos especificado.|  
|[setRef](../../../connect/jdbc/reference/setref-method-sqlserverpreparedstatement.md)|Establece el parámetro designado en el objeto de referencia especificado.|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|(Se hereda de [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md).) Establece la respuesta de modo de almacenamiento en búfer para esta [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto entre mayúsculas y minúsculas **cadena completa** o **adaptable**.|  
|[setShort](../../../connect/jdbc/reference/setshort-method-sqlserverpreparedstatement.md)|Establece el parámetro designado para especificado **corto** valor.|  
|[setString](../../../connect/jdbc/reference/setstring-method-sqlserverpreparedstatement.md)|Establece el parámetro designado para especificado **cadena** valor.|  
|[setSQLXML](../../../connect/jdbc/reference/setsqlxml-method-sqlserverpreparedstatement.md)|Establece el parámetro designado para especificado **SQLXML** objeto.|  
|[setTime](../../../connect/jdbc/reference/settime-method-sqlserverpreparedstatement.md)|Establece el parámetro designado para el valor de hora especificado.|  
|[setTimestamp](../../../connect/jdbc/reference/settimestamp-method-sqlserverpreparedstatement.md)|Establece el parámetro designado para el valor de marca de tiempo especificado.|  
|[setUnicodeStream](../../../connect/jdbc/reference/setunicodestream-method-sqlserverpreparedstatement.md)|Establece el número de parámetro designado en el flujo de entrada especificado, que tendrá el número de bytes especificado.|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverpreparedstatement.md)|Establece el parámetro designado para el valor de URL especificado.|  
|[Unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverpreparedstatement.md)|Devuelve un objeto que implementa la interfaz especificada para permitir el acceso a la [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-métodos específicos.|  
  
## <a name="inherited-methods"></a>Métodos heredados  
  
|Clase heredada de:|Métodos|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerStatement|cancel, clearWarnings, execute, executeUpdate, getConnection, getFetchDirection, getFetchSize, getGeneratedKeys, getMaxFieldSize, getMaxRows, getMoreResults, getQueryTimeout, getResultSet, getResultSetConcurrency, getResultSetHoldability, getResultSetType, getUpdateCount, getWarnings, isPoolable, setCursorName, setEscapeProcessing, setFetchDirection, setFetchSize, setMaxFieldSize, setMaxRows, setPoolable, setQueryTimeout|  
|java.lang.Object|clone, equals, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Statement|cancel, clearWarnings, execute, executeUpdate, getConnection, getFetchDirection, getFetchSize, getGeneratedKeys, getMaxFieldSize, getMaxRows, getMoreResults, getQueryTimeout, getResultSet, getResultSetConcurrency, getResultSetHoldability, getResultSetType, getUpdateCount, getWarnings, setCursorName, setEscapeProcessing, setFetchDirection, setFetchSize, setMaxFieldSize, setMaxRows, setQueryTimeout|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>Vea también  
 [Clase SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md)  
  
  

