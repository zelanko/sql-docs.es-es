---
title: Usar palabras clave de cadena de conexión con el controlador OLE DB para SQL Server | Documentos de Microsoft
description: Usar palabras clave de cadena de conexión con el controlador OLE DB para SQL Server
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb|applications
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
f1_keywords:
- sql13.swb.connecttoserver.options.registeredservers.f1
helpviewer_keywords:
- data access [OLE DB Driver for SQL Server], connection string keywords
- MSOLEDBSQL, connection string keywords
- connection strings [OLE DB Driver for SQL Server]
- OLE DB Driver for SQL Server, connection string keywords
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.workload: Active
ms.openlocfilehash: f4ac4a2231ea983e93c9c418bdd309cf45ed6cc2
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="using-connection-string-keywords-with-ole-db-driver-for-sql-server"></a>Usar palabras clave de cadena de conexión con el controlador OLE DB para SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Algún controlador OLE DB para las API de SQL Server utilizan las cadenas de conexión para especificar atributos de conexión. Las cadenas de conexión son listas de palabras clave y valores asociados; cada palabra clave identifica un atributo de conexión determinado.  
  
> **Nota:** controlador OLE DB para SQL Server permite la ambigüedad en las cadenas de conexión para mantener la compatibilidad con versiones anteriores (por ejemplo, algunas palabras clave se puede especificar más de una vez y puede permitirse palabras clave en conflicto cuya resolución se base en la posición o prioridad). Las versiones futuras del controlador de OLE DB para SQL Server quizás no permitan ambigüedad en las cadenas de conexión. Es recomendable para modificar las aplicaciones para usar el controlador OLE DB para SQL Server para eliminar cualquier dependencia de ambigüedad de la cadena de conexión.  
  
 Las secciones siguientes describen las palabras clave que pueden usarse con el controlador OLE DB para SQL Server y ActiveX Data Objects (ADO) cuando se usa el controlador OLE DB para SQL Server como el proveedor de datos.  

  
## <a name="ole-db-driver-connection-string-keywords"></a>Palabras de clave de cadena de conexión de controlador OLE DB  
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
|**Dirección**|SSPROP_INIT_NETWORKADDRESS|Dirección de red del servidor en el que se ejecuta una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. **Dirección** suele ser el nombre de red del servidor, pero puede ser otros nombres como una canalización, una dirección IP o una dirección de puerto y el socket de TCP/IP.<br /><br /> Si especifica una dirección IP, asegúrese de que los protocolos TCP/IP o de canalizaciones con nombre estén habilitados en el Administrador de configuración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> El valor de **dirección** tiene prioridad sobre el valor pasado a **Server** en cadenas de conexión cuando se utiliza el controlador OLE DB para SQL Server. Tenga en cuenta también que `Address=;` se conectará al servidor especificado en el **Server** (palabra clave), mientras que `Address= ;, Address=.;`, `Address=localhost;`, y `Address=(local);` establecerán una conexión al servidor local.<br /><br /> La sintaxis completa de la **dirección** palabra clave es como sigue:<br /><br /> [*protocolo ***:**]* dirección *[**, *** puerto &#124;\pipe\pipename*]<br /><br /> *protocolo* puede ser **tcp** (TCP/IP), **lpc** (memoria compartida) o **np** (canalizaciones con nombre). Para obtener más información acerca de los protocolos, consulte [configurar protocolos de cliente](../../../database-engine/configure-windows/configure-client-protocols.md).<br /><br /> Si no *protocolo* ni **red** se especifica la palabra clave, el controlador OLE DB para SQL Server utilizará el orden de protocolo especificado en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.<br /><br /> *puerto* es el puerto para conectarse a, en el servidor especificado. De forma predeterminada, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa el puerto 1433.|   
|**APLICACIÓN**|SSPROP_INIT_APPNAME|Cadena que identifica la aplicación.|  
|**Intención de aplicaciones**|SSPROP_INIT_APPLICATIONINTENT|Declara el tipo de carga de trabajo de la aplicación al conectarse a un servidor. Los valores posibles son **ReadOnly** y **ReadWrite**.<br /><br /> El valor predeterminado es **ReadWrite**. Para obtener más información sobre el controlador OLE DB para la compatibilidad de SQL Server de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [controlador OLE DB para SQL Server admite alta disponibilidad, recuperación ante desastres](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**AttachDBFileName**|SSPROP_INIT_FILENAME|Nombre del archivo principal (incluido el nombre de la ruta de acceso completa) de una base de datos adjuntable. Usar **AttachDBFileName**, también debe especificar el nombre de la base de datos con la palabra clave base de datos de cadena de proveedor. Si la base de datos se ha adjuntado previamente, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no vuelve a adjuntarla (utiliza la base de datos adjuntada como valor predeterminado para la conexión).|  
|**Traducir automáticamente**|SSPROP_INIT_AUTOTRANSLATE|Sinónimo de "AutoTranslate".|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|Configura la traducción de caracteres OEM/ANSI. Los valores reconocidos son "yes" y "no".|  
|**Base de datos**|DBPROP_INIT_CATALOG|Nombre de la base de datos.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Especifica el modo de administración de tipos de datos que debe utilizarse. Los valores reconocidos son "0" para los tipos de datos del proveedor y "80" para los tipos de datos de SQL Server 2000.|  
|**Cifrar**|SSPROP_INIT_ENCRYPT|Especifica si los datos deben cifrarse antes de enviarse a través de la red. Los valores posibles son "yes" y "no". El valor predeterminado es "no".|  
|**FailoverPartner**|SSPROP_INIT_FAILOVERPARTNER|Nombre del servidor de conmutación por error utilizado para la creación de reflejo de la base de datos.|  
|**FailoverPartnerSPN**|SSPROP_INIT_FAILOVERPARTNERSPN|SPN del asociado de conmutación por error. El valor predeterminado es una cadena vacía. Una cadena vacía hace el controlador OLE DB para SQL Server para utilizar el valor predeterminado, SPN generado por proveedor.|  
|**Lenguaje**|SSPROPT_INIT_CURRENTLANGUAGE|Lenguaje [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**MarsConn**|SSPROP_INIT_MARSCONNECTION|Habilita o deshabilita conjuntos de resultados activos múltiples (MARS) en la conexión si el servidor es [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o posterior. Los valores posibles son "yes" y "no". El valor predeterminado es "no".|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|Especifique siempre **MultiSubnetFailover = Yes** al conectarse a la escucha del grupo de disponibilidad de un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] grupo de disponibilidad o una [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instancia de clúster de conmutación por error. **MultiSubnetFailover = Yes** configura el controlador OLE DB para SQL Server proporcionar una detección más rápida y conexión con el servidor (actualmente) activo. Los valores posibles son **Yes** y **No**. El valor predeterminado es **No**. Por ejemplo:<br /><br /> `MultiSubnetFailover=Yes`<br /><br /> Para obtener más información sobre el controlador OLE DB para la compatibilidad de SQL Server de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [controlador OLE DB para SQL Server admite alta disponibilidad, recuperación ante desastres](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**NET**|SSPROP_INIT_NETWORKLIBRARY|Sinónimo de "Network".|  
|**Red**|SSPROP_INIT_NETWORKLIBRARY|Biblioteca de red que se utiliza para establecer una conexión a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.|  
|**Biblioteca de red**|SSPROP_INIT_NETWORKLIBRARY|Sinónimo de "Network".|  
|**Tamaño del paquete**|SSPROP_INIT_PACKETSIZE|Tamaño del paquete de red El valor predeterminado es 4096.|  
|**PersistSensitive**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Acepta las cadenas "yes" y "no" como valores. Cuando es "no", no se permite que el objeto de origen de datos conserve ninguna información confidencial de autenticación.|  
|**PWD**|DBPROP_AUTH_PASSWORD|Contraseña de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Server**|DBPROP_INIT_DATASOURCE|Nombre de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. El valor debe ser el nombre de un servidor de la red, una dirección IP o el nombre de un alias del Administrador de configuración de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].<br /><br /> Si no se especifica, se establece una conexión a la instancia predeterminada en el equipo local.<br /><br /> El **dirección** palabra clave invalida el **Server** palabra clave.<br /><br /> Puede conectarse a la instancia predeterminada en el servidor local especificando uno de los valores siguientes:<br /><br /> **Server =;**<br /><br /> **Server =.;**<br /><br /> **Server=(local);**<br /><br /> **Server=(local);**<br /><br /> **Server=(localhost);**<br /><br /> **Server=(LocalDB)\\**  *nombreDeInstancia* **;**<br /><br /> Para obtener más información sobre la compatibilidad con LocalDB, vea [controlador OLE DB para SQL Server admite LocalDB](../../oledb/features/oledb-driver-for-sql-server-support-for-localdb.md).<br /><br /> Para especificar una instancia con nombre de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], anexar  **\\ ***nombreDeInstancia *.<br /><br /> Cuando se especifica ningún servidor, se realiza una conexión a la instancia predeterminada en el equipo local.<br /><br /> Si especifica una dirección IP, asegúrese de que los protocolos de canalizaciones con nombre o TCP/IP están habilitados en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.<br /><br /> La sintaxis completa de la **Server** palabra clave es como sigue:<br /> <br /> **Server =**[* protocolo***:**] *Servidor*[**, *** puerto*]<br /><br /> *protocolo* puede ser **tcp** (TCP/IP), **lpc** (memoria compartida) o **np** (canalizaciones con nombre).<br /><br /> A continuación se muestra un ejemplo de la especificación de una canalización con nombre:<br /><br /> `np:\\.\pipe\MSSQL$MYINST01\sql\query`<br /><br /> Esta línea especifica un protocolo de canalización con nombre, una canalización con nombre en el equipo local (`\\.\pipe`), el nombre de la instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (`MSSQL$MYINST01`) y el nombre predeterminado de la canalización con nombre (`sql/query`).<br /><br /> Si no un *protocolo* ni **red** se especifica la palabra clave, el controlador OLE DB para SQL Server utilizará el orden de protocolo especificado en [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Configuration Manager.<br /><br /> *puerto* es el puerto para conectarse a, en el servidor especificado. De forma predeterminada, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] usa el puerto 1433.<br /><br /> Se omiten los espacios al principio del valor pasado a **Server** en cadenas de conexión cuando se utiliza el controlador OLE DB para SQL Server.|   
|**ServerSPN**|SSPROP_INIT_SERVERSPN|SPN del servidor. El valor predeterminado es una cadena vacía. Una cadena vacía hace el controlador OLE DB para SQL Server para utilizar el valor predeterminado, SPN generado por proveedor.|  
|**Timeout**|DBPROP_INIT_TIMEOUT|Cantidad de tiempo (en segundos) que hay que esperar a que se complete la inicialización del origen de datos.|  
|**Trusted_Connection**|DBPROP_AUTH_INTEGRATED|Cuando indica a "yes", el controlador OLE DB para SQL Server utilizar el modo de autenticación de Windows para la validación de inicio de sesión. Lo contrario, indica el controlador OLE DB para SQL Server para utilizar un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] se deben especificar el nombre de usuario y una contraseña para la validación de inicio de sesión y las palabras clave UID y PWD.|  
|**TrustServerCertificate**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Acepta las cadenas "yes" y "no" como valores. El valor predeterminado es "no", que significa que se validará el certificado del servidor.|  
|**UID**|DBPROP_AUTH_USERID|Nombre de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**UseProcForPrepare**|SSPROP_INIT_USEPROCFORPREP|Esta palabra clave está en desuso y omite su valor por el controlador OLE DB para SQL Server.|  
|**WSID**|SSPROP_INIT_WSID|El identificador de estación de trabajo.|  
  
 Cadenas de conexión utilizadas por las aplicaciones de OLE DB mediante **IDataInitialize:: GetDatasource** tiene la siguiente sintaxis:  
  
 `connection-string ::= empty-string[;] | attribute[;] | attribute; connection-string`  
  
 `empty-string ::=`  
  
 `attribute ::= attribute-keyword=[quote]attribute-value[quote]`  
  
 `attribute-value ::= character-string`  
  
 `attribute-keyword ::= identifier`  
  
 `quote ::= " | '`  
  
 El uso de la propiedad debe cumplir la sintaxis permitida en su ámbito.  Por ejemplo, **WSID** utiliza llaves (**{}**) caracteres de comillas y **nombre de la aplicación** solo usa (**'**) o dobles (**"**) caracteres de comillas. Solo se pueden entrecomillar las propiedades de cadena. Si se intenta entrecomillar un entero o la propiedad enumerada, se producirá un error que indica que la cadena de conexión no cumple la especificación OLE DB.  
  
 Los valores de atributo pueden incluirse opcionalmente entre comillas simples o dobles, y es una práctica recomendada. Esto evita que se produzcan problemas cuando los valores contienen caracteres no alfanuméricos. El carácter de comillas que se utilice también puede aparecer en los valores, siempre y cuando aparezca duplicado.  
  
 Un carácter de espacio después del signo = de una palabra clave de cadena de conexión se interpretará como un literal, incluso si el valor está entre comillas.  
  
 Si una cadena de conexión tiene más de una de las propiedades enumeradas en la tabla siguiente, se utilizará el valor de la última propiedad.  
  
 La tabla siguiente describen las palabras clave que pueden utilizarse con **IDataInitialize:: GetDatasource**:  
  
|Palabra clave|Propiedad de inicialización|Description|  
|-------------|-----------------------------|-----------------|  
|**Application Name**|SSPROP_INIT_APPNAME|Cadena que identifica la aplicación.|  
|**Intento de aplicación**|SSPROP_INIT_APPLICATIONINTENT|Declara el tipo de carga de trabajo de la aplicación al conectarse a un servidor. Los valores posibles son **ReadOnly** y **ReadWrite**.<br /><br /> El valor predeterminado es **ReadWrite**. Para obtener más información sobre el controlador OLE DB para la compatibilidad de SQL Server de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [controlador OLE DB para SQL Server admite alta disponibilidad, recuperación ante desastres](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**Traducir automáticamente**|SSPROP_INIT_AUTOTRANSLATE|Sinónimo de "AutoTranslate".|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|Configura la traducción de caracteres OEM/ANSI. Los valores reconocidos son "true" y "false".|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|Cantidad de tiempo (en segundos) que hay que esperar a que se complete la inicialización del origen de datos.|  
|**Idioma actual**|SSPROPT_INIT_CURRENTLANGUAGE|Nombre del lenguaje [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Origen de datos**|DBPROP_INIT_DATASOURCE|Nombre de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.<br /><br /> Si no se especifica, se establece una conexión a la instancia predeterminada en el equipo local.<br /><br /> Para obtener más información acerca de la sintaxis válida para las direcciones, vea la descripción de la **Server** (palabra clave), en este tema.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Especifica el modo de administración de tipos de datos que debe utilizarse. Los valores reconocidos son "0" para los tipos de datos del proveedor y "80" para los tipos de datos de [!INCLUDE[ssVersion2000](../../../includes/ssversion2000-md.md)].|  
|**Failover Partner**|SSPROP_INIT_FAILOVERPARTNER|Nombre del servidor de conmutación por error utilizado para la creación de reflejo de la base de datos.|  
|**SPN de asociado de conmutación por error**|SSPROP_INIT_FAILOVERPARTNERSPN|SPN del asociado de conmutación por error. El valor predeterminado es una cadena vacía. Una cadena vacía hace el controlador OLE DB para SQL Server para utilizar el valor predeterminado, SPN generado por proveedor.|  
|**Catálogo original**|DBPROP_INIT_CATALOG|Nombre de la base de datos.|  
|**Nombre de archivo inicial**|SSPROP_INIT_FILENAME|Nombre del archivo principal (incluido el nombre de la ruta de acceso completa) de una base de datos adjuntable. Usar **AttachDBFileName**, también debe especificar el nombre de la base de datos con la palabra clave base de datos de cadena de proveedor. Si la base de datos se ha adjuntado previamente, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no vuelve a adjuntarla (utiliza la base de datos adjuntada como valor predeterminado para la conexión).|  
|**Seguridad integrada**|DBPROP_AUTH_INTEGRATED|Acepta el valor "SSPI" para la autenticación de Windows.|  
|**Conexión MARS**|SSPROP_INIT_MARSCONNECTION|Habilita o deshabilita conjuntos de resultados activos múltiples (MARS) en la conexión. Los valores reconocidos son "true" y "false". El valor predeterminado es "false".|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|Especifique siempre **MultiSubnetFailover = True** al conectarse a la escucha del grupo de disponibilidad de un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] grupo de disponibilidad o una [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instancia de clúster de conmutación por error. **MultiSubnetFailover = True** configura el controlador OLE DB para SQL Server proporcionar una detección más rápida y conexión con el servidor (actualmente) activo. Los valores posibles son **True** o **False**. El valor predeterminado es **False**. Por ejemplo:<br /><br /> `MultiSubnetFailover=True`<br /><br /> Para obtener más información sobre el controlador OLE DB para la compatibilidad de SQL Server de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [controlador OLE DB para SQL Server admite alta disponibilidad, recuperación ante desastres](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**Dirección de red**|SSPROP_INIT_NETWORKADDRESS|Dirección de red de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.<br /><br /> Para obtener más información acerca de la sintaxis válida para las direcciones, vea la descripción de la **dirección** palabra clave, en este tema.|  
|**Biblioteca de red**|SSPROP_INIT_NETWORKLIBRARY|Biblioteca de red que se utiliza para establecer una conexión a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|Tamaño del paquete de red El valor predeterminado es 4096.|  
|**Contraseña**|DBPROP_AUTH_PASSWORD|Contraseña de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Persist Security Info**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Acepta las cadenas "true" y "false" como valores. Cuando es "false", el objeto de origen de datos no se permite para conservar información confidencial de autenticación|  
|**Proveedor**||Para el controlador OLE DB para SQL Server, debe ser "MSOLEDBSQL".|  
|**SPN del servidor**|SSPROP_INIT_SERVERSPN|SPN del servidor. El valor predeterminado es una cadena vacía. Una cadena vacía hace el controlador OLE DB para SQL Server para utilizar el valor predeterminado, SPN generado por proveedor.|  
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
|**Intento de aplicación**|SSPROP_INIT_APPLICATIONINTENT|Declara el tipo de carga de trabajo de la aplicación al conectarse a un servidor. Los valores posibles son **ReadOnly** y **ReadWrite**.<br /><br /> El valor predeterminado es **ReadWrite**. Para obtener más información sobre el controlador OLE DB para la compatibilidad de SQL Server de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [controlador OLE DB para SQL Server admite alta disponibilidad, recuperación ante desastres](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**Application Name**|SSPROP_INIT_APPNAME|Cadena que identifica la aplicación.|  
|**Traducir automáticamente**|SSPROP_INIT_AUTOTRANSLATE|Sinónimo de "AutoTranslate".|  
|**AutoTranslate**|SSPROP_INIT_AUTOTRANSLATE|Configura la traducción de caracteres OEM/ANSI. Los valores reconocidos son "true" y "false".|  
|**Connect Timeout**|DBPROP_INIT_TIMEOUT|Cantidad de tiempo (en segundos) que hay que esperar a que se complete la inicialización del origen de datos.|  
|**Idioma actual**|SSPROPT_INIT_CURRENTLANGUAGE|Nombre del lenguaje [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Origen de datos**|DBPROP_INIT_DATASOURCE|Nombre de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.<br /><br /> Si no se especifica, se establece una conexión a la instancia predeterminada en el equipo local.<br /><br /> Para obtener más información acerca de la sintaxis válida para las direcciones, vea la descripción de la **Server** (palabra clave), en este tema.|  
|**DataTypeCompatibility**|SSPROP_INIT_DATATYPECOMPATIBILITY|Especifica el modo de administración de tipos de datos que se utilizará. Los valores reconocidos son "0" para los tipos de datos del proveedor y "80" para los tipos de datos de SQL Server 2000.|  
|**Failover Partner**|SSPROP_INIT_FAILOVERPARTNER|Nombre del servidor de conmutación por error utilizado para la creación de reflejo de la base de datos.|  
|**SPN de asociado de conmutación por error**|SSPROP_INIT_FAILOVERPARTNERSPN|SPN del asociado de conmutación por error. El valor predeterminado es una cadena vacía. Una cadena vacía hace el controlador OLE DB para SQL Server para utilizar el valor predeterminado, SPN generado por proveedor.|  
|**Catálogo original**|DBPROP_INIT_CATALOG|Nombre de la base de datos.|  
|**Nombre de archivo inicial**|SSPROP_INIT_FILENAME|Nombre del archivo principal (incluido el nombre de la ruta de acceso completa) de una base de datos adjuntable. Usar **AttachDBFileName**, también debe especificar el nombre de la base de datos con la palabra clave base de datos de cadena de proveedor. Si la base de datos se ha adjuntado previamente, [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no vuelve a adjuntarla (utiliza la base de datos adjuntada como valor predeterminado para la conexión).|  
|**Seguridad integrada**|DBPROP_AUTH_INTEGRATED|Acepta el valor "SSPI" para la autenticación de Windows.|  
|**Conexión MARS**|SSPROP_INIT_MARSCONNECTION|Habilita o deshabilita conjuntos de resultados activos múltiples (MARS) en la conexión si el servidor es [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] o posterior. Los valores reconocidos son "true" y "false". El valor predeterminado es "false".|  
|**MultiSubnetFailover**|SSPROP_INIT_MULTISUBNETFAILOVER|Especifique siempre **MultiSubnetFailover = True** al conectarse a la escucha del grupo de disponibilidad de un [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] grupo de disponibilidad o una [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instancia de clúster de conmutación por error. **MultiSubnetFailover = True** configura el controlador OLE DB para SQL Server proporcionar una detección más rápida y conexión con el servidor (actualmente) activo. Los valores posibles son **True** o **False**. El valor predeterminado es **False**. Por ejemplo:<br /><br /> `MultiSubnetFailover=True`<br /><br /> Para obtener más información sobre el controlador OLE DB para la compatibilidad de SQL Server de [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)], consulte [controlador OLE DB para SQL Server admite alta disponibilidad, recuperación ante desastres](../../oledb/features/oledb-driver-for-sql-server-support-for-high-availability-disaster-recovery.md).|  
|**Dirección de red**|SSPROP_INIT_NETWORKADDRESS|Dirección de red de una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.<br /><br /> Para obtener más información acerca de la sintaxis válida para las direcciones, vea la descripción de la **dirección** palabra clave, en este tema.|  
|**Biblioteca de red**|SSPROP_INIT_NETWORKLIBRARY|Biblioteca de red que se utiliza para establecer una conexión a una instancia de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] en la organización.|  
|**Packet Size**|SSPROP_INIT_PACKETSIZE|Tamaño del paquete de red El valor predeterminado es 4096.|  
|**Contraseña**|DBPROP_AUTH_PASSWORD|Contraseña de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Persist Security Info**|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|Acepta las cadenas "true" y "false" como valores. Cuando es "false", no se permite que el objeto de origen de datos conserve ninguna información confidencial de autenticación.|  
|**Proveedor**||Para el controlador OLE DB para SQL Server, debe ser "MSOLEDBSQL".|  
|**SPN del servidor**|SSPROP_INIT_SERVERSPN|SPN del servidor. El valor predeterminado es una cadena vacía. Una cadena vacía hace el controlador OLE DB para SQL Server para utilizar el valor predeterminado, SPN generado por proveedor.|  
|**TrustServerCertificate**|SSPROP_INIT_TRUST_SERVER_CERTIFICATE|Acepta las cadenas "true" y "false" como valores. El valor predeterminado es "false", que significa que se validará el certificado del servidor.|  
|**Use Encryption for Data**|SSPROP_INIT_ENCRYPT|Especifica si los datos deben cifrarse antes de enviarse a través de la red. Los valores posibles son "true" y "false". El valor predeterminado es "false".|  
|**Id. de usuario**|DBPROP_AUTH_USERID|Nombre de inicio de sesión de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].|  
|**Id. de estación de trabajo**|SSPROP_INIT_WSID|El identificador de estación de trabajo.|  
  
 **Tenga en cuenta** en la cadena de conexión, la propiedad "Contraseña anterior" establece SSPROP_AUTH_OLD_PASSWORD, que es la contraseña actual (posiblemente expirada) que no está disponible a través de una propiedad de cadena de proveedor.  
  
## <a name="see-also"></a>Vea también  
 [Compilación de aplicaciones con el controlador OLE DB para SQL Server](../../oledb/applications/building-applications-with-oledb-driver-for-sql-server.md)  
  
  
