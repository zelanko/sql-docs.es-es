---
title: Los miembros de SQLServerConnection | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: jdbc
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3115a533-756b-4c78-aee9-4ba7253c85e0
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 917a5561dd3de7f9f45434aef88bd2eb98661473
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverconnection-members"></a>Miembros SQLServerConnection
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Las siguientes tablas enumeran los miembros expuestos por el [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) clase.  
  
## <a name="constructors"></a>Constructores  
 Ninguno.  
  
## <a name="fields"></a>Campos  
  
|Nombre|Description|  
|----------|-----------------|  
|[TRANSACTION_SNAPSHOT](../../../connect/jdbc/reference/transaction-snapshot-field-sqlserverconnection.md)|Se utiliza para especificar el nivel de aislamiento de transacción de instantáneas.|  
  
## <a name="inherited-fields"></a>Campos heredados  
  
|Clase heredada de:|Description|  
|---------------------------|-----------------|  
|java.sql.Connection|TRANSACTION_NONE, TRANSACTION_READ_COMMITTED, TRANSACTION_READ_UNCOMMITTED, TRANSACTION_REPEATABLE_READ, TRANSACTION_SERIALIZABLE|  
  
## <a name="methods"></a>Métodos  
  
|Nombre|Description|  
|----------|-----------------|  
|[clearWarnings](../../../connect/jdbc/reference/clearwarnings-method-sqlserverconnection.md)|Borra todas las advertencias notificadas para esta [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto.|  
|[Cerrar](../../../connect/jdbc/reference/close-method-sqlserverconnection.md)|Libera la base de datos para este [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto y los recursos JDBC inmediatamente en lugar de esperar a que se liberen automáticamente.|  
|[confirmación](../../../connect/jdbc/reference/commit-method-sqlserverconnection.md)|Hace que todos los cambios realizados desde la anterior confirmación o reversión permanentes y libera los bloqueos de base de datos que se mantienen actualmente por este [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto.|  
|[createBlob](../../../connect/jdbc/reference/createblob-method-sqlserverconnection.md)|Crea un **java.sql.Blob** objeto sin ningún dato.|  
|[createClob](../../../connect/jdbc/reference/createclob-method-sqlserverconnection.md)|Crea un **java.sql.Clob** objeto sin ningún dato.|  
|[createNClob](../../../connect/jdbc/reference/createnclob-method-sqlserverconnection.md)|Crea un **java.sql.NClob** objeto sin ningún dato.|  
|[createStatement](../../../connect/jdbc/reference/createstatement-method-sqlserverconnection.md)|Crea un [SQLServerStatement](../../../connect/jdbc/reference/sqlserverstatement-class.md) objeto para enviar instrucciones SQL a la base de datos.|  
|[createSQLXML](../../../connect/jdbc/reference/createsqlxml-method-sqlserverconnection.md)|Crea un **java.sql.SQLXML** objeto sin ningún dato.|  
|[getAutoCommit](../../../connect/jdbc/reference/getautocommit-method-sqlserverconnection.md)|Devuelve el modo de confirmación automática actual de este [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto.|  
|[getCatalog](../../../connect/jdbc/reference/getcatalog-method-sqlserverconnection.md)|Recupera el nombre del catálogo actual para este [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto.|  
|[Método getClientConnectionID &#40; SQLServerConnection &#41;](../../../connect/jdbc/reference/getclientconnectionid-method-sqlserverconnection.md)|Obtiene el identificador de conexión del intento de conexión más reciente, independientemente de que dicho intento fuera correcto o erróneo.|  
|[getClientInfo](../../../connect/jdbc/reference/getclientinfo-method-sqlserverconnection.md)|Recupera información con respecto a las propiedades de información del cliente que admita el controlador JDBC.|  
|[getHoldability](../../../connect/jdbc/reference/getholdability-method-sqlserverconnection.md)|Recupera la capacidad de alojamiento actual de [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objetos creados mediante este [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto.|  
|[getMetaData](../../../connect/jdbc/reference/getmetadata-method-sqlserverconnection.md)|Recupera un [SQLServerDatabaseMetaData](../../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) objeto que contiene metadatos acerca de la base de datos a la que se [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto representa una conexión.|  
|[getTransactionIsolation](../../../connect/jdbc/reference/gettransactionisolation-method-sqlserverconnection.md)|Recupera el nivel de aislamiento de transacción actual para este [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto.|  
|[getTypeMap](../../../connect/jdbc/reference/gettypemap-method-sqlserverconnection.md)|Recupera el objeto de mapa que está asociado a este [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto.|  
|[getWarnings](../../../connect/jdbc/reference/getwarnings-method-sqlserverconnection.md)|Recupera la primera advertencia que notifican las llamadas en el objeto [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto.|  
|[isClosed](../../../connect/jdbc/reference/isclosed-method-sqlserverconnection.md)|Indica si este [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto se ha cerrado.|  
|[isReadOnly](../../../connect/jdbc/reference/isreadonly-method-sqlserverconnection.md)|Indica si este [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto está en modo de solo lectura.|  
|[isValid](../../../connect/jdbc/reference/isvalid-method-sqlserverconnection.md)|Indica si este [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto no se ha cerrado y sigue siendo válido.|  
|[nativeSQL](../../../connect/jdbc/reference/nativesql-method-sqlserverconnection.md)|Convierte la instrucción SQL establecida en gramática SQL nativa del servidor de la base de datos.|  
|[prepareCall](../../../connect/jdbc/reference/preparecall-method-sqlserverconnection.md)|Crea un [SQLServerCallableStatement](../../../connect/jdbc/reference/sqlservercallablestatement-class.md) objeto para llamar a procedimientos almacenado de la base de datos.|  
|[prepareStatement](../../../connect/jdbc/reference/preparestatement-method-sqlserverconnection.md)|Crea un [SQLServerPreparedStatement](../../../connect/jdbc/reference/sqlserverpreparedstatement-class.md) objeto para enviar instrucciones SQL parametrizadas a la base de datos.|  
|[releaseSavepoint](../../../connect/jdbc/reference/releasesavepoint-method-sqlserverconnection.md)|Quita especificado [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) objeto de la transacción actual.|  
|[reversión](../../../connect/jdbc/reference/rollback-method-sqlserverconnection.md)|Deshace todos los cambios realizados en la transacción actual y libera los bloqueos de base de datos mantenidos actualmente por este [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto.|  
|[setAutoCommit](../../../connect/jdbc/reference/setautocommit-method-sqlserverconnection.md)|Establece el modo de confirmación automática para este [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto en el estado determinado.|  
|[setCatalog](../../../connect/jdbc/reference/setcatalog-method-sqlserverconnection.md)|Establece el nombre de catálogo especificado para seleccionar un subespacio de este [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) base de datos del objeto en el que se va a trabajar.|  
|[setClientInfo](../../../connect/jdbc/reference/setclientinfo-method-sqlserverconnection.md)|Establece el valor de las propiedades de la información del cliente.|  
|[setHoldability](../../../connect/jdbc/reference/setholdability-method-sqlserverconnection.md)|Cambia la capacidad de alojamiento de [SQLServerResultSet](../../../connect/jdbc/reference/sqlserverresultset-class.md) objetos creados mediante este [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) objeto a la capacidad de alojamiento determinada.|  
|[setReadOnly](../../../connect/jdbc/reference/setreadonly-method-sqlserverconnection.md)|Esto coloca [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto en modo de solo lectura como una sugerencia para el controlador JDBC para habilitar las optimizaciones de la base de datos.|  
|[setSavepoint](../../../connect/jdbc/reference/setsavepoint-method-sqlserverconnection.md)|Crea un punto de retorno sin nombre en la transacción actual y devuelve el nuevo [SQLServerSavepoint](../../../connect/jdbc/reference/sqlserversavepoint-class.md) objeto que lo representa.|  
|[setTransactionIsolation](../../../connect/jdbc/reference/settransactionisolation-method-sqlserverconnection.md)|Intenta cambiar el nivel de aislamiento de transacción de este [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto a la que se proporciona.|  
|[setTypeMap](../../../connect/jdbc/reference/settypemap-method-sqlserverconnection.md)|Instala el objeto de TypeMap determinado como la asignación de tipos para este [SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md) objeto.|  
  
## <a name="inherited-methods"></a>Métodos heredados  
  
|Clase heredada de:|Métodos|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.lang.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>Vea también  
 [Clase SQLServerConnection](../../../connect/jdbc/reference/sqlserverconnection-class.md)  
  
  

