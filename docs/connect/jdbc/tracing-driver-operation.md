---
title: Funcionamiento del controlador de seguimiento | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 723aeae7-6504-4585-ba8b-3525115bea8b
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e364f990cc2428d771f3bc57015df0636e23fbfb
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="tracing-driver-operation"></a>Hacer un seguimiento del funcionamiento del controlador
[!INCLUDE[Driver_JDBC_Download](../../includes/driver_jdbc_download.md)]

  El [!INCLUDE[jdbcNoVersion](../../includes/jdbcnoversion_md.md)] admite el uso de seguimiento (o registro) para ayudar a resolver problemas y problemas con el controlador JDBC cuando se utiliza en la aplicación. Para habilitar el uso de la traza, el controlador JDBC usa las API de registro de java.util.logging, que proporciona un conjunto de clases para crear objetos de registrador y LogRecord.  
  
> [!NOTE]  
>  En el caso del componente nativo (sqljdbc_xa.dll) que se incluye con el controlador JDBC, el marco de diagnósticos integrados (BID) habilita el seguimiento. Para obtener información acerca de BID, vea [seguimiento de acceso de datos de SQL Server](http://go.microsoft.com/fwlink/?LinkId=70042).  
  
 Al desarrollar la aplicación, puede realizar llamadas a objetos de registrador, que a su vez crean objetos LogRecord, que, a continuación, se pasan a los objetos de controlador para procesar. Registrador y controlador por los objetos de ambos niveles de registro y, opcionalmente, se procesan los filtros de registro, para regular qué LogRecords. Una vez completadas las operaciones de registro, los objetos de controlador, opcionalmente, pueden utilizar objetos de formateador para publicar la información de registro.  
  
 De forma predeterminada, el marco java.util.logging escribe los resultados en un archivo. Este archivo de registro de salida debe tener permisos de escritura para el contexto en que se ejecuta el controlador JDBC.  
  
> [!NOTE]  
>  Para obtener más información acerca del uso de varios objetos de registro para programar el seguimiento, consulte la sección sobre API de registro de Java en el sitio web de Sun Microsystems.  
  
 En la siguiente sección se describen los niveles y las categorías de registro de los que se puede hacer un seguimiento y se proporciona información sobre cómo habilitar el seguimiento en la aplicación.  
  
## <a name="logging-levels"></a>Niveles de registro  
 Cada mensaje de registro creado tiene un nivel de registro asociado. El nivel de registro determina la importancia del mensaje de registro, que se define mediante la **nivel** clase de java.util.logging. Al habilitar el registro en un nivel, se habilita también en todos los niveles superiores. En esta sección se describen los niveles de registro para las categorías de registro públicas y también para las internas. Para obtener más información acerca de las categorías de registro, vea en este tema la sección Categorías de registro.  
  
 La tabla siguiente describe cada uno de los niveles de registro para categorías de registro públicas.  
  
|Nombre|Description|  
|----------|-----------------|  
|SEVERE|Indica un error grave y es el nivel de registro máximo. En el controlador JDBC, este nivel se utiliza para informar de errores y excepciones.|  
|WARNING|Indica un posible problema.|  
|INFO|Proporciona mensajes informativos.|  
|CONFIG|Proporciona mensajes de configuración. Tenga en cuenta que el controlador JDBC no proporciona actualmente mensajes de configuración.|  
|FINE|Proporciona información de seguimiento básica, que incluye todas las excepciones producidas por los métodos públicos.|  
|FINER|Proporciona información de seguimiento detallada, que incluye todos los puntos de entrada y salida de los métodos públicos junto con los tipos de datos de parámetro asociados y todas las propiedades públicas de la clase pública. Además, parámetros de entrada, parámetros de salida y valores devueltos del método excepto CLOB, BLOB, NCLOB, Reader, \<secuencia > tipos de valor devueltos.|  
|FINEST|Proporciona información de seguimiento muy detallada. Se trata del nivel de registro mínimo.|  
|OFF|Desactiva el registro.|  
|ALL|Habilita el registro de todos los mensajes.|  
  
 La tabla siguiente describe cada uno de los niveles de registro para categorías de registro internas.  
  
|Nombre|Description|  
|----------|-----------------|  
|SEVERE|Indica un error grave y es el nivel de registro máximo. En el controlador JDBC, este nivel se utiliza para informar de errores y excepciones.|  
|WARNING|Indica un posible problema.|  
|INFO|Proporciona mensajes informativos.|  
|FINE|Proporciona información de seguimiento que incluye la creación y destrucción de objetos básicos. Además, incluye todas las excepciones producidas por los métodos públicos.|  
|FINER|Proporciona información de seguimiento detallada, que incluye todos los puntos de entrada y salida de los métodos públicos junto con los tipos de datos de parámetro asociados y todas las propiedades públicas de la clase pública. Además, parámetros de entrada, parámetros de salida y valores devueltos del método excepto CLOB, BLOB, NCLOB, Reader, \<secuencia > tipos de valor devueltos.<br /><br /> Las siguientes categorías de registro en la versión 1.2 del controlador JDBC existían y tenían el nivel de registro FINE: [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md), [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md), XA, y [SQLServerDataSource ](../../connect/jdbc/reference/sqlserverdatasource-class.md). Desde la versión 2.0, se han actualizado al nivel FINER.|  
|FINEST|Proporciona información de seguimiento muy detallada. Se trata del nivel de registro mínimo.<br /><br /> En la versión 1.2 del controlador JDBC existían las siguientes categorías de registro y tenían el nivel de registro FINEST: TDS.DATA y TDS.TOKEN. Desde la versión 2.0, conservan el nivel de registro FINEST.|  
|OFF|Desactiva el registro.|  
|ALL|Habilita el registro de todos los mensajes.|  
  
## <a name="logging-categories"></a>Categorías de registro  
 Cuando se crea un objeto de registrador, debe indicar al objeto qué entidad con nombre o la categoría que está interesado en obtener información de registro. El controlador JDBC admite las siguientes categorías de registro público, que son definidas en el paquete del controlador com.microsoft.sqlserver.jdbc.  
  
|Nombre|Description|  
|----------|-----------------|  
|Conexión|Registra mensajes en el [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) clase. La aplicación puede configurar el nivel de registro como FINER.|  
|.|Registra mensajes en el [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) clase. La aplicación puede configurar el nivel de registro como FINER.|  
|DataSource|Registra mensajes en el [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md) clase. La aplicación puede configurar el nivel de registro como FINE.|  
|ResultSet|Registra mensajes en el [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) clase. La aplicación puede configurar el nivel de registro como FINER.|  
|Controlador|Registra mensajes en el [SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md) clase. La aplicación puede configurar el nivel de registro como FINER.|  
  
 Desde la versión 2.0 del controlador JDBC de Microsoft, el controlador también proporciona el paquete com.microsoft.sqlserver.jdbc.internals, que incluye la compatibilidad de registro con las siguientes categorías de registro interno.  
  
|Nombre|Description|  
|----------|-----------------|  
|AuthenticationJNI|Registra mensajes relativos a las ventanas de problemas de autenticación integran (cuando la **authenticationScheme** propiedad de conexión se establece de forma implícita o explícita en **NativeAuthentication**).<br /><br /> La aplicación puede configurar el nivel de registro como FINEST y FINE.|  
|SQLServerConnection|Registra mensajes en el [SQLServerConnection](../../connect/jdbc/reference/sqlserverconnection-class.md) clase. La aplicación puede configurar el nivel de registro como FINE y FINER.|  
|SQLServerDataSource|Registra mensajes en el [SQLServerDataSource](../../connect/jdbc/reference/sqlserverdatasource-class.md), [SQLServerConnectionPoolDataSource](../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md), y [SQLServerPooledConnection](../../connect/jdbc/reference/sqlserverpooledconnection-class.md) clases.<br /><br /> La aplicación puede configurar el nivel de registro como FINER.|  
|InputStream|Registra mensajes relativos a los siguientes tipos de datos: java.io.InputStream, java.io.Reader y a los tipos de datos que tienen un especificador máximo, como varchar, nvarchar y los tipos de datos varbinary.<br /><br /> La aplicación puede configurar el nivel de registro como FINER.|  
|SQLServerException|Registra mensajes en el [SQLServerException](../../connect/jdbc/reference/sqlserverexception-class.md) clase. La aplicación puede configurar el nivel de registro como FINE.|  
|SQLServerResultSet|Registra mensajes en el [SQLServerResultSet](../../connect/jdbc/reference/sqlserverresultset-class.md) clase. La aplicación puede configurar el nivel de registro como FINE, FINER y FINEST.|  
|SQLServerStatement|Registra mensajes en el [SQLServerStatement](../../connect/jdbc/reference/sqlserverstatement-class.md) clase. La aplicación puede configurar el nivel de registro como FINE, FINER y FINEST.|  
|XA|Registra mensajes para todas las transacciones XA de la [SQLServerXADataSource](../../connect/jdbc/reference/sqlserverxadatasource-class.md) clase. La aplicación puede configurar el nivel de registro como FINE y FINER.|  
|KerbAuthentication|Registra mensajes relativos a la autenticación de Kerberos de tipo 4 (cuando la **authenticationScheme** propiedad de conexión se establece en **Kerberos**). La aplicación puede configurar el nivel de registro como FINE o FINER.|  
|TDS.DATA|Registra mensajes que contienen la conversación de nivel de protocolo TDS entre el controlador y SQL Server. Los contenidos detallados de cada paquete TDS enviado y recibido se registran en ASCII y como hexadecimales. No se registran las credenciales de inicio de sesión (nombres y contraseñas de usuarios). Todos los demás datos se registran.<br /><br /> Esta categoría crea mensajes muy detallados y solo se puede habilitar si se establece el nivel de registro en FINEST.|  
|TDS.Channel|Esta categoría realiza un seguimiento del canal de comunicaciones TDS con SQL Server. El mensaje registrado incluye la apertura y cierre de sockets, así como lecturas y escrituras. También realiza seguimientos de mensajes relacionados con el establecimiento de una conexión de Capa de sockets seguros (SSL) con SQL Server.<br /><br /> Esta categoría solo puede ser habilitada configurando el nivel de registro en FINE, FINER o FINEST.|  
|TDS.Writer|Esta categoría realiza un seguimiento de las escrituras en el canal TDS. Tenga en cuenta que solo se hace un seguimiento de la longitud de las escrituras, no de los contenidos. Esta categoría también hace un seguimiento de los problemas que se producen cuando una señal de atención es enviada al servidor para cancelar la ejecución de una instrucción.<br /><br /> Esta categoría solo puede ser habilitada configurando el nivel de registro en FINEST.|  
|TDS.Reader|Esta categoría realiza un seguimiento de determinadas operaciones de lectura desde el canal TDS en el nivel FINEST. En el nivel FINEST, el seguimiento puede ser muy detallado. En los niveles WARNING y SEVERE, esta categoría realiza un seguimiento cuando el controlador recibe un protocolo TDS no válido antes de que el controlador cierre la conexión.<br /><br /> Esta categoría solo puede ser habilitada configurando el nivel de registro en FINER y FINEST.|  
|TDS.Command|Esta categoría realiza un seguimiento de las transiciones de estado de bajo nivel y otra información asociada a la ejecución de comandos TDS, como [!INCLUDE[tsql](../../includes/tsql_md.md)] ejecuciones de instrucciones, cursores ResultSet, confirmaciones y así sucesivamente.<br /><br /> Esta categoría solo puede ser habilitada configurando el nivel de registro en FINEST.|  
|TDS.TOKEN|Esta categoría registra solo los tokens de los paquetes TDS y es menos detallado que la categoría TDS.DATA. Solo se puede habilitar configurando el nivel de registro en FINEST.<br /><br /> En el nivel FINEST, esta categoría hace un seguimiento de los tokens TDS conforme son procesados en la respuesta. En el nivel SEVERE, esta categoría hace un seguimiento cuando encuentra un token TDS no válido.|  
|SQLServerDatabaseMetaData|Registra mensajes en el [SQLServerDatabaseMetaData](../../connect/jdbc/reference/sqlserverdatabasemetadata-class.md) clase. La aplicación puede configurar el nivel de registro como FINE.|  
|SQLServerResultSetMetaData|Registra mensajes en el [SQLServerResultSetMetaData](../../connect/jdbc/reference/sqlserverresultsetmetadata-class.md) clase. La aplicación puede configurar el nivel de registro como FINE.|  
|SQLServerParameterMetaData|Registra mensajes en el [SQLServerParameterMetaData](../../connect/jdbc/reference/sqlserverparametermetadata-class.md) clase. La aplicación puede configurar el nivel de registro como FINE.|  
|SQLServerBlob|Registra mensajes en el [SQLServerBlob](../../connect/jdbc/reference/sqlserverblob-class.md) clase. La aplicación puede configurar el nivel de registro como FINE.|  
|SQLServerClob|Registra mensajes en el [SQLServerClob](../../connect/jdbc/reference/sqlserverclob-class.md) clase. La aplicación puede configurar el nivel de registro como FINE.|  
|SQLServerSQLXML|Registra mensajes en la clase SQLServerSQLXML interna. La aplicación puede configurar el nivel de registro como FINE.|  
|SQLServerDriver|Registra mensajes en el [SQLServerDriver](../../connect/jdbc/reference/sqlserverdriver-class.md) clase. La aplicación puede configurar el nivel de registro como FINE.|  
|SQLServerNClob|Registra mensajes en el [SQLServerNClob](../../connect/jdbc/reference/sqlservernclob-class.md) clase. La aplicación puede configurar el nivel de registro como FINE.|  
  
## <a name="enabling-tracing-programmatically"></a>Habilitar seguimiento mediante programación  
 Seguimiento se puede habilitar mediante programación mediante la creación de un objeto de registrador y que indica la categoría que se registra. Por ejemplo, el siguiente código muestra cómo habilitar el registro para las instrucciones SQL:  
  
```  
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc.Statement");  
logger.setLevel(Level.FINER);  
```  
  
 Para desactivar el registro en el código, use lo siguiente:  
  
```  
logger.setLevel(Level.OFF);  
```  
  
 Para registrar todas las categorías disponibles, use lo siguiente:  
  
```  
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc");  
logger.setLevel(Level.FINE);  
```  
  
 Para deshabilitar el registro de una categoría específica, use lo siguiente:  
  
```  
Logger logger = Logger.getLogger("com.microsoft.sqlserver.jdbc.Statement");  
logger.setLevel(Level.OFF);  
```  
  
## <a name="enabling-tracing-by-using-the-loggingproperties-file"></a>Habilitar seguimiento mediante el archivo Logging.Properties  
 También puede habilitar el seguimiento mediante el uso de la `logging.properties` archivo, que se encuentra en la `lib` directorio de la instalación de Java Runtime Environment (JRE). Este archivo se puede usar para establecer los valores predeterminados para los registradores y controladores que se usan al habilitar el seguimiento.  
  
 El siguiente es un ejemplo de las opciones que puede usar en el `logging.properties` archivos:  
  
```  
# Specify the handler, the handlers will be installed during VM startup.  
handlers= java.util.logging.FileHandler  
  
# Default global logging level.  
.level= OFF  
  
# default file output is in user's home directory.  
java.util.logging.FileHandler.pattern = %h/java%u.log  
java.util.logging.FileHandler.limit = 5000000  
java.util.logging.FileHandler.count = 20  
java.util.logging.FileHandler.formatter = java.util.logging.SimpleFormatter  
java.util.logging.FileHandler.level = FINEST  
  
# Facility specific properties.  
com.microsoft.sqlserver.jdbc.level=FINEST  
  
```  
  
> [!NOTE]  
>  Puede establecer las propiedades el `logging.properties` archivo mediante el objeto LogManager que forma parte de java.util.logging.  
  
## <a name="see-also"></a>Vea también  
 [Diagnosticar problemas con el controlador JDBC](../../connect/jdbc/diagnosing-problems-with-the-jdbc-driver.md)  
  
  

