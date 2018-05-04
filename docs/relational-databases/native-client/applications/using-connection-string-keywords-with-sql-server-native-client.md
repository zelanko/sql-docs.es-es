---
title: Usar palabras clave de cadena de conexión con SQL Server Native Client | Documentos de Microsoft
ms.custom: ''
ms.date: 08/01/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client|applications
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- sql13.swb.connecttoserver.options.registeredservers.f1
helpviewer_keywords:
- data access [SQL Server Native Client], connection string keywords
- SQLNCLI, connection string keywords
- connection strings [SQL Server Native Client]
- SQL Server Native Client, connection string keywords
ms.assetid: 16008eec-eddf-4d10-ae99-29db26ed6372
caps.latest.revision: 81
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c2fdfe3fcf63bb94ebcc10b05b2fc3894b01b623
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="using-connection-string-keywords-with-sql-server-native-client"></a>Usar palabras clave de cadena de conexión con SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Algunas API de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client usan cadenas de conexión para especificar atributos de conexión. Las cadenas de conexión son listas de palabras clave y valores asociados; cada palabra clave identifica un atributo de conexión determinado.  
  
> **Nota:** [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client permite la ambigüedad en las cadenas de conexión para mantener la compatibilidad con versiones anteriores (por ejemplo, algunas palabras clave se puede especificar más de una vez y puede permitirse palabras clave en conflicto cuya resolución en función de posición o en la prioridad). En futuras versiones de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no se permitirá la ambigüedad en las cadenas de conexión. Es recomendable modificar las aplicaciones a fin de usar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para eliminar cualquier dependencia de ambigüedad en las cadenas de conexión.  
  
 En las siguientes secciones se describen las palabras clave que pueden utilizarse con el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client y los Objetos de datos ActiveX (ADO) cuando se utiliza [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client como proveedor de datos.  
  
## <a name="odbc-driver-connection-string-keywords"></a>Palabras clave de cadena de conexión de controlador ODBC  
 Las aplicaciones ODBC utilizar cadenas de conexión como parámetros para la [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) y [SQLBrowseConnect](../../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md) funciones.  
  
 Las cadenas de conexión utilizadas por ODBC presentan la sintaxis siguiente:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[{]attribute-value[}]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 Los valores de atributo pueden incluirse opcionalmente entre llaves y es una práctica recomendable. Esto evita que se produzcan problemas cuando los valores de atributo contienen caracteres no alfanuméricos. Se supone que la primera llave de cierre del valor termina el valor, de modo que los valores no pueden contener caracteres de llave de cierre.  
  
 En la tabla siguiente se describen las palabras clave que pueden utilizarse con una cadena de conexión ODBC.  
  
|Palabra clave|Description|  
|-------------|-----------------|  
|**Addr**|Sinónimo de "Address".|  
|**Dirección**|Dirección de red del servidor en el que se ejecuta una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. **Dirección** suele ser el nombre de red del servidor, pero puede ser otros nombres como una canalización, una dirección IP o una dirección de puerto y el socket de TCP/IP.<br /><br /> Si especifica una dirección IP, asegúrese de que los protocolos TCP/IP o de canalizaciones con nombre estén habilitados en el Administrador de configuración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> El valor de **dirección** tiene prioridad sobre el valor pasado a **Server** en las cadenas de conexión de ODBC cuando se usa [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Tenga en cuenta también que `Address=;` se conectará al servidor especificado en el **Server** (palabra clave), mientras que `Address= ;, Address=.;`, `Address=localhost;`, y `Address=(local);` establecerán una conexión al servidor local.<br /><br /> La sintaxis completa de la **dirección** palabra clave es como sigue:<br /><br /> [*protocolo ***:**]* dirección *[**, *** puerto &#124;\pipe\pipename*]<br /><br /> *protocolo* puede ser **tcp** (TCP/IP), **lpc** (memoria compartida) o **np** (canalizaciones con nombre). Para obtener más información acerca de los protocolos, consulte [configurar protocolos de cliente](../../../database-engine/configure-windows/configure-client-protocols.md).<br /><br /> Si no *protocolo* ni **red** se especifica la palabra clave, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client usará el orden de protocolo especificado en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.<br /><br /> *puerto* es el puerto para conectarse a, en el servidor especificado. De forma predeterminada, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa el puerto 1433.|  
|**AnsiNPW**|Cuando es "yes", el controlador usa comportamientos definidos por ANSI para controlar las comparaciones NULL, el relleno de datos de caracteres, las advertencias y la concatenación NULL. Cuando es "no", no se exponen los comportamientos definidos por ANSI. Para obtener más información acerca de los comportamientos NPW de ANSI, vea [efectos de las opciones ISO](../../../relational-databases/native-client-odbc-queries/executing-statements/effects-of-iso-options.md).|  
|**APLICACIÓN**|Nombre de la aplicación llama a [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) (opcional). Si se especifica, este valor se almacena en la **master.dbo.sysprocesses** columna **program_name** y devuelto por [sp_who](../../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) y [APP_NAME](../../../t-sql/functions/app-name-transact-sql.md) funciones.|  
|**Intención de aplicaciones**|Declara el tipo de carga de trabajo de la aplicación al conectarse a un servidor. Los valores posibles son **ReadOnly** y **ReadWrite**. El valor predeterminado es **ReadWrite**.  Por ejemplo:<br /><br /> `ApplicationIntent=ReadOnly`<br /><br /> Para obtener más información acerca de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] compatibilidad de Native Client para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [SQL Server nativo compatibilidad del cliente con High Availability, Disaster Recovery](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).|  
|**AttachDBFileName**|Nombre del archivo principal de una base de datos adjuntable. Incluya la ruta de acceso completa y todos los caracteres de escape \ si usa una variable de cadena de caracteres de C:<br /><br /> `AttachDBFileName=c:\\MyFolder\\MyDB.mdf`<br /><br /> Esta base de datos se adjunta y se convierte en la base de datos predeterminada para la conexión. Usar **AttachDBFileName** también debe especificar el nombre de la base de datos en la vista la [SQLDriverConnect](../../../relational-databases/native-client-odbc-api/sqldriverconnect.md) parámetro de base de datos o el atributo de conexión SQL_COPT_CURRENT_CATALOG. Si la base de datos se ha adjuntado previamente, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no vuelve a adjuntarla; utiliza la base de datos adjuntada como valor predeterminado para la conexión.|  
|**AutoTranslate**|Cuando es "yes", las cadenas de caracteres ANSI enviadas entre el cliente y el servidor se traducen mediante la conversión a través de Unicode para minimizar los problemas de caracteres extendidos coincidentes entre las páginas de códigos del cliente y del servidor.<br /><br /> Datos SQL_C_CHAR del cliente enviados a un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] **char**, **varchar**, o **texto** variable, parámetro o columna se convierten de carácter a Unicode mediante la página de códigos de ANSI (ACP) de cliente, después, se convierten de Unicode a carácter mediante la ACP del servidor.<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]**char**, **varchar**, o **texto** datos enviados a una variable SQL_C_CHAR del cliente se convierten de carácter a Unicode mediante la ACP del servidor, después, se convierten de Unicode a carácter mediante la ACP del cliente.<br /><br /> El controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client realiza estas conversiones en el cliente. Esto requiere que la misma página de códigos ANSI (ACP) que se utiliza en el servidor esté disponible en el cliente.<br /><br /> Esta configuración no tiene ningún efecto en las conversiones que se realizan para estas transferencias:<br /><br /> \* Datos de cliente SQL_C_WCHAR de Unicode enviados a **char**, **varchar**, o **texto** en el servidor.<br /><br /> \* **char**, **varchar**, o **texto** datos de servidor que se envían a una variable SQL_C_WCHAR de Unicode en el cliente.<br /><br /> \* Datos de cliente SQL_C_CHAR de ANSI enviados a Unicode **nchar**, **nvarchar**, o **ntext** en el servidor.<br /><br /> \* Unicode **nchar**, **nvarchar**, o **ntext** datos de servidor que se envían a una variable ANSI SQL_C_CHAR en el cliente.<br /><br /> Cuando es "no", no se realiza la traducción de caracteres.<br /><br /> El [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC Native Client no traduce datos para SQL_C_CHAR de caracteres ANSI con cliente enviados a **char**, **varchar**, o **texto** variables, parámetros o columnas en el servidor. No se realiza ninguna traducción en **char**, **varchar**, o **texto** datos enviados desde el servidor a las variables SQL_C_CHAR del cliente.<br /><br /> Si el cliente y [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] están utilizando distintas ACP, pueden malinterpretarse los caracteres extendidos.|  
|**Base de datos**|Nombre de la base de datos de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] predeterminada para la conexión. Si **base de datos** no se especifica, se utiliza la base de datos predeterminada definida para el inicio de sesión. La base de datos predeterminada del origen de datos ODBC invalida la base de datos predeterminada definida para el inicio de sesión. La base de datos debe ser una base de datos a menos que **AttachDBFileName** también se especifica. Si **AttachDBFileName** también se especifica, se adjunta y según el nombre de base de datos especificado por el archivo principal apunta a **base de datos**.|  
|**Controlador**|Nombre del controlador devuelto por [SQLDrivers](../../../relational-databases/native-client-odbc-api/sqldrivers.md). El valor de palabra clave para el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client es "{SQL Server Native Client 11.0}". El **Server** palabra clave es necesaria si **controlador** se especifica y **DriverCompletion** está establecido en SQL_DRIVER_NOPROMPT.<br /><br /> Para obtener más información acerca de los nombres de controladores, consulte [con el encabezado de cliente nativo de SQL Server y los archivos de la biblioteca](../../../relational-databases/native-client/applications/using-the-sql-server-native-client-header-and-library-files.md).|  
|**DSN**|Nombre de un usuario de ODBC u origen de datos del sistema existente. Esta palabra clave invalida los valores que pueden especificarse en el **Server**, **red**, y **dirección** palabras clave.|  
|**Cifrar**|Especifica si los datos deben cifrarse antes de enviarse a través de la red. Los valores posibles son "yes" y "no". El valor predeterminado es "no".|  
|**Reserva**|Esta palabra clave está desusada y el controlador OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client omite su valor.|  
|**Failover_Partner**|Nombre del servidor del asociado de conmutación por error que va a utilizarse si no puede establecerse una conexión al servidor principal.|  
|**FailoverPartnerSPN**|SPN del asociado de conmutación por error. El valor predeterminado es una cadena vacía. Una cadena vacía hace que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utilice el SPN predeterminado generado por el controlador.|  
|**FileDSN**|Nombre de origen de datos de un archivo ODBC existente.|  
|**Lenguaje**|Nombre de idioma de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (opcional). [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]puede almacenar mensajes para varios idiomas en **sysmessages**. Si se conecta a un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] con varios idiomas, **lenguaje** especifica qué conjunto de mensajes que se usa para la conexión.|  
|**MARS_Connection**|Habilita o deshabilita conjuntos de resultados activos múltiples (MARS) en la conexión. Los valores reconocidos son "yes" y "no". El valor predeterminado es "no".|  
|**MultiSubnetFailover**|Especifique siempre **multiSubnetFailover = Yes** al conectarse a la escucha del grupo de disponibilidad de un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] grupo de disponibilidad o una [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instancia de clúster de conmutación por error. **multiSubnetFailover = Yes** configura [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client para proporcionar una detección más rápida y conexión con el servidor (actualmente) activo. Los valores posibles son **Yes** y **No**. El valor predeterminado es **No**. Por ejemplo:<br /><br /> `MultiSubnetFailover=Yes`<br /><br /> Para obtener más información acerca de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] compatibilidad de Native Client para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [SQL Server nativo compatibilidad del cliente con High Availability, Disaster Recovery](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).|  
|**NET**|Sinónimo de "Network".|  
|**Red**|Los valores válidos son **dbnmpntw** (canalizaciones con nombre) y **dbmssocn** (TCP/IP).<br /><br /> Es un error especificar tanto un valor para el **red** prefijo de palabra clave y un protocolo en el **Server** palabra clave.|  
|**PWD**|La contraseña para la cuenta de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que se haya especificado en el parámetro UID. **PWD** no es necesario especificar si el inicio de sesión tiene una contraseña NULL o al utilizar la autenticación de Windows (`Trusted_Connection = yes`).|  
|**QueryLog_On**|Cuando es "yes", se habilita el registro de datos de consultas de ejecución prolongada en la conexión. Cuando es "no", no se registran los datos de consultas de ejecución prolongada.|  
|**QueryLogFile**|Ruta de acceso y nombre completos del archivo que va a utilizarse para registrar los datos en consultas de ejecución prolongada.|  
|**QueryLogTime**|Cadena de caracteres de dígitos que especifica el umbral (en milisegundos) para registrar consultas de ejecución prolongada. Cualquier consulta que no obtenga una respuesta en el intervalo de tiempo especificado se escribe en el archivo de registro de consultas de ejecución prolongada.|  
|**QuotedId**|Cuando es "yes", QUOTED_IDENTIFIERS se establece en ON para la conexión; [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa las reglas ISO con respecto al uso de comillas en instrucciones SQL. Si no es así, QUOTED_IDENTIFIERS se establece en OFF para la conexión. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sigue las reglas [!INCLUDE[tsql](../../../includes/tsql-md.md)] heredadas con respecto al uso de comillas en instrucciones SQL. Para obtener más información, consulte [efectos de las opciones ISO](../../../relational-databases/native-client-odbc-queries/executing-statements/effects-of-iso-options.md).|  
|**Regional**|Cuando es "yes", el controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa la configuración del cliente para realizar conversiones de datos de moneda, fecha y hora a datos de caracteres. La conversión se realiza en un solo sentido; el controlador no reconoce los formatos estándar que no son ODBC para las cadenas de fecha o los valores de moneda incluidos; por ejemplo, un parámetro que se utiliza en una instrucción INSERT o UPDATE. Cuando es "no", el controlador utiliza cadenas estándar de ODBC para representar los datos de moneda, fecha y hora que se convierten en datos de caracteres.|  
|**SaveFile**|Nombre de un archivo de origen de datos ODBC donde se guardan los atributos de la conexión actual si la conexión se establece correctamente.|  
|**Server**|Nombre de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El valor debe ser el nombre de un servidor de la red, una dirección IP o el nombre de un alias del Administrador de configuración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> El **dirección** palabra clave invalida el **Server** palabra clave.<br /><br /> Puede conectarse a la instancia predeterminada en el servidor local especificando uno de los valores siguientes:<br /><br /> **Server =;**<br /><br /> **Server =.;**<br /><br /> **Server=(local);**<br /><br /> **Server=(local);**<br /><br /> **Server=(localhost);**<br /><br /> **Server=(LocalDB)\\**  *nombreDeInstancia* **;**<br /><br /> Para obtener más información sobre la compatibilidad con LocalDB, vea [SQL Server nativo compatibilidad del cliente con LocalDB](../../../relational-databases/native-client/features/sql-server-native-client-support-for-localdb.md).<br /><br /> Para especificar una instancia con nombre de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], anexar  **\\ ***nombreDeInstancia *.<br /><br /> Cuando se especifica ningún servidor, se realiza una conexión a la instancia predeterminada en el equipo local.<br /><br /> Si especifica una dirección IP, asegúrese de que los protocolos de canalizaciones con nombre o TCP/IP están habilitados en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.<br /><br /> La sintaxis completa de la **Server** palabra clave es como sigue:<br /> <br /> **Server =**[* protocolo***:**] *Servidor*[**, *** puerto*]<br /><br /> *protocolo* puede ser **tcp** (TCP/IP), **lpc** (memoria compartida) o **np** (canalizaciones con nombre).<br /><br /> A continuación se muestra un ejemplo de la especificación de una canalización con nombre:<br /><br /> `np:\\.\pipe\MSSQL$MYINST01\sql\query`<br /><br /> Esta línea especifica un protocolo de canalización con nombre, una canalización con nombre en el equipo local (`\\.\pipe`), el nombre de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (`MSSQL$MYINST01`) y el nombre predeterminado de la canalización con nombre (`sql/query`).<br /><br /> Si no un *protocolo* ni **red** se especifica la palabra clave, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client usará el orden de protocolo especificado en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.<br /><br /> *puerto* es el puerto para conectarse a, en el servidor especificado. De forma predeterminada, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa el puerto 1433.<br /><br /> Se omiten los espacios al principio del valor pasado a **Server** en las cadenas de conexión de ODBC cuando se usa [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|**ServerSPN**|SPN del servidor. El valor predeterminado es una cadena vacía. Una cadena vacía hace que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utilice el SPN predeterminado generado por el controlador.|  
|**StatsLog_On**|Cuando es "yes", habilita la captura de los datos de rendimiento del controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client. Cuando es "no", los datos de rendimiento del controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client no están disponibles en la conexión.|  
|**StatsLogFile**|Ruta de acceso y nombre completos del archivo utilizado para registrar las estadísticas de rendimiento del controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client.|  
|**Trusted_Connection**|Cuando es "yes", indica al controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que utilice el modo de autenticación de Windows para la validación del inicio de sesión. De lo contrario, indica al controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que utilice un nombre de usuario y una contraseña de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para la validación del inicio de sesión, y deben especificarse las palabras clave PWD y UID.|  
|**TrustServerCertificate**|Cuando se usa con **Encrypt**, habilita el cifrado mediante un certificado de servidor autofirmado.|  
|**UID**|Cuenta de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] válida. No es necesario especificar un UID cuando se utiliza la autenticación de Windows.|  
|**UseProcForPrepare**|Esta palabra clave está en desuso y su valor se omite por el [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] controlador ODBC de cliente nativo.|  
|**WSID**|Identificador de la estación de trabajo. Normalmente, se trata del nombre de red del equipo donde reside la aplicación (opcional). Si se especifica, este valor se almacena en la **master.dbo.sysprocesses** columna **hostname** y devuelto por [sp_who](../../../relational-databases/system-stored-procedures/sp-who-transact-sql.md) y [HOST_NAME](../../../t-sql/functions/host-name-transact-sql.md) función.|  
  
> **Nota:** configuración de conversión Regional se aplica a la moneda, numéricos, fecha y tipos de datos de tiempo. La configuración de conversión solo es aplicable a la conversión de salida y solo es visible cuando los valores de moneda, numéricos, de fecha o de hora se convierten en cadenas de caracteres.  
  
 El controlador ODBC de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utiliza los valores del Registro de configuración regional del usuario actual. El controlador no respeta la configuración regional del subproceso actual si la aplicación establece tras la conexión, por ejemplo, una llamada a **SetThreadLocale**.  
  
 Modificar el comportamiento regional de un origen de datos puede producir errores en la aplicación. Una aplicación que analiza cadenas de fecha y espera que las cadenas de fecha aparezcan tal y como se definen en ODBC podría verse afectada negativamente por la modificación de este valor.  
  
## <a name="ole-db-provider-connection-string-keywords"></a>Palabras clave de la cadena de conexión del proveedor OLE DB  
 Las aplicaciones OLE DB pueden inicializar los objetos de origen de datos de dos formas:  
  
-   **IDBInitialize:: Initialize**  
  
-   **IDataInitialize:: GetDatasource**  
  
 En el primer caso, se puede usar una cadena de proveedor para inicializar las propiedades de conexión estableciendo la propiedad DBPROP_INIT_PROVIDERSTRING en el conjunto de propiedades DBPROPSET_DBINIT. En el segundo caso, una cadena de inicialización puede pasarse a **IDataInitialize:: GetDatasource** método para inicializar las propiedades de conexión. Ambos métodos inicializan las mismas propiedades de conexión OLE DB, pero se utilizan conjuntos diferentes de palabras clave. El conjunto de palabras clave utilizadas por **IDataInitialize:: GetDatasource** es como mínimo la descripción de las propiedades en el grupo de propiedades de inicialización.  
  
 En cualquier configuración de cadena de proveedor que tenga una propiedad OLE DB correspondiente establecida en algún valor predeterminado o establecida explícitamente en un valor, el valor de la propiedad OLE DB invalidará la configuración de la cadena de proveedor.  
  
 Las propiedades booleanas establecidas en las cadenas de proveedor a través de los valores DBPROP_INIT_PROVIDERSTRING se establecen utilizando los valores "yes" y "no". Las propiedades booleanas establecidas en las cadenas de inicialización mediante **IDataInitialize:: GetDatasource** se establecen utilizando los valores "true" y "false".  
  
 Las aplicaciones que usan **IDataInitialize:: GetDatasource** también se puede utilizar las palabras clave utilizadas por **IDBInitialize:: Initialize** pero solo para las propiedades que no tienen un valor predeterminado. Si una aplicación utiliza tanto la **IDataInitialize:: GetDatasource** palabra clave y el **IDBInitialize:: Initialize** palabra clave en la cadena de inicialización, el **IDataInitialize:: GetDatasource** se utiliza el valor de palabra clave. Se recomienda encarecidamente que las aplicaciones no utilizan **IDBInitialize:: Initialize** palabras clave en **IDataInitialize** cadenas de conexión, como este comportamiento no se puede mantener en futuras versiones.  
  
> [!NOTE]  
>  Una cadena de conexión que se pasa a través de **IDataInitialize:: GetDatasource** se convierten en propiedades y aplica a través de **IDBProperties:: SetProperties**. Si los servicios de componente encuentran la descripción de la propiedad en **IDBProperties:: GetPropertyInfo**, esta propiedad se aplicará como una propiedad independiente. De lo contrario, se aplicará a través de la propiedad DBPROP_PROVIDERSTRING. Por ejemplo, si especifica la cadena de conexión **origen de datos = server1; Server = server2**, **origen de datos** se establecerá como una propiedad, pero **Server** pasa a una cadena de proveedor.  
  
 Si especifica varias instancias de la misma propiedad específica del proveedor, se utilizará el primer valor de la primera propiedad.  
  
 Cadenas de conexión utilizadas por las aplicaciones de OLE DB con DBPROP_INIT_PROVIDERSTRING con **IDBInitialize:: Initialize** tiene la siguiente sintaxis:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[{]attribute-value[}]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 Los valores de atributo pueden incluirse opcionalmente entre llaves y es una práctica recomendable. Esto evita que se produzcan problemas cuando los valores de atributo contienen caracteres no alfanuméricos. Se supone que la primera llave de cierre del valor termina el valor, de modo que los valores no pueden contener caracteres de llave de cierre.  
  
 Un carácter de espacio después del signo = de una palabra clave de cadena de conexión se interpretará como un literal, incluso si el valor está entre comillas.  
  
 En la tabla siguiente se describen las palabras clave que pueden utilizarse con DBPROP_INIT_PROVIDERSTRING.  
  
|Palabra clave|Propiedad de inicialización|Description|  
|-------------|-----------------------------|-----------------|  
|**Addr**|SSPROP_INIT_NETWORKADDRESS|Sinónimo de "Address".|  
|**Dirección**|SSPROP_INIT_NETWORKADDRESS|Dirección de red de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.<br /><br /> Para obtener más información acerca de la sintaxis válida para las direcciones, vea la descripción de la **dirección** palabra clave ODBC, más adelante en este tema.|  
|**APLICACIÓN**|SSPROP_INIT_APPNAME|Cadena que identifica la aplicación.|  
|**Intención de aplicaciones**|SSPROP_INIT_APPLICATIONINTENT|Declara el tipo de carga de trabajo de la aplicación al conectarse a un servidor. Los valores posibles son **ReadOnly** y **ReadWrite**.<br /><br /> El valor predeterminado es **ReadWrite**. Para obtener más información acerca de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] compatibilidad de Native Client para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [SQL Server nativo compatibilidad del cliente con High Availability, Disaster Recovery](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).|  
|**AttachDBFileName**|SSPROP_INIT_FILENAME|Nombre del archivo principal (incluido el nombre de la ruta de acceso completa) de una base de datos adjuntable. Usar **AttachDBFileName**, también debe especificar el nombre de la base de datos con la palabra clave base de datos de cadena de proveedor. Si la base de datos se ha adjuntado previamente, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no vuelve a adjuntarla (utiliza la base de datos adjuntada como valor predeterminado para la conexión).|  
|**Traducir automáticamente**|SSPROP_INIT_AUTOTRANSLATE|Sinónimo de "AutoTranslate".|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|Configura la traducción de caracteres OEM/ANSI. Los valores reconocidos son "yes" y "no".|  
|**Base de datos**|DBPROP_INIT_CATALOG|Nombre de la base de datos.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Especifica el modo de administración de tipos de datos que debe utilizarse. Los valores reconocidos son "0" para los tipos de datos del proveedor y "80" para los tipos de datos de SQL Server 2000.|  
|**Cifrar**|SSPROP_INIT_ENCRYPT|Especifica si los datos deben cifrarse antes de enviarse a través de la red. Los valores posibles son "yes" y "no". El valor predeterminado es "no".|  
|**FailoverPartner**|SSPROP_INIT_FAILOVERPARTNER|Nombre del servidor de conmutación por error utilizado para la creación de reflejo de la base de datos.|  
|**FailoverPartnerSPN**|SSPROP_INIT_FAILOVERPARTNERSPN|SPN del asociado de conmutación por error. El valor predeterminado es una cadena vacía. Una cadena vacía hace que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utilice el SPN predeterminado generado por el proveedor.|  
|**Lenguaje**|SSPROPT_INIT_CURRENTLANGUAGE|Lenguaje [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**MarsConn**|SSPROP_INIT_MARSCONNECTION|Habilita o deshabilita conjuntos de resultados activos múltiples (MARS) en la conexión si el servidor es [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o posterior. Los valores posibles son "yes" y "no". El valor predeterminado es "no".|  
|**NET**|SSPROP_INIT_NETWORKLIBRARY|Sinónimo de "Network".|  
|**Red**|SSPROP_INIT_NETWORKLIBRARY|Biblioteca de red que se utiliza para establecer una conexión a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.|  
|**Biblioteca de red**|SSPROP_INIT_NETWORKLIBRARY|Sinónimo de "Network".|  
|**Tamaño del paquete**|SSPROP_INIT_PACKETSIZE|Tamaño del paquete de red El valor predeterminado es 4096.|  
|**PersistSensitive**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Acepta las cadenas "yes" y "no" como valores. Cuando es "no", no se permite que el objeto de origen de datos conserve ninguna información confidencial de autenticación.|  
|**PWD**|DBPROP_AUTH_PASSWORD|Contraseña de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Server**|DBPROP_INIT_DATASOURCE|Nombre de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.<br /><br /> Si no se especifica, se establece una conexión a la instancia predeterminada en el equipo local.<br /><br /> Para obtener más información acerca de la sintaxis válida para las direcciones, vea la descripción de la **Server** palabra clave ODBC, en este tema.|  
|**ServerSPN**|SSPROP_INIT_SERVERSPN|SPN del servidor. El valor predeterminado es una cadena vacía. Una cadena vacía hace que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utilice el SPN predeterminado generado por el proveedor.|  
|**Timeout**|DBPROP_INIT_TIMEOUT|Cantidad de tiempo (en segundos) que hay que esperar a que se complete la inicialización del origen de datos.|  
|**Trusted_Connection**|DBPROP_AUTH_INTEGRATED|Cuando es "yes", indica al proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que utilice el modo de autenticación de Windows para la validación del inicio de sesión. De lo contrario, indica al proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client que utilice un nombre de usuario y una contraseña de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para la validación del inicio de sesión, y deben especificarse las palabras clave PWD y UID.|  
|**TrustServerCertificate**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Acepta las cadenas "yes" y "no" como valores. El valor predeterminado es "no", que significa que se validará el certificado del servidor.|  
|**UID**|DBPROP_AUTH_USERID|Nombre de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**UseProcForPrepare**|SSPROP_INIT_USEPROCFORPREP|Esta palabra clave está desusada y el proveedor OLE DB de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client omite su valor.|  
|**WSID**|SSPROP_INIT_WSID|El identificador de estación de trabajo.|  
  
 Cadenas de conexión utilizadas por las aplicaciones de OLE DB mediante **IDataInitialize:: GetDatasource** tiene la siguiente sintaxis:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[quote]attribute-value[quote]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 `quote ::= " | '`  
  
 El uso de la propiedad debe cumplir la sintaxis permitida en su ámbito.  Por ejemplo, **WSID** utiliza llaves (**{}**) caracteres de comillas y **nombre de la aplicación** solo usa (**'**) o Double (**"**) caracteres de comillas. Solo se pueden entrecomillar las propiedades de cadena. Si se intenta entrecomillar un entero o la propiedad enumerada, se producirá un error que indica que la cadena de conexión no cumple la especificación OLE DB.  
  
 Los valores de atributo pueden incluirse opcionalmente entre comillas simples o dobles, y es una práctica recomendada. Esto evita que se produzcan problemas cuando los valores contienen caracteres no alfanuméricos. El carácter de comillas que se utilice también puede aparecer en los valores, siempre y cuando aparezca duplicado.  
  
 Un carácter de espacio después del signo = de una palabra clave de cadena de conexión se interpretará como un literal, incluso si el valor está entre comillas.  
  
 Si una cadena de conexión tiene más de una de las propiedades enumeradas en la tabla siguiente, se utilizará el valor de la última propiedad.  
  
 La tabla siguiente describen las palabras clave que pueden utilizarse con **IDataInitialize:: GetDatasource**:  
  
|Palabra clave|Propiedad de inicialización|Description|  
|-------------|-----------------------------|-----------------|  
|**Application Name**|SSPROP_INIT_APPNAME|Cadena que identifica la aplicación.|  
|**Intento de aplicación**|SSPROP_INIT_APPLICATIONINTENT|Declara el tipo de carga de trabajo de la aplicación al conectarse a un servidor. Los valores posibles son **ReadOnly** y **ReadWrite**.<br /><br /> El valor predeterminado es **ReadWrite**. Para obtener más información acerca de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] compatibilidad de Native Client para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [SQL Server nativo compatibilidad del cliente con High Availability, Disaster Recovery](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).|  
|**Traducir automáticamente**|SSPROP_INIT_AUTOTRANSLATE|Sinónimo de "AutoTranslate".|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|Configura la traducción de caracteres OEM/ANSI. Los valores reconocidos son "true" y "false".|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|Cantidad de tiempo (en segundos) que hay que esperar a que se complete la inicialización del origen de datos.|  
|**Idioma actual**|SSPROPT_INIT_CURRENTLANGUAGE|Nombre del lenguaje [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Origen de datos**|DBPROP_INIT_DATASOURCE|Nombre de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.<br /><br /> Si no se especifica, se establece una conexión a la instancia predeterminada en el equipo local.<br /><br /> Para obtener más información acerca de la sintaxis válida para las direcciones, vea la descripción de la **Server** palabra clave ODBC, más adelante en este tema.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Especifica el modo de administración de tipos de datos que debe utilizarse. Los valores reconocidos son "0" para los tipos de datos del proveedor y "80" para los tipos de datos de [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)].|  
|**Failover Partner**|SSPROP_INIT_FAILOVERPARTNER|Nombre del servidor de conmutación por error utilizado para la creación de reflejo de la base de datos.|  
|**SPN de asociado de conmutación por error**|SSPROP_INIT_FAILOVERPARTNERSPN|SPN del asociado de conmutación por error. El valor predeterminado es una cadena vacía. Una cadena vacía hace que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utilice el SPN predeterminado generado por el proveedor.|  
|**Catálogo original**|DBPROP_INIT_CATALOG|Nombre de la base de datos.|  
|**Nombre de archivo inicial**|SSPROP_INIT_FILENAME|Nombre del archivo principal (incluido el nombre de la ruta de acceso completa) de una base de datos adjuntable. Usar **AttachDBFileName**, también debe especificar el nombre de la base de datos con la palabra clave base de datos de cadena de proveedor. Si la base de datos se ha adjuntado previamente, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no vuelve a adjuntarla (utiliza la base de datos adjuntada como valor predeterminado para la conexión).|  
|**Seguridad integrada**|DBPROP_AUTH_INTEGRATED|Acepta el valor "SSPI" para la autenticación de Windows.|  
|**Conexión MARS**|SSPROP_INIT_MARSCONNECTION|Habilita o deshabilita conjuntos de resultados activos múltiples (MARS) en la conexión. Los valores reconocidos son "true" y "false". El valor predeterminado es "false".|  
|**Dirección de red**|SSPROP_INIT_NETWORKADDRESS|Dirección de red de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.<br /><br /> Para obtener más información acerca de la sintaxis válida para las direcciones, vea la descripción de la **dirección** palabra clave ODBC, más adelante en este tema.|  
|**Biblioteca de red**|SSPROP_INIT_NETWORKLIBRARY|Biblioteca de red que se utiliza para establecer una conexión a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|Tamaño del paquete de red El valor predeterminado es 4096.|  
|**Contraseña**|DBPROP_AUTH_PASSWORD|Contraseña de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Persist Security Info**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Acepta las cadenas "true" y "false" como valores. Cuando es "false", el objeto de origen de datos no se permite para conservar información confidencial de autenticación|  
|**Proveedor**||Para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, debe ser "SQLNCLI11".|  
|**SPN del servidor**|SSPROP_INIT_SERVERSPN|SPN del servidor. El valor predeterminado es una cadena vacía. Una cadena vacía hace que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utilice el SPN predeterminado generado por el proveedor.|  
|**TrustServerCertificate**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Acepta las cadenas "true" y "false" como valores. El valor predeterminado es "false", que significa que se validará el certificado del servidor.|  
|**Use Encryption for Data**|SSPROP_INIT_ENCRYPT|Especifica si los datos deben cifrarse antes de enviarse a través de la red. Los valores posibles son "true" y "false". El valor predeterminado es "false".|  
|**Id. de usuario**|DBPROP_AUTH_USERID|Nombre de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Id. de estación de trabajo**|SSPROP_INIT_WSID|El identificador de estación de trabajo.|  
  
 **Tenga en cuenta** en la cadena de conexión, la propiedad "Contraseña anterior" establece SSPROP_AUTH_OLD_PASSWORD, que es la contraseña actual (posiblemente expirada) que no está disponible a través de una propiedad de cadena de proveedor.  
  
## <a name="activex-data-objects-ado-connection-string-keywords"></a>Palabras clave de la cadena de conexión Objetos de datos ActiveX (ADO)  
 Aplicaciones ADO establecen la **ConnectionString** propiedad de **ADODBConnection** objetos o proporcionar una cadena de conexión como un parámetro a la **abiertos** método de **ADODBConnection** objetos.  
  
 Las aplicaciones ADO también pueden utilizar las palabras clave utilizadas por OLE DB **IDBInitialize:: Initialize** método, pero solo para las propiedades que no tienen un valor predeterminado. Si una aplicación utiliza tanto las palabras clave de ADO y el **IDBInitialize:: Initialize** palabras clave en la cadena de inicialización, el valor de palabra clave de ADO que se utilizará. Se recomienda encarecidamente que las aplicaciones utilicen solamente palabras clave de cadena de conexión ADO.  
  
 Las cadenas de conexión utilizadas por ADO presentan la sintaxis siguiente:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=["]attribute-value["]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 Los valores de atributo pueden incluirse opcionalmente entre comillas dobles y es una práctica recomendable. Esto evita que se produzcan problemas cuando los valores contienen caracteres no alfanuméricos. Los valores de atributo no pueden incluir comillas dobles.  
  
 En la tabla siguiente se describen las palabras clave que pueden utilizarse con una cadena de conexión ADO.  
  
|Palabra clave|Propiedad de inicialización|Description|  
|-------------|-----------------------------|-----------------|  
|**Intento de aplicación**|SSPROP_INIT_APPLICATIONINTENT|Declara el tipo de carga de trabajo de la aplicación al conectarse a un servidor. Los valores posibles son **ReadOnly** y **ReadWrite**.<br /><br /> El valor predeterminado es **ReadWrite**. Para obtener más información acerca de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] compatibilidad de Native Client para [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [SQL Server nativo compatibilidad del cliente con High Availability, Disaster Recovery](../../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).|  
|**Application Name**|SSPROP_INIT_APPNAME|Cadena que identifica la aplicación.|  
|**Traducir automáticamente**|SSPROP_INIT_AUTOTRANSLATE|Sinónimo de "AutoTranslate".|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|Configura la traducción de caracteres OEM/ANSI. Los valores reconocidos son "true" y "false".|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|Cantidad de tiempo (en segundos) que hay que esperar a que se complete la inicialización del origen de datos.|  
|**Idioma actual**|SSPROPT_INIT_CURRENTLANGUAGE|Nombre del lenguaje [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Origen de datos**|DBPROP_INIT_DATASOURCE|Nombre de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.<br /><br /> Si no se especifica, se establece una conexión a la instancia predeterminada en el equipo local.<br /><br /> Para obtener más información acerca de la sintaxis válida para las direcciones, vea la descripción de la **Server** palabra clave ODBC, en este tema.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Especifica el modo de administración de tipos de datos que se utilizará. Los valores reconocidos son "0" para los tipos de datos del proveedor y "80" para los tipos de datos de SQL Server 2000.|  
|**Failover Partner**|SSPROP_INIT_FAILOVERPARTNER|Nombre del servidor de conmutación por error utilizado para la creación de reflejo de la base de datos.|  
|**SPN de asociado de conmutación por error**|SSPROP_INIT_FAILOVERPARTNERSPN|SPN del asociado de conmutación por error. El valor predeterminado es una cadena vacía. Una cadena vacía hace que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utilice el SPN predeterminado generado por el proveedor.|  
|**Catálogo original**|DBPROP_INIT_CATALOG|Nombre de la base de datos.|  
|**Nombre de archivo inicial**|SSPROP_INIT_FILENAME|Nombre del archivo principal (incluido el nombre de la ruta de acceso completa) de una base de datos adjuntable. Usar **AttachDBFileName**, también debe especificar el nombre de la base de datos con la palabra clave base de datos de cadena de proveedor. Si la base de datos se ha adjuntado previamente, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no vuelve a adjuntarla (utiliza la base de datos adjuntada como valor predeterminado para la conexión).|  
|**Seguridad integrada**|DBPROP_AUTH_INTEGRATED|Acepta el valor "SSPI" para la autenticación de Windows.|  
|**Conexión MARS**|SSPROP_INIT_MARSCONNECTION|Habilita o deshabilita conjuntos de resultados activos múltiples (MARS) en la conexión si el servidor es [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o posterior. Los valores reconocidos son "true" y "false". El valor predeterminado es "false".|  
|**Dirección de red**|SSPROP_INIT_NETWORKADDRESS|Dirección de red de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.<br /><br /> Para obtener más información acerca de la sintaxis válida para las direcciones, vea la descripción de la **dirección** palabra clave ODBC, en este tema.|  
|**Biblioteca de red**|SSPROP_INIT_NETWORKLIBRARY|Biblioteca de red que se utiliza para establecer una conexión a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|Tamaño del paquete de red El valor predeterminado es 4096.|  
|**Contraseña**|DBPROP_AUTH_PASSWORD|Contraseña de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Persist Security Info**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Acepta las cadenas "true" y "false" como valores. Cuando es "false", no se permite que el objeto de origen de datos conserve ninguna información confidencial de autenticación.|  
|**Proveedor**||Para [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client, debe ser "SQLNCLI11".|  
|**SPN del servidor**|SSPROP_INIT_SERVERSPN|SPN del servidor. El valor predeterminado es una cadena vacía. Una cadena vacía hace que [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Native Client utilice el SPN predeterminado generado por el proveedor.|  
|**TrustServerCertificate**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Acepta las cadenas "true" y "false" como valores. El valor predeterminado es "false", que significa que se validará el certificado del servidor.|  
|**Use Encryption for Data**|SSPROP_INIT_ENCRYPT|Especifica si los datos deben cifrarse antes de enviarse a través de la red. Los valores posibles son "true" y "false". El valor predeterminado es "false".|  
|**Id. de usuario**|DBPROP_AUTH_USERID|Nombre de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Id. de estación de trabajo**|SSPROP_INIT_WSID|El identificador de estación de trabajo.|  
  
 **Tenga en cuenta** en la cadena de conexión, la propiedad "Contraseña anterior" establece SSPROP_AUTH_OLD_PASSWORD, que es la contraseña actual (posiblemente expirada) que no está disponible a través de una propiedad de cadena de proveedor.  
  
## <a name="see-also"></a>Vea también  
 [Creación de aplicaciones con SQL Server Native Client](../../../relational-databases/native-client/applications/building-applications-with-sql-server-native-client.md)  
  
  
