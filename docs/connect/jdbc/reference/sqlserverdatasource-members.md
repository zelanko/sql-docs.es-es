---
title: Miembros SQLServerDataSource | Documentos de Microsoft
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 7e749bc5-d765-4864-be2b-7822d4c20c09
caps.latest.revision: 43
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: eb9919441a3e20fdb02753258e134ba7bedb0ce0
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlserverdatasource-members"></a>Miembros SQLServerDataSource
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Las tablas siguientes enumeran los miembros expuestos por el [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) clase.  
  
## <a name="constructors"></a>Constructores  
  
|Nombre|Description|  
|----------|-----------------|  
|[(De SQLServerDataSource)](../../../connect/jdbc/reference/sqlserverdatasource-constructor.md)|Inicializa una nueva instancia de la [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) clase.|  
  
## <a name="fields"></a>Campos  
 Ninguno.  
  
## <a name="inherited-fields"></a>Campos heredados  
 Ninguno.  
  
## <a name="methods"></a>Métodos  
  
|Nombre|Description|  
|----------|-----------------|  
|[getApplicationIntent](../../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)|Devuelve el valor de la **applicationIntent** propiedad de conexión.|  
|[getApplicationName](../../../connect/jdbc/reference/getapplicationname-method-sqlserverdatasource.md)|Devuelve el nombre de la aplicación.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)|Intenta establecer una conexión con los datos de origen que este [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) objeto representa.|  
|[getDatabaseName](../../../connect/jdbc/reference/getdatabasename-method-sqlserverdatasource.md)|Devuelve el nombre de la base de datos.|  
|[getEncrypt](../../../connect/jdbc/reference/getencrypt-method-sqlserverdatasource.md)|Devuelve un **booleano** valor que indica si está habilitada la propiedad de cifrado.|  
|[getDescription](../../../connect/jdbc/reference/getdescription-method-sqlserverdatasource.md)|Devuelve una descripción del origen de datos.|  
|[getFailoverPartner](../../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md)|Devuelve el nombre del servidor de conmutación por error que se usa en la configuración de la creación de reflejo de la base de datos.|  
|[getHostNameInCertificate](../../../connect/jdbc/reference/gethostnameincertificate-method-sqlserverdatasource.md)|Devuelve el nombre del host que se utiliza para validar el certificado de Capa de sockets seguros (SSL) de SQL Server.|  
|[getInstanceName](../../../connect/jdbc/reference/getinstancename-method-sqlserverdatasource.md)|Devuelve el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] nombre de instancia.|  
|[getLastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md)|Devuelve un **booleano** valor que indica si la propiedad lastUpdateCount está habilitada.|  
|[getLockTimeout](../../../connect/jdbc/reference/getlocktimeout-method-sqlserverdatasource.md)|Devuelve un **int** valor que indica el número de milisegundos que espera a que la base de datos antes de informar de un tiempo de espera de bloqueo.|  
|[getLoginTimeout](../../../connect/jdbc/reference/getlogintimeout-method-sqlserverdatasource.md)|Devuelve el número de segundos que este [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) objeto esperará mientras intenta realizar una conexión.|  
|[getLogWriter](../../../connect/jdbc/reference/getlogwriter-method-sqlserverdatasource.md)|Devuelve un flujo de salida de caracteres que se va a utilizar para todos los mensajes de registro y seguimiento.|  
|[getMultiSubnetFailover](../../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)|Devuelve el valor de la **multiSubnetFailover** propiedad de conexión.|  
|[getPacketSize](../../../connect/jdbc/reference/getpacketsize-method-sqlserverdatasource.md)|Devuelve el tamaño de paquete de red actual que se utiliza para comunicarse con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], especificado en bytes.|  
|[getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md)|Devuelve el número de puerto actual utilizado para comunicarse con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
|[getReference](../../../connect/jdbc/reference/getreference-method-sqlserverdatasource.md)|Devuelve una referencia a este [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) objeto.|  
|[getResponseBuffering](../../../connect/jdbc/reference/getresponsebuffering-method-sqlserverdatasource.md)|Devuelve la respuesta del modo de almacenamiento en búfer para esta [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) objeto.|  
|[método getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md)|Devuelve el tipo de cursor predeterminado usado para todos los conjuntos de resultados creados mediante este [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) objeto.|  
|[getSendStringParametersAsUnicode](../../../connect/jdbc/reference/getsendstringparametersasunicode-method-sqlserverdatasource.md)|Devuelve un **booleano** valor que indica si está habilitado el envío de parámetros de cadena al servidor en formato UNICODE.|  
|[getSendTimeAsDatetime](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md)|Devuelve el valor de la **SendTimeAsDatetime** propiedad de conexión.|  
|[getServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md)|Devuelve el nombre del equipo que ejecuta [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
|[getTrustServerCertificate](../../../connect/jdbc/reference/gettrustservercertificate-method-sqlserverdatasource.md)|Devuelve un **booleano** valor que indica si la propiedad trustServerCertificate está habilitada.|  
|[getTrustStore](../../../connect/jdbc/reference/gettruststore-method-sqlserverdatasource.md)|Devuelve la ruta de acceso (incluido el nombre de archivo) del archivo trustStore del certificado.|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md)|Devuelve la dirección URL utilizada para conectarse al origen de datos.|  
|[getUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md)|Devuelve el nombre de usuario usado para conectar al origen de datos.|  
|[getUseSQLServerBaseDate](../../../connect/jdbc/reference/getsendtimeasdatetime-method-sqlserverdatasource.md)|Devuelve el valor de la propiedad de conexión useSQLServerBaseDate.|  
|[getWorkstationID](../../../connect/jdbc/reference/getworkstationid-method-sqlserverdatasource.md)|Devuelve el nombre del nombre del equipo cliente usado para conectarse al origen de datos.|  
|[getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md)|Devuelve un **booleano** valor que indica si está habilitada la conversión de Estados SQL Estados conformes a XOPEN.|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverdatasource.md)|Indica si este objeto de origen de datos es un contenedor para la interfaz especificada.|  
|[setApplicationIntent](../../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)|Establece el valor de la **applicationIntent** propiedad de conexión.|  
|[setApplicationName](../../../connect/jdbc/reference/setapplicationname-method-sqlserverdatasource.md)|Establece el nombre de la aplicación.|  
|[setAuthenticationScheme](../../../connect/jdbc/reference/setauthenticationscheme-sqlserverdatasource.md)|Indica el tipo de seguridad integrada que desea que use la aplicación.|  
|[setDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md)|Establece el nombre de la base de datos a la que se va a efectuar la conexión.|  
|[setDescription](../../../connect/jdbc/reference/setdescription-method-sqlserverdatasource.md)|Establece la descripción del origen de datos.|  
|[setEncrypt](../../../connect/jdbc/reference/setencrypt-method-sqlserverdatasource.md)|Establece un **booleano** valor que indica si está habilitada la propiedad de cifrado.|  
|[setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md)|Establece el nombre del servidor de conmutación por error que se usa en la configuración de la creación de reflejo de la base de datos.|  
|[setHostNameInCertificate](../../../connect/jdbc/reference/sethostnameincertificate-method-sqlserverdatasource.md)|Establece el nombre de host que se va a utilizar para validar el certificado de Capa de sockets seguros (SSL) de SQL Server.|  
|[setInstanceName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md)|Establece el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] nombre de instancia.|  
|[setIntegratedSecurity](../../../connect/jdbc/reference/setintegratedsecurity-method-sqlserverdatasource.md)|Establece un **booleano** valor que indica si la propiedad integratedSecurity está habilitada.|  
|[setLastUpdateCount](../../../connect/jdbc/reference/setlastupdatecount-method-sqlserverdatasource.md)|Establece un **booleano** valor que indica si la propiedad lastUpdateCount está habilitada.|  
|[setLockTimeout](../../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md)|Establece una **int** valor que indica el número de milisegundos que transcurrirán antes de que la base de datos notifique un tiempo de espera de bloqueo.|  
|[setLoginTimeout](../../../connect/jdbc/reference/setlogintimeout-method-sqlserverdatasource.md)|Establece el número de segundos que esto [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) objeto esperará mientras intenta realizar una conexión.|  
|[setLogWriter](../../../connect/jdbc/reference/setlogwriter-method-sqlserverdatasource.md)|Establece un flujo de salida de caracteres que se utilizará para todos los mensajes de registro y seguimiento.|  
|[setMultiSubnetFailover](../../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)|Establece el valor de la **multiSubnetFailover** propiedad de conexión.|  
|[setPacketSize](../../../connect/jdbc/reference/setpacketsize-method-sqlserverdatasource.md)|Establece el tamaño de paquete de red actual que se utiliza para comunicarse con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)], especificado en bytes.|  
|[setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md)|Establece la contraseña utilizada para conectarse a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
|[setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md)|Establece el número de puerto usado para comunicarse con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
|[setResponseBuffering](../../../connect/jdbc/reference/setresponsebuffering-method-sqlserverdatasource.md)|Establece la respuesta para las conexiones creadas utilizando el modo de almacenamiento en búfer [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) objeto.|  
|[setSelectMethod](../../../connect/jdbc/reference/setselectmethod-method-sqlserverdatasource.md)|Establece el tipo de cursor predeterminado usado para todos los conjuntos de resultados creados mediante este [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md) objeto.|  
|[setSendStringParametersAsUnicode](../../../connect/jdbc/reference/setsendstringparametersasunicode-method-sqlserverdatasource.md)|Establece un **booleano** valor que indica si está habilitado el envío de parámetros de cadena al servidor en formato UNICODE.|  
|[setSendTimeAsDatetime](../../../connect/jdbc/reference/setsendtimeasdatetime-method-sqlserverdatasource.md)|Especifica cómo enviar los valores java.sql.Time al servidor.|  
|[setServerName](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md)|Establece el nombre del equipo que ejecuta [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
|[setTrustServerCertificate](../../../connect/jdbc/reference/settrustservercertificate-method-sqlserverdatasource.md)|Establece un **booleano** valor que indica si la propiedad trustServerCertificate está habilitada.|  
|[setTrustStore](../../../connect/jdbc/reference/settruststore-method-sqlserverdatasource.md)|Establece la ruta de acceso (incluido el nombre de archivo) del archivo trustStore del certificado.|  
|[setTrustStorePassword](../../../connect/jdbc/reference/settruststorepassword-method-sqlserverdatasource.md)|Establece la contraseña que se usa para comprobar la integridad de los datos trustStore.|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md)|Establece la dirección URL que se utiliza para la conexión al origen de datos.|  
|[setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md)|Establece el nombre de usuario usado para conectar al origen de datos.|  
|[setWorkstationID](../../../connect/jdbc/reference/setworkstationid-method-sqlserverdatasource.md)|Establece el nombre del nombre del equipo cliente que se utiliza para la conexión al origen de datos.|  
|[setXopenStates](../../../connect/jdbc/reference/setxopenstates-method-sqlserverdatasource.md)|Establece un **booleano** valor que indica si está habilitada la conversión de Estados SQL Estados conformes a XOPEN.|  
|[Unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverdatasource.md)|Devuelve un objeto que implementa la interfaz especificada para permitir el acceso a la [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-métodos específicos.|  
  
## <a name="inherited-methods"></a>Métodos heredados  
  
|Clase heredada de:|Métodos|  
|---------------------------|-------------|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
  
## <a name="see-also"></a>Vea también  
 [Clase SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)  
  
  
