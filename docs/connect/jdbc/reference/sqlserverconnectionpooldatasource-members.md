---
title: Los miembros de SQLServerConnectionPoolDataSource | Documentos de Microsoft
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
ms.topic: article
ms.assetid: dac0337e-8088-488c-a25a-801a2190f6ca
caps.latest.revision: 25
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5baf7d403430f7021b9edfa7f706c4159e38bb4f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sqlserverconnectionpooldatasource-members"></a>Miembros SQLServerConnectionPoolDataSource
[!INCLUDE[Driver_JDBC_Download](../../../includes/driver_jdbc_download.md)]

  Las siguientes tablas enumeran los miembros expuestos por el [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md) clase.  
  
## <a name="constructors"></a>Constructores  
  
|Nombre|Description|  
|----------|-----------------|  
|[(De SQLServerConnectionPoolDataSource)](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-constructor.md)|Inicializa una nueva instancia de la [SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md) clase.|  
  
## <a name="fields"></a>Campos  
 Ninguno.  
  
## <a name="inherited-fields"></a>Campos heredados  
 Ninguno.  
  
## <a name="methods"></a>Métodos  
  
|Nombre|Description|  
|----------|-----------------|  
|[getApplicationIntent](../../../connect/jdbc/reference/getapplicationintent-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) devuelve el valor de la **applicationIntent** propiedad de conexión.|  
|[getApplicationName](../../../connect/jdbc/reference/getapplicationname-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) devuelve el nombre de la aplicación.|  
|[getConnection](../../../connect/jdbc/reference/getconnection-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) intenta establecer una conexión con el origen de datos que representa este objeto de origen de datos.|  
|[GetDatabaseName](../../../connect/jdbc/reference/getdatabasename-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) devuelve el nombre de la base de datos.|  
|[GetDescription](../../../connect/jdbc/reference/getdescription-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) devuelve una descripción del origen de datos.|  
|[getFailoverPartner](../../../connect/jdbc/reference/getfailoverpartner-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) devuelve el nombre del servidor de conmutación por error que se utiliza en una configuración de creación de reflejo de la base de datos.|  
|[getInstanceName](../../../connect/jdbc/reference/getinstancename-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) devuelve el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] nombre de instancia.|  
|[getLastUpdateCount](../../../connect/jdbc/reference/getlastupdatecount-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) devuelve un **booleano** valor que indica si la propiedad lastUpdateCount está habilitada.|  
|[getLockTimeout](../../../connect/jdbc/reference/getlocktimeout-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) devuelve un **int** valor que indica el número de milisegundos que esperará la base de datos antes de informar de un tiempo de espera de bloqueo.|  
|[getLoginTimeout](../../../connect/jdbc/reference/getlogintimeout-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) devuelve el número de segundos que esperará este objeto de origen de datos al intentar establecer una conexión.|  
|[getLogWriter](../../../connect/jdbc/reference/getlogwriter-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) devuelve un flujo de salida de caracteres que se utilizará para todos los mensajes de registro y seguimiento.|  
|[getMultiSubnetFailover](../../../connect/jdbc/reference/getmultisubnetfailover-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) devuelve el valor de la **multiSubnetFailover** propiedad de conexión.|  
|[getPooledConnection](../../../connect/jdbc/reference/getpooledconnection-method-sqlserverconnectionpooldatasource.md)|Intenta establecer una conexión a bases de datos físicas que se pueda utilizar como una conexión agrupada.|  
|[getPortNumber](../../../connect/jdbc/reference/getportnumber-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) devuelve el número de puerto actual que se usa para comunicarse con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
|[GetReference](../../../connect/jdbc/reference/getreference-method-sqlserverconnectionpooldatasource.md)|Devuelve una referencia a este objeto de origen de datos.|  
|[método getSelectMethod](../../../connect/jdbc/reference/getselectmethod-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) devuelve el tipo de cursor predeterminado que se utiliza para todos los conjuntos de resultados que se crean con el objeto de origen de datos.|  
|[getSendStringParametersAsUnicode](../../../connect/jdbc/reference/getsendstringparametersasunicode-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) devuelve un **booleano** valor que indica si está habilitado el envío de parámetros de cadena al servidor en formato UNICODE.|  
|[GetServerName](../../../connect/jdbc/reference/getservername-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) devuelve el nombre del equipo que está ejecutando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
|[getURL](../../../connect/jdbc/reference/geturl-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) devuelve la dirección URL que se utiliza para conectarse al origen de datos.|  
|[GetUser](../../../connect/jdbc/reference/getuser-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) devuelve el nombre de usuario que se usa para conectarse al origen de datos.|  
|[getWorkstationID](../../../connect/jdbc/reference/getworkstationid-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) devuelve el nombre del cliente en nombre de equipo que se utiliza para conectarse al origen de datos.|  
|[getXopenStates](../../../connect/jdbc/reference/getxopenstates-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) devuelve un **booleano** valor que indica si está habilitada la conversión de Estados SQL Estados conformes a XOPEN.|  
|[isWrapperFor](../../../connect/jdbc/reference/iswrapperfor-method-sqlserverconnectionpooldatasource.md)|Indica si este objeto es un contenedor para la interfaz especificada.|  
|[setApplicationIntent](../../../connect/jdbc/reference/setapplicationintent-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) establece el valor de la **applicationIntent** propiedad de conexión.|  
|[SetApplicationName](../../../connect/jdbc/reference/setapplicationname-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) establece el nombre de la aplicación.|  
|[setAuthenticationSceme](../../../connect/jdbc/reference/setauthenticationscheme-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) indica el tipo de seguridad integrada que desea que su aplicación para que use.|  
|[setDatabaseName](../../../connect/jdbc/reference/setdatabasename-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) establece el nombre de la base de datos al que conectarse.|  
|[setDescription](../../../connect/jdbc/reference/setdescription-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) establece la descripción del origen de datos.|  
|[setFailoverPartner](../../../connect/jdbc/reference/setfailoverpartner-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) establece el nombre del servidor de conmutación por error que se utiliza en una configuración de creación de reflejo de la base de datos.|  
|[setInstanceName](../../../connect/jdbc/reference/setinstancename-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) establece el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)] nombre de instancia.|  
|[setIntegratedSecurity](../../../connect/jdbc/reference/setintegratedsecurity-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) establece un **booleano** valor que indica si la propiedad integratedSecurity está habilitada.|  
|[setLastUpdateCount](../../../connect/jdbc/reference/setlastupdatecount-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) establece un **booleano** valor que indica si la propiedad lastUpdateCount está habilitada.|  
|[setLockTimeout](../../../connect/jdbc/reference/setlocktimeout-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) establece un **int** valor que indica el número de milisegundos que transcurrirán antes de que la base de datos notifique un tiempo de espera de bloqueo.|  
|[setLoginTimeout](../../../connect/jdbc/reference/setlogintimeout-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) establece el número de segundos que esperará este objeto de origen de datos al intentar establecer una conexión.|  
|[setLogWriter](../../../connect/jdbc/reference/setlogwriter-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) establece un flujo de salida de caracteres que se utilizará para todos los mensajes de registro y seguimiento.|  
|[setMultiSubnetFailover](../../../connect/jdbc/reference/setmultisubnetfailover-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) establece el valor de la **multiSubnetFailover** propiedad de conexión.|  
|[setPassword](../../../connect/jdbc/reference/setpassword-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) establece la contraseña que se usarán para conectarse a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
|[setPortNumber](../../../connect/jdbc/reference/setportnumber-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) establece el número de puerto que se usará para comunicarse con [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
|[setSelectMethod](../../../connect/jdbc/reference/setselectmethod-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) establece el tipo de cursor predeterminado que se utiliza para todos los conjuntos de resultados que se crean con el objeto de origen de datos.|  
|[setSendStringParametersAsUnicode](../../../connect/jdbc/reference/setsendstringparametersasunicode-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) establece un **booleano** valor que indica si está habilitado el envío de parámetros de cadena al servidor en formato UNICODE.|  
|[setServerName](../../../connect/jdbc/reference/setservername-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) establece el nombre del equipo que está ejecutando [!INCLUDE[ssNoVersion](../../../includes/ssnoversion_md.md)].|  
|[setURL](../../../connect/jdbc/reference/seturl-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) establece la dirección URL que se utiliza para conectarse al origen de datos.|  
|[setUser](../../../connect/jdbc/reference/setuser-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) establece el nombre de usuario que se usa para conectarse al origen de datos.|  
|[setWorkstationID](../../../connect/jdbc/reference/setworkstationid-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) establece el cliente en nombre de equipo que se utiliza para conectarse al origen de datos.|  
|[setXopenStates](../../../connect/jdbc/reference/setxopenstates-method-sqlserverdatasource.md)|(Se hereda de [SQLServerDataSource](../../../connect/jdbc/reference/sqlserverdatasource-class.md)) establece un **booleano** valor que indica si está habilitada la conversión de Estados SQL Estados conformes a XOPEN.|  
|[Unwrap](../../../connect/jdbc/reference/unwrap-method-sqlserverconnectionpooldatasource.md)|Devuelve un objeto que implementa la interfaz especificada para permitir el acceso a la [!INCLUDE[jdbcNoVersion](../../../includes/jdbcnoversion_md.md)]-métodos específicos.|  
  
## <a name="inherited-methods"></a>Métodos heredados  
  
|Clase heredada de:|Métodos|  
|---------------------------|-------------|  
|com.microsoft.sqlserver.jdbc.SQLServerDataSource|getApplicationName, getConnection, getDatabaseName, getDescription, getFailoverPartner, getInstanceName, getLastUpdateCount, getLockTimeout, getLoginTimeout, getLogWriter, getPortNumber, getSelectMethod, getSendStringParametersAsUnicode, getServerName, getURL, getUser, getWorkstationID, getXopenStates, setApplicationName, setDatabaseName, setDescription, setFailoverPartner, setInstanceName, setIntegratedSecurity, setLastUpdateCount, setLockTimeout, setLoginTimeout, setLogWriter, setPassword, setPortNumber, setSelectMethod, setSendStringParametersAsUnicode, setServerName, setURL, setUser, setWorkstationID, setXopenStates|  
|java.lang.Object|clone, equals, finalize, getClass, hashCode, notify, notifyAll, toString, wait|  
|java.sql.Wrapper|isWrapperFor, unwrap|  
|javax.sql.ConnectionPoolDataSource|getLoginTimeout, getLogWriter, setLoginTimeout, setLogWriter, getPooledConnection|  
  
## <a name="see-also"></a>Vea también  
 [Clase SQLServerConnectionPoolDataSource](../../../connect/jdbc/reference/sqlserverconnectionpooldatasource-class.md)  
  
  
