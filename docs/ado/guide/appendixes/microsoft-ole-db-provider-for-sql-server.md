---
title: Proveedor Microsoft OLE DB para SQL Server | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- providers [ADO], OLE DB provider for SQL Server
- OLE DB provider for SQL Server [ADO]
- SQLOLEDB [ADO]
ms.assetid: 99bc40c4-9181-4ca1-a06f-9a1a914a0b7b
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 41eae162370ed26a1d84428f1c4e6a5d7eb5e2c7
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/12/2018
ms.locfileid: "38980697"
---
# <a name="microsoft-ole-db-provider-for-sql-server-overview"></a>Proveedor Microsoft OLE DB para Introducción a SQL Server
El proveedor Microsoft OLE DB para SQL Server, SQLOLEDB, permite que ADO tener acceso a Microsoft SQL Server.

**Nota:** no se recomienda utilizar este controlador para el nuevo desarrollo. El nuevo proveedor de OLE DB se llama a la [controlador OLE DB de Microsoft para SQL Server](../../../connect/oledb/oledb-driver-for-sql-server.md) (MSOLEDBSQL) que se actualizará con las características más recientes del servidor en el futuro.

## <a name="connection-string-parameters"></a>Parámetros de cadena de conexión
 Para conectarse a este proveedor, establezca el *proveedor* argumento para el [ConnectionString](../../../ado/reference/ado-api/connectionstring-property-ado.md) propiedad:

```
SQLOLEDB
```

 Este valor también se puede establecer o leer utilizando el [proveedor](../../../ado/reference/ado-api/provider-property-ado.md) propiedad.

## <a name="typical-connection-string"></a>Cadena de conexión típica
 Una cadena de conexión típica para este proveedor es:

```
"Provider=SQLOLEDB;Data Source=serverName;"
Initial Catalog=databaseName;
User ID=MyUserID;Password=MyPassword;"
```

 La cadena consta de estas palabras clave:

|Palabra clave|Descripción|
|-------------|-----------------|
|**Proveedor**|Especifica el proveedor OLE DB para SQL Server.|
|**Origen de datos** o **Server**|Especifica el nombre de un servidor.|
|**Catálogo inicial** o **base de datos**|Especifica el nombre de una base de datos en el servidor.|
|**Id. de usuario** o **uid**|Especifica el nombre de usuario (para autenticación de SQL Server).|
|**Contraseña** o **pwd**|Especifica la contraseña de usuario (para autenticación de SQL Server).|

> [!NOTE]
>  Si se conecta a un proveedor de origen de datos que admite la autenticación de Windows, debe especificar **Trusted_Connection = yes** o **Integrated Security = SSPI** en lugar de Id. de usuario y contraseña información de la cadena de conexión.

## <a name="provider-specific-connection-parameters"></a>Parámetros de conexión específica del proveedor
 El proveedor admite varios parámetros de conexión específica del proveedor además de los definidos por ADO. Como con las propiedades de conexión ADO, se pueden establecer estas propiedades específicas del proveedor a través de la [propiedades](../../../ado/reference/ado-api/properties-collection-ado.md) colección de un [conexión](../../../ado/reference/ado-api/connection-object-ado.md) o puede establecerse como parte de la **ConnectionString**.

|Parámetro|Descripción|
|---------------|-----------------|
|Trusted_Connection|Indica el modo de autenticación de usuario. Esto se puede establecer en **Sí** o **No**. El valor predeterminado es **No**. Si esta propiedad se establece en **Sí**, SQLOLEDB utiliza el modo de autenticación de Microsoft Windows NT para autorizar el acceso de usuario a la base de datos de SQL Server especificado por el **ubicación** y [origen de datos ](../../../ado/reference/ado-api/datasource-property-ado.md) los valores de propiedad. Si esta propiedad se establece en **No**, SQLOLEDB utiliza el modo mixto para autorizar el acceso de usuario a la base de datos de SQL Server. El inicio de sesión de SQL Server y la contraseña se especifican en el **Id. de usuario** y **contraseña** propiedades.|
|Idioma actual|Indica un nombre de idioma de SQL Server. Identifica el lenguaje que se usa para la selección y el formato de mensajes del sistema. El idioma debe instalarse en el servidor SQL Server, apertura en caso contrario, se producirá un error en la conexión.|
|Dirección de red|Indica la dirección de red de SQL Server especificado por el **ubicación** propiedad.|
|Biblioteca de red|Indica el nombre de la biblioteca de red (DLL) utilizada para comunicarse con el servidor SQL Server. El nombre no debe incluir la ruta de acceso ni la extensión de nombre de archivo .dll. El valor predeterminado es proporcionado por la configuración de cliente de SQL Server.|
|Usar procedimiento para preparar|Determina si SQL Server crea los procedimientos almacenados temporales cuando se preparan los comandos (mediante el **Prepared** propiedad).|
|Traducir automáticamente|Indica si se convierten los caracteres OEM/ANSI. Esta propiedad puede establecerse en **True** o **False**. El valor predeterminado es **True**. Si esta propiedad se establece en **True**, SQLOLEDB realiza la conversión de caracteres OEM/ANSI cuando se recuperan de las cadenas de caracteres multibyte o envía a SQL Server. Si esta propiedad se establece en **False**, SQLOLEDB no realiza la conversión de caracteres OEM/ANSI en los datos de cadena de caracteres multibyte.|
|Tamaño del paquete|Indica un tamaño de paquete de red en bytes. El valor de propiedad de tamaño de paquete debe estar entre 512 y 32767. El tamaño de paquete de red SQLOLEDB predeterminado es 4096.|
|Application Name|Indica el nombre de la aplicación cliente.|
|Id. de estación de trabajo|Cadena que identifica la estación de trabajo.|

## <a name="command-object-usage"></a>Uso del objeto Command
 SQLOLEDB acepta una amalgama de ODBC, ANSI y específicas de SQL Server Transact-SQL como sintaxis válida. Por ejemplo, la siguiente instrucción SQL utiliza una secuencia de escape de ODBC SQL para especificar la función de cadena LCASE:

```
SELECT customerid={fn LCASE(CustomerID)} FROM Customers

```

 LCASE devuelve una cadena de caracteres, convirtiendo todos los caracteres en mayúscula en sus equivalentes en minúscula. La función de cadena ANSI SQL LOWER realiza la misma operación, por lo que la siguiente instrucción SQL es un equivalente a la instrucción ODBC presentada anteriormente ANSI:

```
SELECT customerid=LOWER(CustomerID) FROM Customers

```

 SQLOLEDB procesa correctamente cualquiera de las formas de la instrucción cuando se especifica como texto de un comando.

## <a name="stored-procedures"></a>Procedimientos almacenados
 Al ejecutar un servidor SQL Server mediante un comando SQLOLEDB de procedimiento almacenado, utilice la secuencia de escape de llamada de procedimiento ODBC en el texto del comando. SQLOLEDB, a continuación, utiliza el mecanismo de llamada a procedimiento remoto de SQL Server para optimizar el procesamiento de comandos. Por ejemplo, la siguiente instrucción SQL de ODBC es el texto de comando preferido sobre el formulario de Transact-SQL:

## <a name="odbc-sql"></a>ODBC SQL

```
{call SalesByCategory('Produce', '1995')}

```

## <a name="transact-sql"></a>Transact-SQL

```
EXECUTE SalesByCategory 'Produce', '1995'

```

## <a name="sql-server-features"></a>Características de SQL Server
 Con SQL Server, ADO puede usar XML para **comando** indicar y recuperar los resultados en formato de secuencia XML en lugar de en **Recordset** objetos. Para obtener más información, consulte [mediante secuencias de entrada de comando](../../../ado/guide/data/command-streams.md) y [recuperar conjuntos de resultados en secuencias](../../../ado/guide/data/retrieving-resultsets-into-streams.md).

### <a name="accessing-sqlvariant-data-using-mdac-27-mdac-28-or-windows-dac-60"></a>Acceso a datos de sql_variant con MDAC 2.7, MDAC 2.8 o Windows DAC 6.0
 Microsoft SQL Server tiene un tipo de datos denominado **sql_variant**. Similar de OLE DB **DBTYPE_VARIANT**, **sql_variant** tipo de datos puede almacenar datos de varios tipos diferentes. Sin embargo, hay algunas diferencias importantes entre **DBTYPE_VARIANT** y **sql_variant**. ADO también controla los datos almacenados como un **sql_variant** valor de forma diferente a cómo controla los otros tipos de datos. En la lista siguiente se describe los problemas para tener en cuenta al acceder a datos de SQL Server almacenados en columnas de tipo **sql_variant**.

-   En Windows Data Access Components (Windows DAC) 6.0, MDAC 2.8 y MDAC 2.7, es compatible con el proveedor OLE DB para SQL Server la **sql_variant** tipo. El proveedor OLE DB para ODBC no lo hace.

-   El **sql_variant** tipo coincide exactamente el **DBTYPE_VARIANT** tipo de datos.  El **sql_variant** tipo es compatible con unos nuevos subtipos no admitidas **DBTYPE_VARIANT,** incluidos **GUID**, **ANSI** (no UNICODE) las cadenas, y **BIGINT**. Mediante subtipos distintos de los enumerados anteriormente funcionará correctamente.

-   El **sql_variant** subtipo **numérico** no coincide con el **DBTYPE_DECIMAL** de tamaño.

-   Varias conversiones de tipos de datos dará como resultado los tipos que no coinciden. Por ejemplo, forzar una **sql_variant** con un subtipo de **GUID** a un **DBTYPE_VARIANT** dará como resultado un subtipo de **safearray**(bytes) . Convertir este tipo de copia en un **sql_variant** dará como resultado un subtipo del nuevo **matriz**(bytes).

-   **Conjunto de registros** los campos que contienen **sql_variant** los datos se pueden enviar de forma remota (serializa) o persistente sólo si el **sql_variant** contiene subtipos específicos. Intentando remoto o conservar los datos con los siguientes no admitidos subtipos provocará un error de tiempo de ejecución (conversión no admitida) desde el proveedor de persistencia de Microsoft (MSPersist): **VT_VARIANT**, **VT_RECORD**, **VT_ILLEGAL**, **VT_UNKNOWN**, **VT_BSTR**, y **VT_DISPATCH.**

-   El proveedor OLE DB para SQL Server en Windows DAC 6.0, MDAC 2.8 y MDAC 2.7 tiene una propiedad dinámica llamada **permitir variantes nativas** que, como el nombre implica, permite a los desarrolladores tener acceso a la **sql_variant** en su formato nativo en contraposición a un **DBTYPE_VARIANT**. Si se establece esta propiedad y un **Recordset** se abre con el motor de Cursor de cliente (**adUseClient**), el **Recordset.Open** llamada producirá un error. Si se establece esta propiedad y un **Recordset** se abre con los cursores de servidor (**adUseServer**), el **Recordset.Open** llamada se realizará correctamente, pero tienen acceso a columnas de tipo **sql_variant** producirá un error.

-   En aplicaciones cliente que utilizan MDAC 2.5, **sql_variant** datos pueden usarse con consultas en Microsoft SQL Server. Sin embargo, los valores de la **sql_variant** datos se tratan como cadenas. Estas aplicaciones cliente deben actualizarse a MDAC 2.7, MDAC 2.8 o Windows DAC 6.0.

## <a name="recordset-behavior"></a>Comportamiento del conjunto de registros
 SQLOLEDB no puede utilizar cursores de SQL Server para admitir la variedad de resultados generado por muchos comandos. Si un consumidor solicita un conjunto de registros que requieren compatibilidad con cursores de SQL Server, se produce un error si el texto del comando utilizado genera más de un único conjunto de registros como su resultado.

 Conjuntos de registros SQLOLEDB desplazables son compatibles con cursores de SQL Server. SQL Server impone limitaciones en los cursores que son sensibles a los cambios realizados por otros usuarios de la base de datos. En concreto, no se puede ordenar las filas de algunos cursores, y puede producir un error al intentar crear un conjunto de registros mediante un comando que contiene una cláusula SQL ORDER BY.

## <a name="dynamic-properties"></a>Propiedades dinámicas
 El proveedor Microsoft OLE DB para SQL Server inserta varias propiedades dinámicas en la **propiedades** colección de los no abierto [conexión](../../../ado/reference/ado-api/connection-object-ado.md), [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md)y [ Comando](../../../ado/reference/ado-api/command-object-ado.md) objetos.

 Las tablas siguientes son un índice cruzado de los nombres de ADO y OLE DB para cada propiedad dinámica. Referencia de la base de datos del programador de OLE se refiere a un nombre de la propiedad ADO con el término "Description". Puede encontrar más información acerca de estas propiedades en referencia del programador de OLE DB. Busque el nombre de propiedad de OLE DB en el índice o vea [Apéndice C: propiedades de OLE DB](http://msdn.microsoft.com/deded3ff-f508-4e1b-b2b1-fd9afd3bd292).

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
|Tiempo de espera de la conexión|DBPROP_INIT_TIMEOUT|
|Catálogo actual|DBPROP_CURRENTCATALOG|
|Origen de datos|DBPROP_INIT_DATASOURCE|
|Data Source Name|DBPROP_DATASOURCENAME|
|Objeto de origen de datos modelo de subprocesos|DBPROP_DSOTHREADMODEL|
|Nombre DBMS|DBPROP_DBMSNAME|
|Versión DBMS|DBPROP_DBMSVER|
|Propiedades extendidas|DBPROP_INIT_PROVIDERSTRING|
|Compatibilidad GROUP BY|DBPROP_GROUPBY|
|Compatibilidad con tablas heterogéneas|DBPROP_HETEROGENEOUSTABLES|
|Minúsculas en identificadores|DBPROP_IDENTIFIERCASE|
|Catálogo original|DBPROP_INIT_CATALOG|
|Niveles de aislamiento|DBPROP_SUPPORTEDTXNISOLEVELS|
|Retención de aislamiento|DBPROP_SUPPORTEDTXNISORETAIN|
|Identificador de configuración regional|DBPROP_INIT_LCID|
|Tamaño máximo de índice|DBPROP_MAXINDEXSIZE|
|Tamaño máximo de fila|DBPROP_MAXROWSIZE|
|Tamaño máximo de fila incluye BLOB|DBPROP_MAXROWSIZEINCLUDESBLOB|
|Número máximo de tablas en SELECT|DBPROP_MAXTABLESINSELECT|
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
|Persist Security Info|DBPROP_AUTH_PERSIST_SENSITIVE_AUTHINFO|
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
|Bloquear objetos de almacenamiento|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo de marcador|DBPROP_BOOKMARKTYPE|
|Admite marcadores|DBPROP_IROWSETLOCATE|
|Cambiar filas insertadas|DBPROP_CHANGEINSERTEDROWS|
|Privilegios de columna|DBPROP_COLUMNRESTRICT|
|Notificación de conjunto de columnas|DBPROP_NOTIFYCOLUMNSET|
|Tiempo de espera de comando|DBPROP_COMMANDTIMEOUT|
|Aplazar la columna|DBPROP_DEFERRED|
|Actualizaciones de objetos de almacenamiento de retraso|DBPROP_DELAYSTORAGEOBJECTS|
|Buscar hacia atrás|DBPROP_CANFETCHBACKWARDS|
|Conservar filas|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|Filas inmóviles|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsestLocate|
|IRowsetResynch||
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
|ISupportErrorInfo|DBPROP_ISupportErrorInfo|
|Marcadores literales|DBPROP_LITERALBOOKMARKS|
|Identidad de fila literal|DBPROP_LITERALIDENTITY|
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
|Notificación de cambio de posición de captura del conjunto de filas|DBPROP_NOTIFYROWSETFETCHPOSISIONCHANGE|
|Notificación de liberación del conjunto de filas|DBPROP_NOTIFYROWSETRELEASE|
|Desplazar hacia atrás|DBPROP_CANSCROLLBACKWARDS|
|Cursor de servidor|DBPROP_SERVERCURSOR|
|Omitir marcadores eliminados|DBPROP_BOOKMARKSKIPPED|
|Identidad de fila segura|DBPROP_STRONGITDENTITY|
|Filas únicas|DBPROP_UNIQUEROWS|
|Posibilidad de actualización|DBPROP_UPDATABILITY|
|Utilizar marcadores|DBPROP_BOOKMARKS|

## <a name="command-dynamic-properties"></a>Propiedades dinámicas de comando
 Las siguientes propiedades se agregan a la **propiedades** colección de la **comando** objeto.

|Nombre de la propiedad ADO|Nombre de propiedad OLE DB|
|-----------------------|--------------------------|
|Orden de acceso|DBPROP_ACCESSORDER|
|Ruta de acceso base|SSPROP_STREAM_BASEPATH|
|Bloquear objetos de almacenamiento|DBPROP_BLOCKINGSTORAGEOBJECTS|
|Tipo de marcador|DBPROP_BOOKMARKTYPE|
|Admite marcadores|DBPROP_IROWSETLOCATE|
|Cambiar filas insertadas|DBPROP_CHANGEINSERTEDROWS|
|Privilegios de columna|DBPROP_COLUMNRESTRICT|
|Notificación de conjunto de columnas|DBPROP_NOTIFYCOLUMNSET|
|Tipo de contenido|SSPROP_STREAM_CONTENTTYPE|
|Captura de cursor automáticamente|SSPROP_CURSORAUTOFETCH|
|Aplazar la columna|DBPROP_DEFERRED|
|Preparación diferida|SSPROP_DEFERPREPARE|
|Actualizaciones de objetos de almacenamiento de retraso|DBPROP_DELAYSTORAGEOBJECTS|
|Buscar hacia atrás|DBPROP_CANFETCHBACKWARDS|
|Conservar filas|DBPROP_CANHOLDROWS|
|IAccessor|DBPROP_IAccessor|
|IColumnsInfo|DBPROP_IColumnsInfo|
|IColumnsRowset|DBPROP_IColumnsRowset|
|IConnectionPointContainer|DBPROP_IConnectionPointContainer|
|IConvertType|DBPROP_IConvertType|
|Filas inmóviles|DBPROP_IMMOBILEROWS|
|IRowset|DBPROP_IRowset|
|IRowsetChange|DBPROP_IRowsetChange|
|IRowsetIdentity|DBPROP_IRowsetIdentity|
|IRowsetInfo|DBPROP_IRowsetInfo|
|IRowsetLocate|DBPROP_IRowsetLocate|
|IRowsetResynch|DBPROP_IRowsetResynch|
|IRowsetScroll|DBPROP_IRowsetScroll|
|IRowsetUpdate|DBPROP_IRowsetUpdate|
|ISequentialStream|DBPROP_ISequentialStream|
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
|Propiedad codificación de salida|DBPROP_OUTPUTENCODING|
|Propiedad de salida de Stream|DBPROP_OUTPUTSTREAM|
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
|Cursor de servidor|DBPROP_SERVERCURSOR|
|Datos del servidor durante la inserción|DBPROP_SERVERDATAONINSERT|
|Omitir marcadores eliminados|DBPROP_BOOKMARKSKIP|
|Identidad de fila segura|DBPROP_STRONGIDENTITY|
|Posibilidad de actualización|DBPROP_UPDATABILITY|
|Utilizar marcadores|DBPROP_BOOKMARKS|
|Raíz XML|SSPROP_STREAM_XMLROOT|
|XSL|SSPROP_STREAM_XSL|

 Para detalles de implementación específicos y funcional sobre el proveedor OLE DB de Microsoft SQL Server, consulte el [proveedor de SQL Server](http://msdn.microsoft.com/adf1d6c4-5930-444a-9248-ff1979729635).

## <a name="see-also"></a>Vea también
 [Propiedad ConnectionString (ADO)](../../../ado/reference/ado-api/connectionstring-property-ado.md) [proveedor (propiedad, ADO)](../../../ado/reference/ado-api/provider-property-ado.md) [el objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)
