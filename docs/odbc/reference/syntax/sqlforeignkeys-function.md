---
title: "Función SQLForeignKeys | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLForeignKeys
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLForeignKeys
helpviewer_keywords:
- SQLForeignKeys function [ODBC]
ms.assetid: 07f3f645-f643-4d39-9a10-70a72f24e608
caps.latest.revision: 24
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 0d56fd87c4c9612fb520b1a54b9d0c2cab645223
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlforeignkeys-function"></a>Función SQLForeignKeys
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: ODBC  
  
 **Resumen**  
 **SQLForeignKeys** puede devolver:  
  
-   Una lista de las claves externas de la tabla especificada (las columnas de la tabla especificada que hacen referencia a claves principales de otras tablas).  
  
-   Una lista de las claves externas de otras tablas que hacen referencia a la clave principal de la tabla especificada.  
  
 El controlador devuelve cada lista como un conjunto de resultados en la instrucción especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLForeignKeys(  
     SQLHSTMT       StatementHandle,  
     SQLCHAR *      PKCatalogName,  
     SQLSMALLINT    NameLength1,  
     SQLCHAR *      PKSchemaName,  
     SQLSMALLINT    NameLength2,  
     SQLCHAR *      PKTableName,  
     SQLSMALLINT    NameLength3,  
     SQLCHAR *      FKCatalogName,  
     SQLSMALLINT    NameLength4,  
     SQLCHAR *      FKSchemaName,  
     SQLSMALLINT    NameLength5,  
     SQLCHAR *      FKTableName,  
     SQLSMALLINT    NameLength6);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *PKCatalogName*  
 [Entrada] Nombre del catálogo de tabla de clave principal. Si un controlador admite catálogos para algunas tablas pero no para otros usuarios, por ejemplo, cuando el controlador JDBC recupera datos de los DBMS tiene diferentes, una cadena vacía ("") indica las tablas que no tiene catálogos. *PKCatalogName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *PKCatalogName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *PKCatalogName* es un argumento normal; se trata literalmente y su caso es significativo. Para obtener más información, consulte [argumentos de las funciones de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Longitud de **PKCatalogName*, en caracteres.  
  
 *PKSchemaName*  
 [Entrada] Nombre del esquema de tabla de clave principal. Si un controlador es compatible con esquemas para algunas tablas pero no para otros usuarios, por ejemplo, cuando el controlador JDBC recupera datos de los DBMS tiene diferentes, una cadena vacía ("") indica las tablas que no tengan esquemas. *PKSchemaName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *PKSchemaName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *PKSchemaName* es un argumento normal; se trata literalmente y su caso es significativo.  
  
 *NameLength2*  
 [Entrada] Longitud de **PKSchemaName*, en caracteres.  
  
 *PKTableName*  
 [Entrada] Nombre de tabla de clave principal. *PKTableName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *PKTableName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *PKTableName* es un argumento normal; se trata literalmente y su caso es significativo.  
  
 *NameLength3*  
 [Entrada] Longitud de **PKTableName*, en caracteres.  
  
 *FKCatalogName*  
 [Entrada] Nombre del catálogo de tabla de clave externa. Si un controlador admite catálogos para algunas tablas pero no para otros usuarios, por ejemplo, cuando el controlador JDBC recupera datos de los DBMS tiene diferentes, una cadena vacía ("") indica las tablas que no tiene catálogos. *FKCatalogName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *FKCatalogName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *FKCatalogName* es un argumento normal; se trata literalmente y su caso es significativo.  
  
 *NameLength4*  
 [Entrada] Longitud de **FKCatalogName*, en caracteres.  
  
 *FKSchemaName*  
 [Entrada] Nombre del esquema de tabla de clave externa. Si un controlador es compatible con esquemas para algunas tablas pero no para otros usuarios, por ejemplo, cuando el controlador JDBC recupera datos de los DBMS tiene diferentes, una cadena vacía ("") indica las tablas que no tengan esquemas. *FKSchemaName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *FKSchemaName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *FKSchemaName* es un argumento normal; se trata literalmente y su caso es significativo.  
  
 *NameLength5*  
 [Entrada] Longitud de **FKSchemaName*, en caracteres.  
  
 *FKTableName*  
 [Entrada] Nombre de tabla de clave externa. *FKTableName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *FKTableName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *FKTableName* es un argumento normal; se trata literalmente y su caso es significativo.  
  
 *NameLength6*  
 [Entrada] Longitud de **FKTableName*, en caracteres.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLForeignKeys** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL _HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE suelen ser devueltos por **SQLForeignKeys** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08S01|Error de vínculo de comunicación|El vínculo de comunicación entre el controlador y el origen de datos al que se conectó el controlador no pudo antes del procesamiento de la función se ha completado.|  
|24000|Estado de cursor no válido|Un cursor estaba abierto en el *StatementHandle*, y **SQLFetch** o **SQLFetchScroll** si se hubiese llamado. Este error se devuelve mediante el Administrador de controladores si **SQLFetch** o **SQLFetchScroll** no se devuelve SQL_NO_DATA y se devuelve el controlador si **SQLFetch** o **SQLFetchScroll** devuelva SQL_NO_DATA.<br /><br /> Un cursor estaba abierto en el *StatementHandle*, pero **SQLFetch** o **SQLFetchScroll** si no se hubiese llamado.|  
|40001|Error de serialización.|La transacción se revirtió debido a un interbloqueo de recurso con otra transacción.|  
|40003|Finalización de instrucciones desconocida|Error en la conexión asociada durante la ejecución de esta función, y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar memoria que es necesario para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle*, y, a continuación, se llama a la función de nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle* desde un subproceso distinto en un aplicaciones multiproceso.|  
|HY009|Uso no válido del puntero null|(DM) los argumentos *PKTableName* y *FKTableName* eran ambos punteros null.<br /><br /> El atributo de instrucción SQL_ATTR_METADATA_ID se estableció en SQL_TRUE, el *FKCatalogName* o *PKCatalogName* argumento era un puntero nulo y la SQL_CATALOG_NAME *deltipodeinformación*devuelve que los nombres de catálogo se admite.<br /><br /> (DM) se estableció el atributo de instrucción de SQL_ATTR_METADATA_ID en SQL_TRUE y el *FKSchemaName*, *PKSchemaName*, *FKTableName*, o *PKTableName * argumento era un puntero nulo.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónica aún se estaba ejecutando cuando se llamó a la función SQLForeignKeys.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* devolvió SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica (no esta uno) para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el * StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el valor de uno de los argumentos de longitud de nombre era menor que 0 pero no es igual a SQL_NTS.|  
|||El valor de uno de los argumentos de longitud de nombre supera el valor de longitud máxima para el nombre correspondiente. (Vea "Comentarios".)|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|Se especificó un nombre de catálogo y del origen de datos o el controlador no admite catálogos.<br /><br /> Se especificó un nombre de esquema y el controlador o el origen de datos no admite los esquemas.|  
|||La combinación de la configuración actual de los atributos de instrucción SQL_ATTR_CONCURRENCY y SQL_ATTR_CURSOR_TYPE no era compatible con el controlador u origen de datos.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y el atributo de instrucción SQL_ATTR_CURSOR_TYPE se estableció en un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Se agotó el tiempo de espera|El período de tiempo de espera de consulta finalizó antes de que el origen de datos devuelve el conjunto de resultados. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *StatementHandle* no admite la función.|  
|IM017|Sondeo está deshabilitado en el modo de notificación asincrónica|Cada vez que se utiliza el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** se debe llamar en el identificador para realizar el procesamiento posterior a la y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 Para obtener información acerca de cómo se podría utilizar la información devuelta por esta función, vea [usa de datos del catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Si \* *PKTableName* contiene un nombre de tabla **SQLForeignKeys** devuelve un conjunto de resultados que contiene la clave principal de la tabla especificada y todas las claves externas que hacen referencia a él. La lista de las claves externas de otras tablas no incluye las claves externas que apuntan a las restricciones unique en la tabla especificada.  
  
 Si \* *FKTableName* contiene un nombre de tabla **SQLForeignKeys** devuelve un conjunto de resultados que contiene todas las claves externas de la tabla especificada que apuntan las claves principales de otras tablas y la claves principales en las demás tablas a los que hacen referencia. La lista de las claves externas de la tabla especificada no contiene claves externas que hacen referencia a las restricciones unique en otras tablas.  
  
 Si ambos \* *PKTableName* y \* *FKTableName* contienen nombres de tabla, **SQLForeignKeys** devuelve las claves externas en la tabla especificada en \* *FKTableName* que hacen referencia a la clave principal de la tabla especificada en **PKTableName*. Debe ser una clave como máximo.  
  
> [!NOTE]  
>  Para obtener más información sobre el uso general, los argumentos y los datos devueltos de funciones de catálogo ODBC, vea [funciones de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 **SQLForeignKeys** devuelve los resultados como un conjunto de resultados estándar. Si se solicitan las claves externas asociadas con una clave principal, el conjunto de resultados se ordena por FKTABLE_CAT, FKTABLE_SCHEM, FKTABLE_NAME y KEY_SEQ. Si se solicitan las claves principales asociadas con una clave externa, el conjunto de resultados se ordena por PKTABLE_CAT, PKTABLE_SCHEM, PKTABLE_NAME y KEY_SEQ. En la tabla siguiente se enumera las columnas del conjunto de resultados.  
  
 Las longitudes de las columnas VARCHAR no se muestran en la tabla. las longitudes reales dependen del origen de datos. Para determinar la longitud real de la PKTABLE_CAT o FKTABLE_CAT, PKTABLE_SCHEM o FKTABLE_SCHEM, PKTABLE_NAME o FKTABLE_NAME y PKCOLUMN_NAME o FKCOLUMN_NAME columnas, una aplicación puede llamar a **SQLGetInfo** con el SQL_MAX_ Opciones de CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN y SQL_MAX_COLUMN_NAME_LEN.  
  
 Las columnas siguientes se cambió para ODBC 3*. x.* Los cambios de nombre de columna no afectan a la compatibilidad con versiones anteriores porque las aplicaciones enlazar por número de columna.  
  
|Columna de ODBC 2.0|ODBC 3*.x* columna|  
|---------------------|-----------------------|  
|PKTABLE_QUALIFIER|PKTABLE_CAT|  
|PKTABLE_OWNER|PKTABLE_SCHEM|  
|FKTABLE_QUALIFIER|FK_TABLE_CAT|  
|FKTABLE_OWNER|FKTABLE_SCHEM|  
  
 En la tabla siguiente se enumera las columnas del conjunto de resultados. El controlador, se pueden definir columnas adicionales más allá de la columna 14 (comentarios). Una aplicación debe tener acceso a columnas específicas del controlador contando hacia abajo desde el final del conjunto en lugar de especificar una posición ordinal explícitos de resultados. Para obtener más información, consulte [datos devueltos por las funciones de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nombre de columna|Número de columna|Tipo de datos|Comentarios|  
|-----------------|-------------------|---------------|--------------|  
|PKTABLE_CAT (ODBC 1.0)|1|Varchar|Nombre de catálogo de la tabla de clave principal; Es NULL si no es aplicable al origen de datos. Si un controlador admite catálogos para algunas tablas pero no para otros, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para las tablas que no tiene catálogos.|  
|PKTABLE_SCHEM (ODBC 1.0)|2|Varchar|Nombre del esquema de tabla de clave principal; Es NULL si no es aplicable al origen de datos. Si un controlador es compatible con esquemas para algunas tablas pero no para otros, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para las tablas que no tengan esquemas.|  
|PKTABLE_NAME (ODBC 1.0)|3|Varchar no NULL|Nombre de tabla de clave principal.|  
|PKCOLUMN_NAME (ODBC 1.0)|4|Varchar no NULL|Nombre de columna de clave principal. El controlador devuelve una cadena vacía para una columna que no tiene un nombre.|  
|FKTABLE_CAT (ODBC 1.0)|5|Varchar|Nombre de catálogo de la tabla de clave externa; Es NULL si no es aplicable al origen de datos. Si un controlador admite catálogos para algunas tablas pero no para otros, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para las tablas que no tiene catálogos.|  
|FKTABLE_SCHEM (ODBC 1.0)|6|Varchar|Nombre del esquema de tabla de clave externa; Es NULL si no es aplicable al origen de datos. Si un controlador es compatible con esquemas para algunas tablas pero no para otros, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para las tablas que no tengan esquemas.|  
|FKTABLE_NAME (ODBC 1.0)|7|Varchar no NULL|Nombre de tabla de clave externa.|  
|FKCOLUMN_NAME (ODBC 1.0)|8|Varchar no NULL|Nombre de columna de clave externa. El controlador devuelve una cadena vacía para una columna que no tiene un nombre.|  
|KEY_SEQ (ODBC 1.0)|9|Smallint no NULL|Número de secuencia de la columna de clave (a partir de 1).|  
|UPDATE_RULE (ODBC 1.0)|10|Smallint|Acción que se aplicará a la clave externa cuando la operación de SQL es **actualización**. Puede tener uno de los siguientes valores. (La tabla que se hace referencia es la tabla que contiene la clave principal; la tabla de referencia es la tabla que contiene la clave externa).<br /><br /> SQL_CASCADE: Cuando se actualiza la clave principal de la tabla de referencia, también se actualiza la clave externa de la tabla de referencia.<br /><br /> SQL_NO_ACTION: Si una actualización de la clave principal de la tabla de referencia provocaría una "referencia pendiente" en la tabla de referencia (es decir, filas de la tabla de referencia no tendría ningún homólogos en la tabla de referencia), se rechaza la actualización. Si una actualización de la clave externa de la tabla de referencia introduce un valor que no existe como un valor de la clave principal de la tabla de referencia, se rechaza la actualización. (Esta acción es igual que la acción SQL_RESTRICT en ODBC 2*.x*.)<br /><br /> SQL_SET_NULL: Cuando se actualizan una o varias filas en la tabla de referencia de tal manera que se modifican uno o más componentes de la clave principal, se establecen los componentes de la clave externa en la tabla de referencia que corresponden a los componentes modificados de la clave principal en NULL en todas las filas coincidentes de la tabla de referencia.<br /><br /> SQL_SET_DEFAULT: Son los componentes de la clave externa en la tabla de referencia que corresponden a los componentes modificados de la clave principal cuando se actualizan una o varias filas en la tabla de referencia de tal manera que se modifican uno o más componentes de la clave principal, establecer valores predeterminados es aplicable en todas las filas coincidentes de la tabla de referencia.<br /><br /> Es NULL si no es aplicable al origen de datos.|  
|DELETE_RULE (ODBC 1.0)|11|Smallint|Acción que se aplicará a la clave externa cuando la operación de SQL es **eliminar**. Puede tener uno de los siguientes valores. (La tabla que se hace referencia es la tabla que contiene la clave principal; la tabla de referencia es la tabla que contiene la clave externa).<br /><br /> SQL_CASCADE: Cuando se elimina una fila en la tabla de referencia, también se eliminan todas las filas coincidentes en las tablas de referencia.<br /><br /> SQL_NO_ACTION: Si una eliminación de una fila en la tabla de referencia provocaría una "referencia pendiente" en la tabla de referencia (es decir, filas de la tabla de referencia no tendría ningún homólogos en la tabla de referencia), se rechaza la actualización. (Esta acción es igual que la acción SQL_RESTRICT en ODBC 2*.x*.)<br /><br /> SQL_SET_NULL: Cuando se eliminan una o varias filas en la tabla de referencia, cada componente de la clave externa de la tabla de referencia se establece en NULL en todas las filas coincidentes de la tabla de referencia.<br /><br /> SQL_SET_DEFAULT: Cuando se eliminan una o varias filas en la tabla de referencia, cada componente de la clave externa de la tabla de referencia se establece en el valor predeterminado es aplicable en todas las filas coincidentes de la tabla de referencia.<br /><br /> Es NULL si no es aplicable al origen de datos.|  
|COLUMNAS FK_NAME (ODBC 2.0)|12|Varchar|Nombre de clave externa. Es NULL si no es aplicable al origen de datos.|  
|PK_NAME (ODBC 2.0)|13|Varchar|Nombre de clave principal. Es NULL si no es aplicable al origen de datos.|  
|APLAZAMIENTO DE NO (ODBC 3.0)|14|Smallint|SQL_INITIALLY_DEFERRED, SQL_INITIALLY_IMMEDIATE, SQL_NOT_DEFERRABLE.|  
  
## <a name="code-example"></a>Ejemplo de código  
 Como se muestra en la tabla siguiente, este ejemplo utiliza tres tablas, denominadas pedidos, las líneas y los clientes.  
  
|ORDERS|LÍNEAS|CLIENTES|  
|------------|-----------|---------------|  
|ORDERID|ORDERID|CUSTID|  
|CUSTID|LÍNEAS|NAME|  
|OPENDATE|PARTID|DIRECCIÓN|  
|VENDEDOR|CANTIDAD|TELÉFONO|  
|STATUS|||  
  
 En la tabla ORDERS, CUSTID identifica al cliente a los que se ha realizado la venta. Es una clave externa que hace referencia a CUSTID en la tabla CUSTOMERS.  
  
 En la tabla de líneas, ORDERID identifica el pedido de ventas al que está asociado el artículo de línea. Es una clave externa que hace referencia a ORDERID de la tabla ORDERS.  
  
 Este ejemplo llama **SQLPrimaryKeys** para obtener la clave principal de la tabla ORDERS. El conjunto de resultados tendrá una fila; las columnas importantes se muestran en la tabla siguiente.  
  
|TABLE_NAME|COLUMN_NAME|KEY_SEQ|  
|-----------------|------------------|--------------|  
|ORDERS|ORDERID|1|  
  
 A continuación, en el ejemplo se llama **SQLForeignKeys** para obtener las claves externas de otras tablas que hacen referencia a la clave principal de la tabla ORDERS. El conjunto de resultados tendrá una fila; las columnas importantes se muestran en la tabla siguiente.  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|ORDERS|CUSTID|LÍNEAS|CUSTID|1|  
  
 Por último, en el ejemplo se llama **SQLForeignKeys** para obtener las claves externas en la tabla ORDERS que hacen referencia a las claves principales de otras tablas. El conjunto de resultados tendrá una fila; las columnas importantes se muestran en la tabla siguiente.  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|CLIENTES|CUSTID|ORDERS|CUSTID|1|  
  
```  
#define TAB_LEN SQL_MAX_TABLE_NAME_LEN + 1  
#define COL_LEN SQL_MAX_COLUMN_NAME_LEN + 1  
  
LPSTR   szTable;              /* Table to display */  
  
UCHAR szPkTable[TAB_LEN];   /* Primary key table name */  
UCHAR szFkTable[TAB_LEN];   /* Foreign key table name */  
UCHAR szPkCol[COL_LEN];     /* Primary key column */  
UCHAR szFkCol[COL_LEN];     /* Foreign key column */  
  
SQLHSTMT      hstmt;  
SQLINTEGER    cbPkTable, cbPkCol, cbFkTable, cbFkCol, cbKeySeq;  
SQLSMALLINT   iKeySeq;  
SQLRETURN     retcode;  
  
// Bind the columns that describe the primary and foreign keys.  
// Ignore the table schema, name, and catalog for this example.  
  
SQLBindCol(hstmt, 3, SQL_C_CHAR, szPkTable, TAB_LEN, &cbPkTable);  
SQLBindCol(hstmt, 4, SQL_C_CHAR, szPkCol, COL_LEN, &cbPkCol);  
SQLBindCol(hstmt, 5, SQL_C_SSHORT, &iKeySeq, TAB_LEN, &cbKeySeq);  
SQLBindCol(hstmt, 7, SQL_C_CHAR, szFkTable, TAB_LEN, &cbFkTable);  
SQLBindCol(hstmt, 8, SQL_C_CHAR, szFkCol, COL_LEN, &cbFkCol);  
  
strcpy_s(szTable, sizeof(szTable), "ORDERS");  
  
/* Get the names of the columns in the primary key. */  
  
retcode = SQLPrimaryKeys(hstmt,  
         NULL, 0,             /* Catalog name */  
         NULL, 0,             /* Schema name */  
         szTable, SQL_NTS);   /* Table name */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL SUCCESS_WITH_INFO)) {  
  
   /* Fetch and display the result set. This will be a list of the */  
   /* columns in the primary key of the ORDERS table. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "Table: %s Column: %s Key Seq: %hd \n", szPkTable, szPkCol,  
      iKeySeq);  
}  
  
/* Close the cursor (the hstmt is still allocated). */  
  
SQLFreeStmt(hstmt, SQL_CLOSE);  
  
/* Get all the foreign keys that refer to ORDERS primary key.*/   
  
retcode = SQLForeignKeys(hstmt,  
         NULL, 0,            /* Primary catalog */  
         NULL, 0,            /* Primary schema */  
         szTable, SQL_NTS,   /* Primary table */  
         NULL, 0,            /* Foreign catalog */  
         NULL, 0,            /* Foreign schema */  
         NULL, 0);           /* Foreign table */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL_SUCCESS_WITH_INFO)) {  
  
/* Fetch and display the result set. This will be all of the */  
/* foreign keys in other tables that refer to the ORDERS */  
/* primary key. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "%-s ( %-s ) <-- %-s ( %-s )\n", szPkTable,  
               szPkCol, szFkTable, szFkCol);  
}  
  
/* Close the cursor (the hstmt is still allocated). */  
  
SQLFreeStmt(hstmt, SQL_CLOSE);  
  
/* Get all the foreign keys in the ORDERS table. */  
  
retcode = SQLForeignKeys(hstmt,  
         NULL, 0,             /* Primary catalog */  
         NULL, 0,             /* Primary schema */  
         NULL, 0,             /* Primary table */  
         NULL, 0,             /* Foreign catalog */  
         NULL, 0,             /* Foreign schema */  
         szTable, SQL_NTS);   /* Foreign table */  
  
while ((retcode == SQL_SUCCESS) || (retcode == SQL_SUCCESS_WITH_INFO)) {  
  
/* Fetch and display the result set. This will be all of the */  
/* primary keys in other tables that are referred to by foreign */  
/* keys in the ORDERS table. */  
  
   retcode = SQLFetch(hstmt);  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
      fprintf(out, "%-s ( %-s )--> %-s ( %-s )\n", szFkTable, szFkCol, szPkTable, szPkCol);  
}  
  
/* Free the hstmt. */  
SQLFreeStmt(hstmt, SQL_DROP);  
```  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con una columna en un conjunto de resultados|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelar el procesamiento de una instrucción|[SQLCancel, función](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Capturar una sola fila o un bloque de datos en una dirección de solo avance|[SQLFetch, función](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Captura un bloque de datos o desplazarse a través de un resultado de conjunto|[SQLFetchScroll, función](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Devuelve las columnas de una clave principal|[SQLPrimaryKeys, función](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
|Devolver estadísticas de las tablas e índices|[Función SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)

