---
title: Función SQLCopyDesc (SQLCopyDesc) Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLCopyDesc
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLCopyDesc
helpviewer_keywords:
- SQLCopyDesc function [ODBC]
ms.assetid: d5450895-3824-44c4-8aa4-d4f9752a9602
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ef1fa5b319e8d72d5b70e6f2010e493eec6f844a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301232"
---
# <a name="sqlcopydesc-function"></a>Función SQLCopyDesc
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 3.0: ISO 92  
  
 **Resumen**  
 **SQLCopyDesc** copia la información del descriptor de un identificador de descriptor a otro.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLCopyDesc(  
     SQLHDESC     SourceDescHandle,  
     SQLHDESC     TargetDescHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *SourceDescHandle*  
 [Entrada] Identificador del descriptor de origen.  
  
 *TargetDescHandle*  
 [Entrada] Identificador del descriptor de destino. El *TargetDescHandle* argumento puede ser un identificador de un descriptor de aplicación o un IPD. *TargetDescHandle* no se puede establecer en un identificador de un IRD, o **SQLCopyDesc** devolverá SQLSTATE HY016 (No se puede modificar un descriptor de fila de implementación).  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLCopyDesc** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_DESC y un *control* de *TargetDescHandle*. Si se pasó un *SourceDescHandle* no válido en la llamada, se devolverá SQL_INVALID_HANDLE pero no se devolverá SQLSTATE. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLCopyDesc** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
 Cuando se devuelve un error, la llamada a **SQLCopyDesc** se anula inmediatamente y el contenido de los campos del descriptor *TargetDescHandle* no está definido.  
  
 Dado que **SQLCopyDesc** se puede implementar llamando a **SQLGetDescField** y **SQLSetDescField**, **SQLCopyDesc** puede devolver SQLSTATEs devueltos por **SQLGetDescField** o **SQLSetDescField**.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY007|La declaración asociada no está preparada|*SourceDescHandle* se asoció con un IRD y el identificador de instrucción asociado no estaba en el estado preparado o ejecutado.|  
|HY010|Error de secuencia de funciones|(DM) el identificador de descriptor en *SourceDescHandle* o *TargetDescHandle* se asoció con un *StatementHandle* para el que se llamó a una función de ejecución asincrónica (no esta) y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) el identificador de descriptor en *SourceDescHandle* o *TargetDescHandle* se asoció a un *StatementHandle* para el que **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó y SQLSetPos se llamó y sqlSetPos SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.<br /><br /> (DM) Se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *SourceDescHandle* o *TargetDescHandle*. Esta función asincrónica todavía se estaba ejecutando cuando se llamó a la función **SQLCopyDesc.**<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para uno de los identificadores de instrucción asociados con el *SourceDescHandle* o *TargetDescHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY016|No se puede modificar un descriptor de fila de implementación|*TargetDescHandle* se asoció con un IRD.|  
|HY021|Información de descriptorina incoherente|La información del descriptor comprobada durante una comprobación de coherencia no era coherente. Para obtener más información, vea "Comprobaciones de coherencia" en **SQLSetDescField**.|  
|HY092|Identificador de atributo/opción no válido|La llamada a **SQLCopyDesc** solicitaba una llamada a **SQLSetDescField**, pero * \*ValuePtr* no era válido para el argumento *FieldIdentifier* en *TargetDescHandle*.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) el controlador asociado con el *SourceDescHandle* o *TargetDescHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Una llamada a **SQLCopyDesc** copia los campos del identificador del descriptor de origen en el identificador del descriptor de destino. Los campos solo se pueden copiar en un descriptor de aplicación o en un IPD, pero no en un IRD. Los campos se pueden copiar desde una aplicación o un descriptor de implementación.  
  
 Los campos se pueden copiar de un IRD solo si el identificador de instrucción está en estado preparado o ejecutado; de lo contrario, la función devuelve SQLSTATE HY007 (la instrucción asociada no está preparada).  
  
 Los campos se pueden copiar de una IPD independientemente de si se ha preparado o no una instrucción. Si se ha preparado una instrucción SQL con parámetros dinámicos y se admite y habilita la población automática de la IPD, el controlador rellena el IPD. Cuando **SQLCopyDesc** se llama con el IPD como *El SourceDescHandle*, se copian los campos rellenados. Si el controlador no rellena el IPD, se copia el contenido de los campos originalmente en el IPD.  
  
 Todos los campos del descriptor, excepto SQL_DESC_ALLOC_TYPE (que especifica si el identificador del descriptor se asignó automáticamente o explícitamente), se copian, independientemente de si el campo está definido para el descriptor de destino. Los campos copiados sobrescriben los campos existentes.  
  
 El controlador copia todos los campos descriptores si los *argumentos SourceDescHandle* y *TargetDescHandle* están asociados al mismo controlador, incluso si los controladores están en dos conexiones o entornos diferentes. Si los *argumentos SourceDescHandle* y *TargetDescHandle* están asociados a controladores diferentes, el Administrador de controladores copia campos definidos por ODBC, pero no copia campos definidos por el controlador o campos que ODBC no define para el tipo de descriptor.  
  
 La llamada a **SQLCopyDesc** se anula inmediatamente si se produce un error.  
  
 Cuando se copia el campo SQL_DESC_DATA_PTR, se realiza una comprobación de coherencia en el descriptor de destino. Si se produce un error en la comprobación de coherencia, se devuelve SQLSTATE HY021 (información de descriptor incoherente) y la llamada a **SQLCopyDesc** se anula inmediatamente. Para obtener más información sobre las comprobaciones de coherencia, vea "Comprobaciones de coherencia" en [SQLSetDescRec (función).](../../../odbc/reference/syntax/sqlsetdescrec-function.md)  
  
 Los identificadores de descriptor se pueden copiar entre conexiones incluso si las conexiones están en entornos diferentes. Si el Administrador de controladores detecta que los identificadores de descriptor de origen y de destino no pertenecen a la misma conexión y las dos conexiones pertenecen a controladores independientes, implementa **SQLCopyDesc** realizando una copia campo por campo mediante **SQLGetDescField** y **SQLSetDescField**.  
  
 Cuando **SQLCopyDesc** se llama con un *SourceDescHandle* en un controlador y un *TargetDescHandle* en otro controlador, se borra la cola de errores de *SourceDescHandle.* Esto ocurre porque **SQLCopyDesc** en este caso se implementa mediante llamadas a **SQLGetDescField** y **SQLSetDescField**.  
  
> [!NOTE]  
>  Una aplicación podría asociar un identificador de descriptor asignado explícitamente con un *StatementHandle*, en lugar de llamar a **SQLCopyDesc** para copiar campos de un descriptor a otro. Un descriptor asignado explícitamente se puede asociar a otro *StatementHandle* en el mismo *ConnectionHandle* estableciendo el atributo de instrucción SQL_ATTR_APP_ROW_DESC o SQL_ATTR_APP_PARAM_DESC en el identificador del descriptor asignado explícitamente. Cuando esto se hace, **SQLCopyDesc** no tiene que ser llamado para copiar los valores de campo descriptor de un descriptor a otro. Sin embargo, un identificador de descriptor no se puede asociar a un *StatementHandle* en otro *ConnectionHandle*; para utilizar los mismos valores de campo descriptor en *StatementHandles* en diferentes *ConnectionHandles*, **SQLCopyDesc** debe llamarse.  
  
 Para obtener una descripción de los campos de un encabezado o registro descriptor, vea [SQLSetDescField (Función)](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Para obtener más información sobre los descriptores, consulte [Descriptores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="copying-rows-between-tables"></a>Copia de filas entre tablas  
 Una aplicación puede copiar datos de una tabla a otra sin copiar los datos en el nivel de aplicación. Para ello, la aplicación enlaza los mismos búferes de datos e información de descriptor a una instrucción que captura los datos y la instrucción que inserta los datos en una copia. Esto se puede lograr compartiendo un descriptor de aplicación (enlazando un descriptor asignado explícitamente como ard a una instrucción y el APD en otra) o mediante **SQLCopyDesc** para copiar los enlaces entre el ARD y el APD de las dos instrucciones. Si las instrucciones están en conexiones diferentes, se debe usar **SQLCopyDesc.** Además, se debe llamar a **SQLCopyDesc** para copiar los enlaces entre el IRD y el IPD de las dos instrucciones. Al copiar entre instrucciones en la misma conexión, el tipo de información SQL_ACTIVE_STATEMENTS devuelto por el controlador para una llamada a **SQLGetInfo** debe ser mayor que 1 para que esta operación se realice correctamente. (Este no es el caso cuando se copia a través de conexiones.)  
  
### <a name="code-example"></a>Ejemplo de código  
 En el ejemplo siguiente, las operaciones descriptoras se utilizan para copiar los campos de la tabla PartsSource en la tabla PartsCopy. El contenido de la tabla PartsSource se captura en búferes de conjunto de filas en *hstmt0*. Estos valores se utilizan como parámetros de una instrucción INSERT en *hstmt1* para rellenar las columnas de la tabla PartsCopy. Para ello, los campos del IRD de *hstmt0* se copian en los campos de la IPD de *hstmt1*, y los campos del ARD de *hstmt0* se copian en los campos del APD de *hstmt1*. Utilice **SQLSetDescField** para establecer el atributo SQL_DESC_PARAMETER_TYPE de IPD en SQL_PARAM_INPUT al copiar campos IRD de una instrucción con parámetros de salida a campos IPD que deben ser parámetros de entrada.  
  
```cpp  
#define ROWS 100  
#define DESC_LEN 50  
#define SQL_SUCCEEDED(rc) (rc == SQL_SUCCESS || rc == SQL_SUCCESS_WITH_INFO)  
  
// Template for a row  
typedef struct {  
   SQLINTEGER   sPartID;  
   SQLINTEGER   cbPartID;  
   SQLUCHAR     szDescription[DESC_LENGTH];  
   SQLINTEGER   cbDescription;  
   REAL         sPrice;  
   SQLINTEGER   cbPrice;  
} PartsSource;  
  
PartsSource    rget[ROWS];          // rowset buffer  
SQLUSMALLINT   sts_ptr[ROWS];       // status pointer  
SQLHSTMT       hstmt0, hstmt1;  
SQLHDESC       hArd0, hIrd0, hApd1, hIpd1;  
  
// ARD and IRD of hstmt0  
SQLGetStmtAttr(hstmt0, SQL_ATTR_APP_ROW_DESC, &hArd0, 0, NULL);  
SQLGetStmtAttr(hstmt0, SQL_ATTR_IMP_ROW_DESC, &hIrd0, 0, NULL);  
  
// APD and IPD of hstmt1  
SQLGetStmtAttr(hstmt1, SQL_ATTR_APP_PARAM_DESC, &hApd1, 0, NULL);  
SQLGetStmtAttr(hstmt1, SQL_ATTR_IMP_PARAM_DESC, &hIpd1, 0, NULL);  
  
// Use row-wise binding on hstmt0 to fetch rows  
SQLSetStmtAttr(hstmt0, SQL_ATTR_ROW_BIND_TYPE, (SQLPOINTER) sizeof(PartsSource), 0);  
  
// Set rowset size for hstmt0  
SQLSetStmtAttr(hstmt0, SQL_ATTR_ROW_ARRAY_SIZE, (SQLPOINTER) ROWS, 0);  
  
// Execute a select statement  
SQLExecDirect(hstmt0, "SELECT PARTID, DESCRIPTION, PRICE FROM PARTS ORDER BY 3, 1, 2"",  
               SQL_NTS);  
  
// Bind  
SQLBindCol(hstmt0, 1, SQL_C_SLONG, rget[0].sPartID, 0,   
   &rget[0].cbPartID);  
SQLBindCol(hstmt0, 2, SQL_C_CHAR, &rget[0].szDescription, DESC_LEN,   
   &rget[0].cbDescription);  
SQLBindCol(hstmt0, 3, SQL_C_FLOAT, rget[0].sPrice,   
   0, &rget[0].cbPrice);  
  
// Perform parameter bindings on hstmt1.   
SQLCopyDesc(hArd0, hApd1);  
SQLCopyDesc(hIrd0, hIpd1);  
  
// Set the array status pointer of IRD  
SQLSetStmtAttr(hstmt0, SQL_ATTR_ROW_STATUS_PTR, sts_ptr, SQL_IS_POINTER);  
  
// Set the ARRAY_STATUS_PTR field of APD to be the same  
// as that in IRD.  
SQLSetStmtAttr(hstmt1, SQL_ATTR_PARAM_OPERATION_PTR, sts_ptr, SQL_IS_POINTER);  
  
// Set the hIpd1 records as input parameters  
rc = SQLSetDescField(hIpd1, 1, SQL_DESC_PARAMETER_TYPE, (SQLPOINTER)SQL_PARAM_INPUT, SQL_IS_INTEGER);  
rc = SQLSetDescField(hIpd1, 2, SQL_DESC_PARAMETER_TYPE, (SQLPOINTER)SQL_PARAM_INPUT, SQL_IS_INTEGER);  
rc = SQLSetDescField(hIpd1, 3, SQL_DESC_PARAMETER_TYPE, (SQLPOINTER)SQL_PARAM_INPUT, SQL_IS_INTEGER);  
  
// Prepare an insert statement on hstmt1. PartsCopy is a copy of  
// PartsSource  
SQLPrepare(hstmt1, "INSERT INTO PARTS_COPY VALUES (?, ?, ?)", SQL_NTS);  
  
// In a loop, fetch a rowset, and copy the fetched rowset to PARTS_COPY  
  
rc = SQLFetchScroll(hstmt0, SQL_FETCH_NEXT, 0);  
while (SQL_SUCCEEDED(rc)) {  
  
   // After the call to SQLFetchScroll, the status array has row   
   // statuses. This array is used as input status in the APD  
   // and hence determines which elements of the rowset buffer  
   // are inserted.  
   SQLExecute(hstmt1);  
  
   rc = SQLFetchScroll(hstmt0, SQL_FETCH_NEXT, 0);  
} // while  
```  
  
### <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Obtención de varios campos descriptores|[Función SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Establecer un único campo descriptor|[Función SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Configuración de varios campos descriptores|[Función SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
