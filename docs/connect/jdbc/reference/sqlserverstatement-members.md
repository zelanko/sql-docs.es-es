---
title: Miembros SQLServerStatement | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: jdbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 828cbaa9-ea7a-4986-95c3-5ba0d7d01d83
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d8a22ca95f835f2eec139359f24a486e15cbee2e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlserverstatement-members"></a>Miembros SQLServerStatement
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Las siguientes tablas enumeran los miembros expuestos por el [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) clase.  
  
## <a name="constructors"></a>Constructores  
 Ninguno.  
  
## <a name="fields"></a>Campos  
 Ninguno.  
  
## <a name="inherited-fields"></a>Campos heredados  
  
|Nombre|Description|  
|----------|-----------------|  
|java.sql.Statement|CLOSE_ALL_RESULTS, CLOSE_CURRENT_RESULT, EXECUTE_FAILED, KEEP_CURRENT_RESULT, NO_GENERATED_KEYS, RETURN_GENERATED_KEYS, SUCCESS_NO_INFO|  
  
## <a name="methods"></a>Métodos  
  
|Nombre|Description|  
|----------|-----------------|  
|[addBatch](../../../connect/jdbc/reference/addbatch-method-sqlserverstatement.md)|Agrega el comando SQL determinado a la lista actual de comandos para este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[cancel](../../../connect/jdbc/reference/cancel-method-sqlserverstatement.md)|Cancela la instrucción SQL que se esté ejecutando este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[clearBatch](../../../connect/jdbc/reference/clearbatch-method-sqlserverstatement.md)|Vacía la lista actual de comandos SQL para este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverstatement.md)|Borra todas las advertencias que se notifican en el objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[Cerrar](../../../connect/jdbc/reference/close-method-sqlserverstatement.md)|Esto libera [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) del objeto base de datos y recursos de JDBC inmediatamente en lugar de esperar a que se liberen automáticamente.|  
|[Ejecutar](../../../connect/jdbc/reference/execute-method-sqlserverstatement.md)|Ejecuta la instrucción SQL determinada, que puede devolver varios resultados.|  
|[executeBatch](../../../connect/jdbc/reference/executebatch-method-sqlserverstatement.md)|Envía un lote de comandos a la base de datos para que se ejecute. Si todos los comandos se ejecutan correctamente, devuelve una matriz de recuentos de actualizaciones.|  
|[executeQuery](../../../connect/jdbc/reference/executequery-method-sqlserverstatement.md)|Ejecuta la instrucción SQL especificada y devuelve una sola [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[executeUpdate](../../../connect/jdbc/reference/executeupdate-method-sqlserverstatement.md)|Ejecuta la instrucción SQL determinada, que puede ser una instrucción INSERT, UPDATE, MERGE o DELETE; o una instrucción SQL que no devuelve nada, como una instrucción DDL de SQL.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverstatement.md)|Recupera el [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto que generó este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[getFetchDirection](../../../connect/jdbc/reference/getfetchdirection-method-sqlserverstatement.md)|Recupera la dirección para capturar las filas de tablas de base de datos que es el valor predeterminado de conjuntos de resultados generados desde este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[getFetchSize](../../../connect/jdbc/reference/getfetchsize-method-sqlserverstatement.md)|Recupera el número de resultados del conjunto de filas que el tamaño de captura predeterminado de objetos generados a partir de este conjunto de resultados [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[getGeneratedKeys](../../../connect/jdbc/reference/getgeneratedkeys-method-sqlserverstatement.md)|Recupera cualquiera clave generada automáticamente que se crea como resultado de ejecutar esto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[getMaxFieldSize](../../../connect/jdbc/reference/getmaxfieldsize-method-sqlserverstatement.md)|Recupera el número máximo de bytes que se pueden devolver para los caracteres y valores de columna binaria en un [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto generado por este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[getMaxRows](../../../connect/jdbc/reference/getmaxrows-method-sqlserverstatement.md)|Recupera el número máximo de filas que un [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto generado por este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto puede contener.|  
|[getMoreResults](../../../connect/jdbc/reference/getmoreresults-method-sqlserverstatement.md)|Se desplaza al próximo resultado de esto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[getQueryTimeout](../../../connect/jdbc/reference/getquerytimeout-method-sqlserverstatement.md)|Recupera el número de segundos que la [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)] esperará a que esto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto que se va a ejecutar.|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverstatement.md)|Recupera la respuesta el modo de almacenamiento en búfer para esta [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[getResultSet](../../../connect/jdbc/reference/getresultset-method-sqlserverstatement.md)|Recupera el resultado actual como un [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto.|  
|[getResultSetConcurrency](../../../connect/jdbc/reference/getresultsetconcurrency-method-sqlserverstatement.md)|Recupera el conjunto de resultados de simultaneidad para [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objetos que haya generado por este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[getResultSetHoldability](../../../connect/jdbc/reference/getresultsetholdability-method-sqlserverstatement.md)|Recupera el conjunto de resultados capacidad de alojamiento para [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objetos que haya generado por este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[getResultSetType](../../../connect/jdbc/reference/getresultsettype-method-sqlserverstatement.md)|Recupera el conjunto de resultados tipo para [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objetos que haya generado por este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[getUpdateCount](../../../connect/jdbc/reference/getupdatecount-method-sqlserverstatement.md)|Recupera el resultado actual como un recuento de actualización.|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverstatement.md)|Recupera la primera advertencia que notifica las llamadas en el objeto [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto.|  
|[IsClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverstatement.md)|Indica si este [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto se ha cerrado.|  
|[isPoolable](../../../connect/jdbc/reference/ispoolable-method-sqlserverstatement.md)|Devuelve un valor que indica si una instrucción se puede agregar al grupo de instrucciones proporcionado por el usuario.|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverstatement.md)|Indica si este objeto de instrucción es un contenedor para la interfaz especificada.|  
|[setCursorName](../../../connect/jdbc/reference/setcursorname-method-sqlserverstatement.md)|Establece el nombre de cursor de SQL para la cadena determinada, el cual utilizarán métodos ulteriores.|  
|[setEscapeProcessing](../../../connect/jdbc/reference/setescapeprocessing-method-sqlserverstatement.md)|Establece el modo de procesamiento de escape.|  
|[setFetchDirection](../../../connect/jdbc/reference/setfetchdirection-method-sqlserverstatement.md)|Ofrece una sugerencia al controlador JDBC sobre la dirección en la que se deberían procesar las filas del conjunto de resultados.|  
|[setFetchSize](../../../connect/jdbc/reference/setfetchsize-method-sqlserverstatement.md)|Ofrece una sugerencia al controlador JDBC sobre el número de filas que se deberían capturar en la base de datos cuando se necesitan más filas.|  
|[setMaxFieldSize](../../../connect/jdbc/reference/setmaxfieldsize-method-sqlserverstatement.md)|Establece el límite para el número máximo de bytes en un [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) columna almacena valores de caracteres o binarios para el número de bytes determinado.|  
|[setMaxRows](../../../connect/jdbc/reference/setmaxrows-method-sqlserverstatement.md)|Establece el límite para el número máximo de filas que cualquier [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objeto puede contener el número determinado.|  
|[setPoolable](../../../connect/jdbc/reference/setpoolable-method-sqlserverstatement.md)|Solicita que una instrucción se agrupe o no.|  
|[setQueryTimeout](../../../connect/jdbc/reference/setquerytimeout-method-sqlserverstatement.md)|Establece el número de segundos que esperará el controlador un [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto que se va a ejecutar el número de segundos determinado.|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverstatement.md)|Establece la respuesta de modo de almacenamiento en búfer para esta [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto entre mayúsculas y minúsculas **cadena completa** o **adaptable**.|  
|[Unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverstatement.md)|Devuelve un objeto que implementa la interfaz especificada para permitir el acceso a la [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-métodos específicos.|  
  
## <a name="inherited-methods"></a>Métodos heredados  
  
|Clase heredada de:|Métodos|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>Vea también  
 [Clase SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md)  
  
  
