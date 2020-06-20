---
title: SQLSetConnectAttr | Microsoft Docs
description: Obtenga información sobre los atributos de conexión en SQLSetConnectAttr, incluso cuando se establecen y valores posibles en el controlador ODBC de SQL Server Native Client.
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLSetConnectAttr function
ms.assetid: d21b5cf1-3724-43f7-bc96-5097df0677b4
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 3008664916a8863a00dd36772e4b83cf27e845d5
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/17/2020
ms.locfileid: "84967745"
---
# <a name="sqlsetconnectattr"></a>SQLSetConnectAttr

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client pasa por alto la configuración de SQL_ATTR_CONNECTION_TIMEOUT.  
  
 SQL_ATTR_TRANSLATE_LIB también se ignora; especificando que otra biblioteca de traducción no es compatible. Para permitir que las aplicaciones se trasladen fácilmente para usar un controlador ODBC de Microsoft para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], cualquier valor configurado con SQL_ATTR_TRANSLATE_LIB se copiará en y fuera de un búfer en el Administrador de controladores.  
  
 El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client implementa el aislamiento de transacciones de lectura repetible (REPEATABLE READ) como serializable.  
  
 En [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] se introdujo compatibilidad para un nuevo atributo de aislamiento de transacciones, SQL_COPT_SS_TXN_ISOLATION. Si SQL_COPT_SS_TXN_ISOLATION se establece en SQL_TXN_SS_SNAPSHOT, significa que la transacción tendrá lugar en el nivel de aislamiento de instantáneas.  
  
> [!NOTE]  
> SQL_ATTR_TXN_ISOLATION puede usarse para establecer todos los demás niveles de aislamiento salvo SQL_TXN_SS_SNAPSHOT. Si desea usar el aislamiento de instantáneas, debe establecer SQL_TXN_SS_SNAPSHOT a través de SQL_COPT_SS_TXN_ISOLATION. Sin embargo, puede recuperar el nivel de aislamiento mediante SQL_ATTR_TXN_ISOLATION o SQL_COPT_SS_TXN_ISOLATION.  
  
 La promoción de atributos de instrucción a atributos de conexión ODBC puede tener consecuencias imprevistas. Los atributos de instrucción que solicitan cursores de servidor para el procesamiento del conjunto de resultados pueden promoverse a la conexión. Por ejemplo, el establecimiento del atributo de instrucción ODBC SQL_ATTR_CONCURRENCY a un valor más restrictivo que el valor SQL_CONCUR_READ_ONLY predeterminado indica al controlador que use cursores dinámicos para todas las instrucciones enviadas en la conexión. Si se ejecuta una función de catálogo ODBC en una instrucción en la conexión, se devuelve SQL_SUCCESS_WITH_INFO y un registro de diagnóstico que indica que el comportamiento del cursor se ha modificado a solo lectura. Se produce un error al intentar ejecutar una instrucción SELECT de Transact-SQL que contiene una cláusula COMPUTE en la misma conexión.  
  
 El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client admite varias extensiones específicas del controlador para los atributos de conexión ODBC definidos en sqlncli.h. El controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client puede exigir que el atributo se establezca antes de la conexión, o puede omitir el atributo si ya está establecido. En la tabla siguiente se enumeran las restricciones.  
  
|Atributo de SQL Server|Establecer antes o después de la conexión al servidor|  
|--------------------------|----------------------------------------------|  
|SQL_COPT_SS_ANSI_NPW|Antes|  
|SQL_COPT_SS_APPLICATION_INTENT|Antes|  
|SQL_COPT_SS_ATTACHDBFILENAME|Antes|  
|SQL_COPT_SS_BCP|Antes|  
|SQL_COPT_SS_BROWSE_CONNECT|Antes|  
|SQL_COPT_SS_BROWSE_SERVER|Antes|  
|SQL_COPT_SS_CONCAT_NULL|Antes|  
|SQL_COPT_SS_CONNECTION_DEAD|Después|  
|SQL_COPT_SS_ENCRYPT|Antes|  
|SQL_COPT_SS_ENLIST_IN_DTC|Después|  
|SQL_COPT_SS_ENLIST_IN_XA|Después|  
|SQL_COPT_SS_FALLBACK_CONNECT|Antes|  
|SQL_COPT_SS_FAILOVER_PARTNER|Antes|  
|SQL_COPT_SS_INTEGRATED_SECURITY|Antes|  
|SQL_COPT_SS_MARS_ENABLED|Antes|  
|SQL_COPT_SS_MULTISUBNET_FAILOVER|Antes|  
|SQL_COPT_SS_OLDPWD|Antes|  
|SQL_COPT_SS_PERF_DATA|Después|  
|SQL_COPT_SS_PERF_DATA_LOG|Después|  
|SQL_COPT_SS_PERF_DATA_LOG_NOW|Después|  
|SQL_COPT_SS_PERF_QUERY|Después|  
|SQL_COPT_SS_PERF_QUERY_INTERVAL|Después|  
|SQL_COPT_SS_PERF_QUERY_LOG|Después|  
|SQL_COPT_SS_PRESERVE_CURSORS|Antes|  
|SQL_COPT_SS_QUOTED_IDENT|Es posible usar el|  
|SQL_COPT_SS_TRANSLATE|Es posible usar el|  
|SQL_COPT_SS_TRUST_SERVER_CERTIFICATE|Antes|  
|SQL_COPT_SS_TXN_ISOLATION|Es posible usar el|  
|SQL_COPT_SS_USE_PROC_FOR_PREP|Es posible usar el|  
|SQL_COPT_SS_USER_DATA|Es posible usar el|  
|SQL_COPT_SS_WARN_ON_CP_ERROR|Antes|  
  
 El uso de un atributo anterior a la conexión y el comando equivalente de [!INCLUDE[tsql](../../includes/tsql-md.md)] para la misma sesión, base de datos o estado de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] puede producir un comportamiento inesperado. Por ejemplo,  
  
```  
SQLSetConnectAttr(SQL_COPT_SS_QUOTED_IDENT, SQL_QI_ON) // turn ON via attribute  
SQLDriverConnect(...);  
SQLExecDirect("SET QUOTED_IDENTIFIER OFF") // turn OFF via Transact-SQL  
SQLSetConnectAttr(SQL_ATTR_CURRENT_CATALOG, ...) // restores to pre-connect attribute value  
```  

<a name="sqlcoptssansinpw"></a>
## <a name="sql_copt_ss_ansi_npw"></a>SQL_COPT_SS_ANSI_NPW  
 SQL_COPT_SS_ANSI_NPW habilita o deshabilita el uso de la administración ISO de valores NULL en comparaciones y concatenación, relleno de tipos de datos de caracteres y advertencias. Para obtener más información, vea SET ANSI_NULLS, SET ANSI_PADDING, SET ANSI_WARNINGS y SET CONCAT_NULL_YIELDS_NULL.  
  
|Value|Descripción|  
|-----------|-----------------|  
|SQL_AD_ON|Predeterminada. La conexión usa el comportamiento ANSI predeterminado para administrar comparaciones de valores NULL, relleno, advertencias y concatenaciones de valores NULL.|  
|SQL_AD_OFF|La conexión usa la administración definida por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de valores NULL, relleno de tipo de datos de caracteres y advertencias.|  
  
 Si usa la agrupación de conexiones, SQL_COPT_SS_ANSI_NPW debe establecerse en la cadena de conexión, en lugar de en SQLSetConnectAttr. Una vez realizada una conexión, cualquier intento por cambiar este atributo cuando se use la agrupación de conexiones dará lugar a un error que no se notificará.  

<a name="sqlcoptssapplicationintent"></a>
## <a name="sql_copt_ss_application_intent"></a>SQL_COPT_SS_APPLICATION_INTENT  
 Declara el tipo de carga de trabajo de la aplicación al conectarse a un servidor. Los valores posibles son **ReadOnly** y **ReadWrite**. Por ejemplo:  
  
```  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_APPLICATION_INTENT, TEXT("Readonly"), SQL_NTS)  
```  
  
 El valor predeterminado es **ReadWrite**. Para obtener más información sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la compatibilidad de Native Client con [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] AG, consulte [SQL Server Native Client Support for High Availability, Disaster Recovery](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).  

<a name="sqlcoptssattachdbfilename"></a>
## <a name="sql_copt_ss_attachdbfilename"></a>SQL_COPT_SS_ATTACHDBFILENAME  
 SQL_COPT_SS_ATTACHDBFILENAME especifica el nombre del archivo principal de una base de datos adjuntable. Esta base de datos se adjunta y se convierte en la base de datos predeterminada para la conexión. Para usar SQL_COPT_SS_ATTACHDBFILENAME debe especificar el nombre de la base de datos como el valor del atributo de conexión SQL_ATTR_CURRENT_CATALOG o en el parámetro DATABASE = de una [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md). Si la base de datos se ha adjuntado previamente, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no volverá a adjuntarla.  
  
|Value|Descripción|  
|-----------|-----------------|  
|SQLPOINTER a una cadena de caracteres|La cadena contiene el nombre del archivo principal de la base de datos que va a adjuntarse. Incluya el nombre completo de la ruta de acceso al archivo.|  

<a name="sqlcoptssbcp"></a>
## <a name="sql_copt_ss_bcp"></a>SQL_COPT_SS_BCP  
 SQL_COPT_SS_BCP habilita las funciones de copia masiva en una conexión. Para obtener más información, vea [funciones de copia masiva](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md).  
  
|Value|Descripción|  
|-----------|-----------------|  
|SQL_BCP_OFF|Predeterminada. Las funciones de copia masiva no están disponibles en la conexión.|  
|SQL_BCP_ON|Las funciones de copia masiva están disponibles en la conexión.|  

<a name="sqlcoptssbrowseconnect"></a>
## <a name="sql_copt_ss_browse_connect"></a>SQL_COPT_SS_BROWSE_CONNECT  
 Este atributo se utiliza para personalizar el conjunto de resultados devuelto por [SQLBrowseConnect](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md). SQL_COPT_SS_BROWSE_CONNECT habilita o deshabilita la devolución de información adicional de una instancia enumerada de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esta información puede incluir datos como si el servidor es un clúster, nombres de instancias distintas y el número de versión.  
  
|Value|Descripción|  
|-----------|-----------------|  
|SQL_MORE_INFO_NO|Predeterminada. Devuelve una lista de servidores.|  
|SQL_MORE_INFO_YES|**SQLBrowseConnect** devuelve una cadena extendida de propiedades del servidor.|  

<a name="sqlcoptssbrowseserver"></a>
## <a name="sql_copt_ss_browse_server"></a>SQL_COPT_SS_BROWSE_SERVER  
 Este atributo se utiliza para personalizar el conjunto de resultados devuelto por **SQLBrowseConnect**. SQL_COPT_SS_BROWSE_SERVER especifica el nombre del servidor para el que **SQLBrowseConnect** devuelve la información.  
  
|Value|Descripción|  
|-----------|-----------------|  
|computername|**SQLBrowseConnect** devuelve una lista de instancias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] en el equipo especificado. No se deben usar barras diagonales inversas dobles ( \\ \\ ) para el nombre del servidor (por ejemplo, en lugar de \\ \MyServer, se debe usar mi Server).|  
|NULL|Predeterminada. **SQLBrowseConnect** devuelve información para todos los servidores del dominio.|  

<a name="sqlcoptssconcatnull"></a>
## <a name="sql_copt_ss_concat_null"></a>SQL_COPT_SS_CONCAT_NULL  
 SQL_COPT_SS_CONCAT_NULL habilita o deshabilita el uso de la administración ISO de valores NULL al concatenar cadenas. Para obtener más información, vea SET CONCAT_NULL_YIELDS_NULL.  
  
|Value|Descripción|  
|-----------|-----------------|  
|SQL_CN_ON|Predeterminada. La conexión usa el comportamiento ISO predeterminado para administrar valores NULL al concatenar cadenas.|  
|SQL_CN_OFF|La conexión usa el comportamiento predeterminado definido por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para administrar valores NULL al concatenar cadenas.|  

<a name="sqlcoptssencrypt"></a>
## <a name="sql_copt_ss_encrypt"></a>SQL_COPT_SS_ENCRYPT  
 Controla el cifrado de una conexión.  
  
 El cifrado usa el certificado en el servidor. Una entidad de certificación debe comprobar el certificado, a menos que el atributo de conexión SQL_COPT_SS_TRUST_SERVER_CERTIFICATE se establezca en SQL_TRUST_SERVER_CERTIFICATE_YES o que la cadena de conexión contenga "TrustServerCertificate=yes". Si se cumple alguna de estas condiciones, puede usarse un certificado generado y firmado por el servidor para cifrar la conexión en caso de que no haya ningún certificado en el servidor.  
  
|Value|Descripción|  
|-----------|-----------------|  
|SQL_EN_ON|La conexión se cifrará.|  
|SQL_EN_OFF|La conexión no se cifrará. Este es el valor predeterminado.|  

<a name="sqlcoptssenlistindtc"></a>
## <a name="sql_copt_ss_enlist_in_dtc"></a>SQL_COPT_SS_ENLIST_IN_DTC  
 El cliente llama al método de Microsoft Coordinador de transacciones distribuidas (MS DTC) OLE DB **ITransactionDispenser:: BeginTransaction** para iniciar una transacción de MS DTC y crear un objeto de transacción de MS DTC que representa la transacción. A continuación, la aplicación llama a **SQLSetConnectAttr** con la opción SQL_COPT_SS_ENLIST_IN_DTC para asociar el objeto de transacción a la conexión ODBC. Toda la actividad de base de datos relacionada se realizará bajo la protección de la transacción MS DTC. La aplicación llama a **SQLSetConnectAttr** con SQL_DTC_DONE para finalizar la Asociación de DTC de la conexión.  
  
|Value|Descripción|  
|-----------|-----------------|  
|Objeto DTC*|Objeto de transacción OLE de MS DTC que especifica la transacción que va exportarse a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|SQL_DTC_DONE|Delimita el final de una transacción DTC.|  

<a name="sqlcoptssenlistinxa"></a>
## <a name="sql_copt_ss_enlist_in_xa"></a>SQL_COPT_SS_ENLIST_IN_XA  
 Para iniciar una transacción XA con un procesador de transacciones compatible con XA (TP), el cliente llama a la función Open Group **tx_begin** . A continuación, la aplicación llama a **SQLSetConnectAttr** con un parámetro SQL_COPT_SS_ENLIST_IN_XA de true para asociar la transacción XA a la conexión ODBC. Toda la actividad de base de datos relacionada se realizará bajo la protección de la transacción XA. Para finalizar una asociación XA con una conexión ODBC, el cliente debe llamar a **SQLSetConnectAttr** con un parámetro SQL_COPT_SS_ENLIST_IN_XA de false. Para obtener más información, vea la documentación de Microsoft DTC (Coordinador de transacciones distribuidas).  
  
## <a name="sql_copt_ss_fallback_connect"></a>SQL_COPT_SS_FALLBACK_CONNECT  
 Este atributo ya no se admite.  

<a name="sqlcoptssfailoverpartner"></a>
## <a name="sql_copt_ss_failover_partner"></a>SQL_COPT_SS_FAILOVER_PARTNER  
 Se usa para especificar o recuperar el nombre del asociado de conmutación por error usado para la creación de reflejo de la base de datos en [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], y es una cadena de caracteres terminada en NULL que debe establecerse antes de que se realice la conexión inicial a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Después de realizar la conexión, la aplicación puede consultar este atributo mediante [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) para determinar la identidad del asociado de conmutación por error. Si el servidor principal no tiene ningún asociado de conmutación por error, esta propiedad devolverá una cadena vacía. Esto permite que una aplicación inteligente almacene en memoria caché el servidor de copia de seguridad determinado más recientemente, pero dichas aplicaciones deben tener en cuenta que la información solo se actualiza cuando la conexión se establece por primera vez (o se restablece, si está agrupada) y puede quedar desfasada para conexiones a largo plazo.  
  
 Para obtener más información, vea [Usar la creación de reflejo de la base de datos](../../relational-databases/native-client/features/using-database-mirroring.md).  

<a name="sqlcoptssintegratedsecurity"></a>
## <a name="sql_copt_ss_integrated_security"></a>SQL_COPT_SS_INTEGRATED_SECURITY  
 SQL_COPT_SS_INTEGRATED_SECURITY fuerza el uso de la autenticación de Windows para la validación de acceso en el inicio sesión del servidor. Cuando se utiliza la autenticación de Windows, el controlador omite los valores de identificador de usuario y contraseña proporcionados como parte del procesamiento de **SQLConnect**, [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md)o [SQLBrowseConnect](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md) .  
  
|Value|Descripción|  
|-----------|-----------------|  
|SQL_IS_OFF|Predeterminada. La autenticación de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se usa para validar el identificador de usuario y la contraseña en el inicio de sesión.|  
|SQL_IS_ON|El modo de autenticación de Windows se usa para validar los derechos de acceso a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de un usuario.|  

<a name="sqlcoptssmarsenabled"></a>
## <a name="sql_copt_ss_mars_enabled"></a>SQL_COPT_SS_MARS_ENABLED  
 Este atributo habilita o deshabilita MARS (Multiple Active Result Sets, conjuntos de resultados activos múltiples). De forma predeterminada, MARS está deshabilitado. Este atributo debe establecerse antes de realizar una conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Una vez abierta la conexión a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], MARS seguirá habilitado o deshabilitado a lo largo de toda la conexión.  
  
|Value|Descripción|  
|-----------|-----------------|  
|SQL_MARS_ENABLED_NO|Predeterminada. MARS (Multiple Active Result Sets, conjuntos de resultados activos múltiples) está deshabilitado.|  
|SQL_MARS_ENABLED_YES|MARS está habilitado.|  
  
 Para obtener más información acerca de MARS, vea [utilizar conjuntos de resultados activos múltiples &#40;mars&#41;](../../relational-databases/native-client/features/using-multiple-active-result-sets-mars.md).  

<a name="sqlcoptssmultisubnetfailover"></a>
## <a name="sql_copt_ss_multisubnet_failover"></a>SQL_COPT_SS_MULTISUBNET_FAILOVER  
 Si la aplicación se conecta a un grupo de disponibilidad (AG) de [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] en varias subredes, esta propiedad de conexión configura [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client para proporcionar una detección y conexión más rápidas con el servidor (actualmente) activo. Por ejemplo:  
  
```  
SQLSetConnectAttr(hdbc, SQL_COPT_SS_MULTISUBNET_FAILOVER, SQL_IS_ON, SQL_IS_INTEGER)  
```  
  
 Para obtener más información sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] la compatibilidad de Native Client con [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] AG, consulte [SQL Server Native Client Support for High Availability, Disaster Recovery](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md).  
  
|Value|Descripción|  
|-----------|-----------------|  
|SQL_IS_ON|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client proporciona una reconexión más rápida si se produce una conmutación por error.|  
|SQL_IS_OFF|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client no proporcionará una reconexión más rápida si se produce una conmutación por error.|  

<a name="sqlcoptssoldpwd"></a>
## <a name="sql_copt_ss_oldpwd"></a>SQL_COPT_SS_OLDPWD  
 La expiración de contraseñas para la autenticación de SQL Server se introdujo en [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Se ha agregado el atributo SQL_COPT_SS_OLDPWD para permitir que el cliente especifique la contraseña antigua y la nueva contraseña para la conexión. Cuando se establezca esta propiedad, el proveedor no usará el grupo de conexiones para la primera conexión o para conexiones posteriores, puesto que la cadena de conexión contendrá la "contraseña antigua" que ahora ha cambiado.  
  
 Para más información, consulte [Cambio de contraseñas mediante programación](../../relational-databases/native-client/features/changing-passwords-programmatically.md).  
  
|Value|Descripción|  
|-----------|-----------------|  
|SQL_COPT_SS_OLD_PASSWORD|SQLPOINTER a una cadena de caracteres que contiene la contraseña anterior. Este valor es de solo escritura y debe establecerse antes de la conexión al servidor.|  

<a name="sqlcoptssperfdata"></a>
## <a name="sql_copt_ss_perf_data"></a>SQL_COPT_SS_PERF_DATA  
 SQL_COPT_SS_PERF_DATA inicia o detiene el registro de datos de rendimiento. El nombre del archivo de registro de datos debe establecerse antes de iniciar el registro de datos. Vea SQL_COPT_SS_PERF_DATA_LOG a continuación.  
  
|Value|Descripción|  
|-----------|-----------------|  
|SQL_PERF_START|Inicia el muestreo de datos de rendimiento del controlador.|  
|SQL_PERF_STOP|Detiene el muestreo de datos de rendimiento por parte de los controladores.|  
  
 Para obtener más información, vea [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md).  

<a name="sqlcoptssperfdatalog"></a>
## <a name="sql_copt_ss_perf_data_log"></a>SQL_COPT_SS_PERF_DATA_LOG  
 SQL_COPT_SS_PERF_DATA_LOG asigna el nombre del archivo de registro utilizado para grabar datos de rendimiento. El nombre del archivo de registro es una cadena ANSI o Unicode terminada en NULL, en función de la compilación de la aplicación. El argumento *StringLength* debe ser SQL_NTS.  

<a name="sqlcoptssperfdatalognow"></a>
## <a name="sql_copt_ss_perf_data_log_now"></a>SQL_COPT_SS_PERF_DATA_LOG_NOW  
 SQL_COPT_SS_PERF_DATA_LOG_NOW indica al controlador que escriba una entrada de registro de estadísticas en el disco. El argumento *StringLength* debe ser SQL_NTS.  

<a name="sqlcoptssperfquery"></a>
## <a name="sql_copt_ss_perf_query"></a>SQL_COPT_SS_PERF_QUERY  
 SQL_COPT_SS_PERF_QUERY inicia o detiene el registro de consultas de ejecución prolongada. El nombre del archivo de registro de consultas debe suministrarse antes de iniciar el registro. La aplicación puede definir la "ejecución prolongada" estableciendo el intervalo para el registro.  
  
|Value|Descripción|  
|-----------|-----------------|  
|SQL_PERF_START|Inicia el registro de consultas de ejecución prolongada.|  
|SQL_PERF_STOP|Detiene el registro de las consultas de ejecución prolongada.|  
  
 Para obtener más información, vea [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md).  

<a name="sqlcoptssperfqueryinterval"></a>
## <a name="sql_copt_ss_perf_query_interval"></a>SQL_COPT_SS_PERF_QUERY_INTERVAL  
 SQL_COPT_SS_PERF_QUERY_INTERVAL establece el umbral de registro de consultas en milisegundos. Las consultas que no se resuelven dentro del umbral se graban en el archivo de registro de consultas de ejecución prolongada. No existe un límite superior en el umbral de consultas. Un valor de umbral de consulta igual a cero da lugar al registro de todas las consultas.  

<a name="sqlcoptssperfquerylog"></a>
## <a name="sql_copt_ss_perf_query_log"></a>SQL_COPT_SS_PERF_QUERY_LOG  
 SQL_COPT_SS_PERF_QUERY_LOG asigna el nombre de un archivo de registro para grabar los datos de consulta de ejecución prolongada. El nombre del archivo de registro es una cadena ANSI o Unicode terminada en NULL, en función de la compilación de la aplicación. El argumento *StringLength* debe ser SQL_NTS o la longitud de la cadena en bytes.  

<a name="sqlcoptsspreservecursors"></a>
## <a name="sql_copt_ss_preserve_cursors"></a>SQL_COPT_SS_PRESERVE_CURSORS  
 Este atributo permite consultar y establecer si la conexión conservará o no los cursores al confirmar o revertir una transacción. El valor es SQL_PC_ON o SQL_PC_OFF. El valor predeterminado es SQL_PC_OFF. Esta configuración controla si el controlador cerrará o no los cursores cuando llame a [SQLEndTran](../../relational-databases/native-client-odbc-api/sqlendtran.md) (o SQLTransact).  
  
|Value|Descripción|  
|-----------|-----------------|  
|SQL_PC_OFF|Predeterminada. Los cursores se cierran cuando la transacción se confirma o se revierte mediante **SQLEndTran**.|  
|SQL_PC_ON|Los cursores no se cierran cuando la transacción se confirma o se revierte mediante **SQLEndTran**, excepto cuando se usa un cursor estático o de conjunto de claves en modo asincrónico. Si se emite una reversión antes de que se complete el rellenado del cursor, se cierra el cursor.|  

<a name="sqlcoptssquotedident"></a>
## <a name="sql_copt_ss_quoted_ident"></a>SQL_COPT_SS_QUOTED_IDENT  
 SQL_COPT_SS_QUOTED_IDENT permite el uso de identificadores entre comillas en instrucciones ODBC y Transact-SQL enviadas en la conexión. Si se especifican identificadores entre comillas, el controlador ODBC de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client admite nombres de objeto no válidos, como "Mi Tabla", que contiene un carácter de espacio en el identificador. Para obtener más información, vea SET QUOTED_IDENTIFIER.  
  
|Value|Descripción|  
|-----------|-----------------|  
|SQL_QI_OFF|La conexión [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no permite identificadores entre comillas en el [!INCLUDE[tsql](../../includes/tsql-md.md)] enviado.|  
|SQL_QI_ON|Predeterminada. La conexión permite identificadores entre comillas en el [!INCLUDE[tsql](../../includes/tsql-md.md)] enviado.|  

<a name="sqlcoptsstranslate"></a>
## <a name="sql_copt_ss_translate"></a>SQL_COPT_SS_TRANSLATE  
 SQL_COPT_SS_TRANSLATE hace que el controlador traduzca los caracteres entre las páginas de códigos del cliente y del servidor a medida que se intercambian datos MBCS. El atributo solo afecta a los datos almacenados en columnas de tipo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Char**, **VARCHAR**y **Text** .  
  
|Value|Descripción|  
|-----------|-----------------|  
|SQL_XL_OFF|El controlador no traduce los caracteres de una página de códigos a otra en los datos de caracteres intercambiados entre el cliente y el servidor.|  
|SQL_XL_ON|Predeterminada. El controlador traduce los caracteres de una página de códigos a otra en los datos de caracteres intercambiados entre el cliente y el servidor. El controlador configura automáticamente la traducción de caracteres, determinando la página de códigos instalada en el servidor y que está usando el cliente.|  

<a name="sqlcoptsstrustservercertificate"></a>
## <a name="sql_copt_ss_trust_server_certificate"></a>SQL_COPT_SS_TRUST_SERVER_CERTIFICATE  
 SQL_COPT_SS_TRUST_SERVER_CERTIFICATE hace que el controlador habilite o deshabilite la validación de certificados cuando se utiliza el cifrado. Este atributo es un valor de lectura/escritura, pero si se establece después de que se haya establecido una conexión no tiene ningún efecto.  
  
 Las aplicaciones cliente podrán consultar esta propiedad una vez que se haya abierto una conexión para determinar la configuración real de cifrado y validación que se está usando.  
  
|Value|Descripción|  
|-----------|-----------------|  
|SQL_TRUST_SERVER_CERTIFICATE_NO|Predeterminada. No está habilitado el cifrado sin validación de certificados.|  
|SQL_TRUST_SERVER_CERTIFICATE_YES|Está habilitado el cifrado sin validación de certificados.|  

<a name="sqlcoptsstxnisolation"></a>
## <a name="sql_copt_ss_txn_isolation"></a>SQL_COPT_SS_TXN_ISOLATION  
 SQL_COPT_SS_TXN_ISOLATION establece el atributo de aislamiento de instantáneas específico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. El aislamiento de instantáneas no puede establecerse mediante SQL_ATTR_TXN_ISOLATION porque el valor es específico de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Sin embargo, puede recuperarse mediante SQL_ATTR_TXN_ISOLATION o SQL_COPT_SS_TXN_ISOLATION.  
  
|Value|Descripción|  
|-----------|-----------------|  
|SQL_TXN_SS_SNAPSHOT|Indica desde una transacción no pueden verse los cambios realizados en otras transacciones y que no podrá ver los cambios aunque realice una nueva consulta.|  
  
 Para obtener más información sobre el aislamiento de instantáneas, vea [trabajar con aislamiento de instantánea](../../relational-databases/native-client/features/working-with-snapshot-isolation.md).  
  
## <a name="sql_copt_ss_use_proc_for_prep"></a>SQL_COPT_SS_USE_PROC_FOR_PREP

 Este atributo ya no se admite.  

<a name="sqlcoptssuserdata"></a>
## <a name="sql_copt_ss_user_data"></a>SQL_COPT_SS_USER_DATA  
 SQL_COPT_SS_USER_DATA establece el puntero a los datos del usuario. Los datos del usuario son memoria propiedad del cliente y se registran por conexión.  
  
 Para obtener más información, vea [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md).  

<a name="sqlcoptsswarnoncperror"></a>
## <a name="sql_copt_ss_warn_on_cp_error"></a>SQL_COPT_SS_WARN_ON_CP_ERROR  
 Este atributo determina si obtendrá una advertencia si se pierden datos durante la conversión de una página de códigos. Esto solo se aplica a los datos que provienen del servidor.  
  
|Value|Descripción|  
|-----------|-----------------|  
|SQL_WARN_YES|Generar advertencias cuando se produzca la pérdida de datos durante la conversión de la página de códigos.|  
|SQL_WARN_NO|(Valor predeterminado) No generar advertencias cuando se produzca la pérdida de datos durante la conversión de la página de códigos.|  
  
## <a name="sqlsetconnectattr-support-for-service-principal-names-spns"></a>Compatibilidad de SQLSetConnectAttr con los nombres principales de servicio (SPN)

 SQLSetConnectAttr se puede usar para establecer el valor de los nuevos atributos de conexión SQL_COPT_SS_SERVER_SPN y SQL_COPT_SS_FAILOVER_PARTNER_SPN. Estos atributos no pueden establecerse cuando hay una conexión abierta; si intenta establecer estos atributos cuando hay una conexión abierta, se devuelve el error HY011 con el mensaje "Operación no válida en este momento". (También se puede usar SQLSetConnectOption para establecer estos valores).  
  
 Para obtener más información acerca de los SPN, consulte [nombres de entidad de seguridad de servicio &#40;spn&#41; en conexiones de cliente &#40;&#41;ODBC ](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md).  

<a name="sqlcoptssconnectiondead"></a>
## <a name="sql_copt_ss_connection_dead"></a>SQL_COPT_SS_CONNECTION_DEAD  
 Este atributo es de solo lectura.  
  
 Para obtener más información acerca de SQL_COPT_SS_CONNECTION_DEAD, vea [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) y [conectarse a un origen de datos &#40;&#41;ODBC ](../../relational-databases/native-client-odbc-communication/connecting-to-a-data-source-odbc.md).  
  
## <a name="example"></a>Ejemplo

 En este ejemplo se registran los datos de rendimiento.  
  
```  
SQLPERF*     pSQLPERF;  
SQLINTEGER   nValue;  
  
// See if you are already logging. SQLPERF* will be NULL if not.  
SQLGetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA, &pSQLPERF,  
    sizeof(SQLPERF*), &nValue);  
  
if (pSQLPERF == NULL)  
    {  
    // Set the performance log file name.  
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA_LOG,  
        (SQLPOINTER) "\\My LogDirectory\\MyServerLog.txt", SQL_NTS);  
  
    // Start logging...  
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA,  
        (SQLPOINTER) SQL_PERF_START, SQL_IS_INTEGER);  
    }  
else  
    {  
    // Take a snapshot now so that your performance statistics are discernible.  
    SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA_LOG_NOW, NULL, 0);  
    }  
  
    // ...perform some action...  
  
// ...take a performance data snapshot...  
SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA_LOG_NOW, NULL, 0);  
  
    // ...perform more actions...  
  
// ...take another snapshot...  
SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA_LOG_NOW, NULL, 0);  
  
// ...and disable logging.  
SQLSetConnectAttr(hDbc, SQL_COPT_SS_PERF_DATA,  
    (SQLPOINTER) SQL_PERF_STOP, SQL_IS_INTEGER);  
  
// Continue on...  
```  
  
## <a name="see-also"></a>Consulte también

 [SQLSetConnectAttr, función](https://go.microsoft.com/fwlink/?LinkId=59368)   
 [Detalles de implementación de la API de ODBC](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [Funciones de copia masiva](../../relational-databases/native-client-odbc-extensions-bulk-copy-functions/sql-server-driver-extensions-bulk-copy-functions.md)   
 [ESTABLECER ANSI_NULLS &#40;&#41;de Transact-SQL](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [ESTABLECER ANSI_PADDING &#40;&#41;de Transact-SQL](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [ESTABLECER ANSI_WARNINGS &#40;&#41;de Transact-SQL](../../t-sql/statements/set-ansi-warnings-transact-sql.md)   
 [ESTABLECER CONCAT_NULL_YIELDS_NULL &#40;&#41;de Transact-SQL](../../t-sql/statements/set-concat-null-yields-null-transact-sql.md)   
 [ESTABLECER QUOTED_IDENTIFIER &#40;&#41;de Transact-SQL](../../t-sql/statements/set-quoted-identifier-transact-sql.md)   
 [SQLPrepare (función)](https://go.microsoft.com/fwlink/?LinkId=59360)   
 [SQLGetInfo](../../relational-databases/native-client-odbc-api/sqlgetinfo.md)  
  
  
