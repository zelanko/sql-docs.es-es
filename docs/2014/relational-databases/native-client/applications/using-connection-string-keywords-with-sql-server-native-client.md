---
title: Usar palabras clave de cadena de conexión con SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client  - "database-engine" - "docset-sql-devref"
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- data access [SQL Server Native Client], connection string keywords
- SQLNCLI, connection string keywords
- connection strings [SQL Server Native Client]
- SQL Server Native Client, connection string keywords
ms.assetid: 16008eec-eddf-4d10-ae99-29db26ed6372
caps.latest.revision: 79
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 8f3c3607adf896b799bd323b834e4ae53313a679
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37429154"
---
# <a name="using-connection-string-keywords-with-sql-server-native-client"></a>Usar palabras clave de cadena de conexión con SQL Server Native Client
  Algunas API de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client usan cadenas de conexión para especificar atributos de conexión. Las cadenas de conexión son listas de palabras clave y valores asociados; cada palabra clave identifica un atributo de conexión determinado.  
  
 **Tenga en cuenta.** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client permite la ambigüedad en las cadenas de conexión para mantener la compatibilidad con versiones anteriores (por ejemplo, algunas palabras clave pueden especificarse más de una vez y pueden permitirse palabras clave en conflicto cuya resolución se base en la posición o en la prioridad). En futuras versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no se permitirá la ambigüedad en las cadenas de conexión. Es recomendable modificar las aplicaciones a fin de usar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para eliminar cualquier dependencia de ambigüedad en las cadenas de conexión.  
  
 En las siguientes secciones se describen las palabras clave que pueden utilizarse con el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client y los Objetos de datos ActiveX (ADO) cuando se utiliza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client como proveedor de datos.  
  
## <a name="odbc-driver-connection-string-keywords"></a>Palabras clave de la cadena de conexión del controlador ODBC  
 Las aplicaciones ODBC utilizar cadenas de conexión como parámetros para el [SQLDriverConnect](../../native-client-odbc-api/sqldriverconnect.md) y [SQLBrowseConnect](../../native-client-odbc-api/sqlbrowseconnect.md) funciones.  
  
 Las cadenas de conexión utilizadas por ODBC presentan la sintaxis siguiente:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[{]attribute-value[}]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 Los valores de atributo pueden incluirse opcionalmente entre llaves y es una práctica recomendable. Esto evita que se produzcan problemas cuando los valores de atributo contienen caracteres no alfanuméricos. Se supone que la primera llave de cierre del valor termina el valor, de modo que los valores no pueden contener caracteres de llave de cierre.  
  
 En la tabla siguiente se describen las palabras clave que pueden utilizarse con una cadena de conexión ODBC.  
  
|Palabra clave|Descripción|  
|-------------|-----------------|  
|`Addr`|Sinónimo de "Address".|  
|`Address`|Dirección de red del servidor en el que se ejecuta una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. `Address` suele ser el nombre de red del servidor, pero también puede ser otros nombres, como una canalización, una dirección IP o un puerto TCP/IP y una dirección de socket.<br /><br /> Si especifica una dirección IP, asegúrese de que los protocolos TCP/IP o de canalizaciones con nombre estén habilitados en el Administrador de configuración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> El valor de `Address` tiene prioridad sobre el valor que se pasa a `Server` en las cadenas de conexión ODBC cuando se utiliza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Tenga también en cuenta que `Address=;` se conectará al servidor especificado en la palabra clave `Server`, mientras que `Address= ;, Address=.;`, `Address=localhost;` y `Address=(local);` establecerán una conexión al servidor local.<br /><br /> La sintaxis completa de la palabra clave `Address` es la siguiente:<br /><br /> [*protocolo*`:`]*dirección*[`,`*puerto &#124;\pipe\pipename*]<br /><br /> *protocolo* puede ser `tcp` (TCP/IP), `lpc` (memoria compartida), o `np` (canalizaciones con nombre). Para obtener más información acerca de los protocolos, consulte [configurar protocolos de cliente](../../../database-engine/configure-windows/configure-client-protocols.md).<br /><br /> Si no *protocolo* ni `Network` se especifica la palabra clave, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client usará el orden de protocolo especificado en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.<br /><br /> *puerto* es el puerto para conectarse a, en el servidor especificado. De forma predeterminada, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa el puerto 1433.|  
|`AnsiNPW`|Cuando es "yes", el controlador usa comportamientos definidos por ANSI para controlar las comparaciones NULL, el relleno de datos de caracteres, las advertencias y la concatenación NULL. Cuando es "no", no se exponen los comportamientos definidos por ANSI. Para obtener más información acerca de los comportamientos NPW de ANSI, vea [los efectos de las opciones ISO](../../native-client-odbc-queries/executing-statements/effects-of-iso-options.md).|  
|`APP`|Nombre de la aplicación que llama [SQLDriverConnect](../../native-client-odbc-api/sqldriverconnect.md) (opcional). Si se especifica, este valor se almacena en el **master.dbo.sysprocesses** columna **program_name** y es devuelto por [sp_who](/sql/relational-databases/system-stored-procedures/sp-who-transact-sql) y [APP_NAME](/sql/t-sql/functions/app-name-transact-sql)funciones.|  
|`ApplicationIntent`|Declara el tipo de carga de trabajo de la aplicación al conectarse a un servidor. Los valores posibles son `ReadOnly` y `ReadWrite`. Por ejemplo: ApplicationIntent = ReadOnly<br /><br /> El valor predeterminado es `ReadWrite`. Para obtener más información acerca de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] compatibilidad del cliente nativo para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [SQL Server Native cliente admite para alta disponibilidad y recuperación ante desastres](../features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).|  
|`AttachDBFileName`|Nombre del archivo principal de una base de datos adjuntable. Incluya la ruta de acceso completa y todos los caracteres de escape \ si usa una variable de cadena de caracteres de C:<br /><br /> `AttachDBFileName=c:\\MyFolder\\MyDB.mdf`<br /><br /> Esta base de datos se adjunta y se convierte en la base de datos predeterminada para la conexión. Para usar `AttachDBFileName` también debe especificar el nombre de la base de datos en uno el [SQLDriverConnect](../../native-client-odbc-api/sqldriverconnect.md) parámetro de base de datos o el atributo de conexión SQL_COPT_CURRENT_CATALOG. Si la base de datos se ha adjuntado previamente, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no vuelve a adjuntarla; utiliza la base de datos adjuntada como valor predeterminado para la conexión.|  
|`AutoTranslate`|Cuando es "yes", las cadenas de caracteres ANSI enviadas entre el cliente y el servidor se traducen mediante la conversión a través de Unicode para minimizar los problemas de caracteres extendidos coincidentes entre las páginas de códigos del cliente y del servidor.<br /><br /> Datos SQL_C_CHAR del cliente enviados a un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **char**, **varchar**, o **texto** variable, parámetro o columna se convierte de carácter a Unicode mediante el cliente Página de códigos ANSI (ACP), a continuación, se convierten de Unicode a carácter mediante la ACP del servidor.<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **char**, **varchar**, o **texto** datos enviados a una variable SQL_C_CHAR del cliente se convierten de carácter a Unicode utilizando la ACP del servidor y luego se convierten de Unicode a carácter mediante el cliente ACP.<br /><br /> El controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client realiza estas conversiones en el cliente. Esto requiere que la misma página de códigos ANSI (ACP) que se utiliza en el servidor esté disponible en el cliente.<br /><br /> Esta configuración no tiene ningún efecto en las conversiones que se realizan para estas transferencias:<br /><br /> -Datos de cliente SQL_C_WCHAR de Unicode enviados a **char**, **varchar**, o **texto** en el servidor.<br />-   **char**, **varchar**, o **texto** datos enviados a una variable SQL_C_WCHAR de Unicode en el cliente del servidor.<br />-Datos de cliente SQL_C_CHAR de ANSI enviados a Unicode **nchar**, **nvarchar**, o **ntext** en el servidor.<br />-Unicode **nchar**, **nvarchar**, o **ntext** datos enviados a una variable ANSI SQL_C_CHAR en el cliente del servidor.<br /><br /> Cuando es "no", no se realiza la traducción de caracteres.<br /><br /> El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de Native Client no traduce los datos SQL_C_CHAR de caracteres cliente ANSI enviados a **char**, **varchar**, o **texto** variables, parámetros o las columnas en el servidor. Se realiza ninguna traducción en **char**, **varchar**, o **texto** datos enviados desde el servidor a las variables SQL_C_CHAR en el cliente.<br /><br /> Si el cliente y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] están utilizando distintas ACP, pueden malinterpretarse los caracteres extendidos.|  
|`Database`|Nombre de la base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] predeterminada para la conexión. Si no se especifica `Database`, se usa la base de datos predeterminada definida para el inicio de sesión. La base de datos predeterminada del origen de datos ODBC invalida la base de datos predeterminada definida para el inicio de sesión. La base de datos debe ser una base de datos existente, a menos que también se especifique `AttachDBFileName`. Si también se especifica `AttachDBFileName`, el archivo principal al que señala se adjunta y se le asigna el nombre de base de datos especificado por `Database`.|  
|`Driver`|Nombre del controlador tal como lo devuelve [SQLDrivers](../../native-client-odbc-api/sqldrivers.md). El valor de palabra clave para el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client es "{SQL Server Native Client 11.0}". Se requiere la palabra clave `Server` si se especifica `Driver` y `DriverCompletion` se establece en SQL_DRIVER_NOPROMPT.<br /><br /> Para obtener más información acerca de los nombres de controlador, consulte [con el encabezado de cliente nativo de SQL Server y los archivos de biblioteca](using-the-sql-server-native-client-header-and-library-files.md).|  
|`DSN`|Nombre de un usuario de ODBC u origen de datos del sistema existente. Esta palabra clave invalida cualquier valor que pueda haberse especificado en las palabras clave `Server`, `Network` y `Address`.|  
|`Encrypt`|Especifica si los datos deben cifrarse antes de enviarse a través de la red. Los valores posibles son "yes" y "no". El valor predeterminado es "no".|  
|`Fallback`|Esta palabra clave está desusada y el controlador OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client omite su valor.|  
|`Failover_Partner`|Nombre del servidor del asociado de conmutación por error que va a utilizarse si no puede establecerse una conexión al servidor principal.|  
|`FailoverPartnerSPN`|SPN del asociado de conmutación por error. El valor predeterminado es una cadena vacía. Una cadena vacía hace que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utilice el SPN predeterminado generado por el controlador.|  
|`FileDSN`|Nombre de origen de datos de un archivo ODBC existente.|  
|`Language`|Nombre de idioma de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (opcional). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] puede almacenar mensajes para varios idiomas en **sysmessages**. Si se conecta a [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con varios lenguajes, `Language` especifica qué conjunto de mensajes se utilizan para la conexión.|  
|`MARS_Connection`|Habilita o deshabilita conjuntos de resultados activos múltiples (MARS) en la conexión. Los valores reconocidos son "yes" y "no". El valor predeterminado es "no".|  
|`MultiSubnetFailover`|Especifique siempre `multiSubnetFailover=Yes` al conectarse a la escucha del grupo de disponibilidad de un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] grupo de disponibilidad o un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instancia en clúster de conmutación por error. `multiSubnetFailover=Yes` configura [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para proporcionar una detección más rápida del servidor (actualmente) activo y una conexión a él. Los valores posibles son `Yes` y `No`. Por ejemplo:<br /><br /> `MultiSubnetFailover=Yes`<br /><br /> El valor predeterminado es `No`. Para obtener más información acerca de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] compatibilidad del cliente nativo para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [SQL Server Native cliente admite para alta disponibilidad y recuperación ante desastres](../features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).|  
|`Net`|Sinónimo de "Network".|  
|`Network`|Los valores válidos son **dbnmpntw** (canalizaciones con nombre) y **dbmssocn** (TCP/IP).<br /><br /> Es un error especificar tanto un valor para la palabra clave `Network` como un prefijo de protocolo en la palabra clave `Server`.|  
|`PWD`|La contraseña para la cuenta de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que se haya especificado en el parámetro UID. No es necesario especificar una `PWD` si el inicio de sesión cuenta con una contraseña con valor NULL o cuando se utiliza la autenticación de Windows (`Trusted_Connection = yes`).|  
|`QueryLog_On`|Cuando es "yes", se habilita el registro de datos de consultas de ejecución prolongada en la conexión. Cuando es "no", no se registran los datos de consultas de ejecución prolongada.|  
|`QueryLogFile`|Ruta de acceso y nombre completos del archivo que va a utilizarse para registrar los datos en consultas de ejecución prolongada.|  
|`QueryLogTime`|Cadena de caracteres de dígitos que especifica el umbral (en milisegundos) para registrar consultas de ejecución prolongada. Cualquier consulta que no obtenga una respuesta en el intervalo de tiempo especificado se escribe en el archivo de registro de consultas de ejecución prolongada.|  
|`QuotedId`|Cuando es "yes", QUOTED_IDENTIFIERS se establece en ON para la conexión; [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa las reglas ISO con respecto al uso de comillas en instrucciones SQL. Si no es así, QUOTED_IDENTIFIERS se establece en OFF para la conexión. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sigue las reglas [!INCLUDE[tsql](../../../includes/tsql-md.md)] heredadas con respecto al uso de comillas en instrucciones SQL. Para obtener más información, consulte [los efectos de las opciones ISO](../../native-client-odbc-queries/executing-statements/effects-of-iso-options.md).|  
|`Regional`|Cuando es "yes", el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa la configuración del cliente para realizar conversiones de datos de moneda, fecha y hora a datos de caracteres. La conversión se realiza en un solo sentido; el controlador no reconoce los formatos estándar que no son ODBC para las cadenas de fecha o los valores de moneda incluidos; por ejemplo, un parámetro que se utiliza en una instrucción INSERT o UPDATE. Cuando es "no", el controlador utiliza cadenas estándar de ODBC para representar los datos de moneda, fecha y hora que se convierten en datos de caracteres.|  
|`SaveFile`|Nombre de un archivo de origen de datos ODBC donde se guardan los atributos de la conexión actual si la conexión se establece correctamente.|  
|`Server`|Nombre de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El valor debe ser el nombre de un servidor de la red, una dirección IP o el nombre de un alias del Administrador de configuración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> La palabra clave `Address` invalida la palabra clave `Server`.<br /><br /> Puede conectarse a la instancia predeterminada en el servidor local especificando uno de los valores siguientes:<br /><br /> -   `Server=;`<br />-   `Server=.;`<br />-   `Server=(local);`<br />-   `Server=(localhost);`<br />-   **Server=(LocalDB)\\**  *nombreDeInstancia* `;`<br /><br /> Para obtener más información sobre la compatibilidad con LocalDB, vea [SQL Server Native Client admite LocalDB](../features/sql-server-native-client-support-for-localdb.md).<br /><br /> Para especificar una instancia con nombre de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], anexar **\\*** nombreDeInstancia*.<br /><br /> Cuando no se especifica ningún servidor, se establece una conexión a la instancia predeterminada en el equipo local.<br /><br /> Si especifica una dirección IP, asegúrese de que los protocolos TCP/IP o de canalizaciones con nombre estén habilitados en el Administrador de configuración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> La sintaxis completa de la palabra clave `Server` es la siguiente:<br /><br /> `Server=`[*protocolo*`:`]*Server*[`,`*puerto*]<br /><br /> *protocolo* puede ser `tcp` (TCP/IP), `lpc` (memoria compartida), o `np` (canalizaciones con nombre).<br /><br /> A continuación se muestra un ejemplo de la especificación de una canalización con nombre:<br /><br /> `np:\\.\pipe\MSSQL$MYINST01\sql\query`<br /><br /> Esta línea especifica un protocolo de canalización con nombre, una canalización con nombre en el equipo local (`\\.\pipe`), el nombre de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (`MSSQL$MYINST01`) y el nombre predeterminado de la canalización con nombre (`sql/query`).<br /><br /> Si no un *protocolo* ni `Network` se especifica la palabra clave, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client usará el orden de protocolo especificado en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.<br /><br /> *puerto* es el puerto para conectarse a, en el servidor especificado. De forma predeterminada, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa el puerto 1433.<br /><br /> Se omiten los espacios al principio del valor pasado a `Server` en las cadenas de conexión ODBC cuando se utiliza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|`ServerSPN`|SPN del servidor. El valor predeterminado es una cadena vacía. Una cadena vacía hace que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utilice el SPN predeterminado generado por el controlador.|  
|`StatsLog_On`|Cuando es "yes", habilita la captura de los datos de rendimiento del controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Cuando es "no", los datos de rendimiento del controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no están disponibles en la conexión.|  
|`StatsLogFile`|Ruta de acceso y nombre completos del archivo utilizado para registrar las estadísticas de rendimiento del controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|`Trusted_Connection`|Cuando es "yes", indica al controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que utilice el modo de autenticación de Windows para la validación del inicio de sesión. De lo contrario, indica al controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que utilice un nombre de usuario y una contraseña de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para la validación del inicio de sesión, y deben especificarse las palabras clave PWD y UID.|  
|`TrustServerCertificate`|Cuando se utiliza con `Encrypt`, habilita el cifrado mediante un certificado de servidor autofirmado.|  
|`UID`|Cuenta de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] válida. No es necesario especificar un UID cuando se utiliza la autenticación de Windows.|  
|`UseProcForPrepare`|Esta palabra clave está en desuso y su valor se omite por el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de cliente nativo.|  
|`WSID`|Identificador de la estación de trabajo. Normalmente, se trata del nombre de red del equipo donde reside la aplicación (opcional). Si se especifica, este valor se almacena en el **master.dbo.sysprocesses** columna **hostname** y es devuelto por [sp_who](/sql/relational-databases/system-stored-procedures/sp-who-transact-sql) y [HOST_NAME](/sql/t-sql/functions/host-name-transact-sql)función.|  
  
 **Configuración de conversión regional se aplica a tipos de datos de tiempo, numérico, fecha y moneda. La configuración de conversión solo es aplicable a la salida de conversión y solo está visible y moneda, numéricos, fecha o valores de hora se convierten en cadenas de caracteres**.  
  
 El controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utiliza los valores del Registro de configuración regional del usuario actual. El controlador no respeta la configuración regional del subproceso actual si la aplicación la establece tras la conexión, por ejemplo, una llamada a **SetThreadLocale**.  
  
 Modificar el comportamiento regional de un origen de datos puede producir errores en la aplicación. Una aplicación que analiza cadenas de fecha y espera que las cadenas de fecha aparezcan tal y como se definen en ODBC podría verse afectada negativamente por la modificación de este valor.  
  
## <a name="ole-db-provider-connection-string-keywords"></a>Palabras clave de la cadena de conexión del proveedor OLE DB  
 Las aplicaciones OLE DB pueden inicializar los objetos de origen de datos de dos formas:  
  
-   **IDBInitialize:: Initialize**  
  
-   **IDataInitialize:: GetDatasource**  
  
 En el primer caso, se puede usar una cadena de proveedor para inicializar las propiedades de conexión estableciendo la propiedad DBPROP_INIT_PROVIDERSTRING en el conjunto de propiedades DBPROPSET_DBINIT. En el segundo caso, se puede pasar una cadena de inicialización para **IDataInitialize:: GetDatasource** método para inicializar las propiedades de conexión. Ambos métodos inicializan las mismas propiedades de conexión OLE DB, pero se utilizan conjuntos diferentes de palabras clave. El conjunto de palabras clave utilizadas por **IDataInitialize:: GetDatasource** es como mínimo, la descripción de las propiedades en el grupo de propiedades de inicialización.  
  
 En cualquier configuración de cadena de proveedor que tenga una propiedad OLE DB correspondiente establecida en algún valor predeterminado o establecida explícitamente en un valor, el valor de la propiedad OLE DB invalidará la configuración de la cadena de proveedor.  
  
 Las propiedades booleanas establecidas en las cadenas de proveedor a través de los valores DBPROP_INIT_PROVIDERSTRING se establecen utilizando los valores "yes" y "no". Las propiedades booleanas establecidas en las cadenas de inicialización mediante **IDataInitialize:: GetDatasource** se establecen utilizando los valores "true" y "false".  
  
 Las aplicaciones que usan **IDataInitialize:: GetDatasource** también se puede usar las palabras clave utilizadas por **IDBInitialize:: Initialize** pero solo para las propiedades que no tienen un valor predeterminado. Si una aplicación utiliza tanto la **IDataInitialize:: GetDatasource** palabra clave y el **IDBInitialize:: Initialize** palabra clave en la cadena de inicialización, el **IDataInitialize:: GetDataSource** se usa el valor de palabra clave. Se recomienda encarecidamente que las aplicaciones no utilicen **IDBInitialize:: Initialize** palabras clave en **IDataInitialize: GetDatasource** las cadenas de conexión, como este comportamiento no se mantenga en futuras versiones.  
  
 **Nota:** pasa una cadena de conexión **IDataInitialize:: GetDatasource** se convierten en propiedades y aplicarse a través de **IDBProperties:: SetProperties**. Si los servicios de componente encuentran la descripción de la propiedad en **IDBProperties:: GetPropertyInfo**, esta propiedad se aplicará como una propiedad independiente. De lo contrario, se aplicará a través de la propiedad DBPROP_PROVIDERSTRING. Por ejemplo, si especifica la cadena de conexión **origen de datos = server1; Server = server2**, `Data Source` se establecerá como una propiedad, pero `Server` pasará a una cadena de proveedor.  
  
 Si especifica varias instancias de la misma propiedad específica del proveedor, se utilizará el primer valor de la primera propiedad.  
  
 Las cadenas de conexión utilizadas por las aplicaciones OLE DB con DBPROP_INIT_PROVIDERSTRING con **IDBInitialize:: Initialize** presentan la sintaxis siguiente:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[{]attribute-value[}]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 Los valores de atributo pueden incluirse opcionalmente entre llaves y es una práctica recomendable. Esto evita que se produzcan problemas cuando los valores de atributo contienen caracteres no alfanuméricos. Se supone que la primera llave de cierre del valor termina el valor, de modo que los valores no pueden contener caracteres de llave de cierre.  
  
 Un carácter de espacio después del signo = de una palabra clave de cadena de conexión se interpretará como un literal, aun cuando el valor esté entre comillas.  
  
 En la tabla siguiente se describen las palabras clave que pueden utilizarse con DBPROP_INIT_PROVIDERSTRING.  
  
|Palabra clave|Propiedad de inicialización|Descripción|  
|-------------|-----------------------------|-----------------|  
|`Addr`|SSPROP_INIT_NETWORKADDRESS|Sinónimo de "Address".|  
|`Address`|SSPROP_INIT_NETWORKADDRESS|Dirección de red de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.<br /><br /> Para obtener más información acerca de la sintaxis válida para las direcciones, vea la descripción de la palabra clave `Address` de ODBC más adelante en este tema.|  
|`APP`|SSPROP_INIT_APPNAME|Cadena que identifica la aplicación.|  
|`ApplicationIntent`|SSPROP_INIT_APPLICATIONINTENT|Declara el tipo de carga de trabajo de la aplicación al conectarse a un servidor. Los valores posibles son `ReadOnly` y `ReadWrite`.<br /><br /> El valor predeterminado es `ReadWrite`. Para obtener más información acerca de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] compatibilidad del cliente nativo para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [SQL Server Native cliente admite para alta disponibilidad y recuperación ante desastres](../features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).|  
|`AttachDBFileName`|SSPROP_INIT_FILENAME|Nombre del archivo principal (incluido el nombre de la ruta de acceso completa) de una base de datos adjuntable. Para usar `AttachDBFileName`, debe especificar también el nombre de la base de datos con la palabra clave Database de la cadena del proveedor. Si la base de datos se ha adjuntado previamente, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no vuelve a adjuntarla (utiliza la base de datos adjuntada como valor predeterminado para la conexión).|  
|`Auto Translate`|SSPROP_INIT_AUTOTRANSLATE|Sinónimo de "AutoTranslate".|  
|`AutoTranslate`|SSPROP_INIT_AUTOTRANSLATE|Configura la traducción de caracteres OEM/ANSI. Los valores reconocidos son "yes" y "no".|  
|`Database`|DBPROP_INIT_CATALOG|Nombre de la base de datos.|  
|`DataTypeCompatibility`|SSPROP_INIT_DATATYPECOMPATIBILITY|Especifica el modo de administración de tipos de datos que debe utilizarse. Los valores reconocidos son "0" para los tipos de datos del proveedor y "80" para los tipos de datos de SQL Server 2000.|  
|`Encrypt`|SSPROP_INIT_ENCRYPT|Especifica si los datos deben cifrarse antes de enviarse a través de la red. Los valores posibles son "yes" y "no". El valor predeterminado es "no".|  
|`FailoverPartner`|SSPROP_INIT_FAILOVERPARTNER|Nombre del servidor de conmutación por error utilizado para la creación de reflejo de la base de datos.|  
|`FailoverPartnerSPN`|SSPROP_INIT_FAILOVERPARTNERSPN|SPN del asociado de conmutación por error. El valor predeterminado es una cadena vacía. Una cadena vacía hace que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utilice el SPN predeterminado generado por el proveedor.|  
|`Language`|SSPROPT_INIT_CURRENTLANGUAGE|Lenguaje [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|`MarsConn`|SSPROP_INIT_MARSCONNECTION|Habilita o deshabilita conjuntos de resultados activos múltiples (MARS) en la conexión si el servidor es [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o posterior. Los valores posibles son "yes" y "no". El valor predeterminado es "no".|  
|`Net`|SSPROP_INIT_NETWORKLIBRARY|Sinónimo de "Network".|  
|`Network`|SSPROP_INIT_NETWORKLIBRARY|Biblioteca de red que se utiliza para establecer una conexión a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.|  
|`Network Library`|SSPROP_INIT_NETWORKLIBRARY|Sinónimo de "Network".|  
|`PacketSize`|SSPROP_INIT_PACKETSIZE|Tamaño del paquete de red El valor predeterminado es 4096.|  
|`PersistSensitive`|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Acepta las cadenas "yes" y "no" como valores. Cuando es "no", no se permite que el objeto de origen de datos conserve ninguna información confidencial de autenticación.|  
|`PWD`|DBPROP_AUTH_PASSWORD|Contraseña de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|`Server`|DBPROP_INIT_DATASOURCE|Nombre de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.<br /><br /> Si no se especifica, se establece una conexión a la instancia predeterminada en el equipo local.<br /><br /> Para obtener más información acerca de la sintaxis válida para las direcciones, vea la descripción de la palabra clave `Server` de ODBC en este tema.|  
|`ServerSPN`|SSPROP_INIT_SERVERSPN|SPN del servidor. El valor predeterminado es una cadena vacía. Una cadena vacía hace que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utilice el SPN predeterminado generado por el proveedor.|  
|`Timeout`|DBPROP_INIT_TIMEOUT|Cantidad de tiempo (en segundos) que hay que esperar a que se complete la inicialización del origen de datos.|  
|`Trusted_Connection`|DBPROP_AUTH_INTEGRATED|Cuando es "yes", indica al proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que utilice el modo de autenticación de Windows para la validación del inicio de sesión. De lo contrario, indica al proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que utilice un nombre de usuario y una contraseña de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para la validación del inicio de sesión, y deben especificarse las palabras clave PWD y UID.|  
|`TrustServerCertificate`|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Acepta las cadenas "yes" y "no" como valores. El valor predeterminado es "no", que significa que se validará el certificado del servidor.|  
|`UID`|DBPROP_AUTH_USERID|Nombre de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|`UseProcForPrepare`|SSPROP_INIT_USEPROCFORPREP|Esta palabra clave está desusada y el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client omite su valor.|  
|`WSID`|SSPROP_INIT_WSID|El identificador de estación de trabajo.|  
  
 Las cadenas de conexión utilizadas por las aplicaciones OLE DB mediante **IDataInitialize:: GetDatasource** presentan la sintaxis siguiente:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[quote]attribute-value[quote]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 `quote ::= " | '`  
  
 El uso de la propiedad debe cumplir la sintaxis permitida en su ámbito.  Por ejemplo, `WSID` usa llaves (`{}`) para los caracteres de comillas y `Application Name` usa caracteres de comillas simples (`'`) o dobles (`"`). Solo se pueden entrecomillar las propiedades de cadena. Si se intenta entrecomillar un entero o la propiedad enumerada, se producirá un error que indica que la cadena de conexión no cumple la especificación OLE DB.  
  
 Los valores de atributo pueden incluirse opcionalmente entre comillas simples o dobles, y es una práctica recomendada. Esto evita que se produzcan problemas cuando los valores contienen caracteres no alfanuméricos. El carácter de comillas que se utilice también puede aparecer en los valores, siempre y cuando aparezca duplicado.  
  
 Un carácter de espacio después del signo = de una palabra clave de cadena de conexión se interpretará como un literal, aun cuando el valor esté entre comillas.  
  
 Si una cadena de conexión tiene más de una de las propiedades enumeradas en la tabla siguiente, se utilizará el valor de la última propiedad.  
  
 La tabla siguiente describen las palabras clave que pueden utilizarse con **IDataInitialize:: GetDatasource**:  
  
|Palabra clave|Propiedad de inicialización|Descripción|  
|-------------|-----------------------------|-----------------|  
|`Application Name`|SSPROP_INIT_APPNAME|Cadena que identifica la aplicación.|  
|`Application Intent`|SSPROP_INIT_APPLICATIONINTENT|Declara el tipo de carga de trabajo de la aplicación al conectarse a un servidor. Los valores posibles son `ReadOnly` y `ReadWrite`.<br /><br /> El valor predeterminado es `ReadWrite`. Para obtener más información acerca de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] compatibilidad del cliente nativo para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [SQL Server Native cliente admite para alta disponibilidad y recuperación ante desastres](../features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).|  
|`Auto Translate`|SSPROP_INIT_AUTOTRANSLATE|Sinónimo de "AutoTranslate".|  
|`AutoTranslate`|SSPROP_INIT_AUTOTRANSLATE|Configura la traducción de caracteres OEM/ANSI. Los valores reconocidos son "true" y "false".|  
|`Connect Timeout`|DBPROP_INIT_TIMEOUT|Cantidad de tiempo (en segundos) que hay que esperar a que se complete la inicialización del origen de datos.|  
|`Current Language`|SSPROPT_INIT_CURRENTLANGUAGE|Nombre del lenguaje [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|`Data Source`|DBPROP_INIT_DATASOURCE|Nombre de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.<br /><br /> Si no se especifica, se establece una conexión a la instancia predeterminada en el equipo local.<br /><br /> Para obtener más información acerca de la sintaxis válida para las direcciones, vea la descripción de la palabra clave `Server` de ODBC más adelante en este tema.|  
|`DataTypeCompatibility`|SSPROP_INIT_DATATYPECOMPATIBILITY|Especifica el modo de administración de tipos de datos que debe utilizarse. Los valores reconocidos son "0" para los tipos de datos del proveedor y "80" para los tipos de datos de [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)].|  
|`Failover Partner`|SSPROP_INIT_FAILOVERPARTNER|Nombre del servidor de conmutación por error utilizado para la creación de reflejo de la base de datos.|  
|`Failover Partner SPN`|SSPROP_INIT_FAILOVERPARTNERSPN|SPN del asociado de conmutación por error. El valor predeterminado es una cadena vacía. Una cadena vacía hace que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utilice el SPN predeterminado generado por el proveedor.|  
|`Initial Catalog`|DBPROP_INIT_CATALOG|Nombre de la base de datos.|  
|`Initial File Name`|SSPROP_INIT_FILENAME|Nombre del archivo principal (incluido el nombre de la ruta de acceso completa) de una base de datos adjuntable. Para usar `AttachDBFileName`, debe especificar también el nombre de la base de datos con la palabra clave DATABASE de la cadena del proveedor. Si la base de datos se ha adjuntado previamente, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no vuelve a adjuntarla (utiliza la base de datos adjuntada como valor predeterminado para la conexión).|  
|`Integrated Security`|DBPROP_AUTH_INTEGRATED|Acepta el valor "SSPI" para la autenticación de Windows.|  
|`MARS Connection`|SSPROP_INIT_MARSCONNECTION|Habilita o deshabilita conjuntos de resultados activos múltiples (MARS) en la conexión. Los valores reconocidos son "true" y "false". El valor predeterminado es "false".|  
|`Network Address`|SSPROP_INIT_NETWORKADDRESS|Dirección de red de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.<br /><br /> Para obtener más información acerca de la sintaxis válida para las direcciones, vea la descripción de la palabra clave `Address` de ODBC más adelante en este tema.|  
|`Network Library`|SSPROP_INIT_NETWORKLIBRARY|Biblioteca de red que se utiliza para establecer una conexión a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.|  
|`Packet Size`|SSPROP_INIT_PACKETSIZE|Tamaño del paquete de red El valor predeterminado es 4096.|  
|`Password`|DBPROP_AUTH_PASSWORD|Contraseña de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|`Persist Security Info`|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Acepta las cadenas "true" y "false" como valores. Cuando es "false", el objeto de origen de datos no se permite para conservar la información confidencial de autenticación|  
|`Provider`||Para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, debe ser "SQLNCLI11".|  
|`Server SPN`|SSPROP_INIT_SERVERSPN|SPN del servidor. El valor predeterminado es una cadena vacía. Una cadena vacía hace que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utilice el SPN predeterminado generado por el proveedor.|  
|`Trust Server Certificate`|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Acepta las cadenas "true" y "false" como valores. El valor predeterminado es "false", que significa que se validará el certificado del servidor.|  
|`Use Encryption for Data`|SSPROP_INIT_ENCRYPT|Especifica si los datos deben cifrarse antes de enviarse a través de la red. Los valores posibles son "true" y "false". El valor predeterminado es "false".|  
|`User ID`|DBPROP_AUTH_USERID|Nombre de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|`Workstation ID`|SSPROP_INIT_WSID|El identificador de estación de trabajo.|  
  
 **Tenga en cuenta** en la cadena de conexión, la propiedad "Contraseña anterior" establece SSPROP_AUTH_OLD_PASSWORD, que es la contraseña actual (posiblemente expirada) que no está disponible a través de una propiedad de cadena del proveedor.  
  
## <a name="activex-data-objects-ado-connection-string-keywords"></a>Palabras clave de la cadena de conexión Objetos de datos ActiveX (ADO)  
 Las aplicaciones ADO establecen la **ConnectionString** propiedad de **ADODBConnection** objetos o proporcionar una cadena de conexión como parámetro a la **abierto** método **ADODBConnection** objetos.  
  
 Las aplicaciones ADO también pueden usar las palabras clave utilizadas por OLE DB **IDBInitialize:: Initialize** método, pero solo para las propiedades que no tienen un valor predeterminado. Si una aplicación utiliza tanto las palabras clave de ADO y el **IDBInitialize:: Initialize** usará las palabras clave en la cadena de inicialización, el valor de palabra clave de ADO. Se recomienda encarecidamente que las aplicaciones utilicen solamente palabras clave de cadena de conexión ADO.  
  
 Las cadenas de conexión utilizadas por ADO presentan la sintaxis siguiente:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=["]attribute-value["]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 Los valores de atributo pueden incluirse opcionalmente entre comillas dobles y es una práctica recomendable. Esto evita que se produzcan problemas cuando los valores contienen caracteres no alfanuméricos. Los valores de atributo no pueden incluir comillas dobles.  
  
 En la tabla siguiente se describen las palabras clave que pueden utilizarse con una cadena de conexión ADO.  
  
|Palabra clave|Propiedad de inicialización|Descripción|  
|-------------|-----------------------------|-----------------|  
|`Application Intent`|SSPROP_INIT_APPLICATIONINTENT|Declara el tipo de carga de trabajo de la aplicación al conectarse a un servidor. Los valores posibles son `ReadOnly` y `ReadWrite`.<br /><br /> El valor predeterminado es `ReadWrite`. Para obtener más información acerca de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] compatibilidad del cliente nativo para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [SQL Server Native cliente admite para alta disponibilidad y recuperación ante desastres](../features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).|  
|`Application Name`|SSPROP_INIT_APPNAME|Cadena que identifica la aplicación.|  
|`Auto Translate`|SSPROP_INIT_AUTOTRANSLATE|Sinónimo de "AutoTranslate".|  
|`AutoTranslate`|SSPROP_INIT_AUTOTRANSLATE|Configura la traducción de caracteres OEM/ANSI. Los valores reconocidos son "true" y "false".|  
|`Connect Timeout`|DBPROP_INIT_TIMEOUT|Cantidad de tiempo (en segundos) que hay que esperar a que se complete la inicialización del origen de datos.|  
|`Current Language`|SSPROPT_INIT_CURRENTLANGUAGE|Nombre del lenguaje [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|`Data Source`|DBPROP_INIT_DATASOURCE|Nombre de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.<br /><br /> Si no se especifica, se establece una conexión a la instancia predeterminada en el equipo local.<br /><br /> Para obtener más información acerca de la sintaxis válida para las direcciones, vea la descripción de la palabra clave `Server` de ODBC en este tema.|  
|`DataTypeCompatibility`|SSPROP_INIT_DATATYPECOMPATIBILITY|Especifica el modo de administración de tipos de datos que se utilizará. Los valores reconocidos son "0" para los tipos de datos del proveedor y "80" para los tipos de datos de SQL Server 2000.|  
|`Failover Partner`|SSPROP_INIT_FAILOVERPARTNER|Nombre del servidor de conmutación por error utilizado para la creación de reflejo de la base de datos.|  
|`Failover Partner SPN`|SSPROP_INIT_FAILOVERPARTNERSPN|SPN del asociado de conmutación por error. El valor predeterminado es una cadena vacía. Una cadena vacía hace que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utilice el SPN predeterminado generado por el proveedor.|  
|`Initial Catalog`|DBPROP_INIT_CATALOG|Nombre de la base de datos.|  
|`Initial File Name`|SSPROP_INIT_FILENAME|Nombre del archivo principal (incluido el nombre de la ruta de acceso completa) de una base de datos adjuntable. Para usar `AttachDBFileName`, debe especificar también el nombre de la base de datos con la palabra clave DATABASE de la cadena del proveedor. Si la base de datos se ha adjuntado previamente, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no vuelve a adjuntarla (utiliza la base de datos adjuntada como valor predeterminado para la conexión).|  
|`Integrated Security`|DBPROP_AUTH_INTEGRATED|Acepta el valor "SSPI" para la autenticación de Windows.|  
|`MARS Connection`|SSPROP_INIT_MARSCONNECTION|Habilita o deshabilita conjuntos de resultados activos múltiples (MARS) en la conexión si el servidor es [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o posterior. Los valores reconocidos son "true" y "false". El valor predeterminado es "false".|  
|`Network Address`|SSPROP_INIT_NETWORKADDRESS|Dirección de red de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.<br /><br /> Para obtener más información acerca de la sintaxis válida para las direcciones, vea la descripción de la palabra clave `Address` de ODBC en este tema.|  
|`Network Library`|SSPROP_INIT_NETWORKLIBRARY|Biblioteca de red que se utiliza para establecer una conexión a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.|  
|`Packet Size`|SSPROP_INIT_PACKETSIZE|Tamaño del paquete de red El valor predeterminado es 4096.|  
|`Password`|DBPROP_AUTH_PASSWORD|Contraseña de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|`Persist Security Info`|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Acepta las cadenas "true" y "false" como valores. Cuando es "false", no se permite que el objeto de origen de datos conserve ninguna información confidencial de autenticación.|  
|`Provider`||Para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, debe ser "SQLNCLI11".|  
|`Server SPN`|SSPROP_INIT_SERVERSPN|SPN del servidor. El valor predeterminado es una cadena vacía. Una cadena vacía hace que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utilice el SPN predeterminado generado por el proveedor.|  
|`Trust Server Certificate`|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Acepta las cadenas "true" y "false" como valores. El valor predeterminado es "false", que significa que se validará el certificado del servidor.|  
|`Use Encryption for Data`|SSPROP_INIT_ENCRYPT|Especifica si los datos deben cifrarse antes de enviarse a través de la red. Los valores posibles son "true" y "false". El valor predeterminado es "false".|  
|`User ID`|DBPROP_AUTH_USERID|Nombre de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|`Workstation ID`|SSPROP_INIT_WSID|El identificador de estación de trabajo.|  
  
 **Tenga en cuenta** en la cadena de conexión, la propiedad "Contraseña anterior" establece SSPROP_AUTH_OLD_PASSWORD, que es la contraseña actual (posiblemente expirada) que no está disponible a través de una propiedad de cadena del proveedor.  
  
## <a name="see-also"></a>Vea también  
 [Generar aplicaciones con SQL Server Native Client](building-applications-with-sql-server-native-client.md)  
  
  
