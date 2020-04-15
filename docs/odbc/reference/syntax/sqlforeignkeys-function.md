---
title: Función SQLForeignKeys ( SQLForeignKeys) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5f2769fb378a5ee989fb6a0351537edb3de03469
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285865"
---
# <a name="sqlforeignkeys-function"></a>Función SQLForeignKeys
**Conformidad**  
 Versión introducida: Cumplimiento de estándares ODBC 1.0: ODBC  
  
 **Resumen**  
 **SQLForeignKeys** puede devolver:  
  
-   Una lista de claves externas en la tabla especificada (columnas en la tabla especificada que hacen referencia a claves principales en otras tablas).  
  
-   Una lista de claves externas en otras tablas que hacen referencia a la clave principal de la tabla especificada.  
  
 El controlador devuelve cada lista como un conjunto de resultados en la instrucción especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
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
 [Entrada] Nombre del catálogo de tablas de claves principales. Si un controlador admite catálogos para algunas tablas pero no para otras, como cuando el controlador recupera datos de diferentes DBMS, una cadena vacía ("") indica las tablas que no tienen catálogos. *PKCatalogName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, *PKCatalogName* se trata como un identificador y su caso no es significativo. Si se SQL_FALSE, *PKCatalogName* es un argumento normal; se trata literalmente, y su caso es significativo. Para obtener más información, vea [Argumentos en funciones](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)de catálogo .  
  
 *NameLength1*  
 [Entrada] Longitud de **PKCatalogName*, en caracteres.  
  
 *PKSchemaName*  
 [Entrada] Nombre del esquema de tabla de claves principal. Si un controlador admite esquemas para algunas tablas pero no para otras, como cuando el controlador recupera datos de diferentes DBMS, una cadena vacía ("") denota las tablas que no tienen esquemas. *PKSchemaName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, *PKSchemaName* se trata como un identificador y su caso no es significativo. Si se SQL_FALSE, *PKSchemaName* es un argumento normal; se trata literalmente, y su caso es significativo.  
  
 *NameLength2*  
 [Entrada] Longitud de **PKSchemaName*, en caracteres.  
  
 *PKTableName*  
 [Entrada] Nombre de la tabla de claves principal. *PKTableName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, *PKTableName* se trata como un identificador y su caso no es significativo. Si se SQL_FALSE, *PKTableName* es un argumento normal; se trata literalmente, y su caso es significativo.  
  
 *NameLength3*  
 [Entrada] Longitud de **PKTableName*, en caracteres.  
  
 *FKCatalogName*  
 [Entrada] Nombre del catálogo de tablas de claves externas. Si un controlador admite catálogos para algunas tablas pero no para otras, como cuando el controlador recupera datos de diferentes DBMS, una cadena vacía ("") indica las tablas que no tienen catálogos. *FKCatalogName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, *FKCatalogName* se trata como un identificador y su caso no es significativo. Si se SQL_FALSE, *FKCatalogName* es un argumento normal; se trata literalmente, y su caso es significativo.  
  
 *NameLength4*  
 [Entrada] Longitud de **FKCatalogName*, en caracteres.  
  
 *FKSchemaName*  
 [Entrada] Nombre de esquema de tabla de claves externas. Si un controlador admite esquemas para algunas tablas pero no para otras, como cuando el controlador recupera datos de diferentes DBMS, una cadena vacía ("") denota las tablas que no tienen esquemas. *FKSchemaName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, *FKSchemaName* se trata como un identificador y su caso no es significativo. Si se SQL_FALSE, *FKSchemaName* es un argumento normal; se trata literalmente, y su caso es significativo.  
  
 *NameLength5*  
 [Entrada] Longitud de **FKSchemaName*, en caracteres.  
  
 *FKTableName*  
 [Entrada] Nombre de tabla de claves externas. *FKTableName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción SQL_ATTR_METADATA_ID se establece en SQL_TRUE, *FKTableName* se trata como un identificador y su caso no es significativo. Si se SQL_FALSE, *FKTableName* es un argumento normal; se trata literalmente, y su caso es significativo.  
  
 *NameLength6*  
 [Entrada] Longitud de **FKTableName*, en caracteres.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLForeignKeys** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *control* de *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE normalmente devueltos por **SQLForeignKeys** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|24000|Estado de cursor no válido|Un cursor estaba abierto en el *StatementHandle*, y **SQLFetch** o **SQLFetchScroll** se había llamado. El Administrador de controladores devuelve este error si **SQLFetch** o **SQLFetchScroll** no ha devuelto SQL_NO_DATA y lo devuelve el controlador si **SQLFetch** o **SQLFetchScroll** ha devuelto SQL_NO_DATA.<br /><br /> Un cursor estaba abierto en el *StatementHandle*, pero **SQLFetch** o **SQLFetchScroll** no se había llamado.|  
|40001|Error de serialización|La transacción se revirtió debido a un interbloqueo de recursos con otra transacción.|  
|40003|Finalización de la declaración desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY008|Operación cancelada|El procesamiento asincrónico se ha habilitado para *StatementHandle*. Se llamó a la función y antes de completar la ejecución, **sqlCancel** o **SQLCancelHandle** se llamó en el *StatementHandle*, y, a continuación, se llamó a la función de nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY009|Uso no válido de puntero nulo|(DM) Los argumentos *PKTableName* y *FKTableName* eran punteros nulos.<br /><br /> El atributo de instrucción SQL_ATTR_METADATA_ID se estableció en SQL_TRUE, el argumento *FKCatalogName* o *PKCatalogName* era un puntero nulo y el SQL_CATALOG_NAME *InfoType* devuelve que se admiten los nombres de catálogo.<br /><br /> (DM) el atributo de instrucción SQL_ATTR_METADATA_ID se estableció en SQL_TRUE y el argumento *FKSchemaName*, *PKSchemaName*, *FKTableName*o *PKTableName* era un puntero nulo.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando se llamó a la función SQLForeignKeys .<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *StatementHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función de ejecución asincrónica (no esta) para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY090|Cadena no válida o longitud de búfer|(DM) El valor de uno de los argumentos de longitud de nombre era menor que 0 pero no igual a SQL_NTS.|  
|||El valor de uno de los argumentos de longitud de nombre superó el valor de longitud máxima para el nombre correspondiente. (Véase "Comentarios.")|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYC00|Característica opcional no implementada|Se especificó un nombre de catálogo y el controlador o el origen de datos no admite catálogos.<br /><br /> Se especificó un nombre de esquema y el controlador o el origen de datos no admite esquemas.|  
|||El controlador o el origen de datos no admitió la combinación de la configuración actual de los atributos de instrucción SQL_ATTR_CONCURRENCY y SQL_ATTR_CURSOR_TYPE.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y el atributo de instrucción SQL_ATTR_CURSOR_TYPE se estableció en un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Tiempo de espera agotado|El período de tiempo de espera de la consulta expiró antes de que el origen de datos devolviera el conjunto de resultados. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 Para obtener información sobre cómo se puede usar la información devuelta por esta función, vea [Usos de datos de catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Si \* *PKTableName* contiene un nombre de tabla, **SQLForeignKeys** devuelve un conjunto de resultados que contiene la clave principal de la tabla especificada y todas las claves externas que hacen referencia a ella. La lista de claves externas de otras tablas no incluye claves externas que apunten a restricciones únicas en la tabla especificada.  
  
 Si \* *FKTableName* contiene un nombre de tabla, **SQLForeignKeys** devuelve un conjunto de resultados que contiene todas las claves externas de la tabla especificada que apuntan a las claves principales de otras tablas y las claves principales de las otras tablas a las que hacen referencia. La lista de claves externas de la tabla especificada no contiene claves externas que hagan referencia a restricciones únicas en otras tablas.  
  
 Si \* *PKTableName* \*y *FKTableName* contienen nombres de tabla, **SQLForeignKeys** \*devuelve las claves externas de la tabla especificada en *FKTableName* que hacen referencia a la clave principal de la tabla especificada en **PKTableName*. Esta debería ser una clave como máximo.  
  
> [!NOTE]  
>  Para obtener más información sobre el uso general, los argumentos y los datos devueltos de las funciones de catálogo ODBC, vea [Funciones](../../../odbc/reference/develop-app/catalog-functions.md)de catálogo .  
  
 **SQLForeignKeys** devuelve los resultados como un conjunto de resultados estándar. Si se solicitan las claves externas asociadas a una clave principal, el conjunto de resultados se ordena por FKTABLE_CAT, FKTABLE_SCHEM, FKTABLE_NAME y KEY_SEQ. Si se solicitan las claves principales asociadas a una clave externa, el conjunto de resultados se ordena mediante PKTABLE_CAT, PKTABLE_SCHEM, PKTABLE_NAME y KEY_SEQ. En la tabla siguiente se enumeran las columnas del conjunto de resultados.  
  
 Las longitudes de las columnas VARCHAR no se muestran en la tabla; las longitudes reales dependen del origen de datos. Para determinar las longitudes reales de la PKTABLE_CAT o FKTABLE_CAT, PKTABLE_SCHEM o FKTABLE_SCHEM, PKTABLE_NAME o FKTABLE_NAME y PKCOLUMN_NAME o FKCOLUMN_NAME columnas, una aplicación puede llamar a **SQLGetInfo** con las opciones SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN, SQL_MAX_TABLE_NAME_LEN y SQL_MAX_COLUMN_NAME_LEN.  
  
 Se ha cambiado el nombre de las siguientes columnas para ODBC 3 *.x.* Los cambios en el nombre de columna no afectan a la compatibilidad con versiones anteriores porque las aplicaciones se enlazan por número de columna.  
  
|Columna ODBC 2.0|Columna ODBC 3 *.x*|  
|---------------------|-----------------------|  
|PKTABLE_QUALIFIER|PKTABLE_CAT|  
|PKTABLE_OWNER|PKTABLE_SCHEM|  
|FKTABLE_QUALIFIER|FK_TABLE_CAT|  
|FKTABLE_OWNER|FKTABLE_SCHEM|  
  
 En la tabla siguiente se enumeran las columnas del conjunto de resultados. El controlador puede definir columnas adicionales más allá de la columna 14 (REMARKS). Una aplicación debe obtener acceso a columnas específicas del controlador mediante la cuenta regresiva desde el final del conjunto de resultados en lugar de especificar una posición ordinal explícita. Para obtener más información, vea [Datos devueltos por funciones](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)de catálogo .  
  
|Nombre de la columna|Número de columna|Tipo de datos|Comentarios|  
|-----------------|-------------------|---------------|--------------|  
|PKTABLE_CAT (ODBC 1.0)|1|Varchar|Nombre del catálogo de tablas de claves principales; NULL si no es aplicable al origen de datos. Si un controlador admite catálogos para algunas tablas pero no para otras, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para aquellas tablas que no tienen catálogos.|  
|PKTABLE_SCHEM (ODBC 1.0)|2|Varchar|Nombre del esquema de tabla de claves principal; NULL si no es aplicable al origen de datos. Si un controlador admite esquemas para algunas tablas pero no para otras, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para las tablas que no tienen esquemas.|  
|PKTABLE_NAME (ODBC 1.0)|3|Varchar no NULL|Nombre de la tabla de claves principal.|  
|PKCOLUMN_NAME (ODBC 1.0)|4|Varchar no NULL|Nombre de columna de clave principal. El controlador devuelve una cadena vacía para una columna que no tiene un nombre.|  
|FKTABLE_CAT (ODBC 1.0)|5|Varchar|Nombre del catálogo de tablas de claves externas; NULL si no es aplicable al origen de datos. Si un controlador admite catálogos para algunas tablas pero no para otras, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para aquellas tablas que no tienen catálogos.|  
|FKTABLE_SCHEM (ODBC 1.0)|6|Varchar|Nombre de esquema de tabla de clave externa; NULL si no es aplicable al origen de datos. Si un controlador admite esquemas para algunas tablas pero no para otras, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para las tablas que no tienen esquemas.|  
|FKTABLE_NAME (ODBC 1.0)|7|Varchar no NULL|Nombre de tabla de claves externas.|  
|FKCOLUMN_NAME (ODBC 1.0)|8|Varchar no NULL|Nombre de columna de clave externa. El controlador devuelve una cadena vacía para una columna que no tiene un nombre.|  
|KEY_SEQ (ODBC 1.0)|9|Smallint no NULL|Número de secuencia de columnas en clave (a partir de 1).|  
|UPDATE_RULE (ODBC 1.0)|10|Smallint|Acción que se aplicará a la clave externa cuando la operación SQL sea **UPDATE**. Puede tener uno de los siguientes valores. (La tabla a la que se hace referencia es la tabla que tiene la clave principal; la tabla de referencia es la tabla que tiene la clave externa.)<br /><br /> SQL_CASCADE: Cuando se actualiza la clave principal de la tabla a la que se hace referencia, también se actualiza la clave externa de la tabla de referencia.<br /><br /> SQL_NO_ACTION: Si una actualización de la clave principal de la tabla a la que se hace referencia provocaría una "referencia colgante" en la tabla de referencia (es decir, las filas de la tabla de referencia no tendrían homólogos en la tabla a la que se hace referencia), se rechaza la actualización. Si una actualización de la clave externa de la tabla de referencia introduciría un valor que no existe como valor de la clave principal de la tabla a la que se hace referencia, se rechaza la actualización. (Esta acción es la misma que la acción SQL_RESTRICT en ODBC 2 *.x*.)<br /><br /> SQL_SET_NULL: cuando una o más filas de la tabla a la que se hace referencia se actualizan de tal manera que se cambian uno o varios componentes de la clave principal, los componentes de la clave externa de la tabla de referencia que corresponden a los componentes modificados de la clave principal se establecen en NULL en todas las filas coincidentes de la tabla de referencia.<br /><br /> SQL_SET_DEFAULT: cuando se actualizan una o varias filas de la tabla a la que se hace referencia de tal manera que se cambian uno o varios componentes de la clave principal, los componentes de la clave externa de la tabla de referencia que corresponden a los componentes modificados de la clave principal se establecen en los valores predeterminados aplicables en todas las filas coincidentes de la tabla de referencia.<br /><br /> NULL si no es aplicable al origen de datos.|  
|DELETE_RULE (ODBC 1.0)|11|Smallint|Acción que se aplicará a la clave externa cuando la operación SQL sea **DELETE**. Puede tener uno de los siguientes valores. (La tabla a la que se hace referencia es la tabla que tiene la clave principal; la tabla de referencia es la tabla que tiene la clave externa.)<br /><br /> SQL_CASCADE: cuando se elimina una fila de la tabla a la que se hace referencia, también se eliminan todas las filas coincidentes de las tablas de referencia.<br /><br /> SQL_NO_ACTION: Si una eliminación de una fila de la tabla a la que se hace referencia provocaría una "referencia colgante" en la tabla de referencia (es decir, las filas de la tabla de referencia no tendrían homólogos en la tabla a la que se hace referencia), se rechaza la actualización. (Esta acción es la misma que la acción SQL_RESTRICT en ODBC 2 *.x*.)<br /><br /> SQL_SET_NULL: cuando se eliminan una o varias filas de la tabla a la que se hace referencia, cada componente de la clave externa de la tabla de referencia se establece en NULL en todas las filas coincidentes de la tabla de referencia.<br /><br /> SQL_SET_DEFAULT: cuando se eliminan una o varias filas de la tabla a la que se hace referencia, cada componente de la clave externa de la tabla de referencia se establece en el valor predeterminado aplicable en todas las filas coincidentes de la tabla de referencia.<br /><br /> NULL si no es aplicable al origen de datos.|  
|FK_NAME (ODBC 2.0)|12|Varchar|Nombre de clave externa. NULL si no es aplicable al origen de datos.|  
|PK_NAME (ODBC 2.0)|13|Varchar|Nombre de clave principal. NULL si no es aplicable al origen de datos.|  
|Deferrabilidad (ODBC 3.0)|14|Smallint|SQL_INITIALLY_DEFERRED, SQL_INITIALLY_IMMEDIATE, SQL_NOT_DEFERRABLE.|  
  
## <a name="code-example"></a>Ejemplo de código  
 Como se muestra en la tabla siguiente, en este ejemplo se utilizan tres tablas, denominadas ORDERS, LINES y CUSTOMERS.  
  
|ORDERS|Líneas|Clientes|  
|------------|-----------|---------------|  
|Orderid|Orderid|CUSTID|  
|CUSTID|Líneas|NAME|  
|OPENDATE|PARTID|Dirección|  
|Vendedor|Cantidad|TELÉFONO|  
|STATUS|||  
  
 En la tabla ORDERS, CUSTID identifica al cliente al que se ha realizado la venta. Es una clave externa que hace referencia al CUSTID en la tabla CLIENTES.  
  
 En la tabla LINES, ORDERID identifica el pedido de ventas con el que está asociado el artículo de línea. Es una clave externa que hace referencia a ORDERID en la tabla ORDERS.  
  
 En este ejemplo se llama a **SQLPrimaryKeys** para obtener la clave principal de la tabla ORDERS. El conjunto de resultados tendrá una fila; las columnas significativas se muestran en la tabla siguiente.  
  
|TABLE_NAME|COLUMN_NAME|KEY_SEQ|  
|-----------------|------------------|--------------|  
|ORDERS|Orderid|1|  
  
 A continuación, el ejemplo llama a **SQLForeignKeys** para obtener las claves externas de otras tablas que hacen referencia a la clave principal de la tabla ORDERS. El conjunto de resultados tendrá una fila; las columnas significativas se muestran en la tabla siguiente.  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|ORDERS|CUSTID|Líneas|CUSTID|1|  
  
 Por último, el ejemplo llama a **SQLForeignKeys** para obtener las claves externas de la tabla ORDERS que hacen referencia a las claves principales de otras tablas. El conjunto de resultados tendrá una fila; las columnas significativas se muestran en la tabla siguiente.  
  
|PKTABLE_NAME|PKCOLUMN_NAME|FKTABLE_NAME|FKCOLUMN_NAME|KEY_SEQ|  
|-------------------|--------------------|-------------------|--------------------|--------------|  
|Clientes|CUSTID|ORDERS|CUSTID|1|  
  
```cpp  
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
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer a una columna en un conjunto de resultados|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelación del procesamiento de extractos|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Obtención de una sola fila o un bloque de datos en una dirección de solo avance|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Obtención de un bloque de datos o desplazamiento por un conjunto de resultados|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Devolver las columnas de una clave principal|[Función SQLPrimaryKeys](../../../odbc/reference/syntax/sqlprimarykeys-function.md)|  
|Devolver estadísticas e índices de tablas|[Función SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
