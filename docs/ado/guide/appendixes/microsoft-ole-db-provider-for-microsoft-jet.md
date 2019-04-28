---
title: Proveedor Microsoft OLE DB para Microsoft Jet | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/08/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- Jet provider for OLE DB [ADO]
- providers [ADO], OLE DB provider for Microsoft Jet
- OLE DB provider for Microsoft Jet [ADO]
ms.assetid: fd956da1-5203-40af-aa7e-fc13a6c6581f
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 986c1bf7f604f531180a14a4456325ce01702b94
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "62855489"
---
# <a name="microsoft-ole-db-provider-for-microsoft-jet-overview"></a>Proveedor Microsoft OLE DB para Microsoft Jet Introducción
El proveedor OLE DB para Microsoft Jet permite ADO tener acceso a bases de datos Microsoft Jet.

## <a name="connection-string-parameters"></a>Parámetros de cadena de conexión
 Para conectarse a este proveedor, establezca el *proveedor* argumento de la [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propiedad al siguiente:

```vb
Microsoft.Jet.OLEDB.4.0
```

 Leer el [proveedor](../../../ado/reference/ado-api/provider-property-ado.md) propiedad devolverá también esta cadena.

## <a name="typical-connection-string"></a>Cadena de conexión típica
 Una cadena de conexión típica para este proveedor es:

```vb
"Provider=Microsoft.Jet.OLEDB.4.0;Data Source=databaseName;User ID=MyUserID;Password=MyPassword;"
```

 La cadena consta de estas palabras clave:

|Palabra clave|Descripción|
|-------------|-----------------|
|**Proveedor**|Especifica el proveedor OLE DB para Microsoft Jet.|
|**Origen de datos**|Especifica el nombre de ruta de acceso y el archivo de base de datos (por ejemplo, `c:\Northwind.mdb`).|
|**Id. de usuario**|Especifica el nombre de usuario. Si no se especifica esta palabra clave, la cadena, "`admin`", se usa de forma predeterminada.|
|**Contraseña**|Especifica la contraseña del usuario. Si no se especifica esta palabra clave, la cadena vacía (""), se usa de forma predeterminada.|

> [!NOTE]
>  Si se conecta a un proveedor de origen de datos que admite la autenticación de Windows, debe especificar **Trusted_Connection = yes** o **Integrated Security = SSPI** en lugar de Id. de usuario y contraseña información de la cadena de conexión.

## <a name="provider-specific-connection-parameters"></a>Parámetros de conexión específica del proveedor
 El proveedor OLE DB para Microsoft Jet admite varias propiedades dinámicas específicas del proveedor además de los que se definen mediante ADO. Igual que con todos los demás **conexión** parámetros, se puede establecer utilizando la **propiedades** colección de la **conexión** objeto o como parte de la cadena de conexión.

 En la tabla siguiente se enumera estas propiedades junto con el nombre de propiedad de OLE DB correspondiente entre paréntesis.

|Parámetro|Descripción|
|---------------|-----------------|
|Cantidad de espacio recuperado de Jet OLEDB:Compact (DBPROP_JETOLEDB_COMPACTFREESPACESIZE)|Indica una estimación de la cantidad de espacio, en bytes, que se puede recuperar mediante la compactación de la base de datos. Este valor solo es válido después de haber establecido una conexión de base de datos.|
|Control de Jet OLEDB: Connection (DBPROP_JETOLEDB_CONNECTIONCONTROL)|Indica si los usuarios pueden conectarse a la base de datos.|
|Jet OLEDB: crear base de datos del sistema (DBPROP_JETOLEDB_CREATESYSTEMDATABASE)|Indica si se debe crear una base de datos del sistema al crear un nuevo origen de datos.|
|Modo de bloqueo de Jet OLEDB: Database (DBPROP_JETOLEDB_DATABASELOCKMODE)|Indica el modo de bloqueo para esta base de datos. El primer usuario para abrir la base de datos determina el modo utilizado mientras la base de datos está abierto.|
|Jet OLEDB:Database Password (DBPROP_JETOLEDB_DATABASEPASSWORD)|Indica la contraseña de la base de datos.|
|Jet OLEDB: no copiar la configuración regional en Compact (DBPROP_JETOLEDB_COMPACT_DONTCOPYLOCALE)|Indica si Jet debe copiar información de configuración regional cuando se compacta una base de datos.|
|Jet OLEDB: cifrar la base de datos (DBPROP_JETOLEDB_ENCRYPTDATABASE)|Indica si se debe cifrar una base de datos compactado. Si no se establece esta propiedad, se cifrará la base de datos compactado si también se cifró la base de datos original.|
|Tipo de Jet OLEDB:Engine (DBPROP_JETOLEDB_ENGINE)|Indica que el motor de almacenamiento usado para tener acceso al almacén de datos actual.|
|Jet Exclusive Async Delay (DBPROP_JETOLEDB_EXCLUSIVEASYNCDELAY)|Indica la longitud máxima de tiempo, en milisegundos, que Jet puede retardar las escrituras asincrónicas en el disco cuando se abre de forma exclusiva la base de datos.<br /><br /> Esta propiedad se omite a menos que **tiempo de espera de transacción de Jet OLEDB: Flush** se establece en 0.|
|Tiempo de espera de Jet OLEDB: Flush transacción (DBPROP_JETOLEDB_FLUSHTRANSACTIONTIMEOUT)|Indica la cantidad de tiempo de espera antes de que se escriben los datos almacenados en una memoria caché de escritura asincrónica en el disco. Esta configuración invalida los valores de **Jet OLEDB: Shared Async Delay** y **Jet Exclusive Async Delay**.|
|Jet OLEDB: transacciones globales de forma masiva (DBPROP_JETOLEDB_GLOBALBULKNOTRANSACTIONS)|Indica si las transacciones de forma masiva SQL son susceptibles de transacción.|
|Jet OLEDB: Ops Global masiva parcial (DBPROP_JETOLEDB_GLOBALBULKPARTIAL)|Indica la contraseña utilizada para abrir la base de datos.|
|Jet OLEDB: sincronización Commit implícito (DBPROP_JETOLEDB_IMPLICITCOMMITSYNC)|Indica si los cambios realizados en las transacciones implícitas internas se escriben en modo sincrónico o asincrónico.|
|Retraso de Jet OLEDB:Lock (DBPROP_JETOLEDB_LOCKDELAY)|Indica el número de milisegundos que transcurrirán antes de intentar adquirir un bloqueo después de un error anterior.|
|Jet OLEDB:Lock Retry (DBPROP_JETOLEDB_LOCKRETRY)|Indica cuántas veces se repite un intento de acceder a una página bloqueada.|
|Tamaño del búfer Jet OLEDB:Max (DBPROP_JETOLEDB_MAXBUFFERSIZE)|Indica la cantidad máxima de memoria, en kilobytes, Jet puede usar antes de empezar a vaciar los cambios en el disco.|
|Jet OLEDB:Max bloqueos por archivo (DBPROP_JETOLEDB_MAXLOCKSPERFILE)|Indica el número máximo de bloqueos de que Jet puede colocar en una base de datos. El valor predeterminado es 9.500.|
|Jet OLEDB: nueva contraseña de base de datos (DBPROP_JETOLEDB_NEWDATABASEPASSWORD)|Indica la nueva contraseña que se establezca para esta base de datos. La contraseña antigua se almacena en **Jet OLEDB: Database Password**.|
|Jet OLEDB:ODBC comando vencen (DBPROP_JETOLEDB_ODBCCOMMANDTIMEOUT)|Indica que el número de milisegundos antes de una consulta remota ODBC de Jet agotará el tiempo.|
|Jet OLEDB:Page bloquea el bloqueo de tabla (DBPROP_JETOLEDB_PAGELOCKSTOTABLELOCK)|Indica cuántas páginas deben estar bloqueadas dentro de una transacción para que Jet intenta promover el bloqueo a un bloqueo de tabla. Si este valor es 0, nunca se promueve el bloqueo.|
|Tiempo de espera de Jet OLEDB:Page (DBPROP_JETOLEDB_PAGETIMEOUT)|Indica el número de milisegundos que esperará Jet antes de comprobar para ver si es su memoria caché no actualizada con el archivo de base de datos.|
|Jet OLEDB:Recycle con valores de prolongada páginas (DBPROP_JETOLEDB_RECYCLELONGVALUEPAGES)|Indica si Jet agresivamente debería intentar recuperar páginas BLOB cuando se liberan.|
|Ruta de acceso de Jet OLEDB:Registry (DBPROP_JETOLEDB_REGPATH)|Indica la clave del registro de Windows que contiene valores para el motor de base de datos Jet.|
|Estadísticas de Jet OLEDB:Reset ISAM (DBPROP_JETOLEDB_RESETISAMSTATS)|Indica si el esquema **Recordset** DBSCHEMA_JETOLEDB_ISAMSTATS debe restablecer sus contadores de rendimiento después de que devuelve información sobre el rendimiento.|
|Jet OLEDB: compartido Async retraso (DBPROP_JETOLEDB_SHAREDASYNCDELAY)|Indica la cantidad máxima de tiempo, en milisegundos, Jet puede retardar las escrituras asincrónicas en el disco cuando la base de datos se abre en modo multiusuario.|
|Base de datos de Jet OLEDB (DBPROP_JETOLEDB_SYSDBPATH)|Indica la ruta de acceso y nombre de archivo para el archivo de información de grupo de trabajo (base de datos del sistema).|
|Modo de confirmación de Jet OLEDB:Transaction (DBPROP_JETOLEDB_TXNCOMMITMODE)|Indica si Jet escribe datos en el disco de forma sincrónica o asincrónica cuando se confirma una transacción.|
|Sincronización de confirmación de Jet OLEDB:User (DBPROP_JETOLEDB_USERCOMMITSYNC)|Indica si los cambios realizados en las transacciones se escriben en modo sincrónico o asincrónico.|

## <a name="provider-specific-recordset-and-command-properties"></a>Conjunto de registros específicos del proveedor y las propiedades de comando
 El proveedor de Jet también admite varias específica del proveedor **Recordset** y **comando** propiedades. Se tiene acceso a estas propiedades y se establece a través del **propiedades** colección de la **Recordset** o **comando** objeto. La tabla muestra el nombre de la propiedad ADO y su nombre de propiedad de OLE DB correspondiente entre paréntesis.

|Nombre de la propiedad|Descripción|
|-------------------|-----------------|
|Transacciones de Jet OLEDB:Bulk (DBPROP_JETOLEDB_BULKNOTRANSACTIONS)|Indica si se negocian operaciones masivas de SQL. Las operaciones masivas de gran tamaño pueden producir un error cuando la transacción debido a retrasos de recursos.|
|Jet OLEDB: Enable Fat Cursors (DBPROP_JETOLEDB_ENABLEFATCURSOR)|Indica si Jet debe almacenar en caché varias filas al rellenar un conjunto de registros para los orígenes de filas remoto.|
|Tamaño de caché de Cursor de Jet OLEDB:Fat (DBPROP_JETOLEDB_FATCURSORMAXROWS)|Indica el número de filas en memoria caché cuando se usa el almacenamiento en caché de datos remotos almacén de filas. Este valor se omite a menos que **Jet OLEDB: Enable Fat Cursors** es True.|
|Jet OLEDB: incoherente (DBPROP_JETOLEDB_INCONSISTENT)|Indica si los resultados de consulta permiten actualizaciones incoherentes.|
|Jet OLEDB: bloqueo granularidad (DBPROP_JETOLEDB_LOCKGRANULARITY)|Indica si una tabla se abre mediante el bloqueo de nivel de fila.|
|Instrucción de paso a través de Jet OLEDB:ODBC (DBPROP_JETOLEDB_ODBCPASSTHROUGH)|Indica que Jet debe pasar el texto SQL en un **comando** objeto para el back-end sin modificaciones.|
|Jet OLEDB:Partial masiva Ops (DBPROP_JETOLEDB_BULKPARTIAL)|Indica el comportamiento de Jet cuando las operaciones DML SQL producirá un error.|
|Jet OLEDB:Pass a través de la consulta Bulk-Op (DBPROP_JETOLEDB_PASSTHROUGHBULKOP)|Indica si las consultas que no devuelven un **Recordset** se pasa sin cambios al origen de datos.|
|(DBPROP_JETOLEDB_ODBCPASSTHROUGHCONNECTSTRING) de la cadena de conexión de Jet OLEDB:Pass a través de la consulta|Indica la cadena de conexión de Jet utilizada para conectarse a un almacén de datos remoto. Este valor se omite a menos que **instrucción de paso a través de Jet OLEDB:ODBC** es True.|
|Jet OLEDB: almacena la consulta (DBPROP_JETOLEDB_STOREDQUERY)|Indica si el texto del comando se debe interpretar como una consulta almacenada en lugar de un comando SQL.|
|Jet OLEDB: validar reglas en conjunto (DBPROP_JETOLEDB_VALIDATEONSET)|Indica si las reglas de validación de Jet se evalúan cuando se establece la columna de datos o cuando se confirman los cambios en la base de datos.|

 De forma predeterminada, el proveedor OLE DB para Microsoft Jet abre las bases de datos Microsoft Jet en modo de lectura/escritura. Para abrir una base de datos en modo de solo lectura, establezca el [modo](../../../ado/reference/ado-api/mode-property-ado.md) propiedad ADO **conexión** objeto **adModeRead**.

## <a name="command-object-usage"></a>Uso del objeto Command
 Texto del comando el [comando](../../../ado/reference/ado-api/command-object-ado.md) objeto utiliza el dialecto de SQL de Microsoft Jet. Puede especificar consultas que devuelven filas, las consultas de acción y los nombres de tabla en el texto de comando; Sin embargo, los procedimientos almacenados no se admiten y no deben especificarse.

## <a name="recordset-behavior"></a>Comportamiento del conjunto de registros
 El motor de base de datos Microsoft Jet no es compatible con los cursores dinámicos. Por lo tanto, el proveedor OLE DB para Microsoft Jet no admite la **adLockDynamic** tipo de cursor. Cuando se solicita un cursor dinámico, el proveedor devolverá un cursor keyset y restablecer el [CursorType](../../../ado/reference/ado-api/cursortype-property-ado.md) propiedad para indicar el tipo de [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md) devuelto. Asimismo, si un actualizable **Recordset** se solicita (**LockType** es **adLockOptimistic**, **adLockBatchOptimistic**, o **adLockPessimistic**) el proveedor también devolverá un cursor keyset y restablecer el **CursorType** propiedad.

## <a name="dynamic-properties"></a>Propiedades dinámicas
 El proveedor OLE DB para Microsoft Jet inserta varias propiedades dinámicas en la **propiedades** colección de los no abierto [conexión](../../../ado/reference/ado-api/connection-object-ado.md), [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)y [Comando](../../../ado/reference/ado-api/command-object-ado.md) objetos.

 Las tablas siguientes son un índice cruzado de los nombres de ADO y OLE DB para cada propiedad dinámica. Referencia de la base de datos del programador de OLE se refiere a un nombre de la propiedad ADO con el término, "Description". Puede encontrar más información acerca de estas propiedades en referencia del programador de OLE DB.

## <a name="connection-dynamic-properties"></a>Propiedades dinámicas de conexión
 Las siguientes propiedades se agregan a la **propiedades** colección de la **conexión** objeto.

|Nombre de la propiedad ADO|Nombre de propiedad OLE DB|
|-----------------------|--------------------------|
|Sesiones activas|DBPROP_ACTIVESESSIONS|
|Anulación asincrónica|DBPROP_ASYNCTXNABORT|
|Confirmación asíncrona|DBPROP_ASYNCTNXCOMMIT|
|Niveles de aislamiento de confirmación automática|DBPROP_SESS_AUTOCOMMITISOLEVELS|
|Ubicación del catálogo|DBPROP_CATALOGLOCATION|
|Término de catálogo|DBPROP_CATALOGTERM|
|Definición de columna|DBPROP_COLUMNDEFINITION|
|Catálogo actual|DBPROP_CURRENTCATALOG|
|Origen de datos|DBPROP_INIT_DATASOURCE|
|Data Source Name|DBPROP_DATASOURCENAME|
|Objeto de origen de datos modelo de subprocesos|DBPROP_DSOTHREADMODEL|
|Nombre DBMS|DBPROP_DBMSNAME|
|Versión DBMS|DBPROP_DBMSVER|
|Compatibilidad GROUP BY|DBPROP_GROUPBY|
|Compatibilidad con tablas heterogéneas|DBPROP_HETEROGENEOUSTABLES|
|Minúsculas en identificadores|DBPROP_IDENTIFIERCASE|
|Niveles de aislamiento|DBPROP_SUPPORTEDTXNISOLEVELS|
|Retención de aislamiento|DBPROP_SUPPORTEDTXNISORETAIN|
|Identificador de configuración regional|DBPROP_INIT_LCID|
|Tamaño máximo de índice|DBPROP_MAXINDEXSIZE|
|Tamaño máximo de fila|DBPROP_MAXROWSIZE|
|Tamaño máximo de fila incluye BLOB|DBPROP_MAXROWSIZEINCLUDESBLOB|
|Número máximo de tablas en SELECT|DBPROP_MAXTABLESINSELECT|
|Modo|DBPROP_INIT_MODE|
|Varios conjuntos de parámetros|DBPROP_MULTIPLEPARAMSETS|
|Varios resultados|DBPROP_MULTIPLERESULTS|
|Varios objetos de almacenamiento|DBPROP_MULTIPLESTORAGEOBJECTS|
|Actualización de varias tablas|DBPROP_MULTITABLEUPDATE|
|Orden de intercalación de NULL|DBPROP_NULLCOLLATION|
|Comportamiento de concatenación de NULL|DBPROP_CONCATNULLBEHAVIOR|
|Versión OLE DB|DBPROP_PROVIDEROLEDBVER|
|Compatibilidad con objetos OLE|DBPROP_OLEOBJECTS|
|Conjunto de filas abierto|DBPROP_OPENROWSETSUPPORT|
|Columnas ORDER BY en la lista de selección|DBPROP_ORDERBYCOLUMNSINSELECT|
|Disponibilidad de parámetro de salida|DBPROP_OUTPUTPARAMETERAVAILABILITY|
|Pasar por Ref descriptores de acceso|DBPROP_BYREFACCESSORS|
|Contraseña|DBPROP_AUTH_PASSWORD|
|Tipo de Id.|DBPROP_PERSISTENTIDTYPE|
|Preparar el comportamiento de anulación|DBPROP_PREPAREABORTBEHAVIOR|
|Preparar el comportamiento de confirmación|DBPROP_PREPARECOMMITBEHAVIOR|
|Término de procedimiento|DBPROP_PROCEDURETERM|
|Pedir datos|DBPROP_INIT_PROMPT|
|Nombre descriptivo del proveedor|DBPROP_PROVIDERFRIENDLYNAME|
|Provider Name|DBPROP_PROVIDERFILENAME|
|Versión del proveedor|DBPROP_PROVIDERVER|
|Origen de datos de solo lectura|DBPROP_DATASOURCEREADONLY|
|Conversiones de conjunto de filas en el comando|DBPROP_ROWSETCONVERSIONSONCOMMAND|
|Término de esquema|DBPROP_SCHEMATERM|
|Uso del esquema|DBPROP_SCHEMAUSAGE|
|Compatibilidad con SQL|DBPROP_SQLSUPPORT|
|Almacenamiento estructurado|DBPROP_STRUCTUREDSTORAGE|
|Compatibilidad para subconsultas|DBPROP_SUBQUERIES|
|Término de tabla|DBPROP_TABLETERM|
|Transacción de DDL|DBPROP_SUPPORTEDTXNDDL|
|Id. de usuario|DBPROP_AUTH_USERID|
|Nombre de usuario|DBPROP_USERNAME|
|Identificador de ventana|DBPROP_INIT_HWND|

## <a name="recordset-dynamic-properties"></a>Propiedades del conjunto de registros dinámicos
 Las siguientes propiedades se agregan a la **propiedades** colección de la **Recordset** objeto.

|Nombre de la propiedad ADO|Nombre de propiedad OLE DB|
|-----------------------|--------------------------|
|Orden de acceso|DBPROP_ACCESSORDER|
|Conjunto de filas de sólo anexar|DBPROP_APPENDONLY|
|Bloquear objetos de almacenamiento|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo de marcador|DBPROP_BOOKMARKTYPE|
|Admite marcadores|DBPROP_IROWSETLOCATE|
|Marcadores solicitados|DBPROP_ORDEREDBOOKMARKS|
|Almacenar en caché columnas aplazadas|DBPROP_CACHEDEFERRED|
|Cambiar filas insertadas|DBPROP_CHANGEINSERTEDROWS|
|Privilegios de columna|DBPROP_COLUMNRESTRICT|
|Notificación de conjunto de columnas|DBPROP_NOTIFYCOLUMNSET|
|Escritura de la columna|DBPROP_MAYWRITECOLUMN|
|Aplazar la columna|DBPROP_DEFERRED|
|Actualizaciones de objetos de almacenamiento de retraso|DBPROP_DELAYSTORAGEOBJECTS|
|Buscar hacia atrás|DBPROP_CANFETCHBACKWARDS|
|Conservar filas|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|ILockBytes|DBPROP_ILockBytes|
|Filas inmóviles|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetIndex|DBPROP_IRowsetIndex|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsestLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|IStorage|DBPROP_IStorage|
|IStream|DBPROP_IStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|Marcadores literales|DBPROP_LITERALBOOKMARKS|
|Identidad de fila literal|DBPROP_LITERALIDENTITY|
|Número máximo de filas abierto|DBPROP_MAXOPENROWS|
|Máximo de filas pendientes|DBPROP_MAXPENDINGROWS|
|Número máximo de filas|DBPROP_MAXROWS|
|Utilización de la memoria|DBPROP_MEMORYUSAGE|
|Granularidad de notificación|DBPROP_NOTIFICATIONGRANULARITY|
|Fases de notificación|DBPROP_NOTIFICATIONPHASES|
|Objetos de transacción|DBPROP_TRANSACTEDOBJECT|
|Cambios visibles de otros usuarios|DBPROP_OTHERUPDATEDELETE|
|Inserciones visibles de otros usuarios|DBPROP_OTHERINSERT|
|Propios cambios visibles|DBPROP_OWNUPDATEDELETE|
|Propias inserciones visibles|DBPROP_OWNINSERT|
|Conservar al anular|DBPROP_ABORTPRESERVE|
|Conservar al confirmar|DBPROP_COMMITPRESERVE|
|Reinicio rápido|DBPROP_QUICKRESTART|
|Eventos reentrantes|DBPROP_REENTRANTEVENTS|
|Quitar filas eliminadas|DBPROP_REMOVEDELETED|
|Comunicar múltiples cambios|DBPROP_REPORTMULTIPLECHANGES|
|Devolver inserciones pendientes|DBPROP_RETURNPENDINGINSERTS|
|Notificación de eliminación de fila|DBPROP_NOTIFYROWDELETE|
|Primera notificación de cambio de fila|DBPROP_NOTIFYROWFIRSTCHANGE|
|Notificación de inserción de fila|DBPROP_NOTIFYROWINSERT|
|Privilegios de fila|DBPROP_ROWRESTRICT|
|Notificación de resincronización de fila|DBPROP_NOTIFYROWRESYNCH|
|Modelo de subprocesos de fila|DBPROP_ROWTHREADMODEL|
|Notificación de cambio de deshacer de fila|DBPROP_NOTIFYROWUNDOCHANGE|
|Notificación de eliminación de deshacer de fila|DBPROP_NOTIFYROWUNDODELETE|
|Notificación de inserción de deshacer de fila|DBPROP_NOTIFYROWUNDOINSERT|
|Notificación de actualización de fila|DBPROP_NOTIFYROWUPDATE|
|Notificación de cambio de posición de captura del conjunto de filas|DBPROP_NOTIFYROWSETFETCHPOSISIONCHANGE|
|Notificación de liberación del conjunto de filas|DBPROP_NOTIFYROWSETRELEASE|
|Desplazar hacia atrás|DBPROP_CANSCROLLBACKWARDS|
|Omitir marcadores eliminados|DBPROP_BOOKMARKSKIPPED|
|Identidad de fila segura|DBPROP_STRONGITDENTITY|
|Posibilidad de actualización|DBPROP_UPDATABILITY|
|Utilizar marcadores|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>Propiedades dinámicas de comando
 Las siguientes propiedades se agregan a la **propiedades** colección de la **comando** objeto.

|Nombre de la propiedad ADO|Nombre de propiedad OLE DB|
|-----------------------|--------------------------|
|Orden de acceso|DBPROP_ACCESSORDER|
|Conjunto de filas de sólo anexar|DBPROP_APPENDONLY|
|Bloquear objetos de almacenamiento|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo de marcador|DBPROP_BOOKMARKTYPE|
|Admite marcadores|DBPROP_IROWSETLOCATE|
|Cambiar filas insertadas|DBPROP_CHANGEINSERTEDROWS|
|Privilegios de columna|DBPROP_COLUMNRESTRICT|
|Notificación de conjunto de columnas|DBPROP_NOTIFYCOLUMNSET|
|Aplazar la columna|DBPROP_DEFERRED|
|Actualizaciones de objetos de almacenamiento de retraso|DBPROP_DELAYSTORAGEOBJECTS|
|Buscar hacia atrás|DBPROP_CANFETCHBACKWARDS|
|Conservar filas|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|ILockBytes|DBPROP_ILockBytes|
|Filas inmóviles|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetIndex|DBPROP_IRowsetIndex|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsetLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|IStorage|DBPROP_IStorage|
|IStream|DBPROP_IStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|Marcadores literales|DBPROP_LITERALBOOKMARKS|
|Identidad de fila literal|DBPROP_LITERALIDENTITY|
|Modo de bloqueo|DBPROP_LOCKMODE|
|Número máximo de filas abierto|DBPROP_MAXOPENROWS|
|Máximo de filas pendientes|DBPROP_MAXPENDINGROWS|
|Número máximo de filas|DBPROP_MAXROWS|
|Granularidad de notificación|DBPROP_NOTIFICATIONGRANULARITY|
|Fases de notificación|DBPROP_NOTIFICATIONPHASES|
|Objetos de transacción|DBPROP_TRANSACTEDOBJECT|
|Cambios visibles de otros usuarios|DBPROP_OTHERUPDATEDELETE|
|Inserciones visibles de otros usuarios|DBPROP_OTHERINSERT|
|Propios cambios visibles|DBPROP_OWNUPDATEDELETE|
|Propias inserciones visibles|DBPROP_OWNINSERT|
|Conservar al anular|DBPROP_ABORTPRESERVE|
|Conservar al confirmar|DBPROP_COMMITPRESERVE|
|Reinicio rápido|DBPROP_QUICKRESTART|
|Eventos reentrantes|DBPROP_REENTRANTEVENTS|
|Quitar filas eliminadas|DBPROP_REMOVEDELETED|
|Comunicar múltiples cambios|DBPROP_REPORTMULTIPLECHANGES|
|Devolver inserciones pendientes|DBPROP_RETURNPENDINGINSERTS|
|Notificación de eliminación de fila|DBPROP_NOTIFYROWDELETE|
|Primera notificación de cambio de fila|DBPROP_NOTIFYROWFIRSTCHANGE|
|Notificación de inserción de fila|DBPROP_NOTIFYROWINSERT|
|Privilegios de fila|DBPROP_ROWRESTRICT|
|Notificación de resincronización de fila|DBPROP_NOTIFYROWRESYNCH|
|Modelo de subprocesos de fila|DBPROP_ROWTHREADMODEL|
|Notificación de cambio de deshacer de fila|DBPROP_NOTIFYROWUNDOCHANGE|
|Notificación de eliminación de deshacer de fila|DBPROP_NOTIFYROWUNDODELETE|
|Notificación de inserción de deshacer de fila|DBPROP_NOTIFYROWUNDOINSERT|
|Notificación de actualización de fila|DBPROP_NOTIFYROWUPDATE|
|Notificación de cambio de posición de captura del conjunto de filas|DBPROP_NOTIFYROWSETFETCHPOSITIONCHANGE|
|Notificación de liberación del conjunto de filas|DBPROP_NOTIFYROWSETRELEASE|
|Desplazar hacia atrás|DBPROP_CANSCROLLBACKWARDS|
|Datos del servidor durante la inserción|DBPROP_SERVERDATAONINSERT|
|Omitir marcadores eliminados|DBPROP_BOOKMARKSKIP|
|Identidad de fila segura|DBPROP_STRONGIDENTITY|
|Posibilidad de actualización|DBPROP_UPDATABILITY|
|Utilizar marcadores|DBPROP_BOOKMARKS|

 Para detalles de implementación específicos y funcional sobre el proveedor OLE DB para Microsoft Jet, vea [proveedor Jet](https://msdn.microsoft.com/library/windows/desktop/ms722791.aspx) en la documentación de OLE DB.
