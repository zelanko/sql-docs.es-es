---
title: "Función SQLCopyDesc | Documentos de Microsoft"
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
- SQLCopyDesc
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLCopyDesc
helpviewer_keywords:
- SQLCopyDesc function [ODBC]
ms.assetid: d5450895-3824-44c4-8aa4-d4f9752a9602
caps.latest.revision: 19
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e8e7383a16b40a966612784e864594588cc37199
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlcopydesc-function"></a>SQLCopyDesc (función)
**Conformidad**  
 Versión introdujo: ODBC 3.0 normativas: ISO 92  
  
 **Resumen**  
 **SQLCopyDesc** copia información del descriptor de identificador de descriptor de una a otra.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLCopyDesc(  
     SQLHDESC     SourceDescHandle,  
     SQLHDESC     TargetDescHandle);  
```  
  
## <a name="arguments"></a>Argumentos  
 *SourceDescHandle*  
 [Entrada] Identificador de descriptor de origen.  
  
 *TargetDescHandle*  
 [Entrada] Identificador de descriptor de destino. El *TargetDescHandle* argumento puede ser un identificador de un descriptor de la aplicación o un IPD. *TargetDescHandle* no puede establecerse en un identificador de un IRD o **SQLCopyDesc** devolverá HY016 SQLSTATE (no se puede modificar un descriptor de fila de implementación).  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLCopyDesc** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_DESC y un *controlar* de *TargetDescHandle*. Si no es válida *SourceDescHandle* se pasó en la llamada, se devolverá SQL_INVALID_HANDLE pero ningún SQLSTATE se devolverá. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLCopyDesc** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
 Cuando se devuelve un error, la llamada a **SQLCopyDesc** se anula inmediatamente y el contenido de los campos de la *TargetDescHandle* descriptor son indefinidos.  
  
 Dado que **SQLCopyDesc** puede implementarse mediante una llamada a **SQLGetDescField** y **SQLSetDescField**, **SQLCopyDesc** puede devolver SQLSTATE devuelto por **SQLGetDescField** o **SQLSetDescField**.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08S01|Error de vínculo de comunicación|El vínculo de comunicación entre el controlador y el origen de datos al que se conectó el controlador no pudo antes del procesamiento de la función se ha completado.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY007|La instrucción asociada no está preparada|*SourceDescHandle* se asoció con un IRD, y el identificador de instrucción asociado no estaba en estado preparado o ejecutado.|  
|HY010|Error de secuencia de función|(DM) el descriptor de controlar en *SourceDescHandle* o *TargetDescHandle* se asoció una *StatementHandle* para que una función ejecuta de forma asincrónica (not Este uno) se llamó y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) el descriptor de controlar en *SourceDescHandle* o *TargetDescHandle* se asoció una *StatementHandle* que **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llama y se devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión que está asociado el *SourceDescHandle* o *TargetDescHandle*. Esta función asincrónica aún estaba ejecutando cuando el **SQLCopyDesc** se llamó la función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llama para uno de los identificadores de instrucción asociados a la *SourceDescHandle* o *TargetDescHandle* devolvió SQL_PARAM_DATA_AVAILABLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY016|No se puede modificar un descriptor de fila de implementación|*TargetDescHandle* se asoció con un IRD.|  
|HY021|Información de descriptor incoherente|La información del descriptor comprueba durante una comprobación de coherencia no era coherente. Para obtener más información, consulte "Comprobaciones de coherencia" en **SQLSetDescField**.|  
|HY092|Identificador de opción o atributo no válido|La llamada a **SQLCopyDesc** se le solicite una llamada a **SQLSetDescField**, pero * \*ValuePtr* no era válido para el *FieldIdentifier* argumento en *TargetDescHandle*.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *SourceDescHandle* o *TargetDescHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Una llamada a **SQLCopyDesc** copias controlen los campos del descriptor de origen para el identificador de descriptor de destino. Campos pueden copiarse únicamente a un descriptor de la aplicación o un IPD, pero no a un IRD. Campos se pueden copiar desde una aplicación o un descriptor de implementación.  
  
 Campos pueden copiarse desde un IRD sólo si el identificador de instrucción está en el estado de preparadas o ejecutado. en caso contrario, la función devuelve SQLSTATE HY007 (la instrucción asociada no está preparada).  
  
 Campos pueden copiarse desde un IPD si no se ha preparado una instrucción. Si se ha preparado una instrucción SQL con parámetros dinámicos y el rellenado automático de la IPD es admitir y tener habilitado, el IPD se rellena con el controlador. Cuando **SQLCopyDesc** se llama con el IPD como el *SourceDescHandle*, se copian los campos rellenos. Si no se llena el IPD con el controlador, se copia el contenido de los campos originalmente en el IPD.  
  
 Todos los campos del descriptor, excepto SQL_DESC_ALLOC_TYPE (que especifica si el identificador de descriptor se ha asignado de forma automática o explícitamente), se copian, si el campo está definido para el descriptor de destino o no. Campos copiados sobrescriben los campos existentes.  
  
 El controlador copia todos los campos de descriptor si la *SourceDescHandle* y *TargetDescHandle* argumentos están asociados con el mismo controlador, incluso si los controladores están en dos conexiones diferentes o entornos. Si el *SourceDescHandle* y *TargetDescHandle* argumentos están asociados con distintos controladores, el Administrador de controladores copia los campos definidos por ODBC, pero no copia los campos definidos por el controlador o campos que no están definidas por ODBC para el tipo de descriptor.  
  
 La llamada a **SQLCopyDesc** se anula inmediatamente si se produce un error.  
  
 Cuando se copia el campo SQL_DESC_DATA_PTR, se realiza una comprobación de coherencia en el descriptor de destino. Si se produce un error en la comprobación de coherencia, SQLSTATE HY021 (información de descriptor incoherente) se devuelve y la llamada a **SQLCopyDesc** se anula inmediatamente. Para obtener más información sobre las comprobaciones de coherencia, consulte "Comprobaciones de coherencia" en [sqlsetdescrec, función](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
 Identificadores de descriptor pueden copiarse a través de conexiones, incluso si las conexiones están en distintos entornos. Si el Administrador de controladores detecta que pertenecen el origen y el descriptor de destino identificadores no pertenecen a la misma conexión y las dos conexiones para separar los controladores, implementa **SQLCopyDesc** mediante la realización de un campo por campo copiar con **SQLGetDescField** y **SQLSetDescField**.  
  
 Cuando **SQLCopyDesc** se llama con un *SourceDescHandle* en un controlador y una *TargetDescHandle* en otro controlador, la cola de errores de la * SourceDescHandle* está desactivada. Esto ocurre porque **SQLCopyDesc** en este caso, se implementa mediante llamadas a **SQLGetDescField** y **SQLSetDescField**.  
  
> [!NOTE]  
>  Es posible que una aplicación pueda asociar un identificador de descriptor asignado explícitamente con una *StatementHandle*, en lugar de llamar a **SQLCopyDesc** para copiar los campos del descriptor de uno a otro. Un descriptor asignado explícitamente puede asociarse con otra *StatementHandle* en la misma *IdentificadorConexión* estableciendo la instrucción SQL_ATTR_APP_ROW_DESC o SQL_ATTR_APP_PARAM_DESC atributo para el identificador del descriptor asignado explícitamente. Cuando esto sucede, **SQLCopyDesc** no es necesario que se llama para copiar los valores de campo de descriptor de un descriptor a otro. Un identificador de descriptor no se asociará con un *StatementHandle* en otro *IdentificadorConexión*, sin embargo, para usar los mismos valores de campo de descriptor en *StatementHandles*en diferentes *ConnectionHandles*, **SQLCopyDesc** debe llamarse.  
  
 Para obtener una descripción de los campos de un encabezado de descriptor o el registro, consulte [sqlsetdescfield, función](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Para obtener más información sobre descriptores, consulte [descriptores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="copying-rows-between-tables"></a>Copiar datos entre tablas  
 Una aplicación puede copiar datos de una tabla a otra sin copiar los datos en el nivel de aplicación. Para ello, la aplicación enlaza el mismo búferes de datos y la información del descriptor de una instrucción que captura los datos y la instrucción que inserta los datos en una copia. Esto puede realizarse mediante el uso compartido de un descriptor de la aplicación (enlazar un descriptor asignado explícitamente como el Descartar para una instrucción y el APD en otro) o mediante el uso de **SQLCopyDesc** para copiar los enlaces entre la descartar y APD de las dos instrucciones. Si las instrucciones que se encuentran en diferentes conexiones **SQLCopyDesc** debe utilizarse. Además, **SQLCopyDesc** debe llamarse para copiar los enlaces entre IRD y el IPD de las dos instrucciones. Cuando se copian a través de las instrucciones en la misma conexión, el tipo de información de SQL_ACTIVE_STATEMENTS devuelto por el controlador para una llamada a **SQLGetInfo** debe ser mayor que 1 para realizar esta operación correctamente. (Esto no es el caso cuando se copian a través de conexiones.)  
  
### <a name="code-example"></a>Ejemplo de código  
 En el ejemplo siguiente, se usan operaciones de descriptor para copiar los campos de la tabla PartsSource en la tabla PartsCopy. El contenido de la tabla PartsSource se captura en búferes de conjunto de filas en *hstmt0*. Estos valores se utilizan como parámetros de una instrucción INSERT en *hstmt1* para rellenar las columnas de la tabla PartsCopy. Para ello, los campos de IRD de *hstmt0* se copian en los campos de la IPD de *hstmt1*y los campos de la descartar de *hstmt0* se copian en los campos de la APD de *hstmt1*. Use **SQLSetDescField** para establecer el atributo SQL_DESC_PARAMETER_TYPE del IPD en SQL_PARAM_INPUT al copiar los campos IRD de una instrucción con parámetros de salida a los campos IPD que deben ser parámetros de entrada.  
  
```  
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
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Obtener varios campos de descriptor|[Sqlgetdescrec, función](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Establecer un campo único descriptor|[Sqlsetdescfield, función](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Configuración de varios campos de descriptor|[Sqlsetdescrec, función](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)

