---
title: Función SQLTablePrivileges | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLTablePrivileges
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLTablePrivileges
helpviewer_keywords:
- SQLTablePrivileges function [ODBC]
ms.assetid: 8cfdb64f-64c5-47e6-ad57-0533ac630afa
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 81659ae2cab2343a7fcf03327cbdc89c0db6c8c0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "65536305"
---
# <a name="sqltableprivileges-function"></a>Función SQLTablePrivileges
**Conformidad**  
 Versión de introducción: Cumplimiento de estándares 1.0 de ODBC: ODBC  
  
 **Resumen**  
 **SQLTablePrivileges** devuelve una lista de tablas y los privilegios asociados con cada tabla. El controlador devuelve la información como un conjunto de resultados en la instrucción especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLTablePrivileges(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CatalogName,  
     SQLSMALLINT   NameLength1,  
     SQLCHAR *     SchemaName,  
     SQLSMALLINT   NameLength2,  
     SQLCHAR *     TableName,  
     SQLSMALLINT   NameLength3);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *CatalogName*  
 [Entrada] Catálogo de la tabla. Si un controlador es compatible con los catálogos para algunas tablas pero no para otros factores, como cuando el controlador recupera datos de los DBMS tiene diferentes, una cadena vacía ("") indica las tablas que no tengan los catálogos. *CatalogName* no puede contener un patrón de búsqueda de cadena.  
  
 Si el atributo de instrucción de SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *CatalogName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *CatalogName* es un argumento normal; se trata literalmente y su caso es significativo. Para obtener más información, consulte [argumentos en funciones de catálogo](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md).  
  
 *NameLength1*  
 [Entrada] Longitud en caracteres de **CatalogName*.  
  
 *SchemaName*  
 [Entrada] Patrón de búsqueda de cadena para los nombres de esquema. Si un controlador es compatible con los esquemas para algunas tablas pero no para otros factores, como cuando el controlador recupera datos de los DBMS tiene diferentes, una cadena vacía ("") indica las tablas que no tiene esquemas.  
  
 Si el atributo de instrucción de SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *SchemaName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *SchemaName* es un argumento de valor de patrón; se trata literalmente y su caso es significativo.  
  
 *NameLength2*  
 [Entrada] Longitud en caracteres de **SchemaName*.  
  
 *TableName*  
 [Entrada] Patrón de búsqueda de cadena para los nombres de tabla.  
  
 Si el atributo de instrucción de SQL_ATTR_METADATA_ID está establecido en SQL_TRUE, *TableName* se trata como un identificador y su caso no es significativo. Si es SQL_FALSE, *TableName* es un argumento de valor de patrón; se trata literalmente y su caso es significativo.  
  
 *NameLength3*  
 [Entrada] Longitud en caracteres de **TableName*.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLTablePrivileges** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLTablePrivileges** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores . El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08S01|Error de vínculo de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos a la que se ha conectado el controlador antes del procesamiento de la función se ha completado.|  
|24000|Estado de cursor no válido|Un cursor estaba abierto en el *StatementHandle*, y **SQLFetch** o **SQLFetchScroll** hubiera llamado. Este error se devuelve mediante el Administrador de controladores si **SQLFetch** o **SQLFetchScroll** no se devolvió SQL_NO_DATA y es devuelto por el controlador si **SQLFetch** o **SQLFetchScroll** devuelva SQL_NO_DATA.<br /><br /> Un cursor estaba abierto en el *StatementHandle*, pero **SQLFetch** o **SQLFetchScroll** no se había llamado.|  
|40001|Error de serialización.|Debido a un interbloqueo de recurso con otra transacción se revirtió la transacción.|  
|40003|Finalización de instrucción desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. El **SQLTablePrivileges** se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el  *StatementHandle*. El **SQLTablePrivileges** función se llamó de nuevo en el *StatementHandle*.<br /><br /> El **SQLTablePrivileges** se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el  *StatementHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY009|Uso no válido del puntero nulo|El atributo de instrucción SQL_ATTR_METADATA_ID estuviera establecido en SQL_TRUE, el *CatalogName* argumento era un puntero nulo y la SQL_CATALOG_NAME *InfoType* devuelve que los nombres de catálogo es compatibles.<br /><br /> (DM) se estableció el atributo de instrucción SQL_ATTR_METADATA_ID en SQL_TRUE y el *SchemaName* o *TableName* argumento era un puntero nulo.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Aún estaba ejecutando esta función asincrónica cuando el **SQLTablePrivileges** se llamó a la función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* y devuelven SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función que se ejecuta asincrónicamente (no ésta) para el *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el valor de uno de los argumentos de longitud de nombre era menor que 0 pero no es igual a SQL_NTS.<br /><br /> El valor de uno de los argumentos de longitud del nombre supera el valor de longitud máxima para el calificador correspondiente o el nombre.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|Se especificó un catálogo, y el controlador o el origen de datos no admite catálogos.<br /><br /> Se especificó un esquema y el controlador o el origen de datos no admite esquemas.<br /><br /> Se especificó un patrón de búsqueda de cadena para el esquema de tabla, el nombre de la tabla o el nombre de columna y el origen de datos no admite patrones de búsqueda para uno o varios de estos argumentos.<br /><br /> La combinación de la configuración actual de los atributos de instrucción SQL_ATTR_CONCURRENCY y SQL_ATTR_CURSOR_TYPE no era compatible con el controlador u origen de datos.<br /><br /> El atributo de instrucción SQL_ATTR_USE_BOOKMARKS se estableció en SQL_UB_VARIABLE y se ha establecido el atributo de instrucción SQL_ATTR_CURSOR_TYPE a un tipo de cursor para el que el controlador no admite marcadores.|  
|HYT00|Se agotó el tiempo de espera|Ha expirado el período de tiempo de espera de consulta antes de que el origen de datos devuelva el conjunto de resultados. El período de tiempo de espera se establece a través de **SQLSetStmtAttr**, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|Sondeo se deshabilita en modo de notificación asincrónica|Cada vez que se usa el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 El *SchemaName* y *TableName* argumentos aceptan modelos de búsqueda. Para obtener más información acerca de los patrones de búsqueda válidos, vea [argumentos de valor de patrón](../../../odbc/reference/develop-app/pattern-value-arguments.md).  
  
 **SQLTablePrivileges** devuelve los resultados como un conjunto de resultados estándar, ordenado por TABLE_CAT, según TABLE_SCHEM, TABLE_NAME, PRIVILEGIO y receptor.  
  
 Para determinar las longitudes de las columnas TABLE_CAT, según TABLE_SCHEM y TABLE_NAME reales, una aplicación puede llamar a **SQLGetInfo** con las opciones SQL_MAX_CATALOG_NAME_LEN, SQL_MAX_SCHEMA_NAME_LEN y SQL_MAX_TABLE_NAME_LEN.  
  
> [!NOTE]  
>  Para obtener más información sobre el uso general, los argumentos y los datos devueltos de funciones de catálogo ODBC, vea [funciones de catálogo](../../../odbc/reference/develop-app/catalog-functions.md).  
  
 Las columnas siguientes se han cambiado para ODBC 3 *.x*. Los cambios de nombre de columna no afectan a la compatibilidad con versiones anteriores porque el enlace de aplicaciones por número de columna.  
  
|Columna de ODBC 2.0|ODBC 3 *.x* columna|  
|---------------------|-----------------------|  
|TABLE_QUALIFIER|TABLE_CAT|  
|TABLE_OWNER|TABLE_SCHEM|  
  
 En la tabla siguiente se enumera las columnas del conjunto de resultados. Las columnas adicionales más allá de la columna 7 (IS_GRANTABLE) pueden definirse mediante el controlador. Una aplicación debe tener acceso a las columnas específicas del controlador mediante la cuenta atrás desde el final del conjunto de resultados, en lugar de especificar una posición ordinal explícita. Para obtener más información, consulte [datos devueltos por las funciones de catálogo](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md).  
  
|Nombre de columna|Número de columna|Tipo de datos|Comentarios|  
|-----------------|-------------------|---------------|--------------|  
|TABLE_CAT (ODBC 1.0)|1|Varchar|Nombre del catálogo; Es NULL si no es aplicable al origen de datos. Si un controlador es compatible con los catálogos para algunas tablas pero no para otros, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para las tablas que no tengan los catálogos.|  
|SEGÚN TABLE_SCHEM (ODBC 1.0)|2|Varchar|Nombre del esquema; Es NULL si no es aplicable al origen de datos. Si un controlador es compatible con los esquemas para algunas tablas pero no para otros, como cuando el controlador recupera datos de diferentes DBMS, devuelve una cadena vacía ("") para las tablas que no tiene esquemas.|  
|TABLE_NAME (ODBC 1.0)|3|Varchar no es NULL|Nombre de la tabla.|  
|OTORGANTE DE PERMISOS (ODBC 1.0)|4|Varchar|Nombre del usuario que concedió el privilegio; Es NULL si no es aplicable al origen de datos.<br /><br /> Para todas las filas en el que el valor de la columna receptor es el propietario del objeto, la columna GRANTOR será "_SYSTEM".|  
|RECEPTOR DE (ODBC 1.0)|5|Varchar no es NULL|Nombre del usuario a quien se concedió el privilegio.|  
|PRIVILEGIO DE (ODBC 1.0)|6|Varchar no es NULL|El privilegio de tabla. Puede ser uno de los siguientes o un privilegio específicas del origen de datos.<br /><br /> SELECCIONE: Se permite al receptor de permisos para recuperar datos de una o varias columnas de la tabla.<br /><br /> INSERTAR: El receptor tiene permiso para insertar nuevas filas que contienen datos de una o más columnas en la tabla.<br /><br /> ACTUALIZACIÓN: Se permite al receptor de permisos para actualizar los datos en una o varias columnas de la tabla.<br /><br /> ELIMINAR: El receptor tiene permiso para eliminar filas de datos de la tabla.<br /><br /> REFERENCIAS: Se permite que grantee para hacer referencia a una o varias columnas de la tabla dentro de una restricción (por ejemplo, un único, referencial, o una restricción check de tabla).<br /><br /> El ámbito de acción permitida al receptor de permisos por un privilegio de tabla determinada es depende del origen de datos. Por ejemplo, el privilegio UPDATE podría permitir que grantee actualizara todas las columnas de una tabla en un origen de datos y solo aquellas columnas para el que el grantor tiene el privilegio UPDATE en otro origen de datos.|  
|IS_GRANTABLE (ODBC 1.0)|7|Varchar|Indica si se permite que grantee conceda el privilegio a otros usuarios; "Sí", "NO", o NULL si desconocido o no es aplicable al origen de datos.<br /><br /> Un privilegio es que pueden concederse o no se puede conceder pero no ambos. El conjunto de resultados devuelto por **SQLColumnPrivileges** nunca contendrá dos filas para el que todas las columnas excepto la columna IS_GRANTABLE contienen el mismo valor.|  
  
## <a name="code-example"></a>Ejemplo de código  
 Para obtener un ejemplo de código de una función similar, consulte [SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con una columna en un conjunto de resultados|[Función SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Procesamiento de una instrucción de cancelación|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devuelve los privilegios para una o varias columnas|[Función SQLColumnPrivileges](../../../odbc/reference/syntax/sqlcolumnprivileges-function.md)|  
|Devolver las columnas de una o varias tablas|[Función SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md)|  
|Obtención de una sola fila o un bloque de datos en una dirección de solo avance|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Obtención de un bloque de datos o desplazarse a través de un resultado de conjunto|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Devolver estadísticas de tablas e índices|[Función SQLStatistics](../../../odbc/reference/syntax/sqlstatistics-function.md)|  
|Devuelve una lista de tablas en un origen de datos|[Función SQLTables](../../../odbc/reference/syntax/sqltables-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
