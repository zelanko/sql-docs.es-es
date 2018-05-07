---
title: Función SQLDescribeParam | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLDescribeParam
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDescribeParam
helpviewer_keywords:
- SQLDescribeParam function [ODBC]
ms.assetid: 1f5b63c4-2f3e-44da-b155-876405302281
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 584e24e074a89670f0182fdfc29be1017b0a6ad6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqldescribeparam-function"></a>Función SQLDescribeParam
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: ODBC  
  
 **Resumen**  
 **SQLDescribeParam** devuelve la descripción de un marcador de parámetro asociado con una instrucción SQL preparada. Esta información también está disponible en los campos de la IPD.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLDescribeParam(  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ParameterNumber,  
      SQLSMALLINT *   DataTypePtr,  
      SQLULEN *       ParameterSizePtr,  
      SQLSMALLINT *   DecimalDigitsPtr,  
      SQLSMALLINT *   NullablePtr);  
```  
  
## <a name="argument"></a>Argumento  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *ParameterNumber*  
 [Entrada] Número de marcador de parámetro secuencialmente ordenados en orden creciente de los parámetros, comenzando por 1.  
  
 *DataTypePtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el tipo de datos SQL del parámetro. Este valor se lee desde el campo de registro SQL_DESC_CONCISE_TYPE de la IPD. Esto puede ser alguno de los valores de la [tipos de datos SQL](../../../odbc/reference/appendixes/sql-data-types.md) sección del apéndice D: tipos de datos o un tipo de datos SQL específico del controlador.  
  
 En ODBC 3. *x*, SQL_TYPE_DATE, SQL_TYPE_TIME y SQL_TYPE_TIMESTAMP se devolverán en  *\*DataTypePtr* de fecha, hora o datos de marca de tiempo, respectivamente; en ODBC 2. *x*, SQL_DATE, SQL_TIME o SQL_TIMESTAMP se devolverá. El Administrador de controladores realiza las asignaciones necesarias cuando una API ODBC 2. *x* aplicación está trabajando con una aplicación ODBC 3. *x* controlador o cuando una aplicación ODBC 3. *x* aplicación está trabajando con una API ODBC 2. *x* controlador.  
  
 Cuando *ColumnNumber* es igual a 0 (para una columna de marcador), se devuelve SQL_BINARY en  *\*DataTypePtr* marcadores de longitud variable. (SQL_INTEGER se devuelve si se usan marcadores por una aplicación ODBC 3. *x* aplicación trabajar con una API ODBC 2. *x* controlador o una API ODBC 2. *x* aplicación trabajar con una aplicación ODBC 3. *x* controlador.)  
  
 Para obtener más información, consulte [tipos de datos SQL](../../../odbc/reference/appendixes/sql-data-types.md) en tipos de datos de apéndice D:. Para obtener información acerca de los tipos de datos SQL específico del controlador, consulte la documentación del controlador.  
  
 *ParameterSizePtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el tamaño, en caracteres, de la columna o expresión de marcador de parámetro correspondiente de acuerdo con el origen de datos. Para obtener más información sobre el tamaño de columna, vea [tamaño de la columna, dígitos decimales, transferencia de longitud de bytes y el tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
 *DecimalDigitsPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número de dígitos decimales de la columna o expresión del parámetro correspondiente de acuerdo con el origen de datos. Para obtener más información acerca de dígitos decimales, vea [tamaño de la columna, dígitos decimales, transferencia de longitud de bytes y el tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
 *NullablePtr*  
 [Salida] Puntero a un búfer en el que se va a devolver un valor que indica si el parámetro permite valores NULL. Este valor se lee desde el campo SQL_DESC_NULLABLE el IPD. Uno de los siguientes:  
  
-   SQL_NO_NULLS: El parámetro no permite valores NULL (es decir, el valor predeterminado).  
  
-   SQL_NULLABLE: El parámetro admite valores NULL.  
  
-   SQL_NULLABLE_UNKNOWN: El controlador no puede determinar si el parámetro admite valores NULL.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLDescribeParam** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE suelen ser devueltos por **SQLDescribeParam** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07009|Índice de descriptor no válido|(DM) el valor especificado para el argumento *ParameterNumber* es menor que 1.<br /><br /> El valor especificado para el argumento *ParameterNumber* era mayor que el número de parámetros en la instrucción SQL asociada.<br /><br /> El marcador de parámetro formaba parte de una instrucción DML no.<br /><br /> El marcador de parámetro formaba parte de un **seleccione** lista.|  
|08S01|Error de vínculo de comunicación|El vínculo de comunicación entre el controlador y el origen de datos al que se conectó el controlador no pudo antes del procesamiento de la función se ha completado.|  
|21S01|Lista de valores insertados no coincide con la lista de columnas|El número de parámetros en el **insertar** instrucción no coincidía con el número de columnas en la tabla mencionada en la instrucción.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar memoria que es necesario para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle*. A continuación, se llama a la función nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle* desde un subproceso distinto en un aplicaciones multiproceso.|  
|HY010|Error de secuencia de función|(DM) se llama a la función antes de llamar a **SQLPrepare** o **SQLExecDirect** para el *StatementHandle*.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónica aún estaba ejecutando cuando el **SQLDescribeParam** se llamó la función.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica (no esta uno) para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *StatementHandle* no admite la función.|  
|IM017|Sondeo está deshabilitado en el modo de notificación asincrónica|Cada vez que se utiliza el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** se debe llamar en el identificador para realizar el procesamiento posterior a la y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 Marcadores de parámetros se numeran en orden creciente de los parámetros, comenzando por 1, en el orden en que aparecen en la instrucción SQL.  
  
 **SQLDescribeParam** no devuelve el tipo (entrada, entrada/salida o de salida) de un parámetro en una instrucción SQL. Excepto en las llamadas a procedimientos, todos los parámetros en instrucciones SQL son parámetros de entrada. Para determinar el tipo de cada parámetro en una llamada a un procedimiento, una aplicación llama **SQLProcedureColumns**.  
  
 Para obtener más información, consulte [que describe parámetros](../../../odbc/reference/develop-app/describing-parameters.md).  
  
## <a name="code-example"></a>Ejemplo de código  
 En el ejemplo siguiente se pide al usuario una instrucción SQL y, a continuación, se prepara esa instrucción. A continuación, llama a **SQLNumParams** para determinar si la instrucción contiene todos los parámetros. Si la instrucción contiene parámetros, llama a **SQLDescribeParam** para describir los parámetros y **SQLBindParameter** para enlazarlos. Por último, pide al usuario para los valores de los parámetros y, a continuación, ejecuta la instrucción.  
  
```  
SQLCHAR       Statement[100];  
SQLSMALLINT   NumParams, i, DataType, DecimalDigits, Nullable;  
SQLUINTEGER   ParamSize;  
SQLHSTMT      hstmt;  
  
// Prompt the user for an SQL statement and prepare it.  
GetSQLStatement(Statement);  
SQLPrepare(hstmt, Statement, SQL_NTS);  
  
// Check to see if there are any parameters. If so, process them.  
SQLNumParams(hstmt, &NumParams);  
if (NumParams) {  
   // Allocate memory for three arrays. The first holds pointers to buffers in which  
   // each parameter value will be stored in character form. The second contains the  
   // length of each buffer. The third contains the length/indicator value for each  
   // parameter.  
   SQLPOINTER * PtrArray = (SQLPOINTER *) malloc(NumParams * sizeof(SQLPOINTER));  
   SQLINTEGER * BufferLenArray = (SQLINTEGER *) malloc(NumParams * sizeof(SQLINTEGER));  
   SQLINTEGER * LenOrIndArray = (SQLINTEGER *) malloc(NumParams * sizeof(SQLINTEGER));  
  
   for (i = 0; i < NumParams; i++) {  
   // Describe the parameter.  
   SQLDescribeParam(hstmt, i + 1, &DataType, &ParamSize, &DecimalDigits, &Nullable);  
  
   // Call a helper function to allocate a buffer in which to store the parameter  
   // value in character form. The function determines the size of the buffer from  
   // the SQL data type and parameter size returned by SQLDescribeParam and returns  
   // a pointer to the buffer and the length of the buffer.  
   AllocParamBuffer(DataType, ParamSize, &PtrArray[i], &BufferLenArray[i]);  
  
   // Bind the memory to the parameter. Assume that we only have input parameters.  
   SQLBindParameter(hstmt, i + 1, SQL_PARAM_INPUT, SQL_C_CHAR, DataType, ParamSize,  
         DecimalDigits, PtrArray[i], BufferLenArray[i],  
         &LenOrIndArray[i]);  
  
   // Prompt the user for the value of the parameter and store it in the memory  
   // allocated earlier. For simplicity, this function does not check the value  
   // against the information returned by SQLDescribeParam. Instead, the driver does  
   // this when the statement is executed.  
   GetParamValue(PtrArray[i], BufferLenArray[i], &LenOrIndArray[i]);  
   }  
}  
  
// Execute the statement.  
SQLExecute(hstmt);  
  
// Process the statement further, such as retrieving results (if any) and closing the  
// cursor (if any). Code not shown.  
  
// Free the memory allocated for each parameter and the memory allocated for the arrays  
// of pointers, buffer lengths, and length/indicator values.  
for (i = 0; i < NumParams; i++) free(PtrArray[i]);  
free(PtrArray);  
free(BufferLenArray);  
free(LenOrIndArray);  
```  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con un parámetro|[Función SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Cancelar el procesamiento de una instrucción|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Ejecutar una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Preparar una instrucción de ejecución|[Función SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
