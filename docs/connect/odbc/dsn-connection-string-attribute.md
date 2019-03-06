---
title: 'DSN y cadenas de conexión palabras clave para el controlador ODBC: SQL Server | Microsoft Docs'
ms.custom: ''
ms.date: 02/04/2019
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
ms.reviewer: MightyPen
ms.author: v-jizho2
author: karinazhou
manager: craigg
ms.openlocfilehash: e2db3b8df9ea63c16e0e96af9df42b7c22adaf80
ms.sourcegitcommit: b3d84abfa4e2922951430772c9f86dce450e4ed1
ms.translationtype: MTE75
ms.contentlocale: es-ES
ms.lasthandoff: 02/22/2019
ms.locfileid: "56662879"
---
# <a name="dsn-and-connection-string-keywords-and-attributes"></a>Atributos y palabras clave de cadena de conexión y DSN

Esta página enumera las palabras clave para las cadenas de conexión y DSN y los atributos de conexión de SQLSetConnectAttr y SQLGetConnectAttr, disponible en el controlador ODBC para SQL Server.

## <a name="supported-dsnconnection-string-keywords-and-connection-attributes"></a>Palabras clave de cadena de conexión o DSN y los atributos de conexión admitidos

En la tabla siguiente se enumera las palabras clave disponibles y los atributos para cada plataforma (L: Linux; M: Mac; W: Windows). Haga clic en la palabra clave o un atributo para obtener más detalles.

| Palabra clave de cadena de conexión y DSN | Atributo de conexión | Plataforma |
|-|-|-|
| [Addr](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [Dirección](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [AnsiNPW](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_ANSI_NPW](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssansinpw) | LMW |
| [APP](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [ApplicationIntent](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_APPLICATION_INTENT](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssapplicationintent) | LMW |
| [AttachDBFileName](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_ATTACHDBFILENAME](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssattachdbfilename) | LMW |
| [Autenticación](../../connect/odbc/dsn-connection-string-attribute.md#authentication---sqlcoptssauthentication) | [SQL_COPT_SS_AUTHENTICATION](../../connect/odbc/dsn-connection-string-attribute.md#authentication---sqlcoptssauthentication) | LMW |
| [AutoTranslate](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_TRANSLATE](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsstranslate) | LMW |
| [ColumnEncryption](../../connect/odbc/dsn-connection-string-attribute.md#columnencryption---sqlcoptsscolumnencryption) | [SQL_COPT_SS_COLUMN_ENCRYPTION](../../connect/odbc/dsn-connection-string-attribute.md#columnencryption---sqlcoptsscolumnencryption) | LMW |
| [ConnectRetryCount](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) | [SQL_COPT_SS_CONNECT_RETRY_COUNT](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) | W |
| [ConnectRetryInterval](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) | [SQL_COPT_SS_CONNECT_RETRY_INTERVAL](../../connect/odbc/windows/connection-resiliency-in-the-windows-odbc-driver.md) | W |
| [Base de datos](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_ATTR_CURRENT_CATALOG](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| [Descripción](../../connect/odbc/dsn-connection-string-attribute.md#description) | | LMW |
| [Controlador](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [DSN](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [Encrypt](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_ENCRYPT](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssencrypt) | LMW |
| [Failover_Partner](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_FAILOVER_PARTNER](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssfailoverpartner) | W |
| [FailoverPartnerSPN](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_FAILOVER_PARTNER_SPN](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md) | W |
| [FileDSN](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [KeystoreAuthentication](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#connection-string-keywords) | | LMW |
| [KeystorePrincipalId](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#connection-string-keywords) | | LMW |
| [KeystoreSecret](../../connect/odbc/using-always-encrypted-with-the-odbc-driver.md#connection-string-keywords) | | LMW |
| [Lenguaje](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [MARS_Connection](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_MARS_ENABLED](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssmarsenabled) | LMW |
| [MultiSubnetFailover](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_MULTISUBNET_FAILOVER](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssmultisubnetfailover) | LMW |
| [Net](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [Network](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [PWD](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [QueryLog_On](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_QUERY](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfquery) | W |
| [QueryLogFile](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_QUERY_LOG](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfquerylog) | W |
| [QueryLogTIme](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_QUERY_INTERVAL](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfqueryinterval) | W |
| [QuotedId](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_QUOTED_IDENT](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssquotedident) | LMW |
| [Regional](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [SaveFile](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [Server](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [ServerSPN](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_SERVER_SPN](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md) | LMW |
| [StatsLog_On](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_DATA](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfdata) | W |
| [StatsLogFile](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_PERF_DATA_LOG](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfdatalog) | W |
| [TransparentNetworkIPResolution](../../connect/odbc/dsn-connection-string-attribute.md#transparentnetworkipresolution---sqlcoptsstnir) | [SQL_COPT_SS_TNIR](../../connect/odbc/dsn-connection-string-attribute.md#transparentnetworkipresolution---sqlcoptsstnir) | LMW |
| [Trusted_Connection](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_INTEGRATED_SECURITY](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssintegratedsecurity) | LMW |
| [TrustServerCertificate](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | [SQL_COPT_SS_TRUST_SERVER_CERTIFICATE](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsstrustservercertificate) | LMW |
| [UID](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| [UseFMTONLY](../../connect/odbc/dsn-connection-string-attribute.md#usefmtonly) | | LMW |
| [WSID](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) | | LMW |
| | [SQL_ATTR_ACCESS_MODE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_ACCESS_MODE) | LMW |
| | [SQL_ATTR_ASYNC_DBC_EVENT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | W |
| | [SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | W |
| | [SQL_ATTR_ASYNC_DBC_PCALLBACK](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | W |
| | [SQL_ATTR_ASYNC_DBC_PCONTEXT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | W |
| | [SQL_ATTR_ASYNC_ENABLE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | W |
| | [SQL_ATTR_AUTO_IPD](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| | [SQL_ATTR_AUTOCOMMIT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_AUTOCOMMIT) | LMW |
| | [SQL_ATTR_CONNECTION_DEAD](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| | [SQL_ATTR_CONNECTION_TIMEOUT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| | [SQL_ATTR_DBC_INFO_TOKEN](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| | [SQL_ATTR_LOGIN_TIMEOUT](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_LOGIN_TIMEOUT) | LMW |
| | [SQL_ATTR_METADATA_ID](../../odbc/reference/syntax/sqlsetconnectattr-function.md) | LMW |
| | [SQL_ATTR_ODBC_CURSORS](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_ODBC_CURSORS) | LMW |
| | [SQL_ATTR_PACKET_SIZE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_PACKET_SIZE) | LMW |
| | [SQL_ATTR_QUIET_MODE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_QUIET_MODE) | LMW |
| | [SQL_ATTR_RESET_CONNECTION](../../odbc/reference/develop-driver/upgrading-a-3-5-driver-to-a-3-8-driver.md#connection-pooling) <br> (SQL_COPT_SS_RESET_CONNECTION) | LMW |  
| | [SQL_ATTR_TRACE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_OPT_TRACE) | LMW |
| | [SQL_ATTR_TRACEFILE](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_OPT_TRACEFILE) | LMW |
| | [SQL_ATTR_TRANSLATE_LIB](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_TRANSLATE_DLL) | LMW |
| | [SQL_ATTR_TRANSLATE_OPTION](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_TRANSLATE_OPTION) | LMW |
| | [SQL_ATTR_TXN_ISOLATION](../../odbc/reference/syntax/sqlsetconnectattr-function.md) <br> (SQL_TXN_ISOLATION) | LMW |
| | [SQL_COPT_SS_ACCESS_TOKEN](dsn-connection-string-attribute.md#sqlcoptssaccesstoken) | LMW |
| | [SQL_COPT_SS_ANSI_OEM](dsn-connection-string-attribute.md#sqlcoptssansioem)| W |
| | [SQL_COPT_SS_BCP](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssbcp) | LMW |
| | [SQL_COPT_SS_BROWSE_CACHE_DATA](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md) | LMW |
| | [SQL_COPT_SS_BROWSE_CONNECT](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssbrowseconnect) | LMW |
| | [SQL_COPT_SS_BROWSE_SERVER](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssbrowseserver) | LMW |
| | [SQL_COPT_SS_CEKEYSTOREDATA](dsn-connection-string-attribute.md#sqlcoptsscekeystoredata) | LMW |
| | [SQL_COPT_SS_CEKEYSTOREPROVIDER](dsn-connection-string-attribute.md#sqlcoptsscekeystoreprovider) | LMW |
| | [SQL_COPT_SS_CLIENT_CONNECTION_ID](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) | LMW |
| | [SQL_COPT_SS_CONCAT_NULL](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssconcatnull) | LMW |
| | [SQL_COPT_SS_CONNECTION_DEAD](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssconnectiondead) | LMW |
| | [SQL_COPT_SS_ENLIST_IN_DTC](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssenlistindtc) | W |
| | [SQL_COPT_SS_ENLIST_IN_XA](dsn-connection-string-attribute.md#sql_copt_ss_enlist_in_xa) | LMW |
| | [SQL_COPT_SS_FALLBACK_CONNECT](dsn-connection-string-attribute.md#sqlcoptssfallbackconnect) | LMW |
| | [SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md) | LMW |
| | [SQL_COPT_SS_MUTUALLY_AUTHENTICATED](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md) | LMW |
| | [SQL_COPT_SS_OLDPWD](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssoldpwd) | LMW |
| | [SQL_COPT_SS_PERF_DATA_LOG_NOW](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssperfdatalognow) | W |
| | [SQL_COPT_SS_PRESERVE_CURSORS](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsspreservecursors) | LMW |
| | [SQL_COPT_SS_TXN_ISOLATION](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsstxnisolation) | LMW |
| | [SQL_COPT_SS_USER_DATA](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptssuserdata) | LMW |
| | [SQL_COPT_SS_WARN_ON_CP_ERROR](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md#sqlcoptsswarnoncperror) | LMW |


Estas son algunas palabras clave de cadena de conexión y los atributos de conexión que no están documentados en [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md), [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) y [Función SQLSetConnectAttr](../../odbc/reference/syntax/sqlsetconnectattr-function.md).

### <a name="description"></a>Descripción

Se utiliza para describir el origen de datos.

### <a name="sqlcoptssansioem"></a>SQL_COPT_SS_ANSI_OEM

Controles de ANSI para la conversión de datos de OEM. 

| Valor del atributo | Descripción |
|-|-|
| SQL_AO_OFF | (Valor predeterminado) No se realiza la traducción. |
| SQL_AO_ON | Se realiza la traducción. |

### <a name="sqlcoptssfallbackconnect"></a>SQL_COPT_SS_FALLBACK_CONNECT

Controla el uso de conexiones de SQL Server reserva. Ésta ya no se admite.

| Valor del atributo | Descripción |
|-|-|
| SQL_FB_OFF | (Valor predeterminado) Reserva conexiones están deshabilitadas. |
| SQL_FB_ON | Se habilitan las conexiones de reserva. |



## <a name="new-connection-string-keywords-and-connection-attributes"></a>Nuevas palabras clave de cadena de conexión y los atributos de conexión

###  <a name="authentication---sqlcoptssauthentication"></a>Autenticación: SQL_COPT_SS_AUTHENTICATION

Establece el modo de autenticación que se utilizará al conectarse a SQL Server. Consulte [mediante Azure Active Directory](using-azure-active-directory.md) para obtener más información.

| Valor de palabra clave | Valor del atributo | Descripción |
|-|-|-|
| |SQL_AU_NONE|(Valor predeterminado) No se ha establecido. Combinación de otros atributos determina el modo de autenticación.|
|SqlPassword|SQL_AU_PASSWORD|Autenticación de SQL Server con nombre de usuario y contraseña.|
|ActiveDirectoryIntegrated|SQL_AU_AD_INTEGRATED|Autenticación integrada de Azure Active Directory.|
|ActiveDirectoryPassword|SQL_AU_AD_PASSWORD|Autenticación de contraseña de Azure Active Directory.|
|ActiveDirectoryInteractive|SQL_AU_AD_INTERACTIVE|Autenticación interactiva de Azure Active Directory.|
|ActiveDirectoryMsi|SQL_AU_AD_MSI|Autenticación de Azure Active Directory Managed Service Identity. Para la identidad asignada por el usuario, UID se establece en el identificador de objeto de la identidad del usuario. |
| |SQL_AU_RESET|Anular. Invalida cualquier DSN o la configuración de la cadena de conexión.|

> [!NOTE]
> Cuando se usa `Authentication` palabra clave o un atributo, especifique explícitamente `Encrypt` si se establece en el valor deseado en la cadena de conexión o DSN / atributo de conexión. Consulte [Using Connection String Keywords with SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md) para obtener más información.

### <a name="columnencryption---sqlcoptsscolumnencryption"></a>ColumnEncryption - SQL_COPT_SS_COLUMN_ENCRYPTION

Controla el cifrado transparente de columna (Always Encrypted). Consulte [utilizando cifrado siempre (ODBC)](using-always-encrypted-with-the-odbc-driver.md) para obtener más información.

| Valor de palabra clave | Valor del atributo | Descripción |
|-|-|-|
|Habilitado|SQL_CE_ENABLED|Habilita siempre cifrado.|
|Deshabilitado|SQL_CE_DISABLED|(Valor predeterminado) Deshabilita siempre cifrado.|
| |SQL_CE_RESULTSETONLY|Habilita el descifrado solo (los resultados y valores devueltos).|

### <a name="transparentnetworkipresolution---sqlcoptsstnir"></a>TransparentNetworkIPResolution - SQL_COPT_SS_TNIR

Intentos de los controles de la característica de resolución de direcciones IP de red transparente, que interactúa con MultiSubnetFailover para permitir una reconexión más rápida. Consulte [utilizando resolución de direcciones IP de red transparente](using-transparent-network-ip-resolution.md) para obtener más información.

| Valor de palabra clave | Valor del atributo| Descripción |
|-|-|-|
|Sí|SQL_IS_ON|(Predeterminado) Habilita la resolución de IP de red transparente.|
|No|SQL_IS_OFF|Deshabilita la resolución de IP de red transparente.|

### <a name="usefmtonly"></a>UseFMTONLY

Controla el uso de SET FMTONLY para los metadatos cuando se conecta a SQL Server 2012 y versiones más recientes.

| Valor de palabra clave | Descripción |
|-|-|
|No|(Valor predeterminado) Si está disponible, utilice sp_describe_first_result_set para metadatos. |
|Sí| Use SET FMTONLY para metadatos. |

### <a name="sqlcoptssaccesstoken"></a>SQL_COPT_SS_ACCESS_TOKEN

Permite el uso de un token de acceso de Azure Active Directory para la autenticación. Consulte [mediante Azure Active Directory](using-azure-active-directory.md) para obtener más información.

| Valor del atributo | Descripción |
|-|-|
| NULL | (Valor predeterminado) No se proporciona ningún token de acceso. |
| ACCESSTOKEN* | Puntero a un token de acceso. |

### <a name="sqlcoptsscekeystoredata"></a>SQL_COPT_SS_CEKEYSTOREDATA

Se comunica con una biblioteca de proveedor de almacén de claves de carga. Vea controles del cifrado transparente de columna (Always Encrypted). Este atributo tiene ningún valor predeterminado. Consulte [proveedores de almacén de claves personalizados](custom-keystore-providers.md) para obtener más información.

| Valor del atributo | Descripción |
|-|-|
| CEKEYSTOREDATA * | Estructura de datos de comunicación para la biblioteca de proveedor de almacén de claves |

### <a name="sqlcoptsscekeystoreprovider"></a>SQL_COPT_SS_CEKEYSTOREPROVIDER

Carga una biblioteca de proveedor de almacén de claves de Always Encrypted o recupera los nombres de bibliotecas de proveedor de almacén de claves de carga. Consulte [proveedores de almacén de claves personalizados](custom-keystore-providers.md) para obtener más información. Este atributo tiene ningún valor predeterminado.

| Valor del atributo | Descripción |
|-|-|
| char * | Ruta de acceso a una biblioteca de proveedor de almacén de claves |

### <a name="sqlcoptssenlistinxa"></a>SQL_COPT_SS_ENLIST_IN_XA

Para habilitar transacciones XA con un procesador de transacciones (TP) compatible con XA, la aplicación necesita llamar a **SQLSetConnectAttr** con sql_copt_ss_enlist_in_xa establecido y un puntero a un `XACALLPARAM` objeto. Esta opción se admite en Windows, Linux (17.3 y versiones posteriores) y Mac.
```
SQLSetConnectAttr(hdbc, SQL_COPT_SS_ENLIST_IN_XA, param, SQL_IS_POINTER);  // XACALLPARAM *param
``` 
 Para asociar una conexión ODBC solo una transacción de XA, proporcionar verdadero o falso con sql_copt_ss_enlist_in_xa establecido en lugar del puntero al llamar a **SQLSetConnectAttr**. Esto solo es válido en Windows y no se puede usar para especificar las operaciones de XA a través de una aplicación cliente. 
 ```
SQLSetConnectAttr(hdbc, SQL_COPT_SS_ENLIST_IN_XA, (SQLPOINTER)TRUE, 0);
``` 

|Valor|Descripción|Plataformas|  
|-----------|-----------------|-----------------|  
|Objeto XACALLPARAM *|El puntero al objeto `XACALLPARAM`.|Windows, Linux y Mac|
|TRUE|Asocia la transacción XA a la conexión ODBC. Todas las actividades de base de datos relacionadas se realizarán bajo la protección de la transacción XA.|Windows|  
|FALSE|Desasocia la transacción con la conexión ODBC.|Windows|

 Consulte [uso de transacciones XA](../../connect/odbc/use-xa-with-dtc.md) para obtener más información acerca de las transacciones XA.
