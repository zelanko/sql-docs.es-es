---
title: FUNción SQLBindParameter ( SQLBindParameter) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLBindParameter
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLBindParameter
helpviewer_keywords:
- SQLBindParameter function [ODBC]
ms.assetid: 38349d4b-be03-46f9-9d6a-e50dd144e225
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 02f50862bcfb0295c7f098afc6856c91e0249f66
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301365"
---
# <a name="sqlbindparameter-function"></a>Función SQLBindParameter

**Conformidad**  
 Versión introducida: Cumplimiento de estándares ODBC 2.0: ODBC  
  
 **Resumen**  
 **SQLBindParameter** enlaza un búfer a un marcador de parámetro en una instrucción SQL. **SQLBindParameter** admite el enlace a un tipo de datos Unicode C, incluso si el controlador subyacente no admite datos Unicode.  
  
> [!NOTE]  
>  Esta función reemplaza la función ODBC 1.0 **SQLSetParam**. Para obtener más información, consulte "Comentarios."  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp
  
SQLRETURN SQLBindParameter(  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ParameterNumber,  
      SQLSMALLINT     InputOutputType,  
      SQLSMALLINT     ValueType,  
      SQLSMALLINT     ParameterType,  
      SQLULEN         ColumnSize,  
      SQLSMALLINT     DecimalDigits,  
      SQLPOINTER      ParameterValuePtr,  
      SQLLEN          BufferLength,  
      SQLLEN *        StrLen_or_IndPtr);  
```
  
## <a name="arguments"></a>Argumentos

 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *ParameterNumber*  
 [Entrada] Número de parámetro, ordenado secuencialmente en orden de parámetros creciente, a partir de 1.  
  
 *InputOutputType*  
 [Entrada] El tipo del parámetro. Para obtener más información, vea "*InputOutputType* Argument" en "Comments."  
  
 *ValueType*  
 [Entrada] El tipo de datos C del parámetro. Para obtener más información, vea "*ValueType* Argument" en "Comments."  
  
 *ParameterType*  
 [Entrada] El tipo de datos SQL del parámetro. Para obtener más información, vea "*ParameterType* Argument" en "Comments."  
  
 *ColumnSize*  
 [Entrada] El tamaño de la columna o expresión del marcador de parámetro correspondiente. Para obtener más información, vea "*ColumnSize* Argument" en "Comments."  
  
 Si la aplicación se ejecutará en un sistema operativo Windows de 64 bits, vea Información de [64 bits de ODBC.](../../../odbc/reference/odbc-64-bit-information.md)  
  
 *DecimalDigits*  
 [Entrada] Los dígitos decimales de la columna o expresión del marcador de parámetro correspondiente. Para obtener más información sobre el tamaño de columna, vea Tamaño de [columna, Dígitos decimales, Transferir longitud de octeto y Tamaño](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)de visualización .  
  
 *ParameterValuePtr*  
 [Entrada diferida] Puntero a un búfer para los datos del parámetro. Para obtener más información, vea "*ParameterValuePtr* Argument" en "Comments."  
  
 *BufferLength*  
 [Entrada/Salida] Longitud del búfer *ParameterValuePtr* en bytes. Para obtener más información, vea "*BufferLength* Argument" en "Comments."  
  
 Consulte Información de [ODBC de 64 bits,](../../../odbc/reference/odbc-64-bit-information.md)si la aplicación se ejecutará en un sistema operativo de 64 bits.  
  
 *StrLen_or_IndPtr*  
 [Entrada diferida] Puntero a un búfer para la longitud del parámetro. Para obtener más información, consulte *"StrLen_or_IndPtr* Argument" en "Comentarios."  
  
## <a name="returns"></a>Devuelve

 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico

 Cuando **SQLBindParameter** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *Control* de *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE normalmente devueltos por **SQLBindParameter** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  

|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|07006|Infracción de atributo de tipo de datos restringido|El tipo de datos identificado por el *ValueType* argumento no se puede convertir al tipo de datos identificado por el *ParameterType* argumento. Tenga en cuenta que **SQLExecDirect**, **SQLExecute**o **SQLPutData** pueden devolver este error en tiempo de ejecución, en lugar de **SQLBindParameter**.|  
|07009|Indice de descriptor no válido|(DM) el valor especificado para el argumento *ParameterNumber* era menor que 1.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el **MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY003|Tipo de búfer de aplicación no válido|El valor especificado por el argumento *ValueType* no era un tipo de datos C o SQL_C_DEFAULT válido.|  
|HY004|Tipo de datos SQL no válido|El valor especificado para el argumento *ParameterType* no era un identificador de tipo de datos SQL ODBC válido ni un identificador de tipo de datos SQL específico del controlador admitido por el controlador.|  
|HY009|Valor de argumento no válido|(DM) el argumento *ParameterValuePtr* era un puntero nulo, el argumento *StrLen_or_IndPtr* era un puntero nulo y el argumento *InputOutputType* no se SQL_PARAM_OUTPUT.<br /><br /> (DM) SQL_PARAM_OUTPUT, donde el argumento *ParameterValuePtr* era un puntero nulo, el tipo C era char o binario y BufferLength (*cbValueMax*) era mayor que 0.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando **SQLBindParameter** se llamó.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *StatementHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función de ejecución asincrónica para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY021|Información de descriptorina incoherente|La información del descriptor comprobada durante una comprobación de coherencia no era coherente. (Consulte la sección "Comprobaciones de coherencia" en **SQLSetDescField**.)<br /><br /> El valor especificado para el argumento *DecimalDigits* estaba fuera del intervalo de valores admitidos por el origen de datos para una columna del tipo de datos SQL especificado por el *ParameterType* argumento.|  
|HY090|Cadena no válida o longitud de búfer|(DM) el valor de *BufferLength* era menor que 0. (Consulte la descripción del campo SQL_DESC_DATA_PTR en **SQLSetDescField**.)|  
|HY104|Precisión o valor de escala no válidos|El valor especificado para el argumento *ColumnSize* o *DecimalDigits* estaba fuera del intervalo de valores admitidos por el origen de datos para una columna del tipo de datos SQL especificado por el *ParameterType* argumento.|  
|HY105|Tipo de parámetro no válido|(DM) el valor especificado para el argumento *InputOutputType* no era válido. (Véase "Comentarios.")|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYC00|Característica opcional no implementada|El controlador o el origen de datos no admite la conversión especificada por la combinación del valor especificado para el argumento *ValueType* y el valor específico del controlador especificado para el argumento *ParameterType*.<br /><br /> El valor especificado para el argumento *ParameterType* era un identificador de tipo de datos SQL ODBC válido para la versión de ODBC admitida por el controlador, pero no era compatible con el controlador o el origen de datos.<br /><br /> El controlador solo admite ODBC 2. *x* y el argumento *ValueType* fue uno de los siguientes:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> y todos los tipos de datos de intervalo C enumerados en [C Tipos](../../../odbc/reference/appendixes/c-data-types.md) de datos en el Apéndice D: Tipos de datos.<br /><br /> El controlador solo admite versiones ODBC anteriores a 3.50 y el argumento *ValueType* se SQL_C_GUID.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *StatementHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios

 Una aplicación llama a **SQLBindParameter** para enlazar cada marcador de parámetro en una instrucción SQL. Los enlaces permanecen en vigor hasta que la aplicación llama **SQLBindParameter** de nuevo, llama a **SQLFreeStmt** con la opción SQL_RESET_PARAMS o llama a **SQLSetDescField** para establecer el SQL_DESC_COUNT campo de encabezado de la APD a 0.  
  
 Para obtener más información acerca de los parámetros, vea Parámetros de [instrucción](../../../odbc/reference/develop-app/statement-parameters.md). Para obtener más información acerca de los tipos de datos de parámetros y marcadores de parámetros, vea Tipos de [datos](../../../odbc/reference/appendixes/parameter-data-types.md) de parámetros y Marcadores de [parámetros](../../../odbc/reference/appendixes/parameter-markers.md) en Apéndice C: Gramática SQL.  
  
## <a name="parameternumber-argument"></a>Argumentación ParameterNumber  
 Si *ParameterNumber* en la llamada a **SQLBindParameter** es mayor que el valor de SQL_DESC_COUNT, **SQLSetDescField** se llama para aumentar el valor de SQL_DESC_COUNT a *ParameterNumber*.  
  
## <a name="inputoutputtype-argument"></a>Argumento InputOutputType  
 El *argumento InputOutputType* especifica el tipo del parámetro. Este argumento establece el campo SQL_DESC_PARAMETER_TYPE de la IPD. Todos los parámetros de las instrucciones SQL que no llaman a procedimientos, como instrucciones **INSERT,** son *parámetros de entrada**.* Los parámetros de las llamadas a procedimientos pueden ser parámetros de entrada, entrada/salida o salida. (Una aplicación llama a **SQLProcedureColumns** para determinar el tipo de un parámetro en una llamada a procedimiento; se supone que los parámetros cuyo tipo no se puede determinar son parámetros de entrada.)  
  
 El argumento *InputOutputType* es uno de los valores siguientes:  
  
-   SQL_PARAM_INPUT. El parámetro marca un parámetro en una instrucción SQL que no llama a un procedimiento, como una instrucción **INSERT,** o marca un parámetro de entrada en un procedimiento. Por ejemplo, los parámetros de **INSERT INTO Employee VALUES (?, ?, ?)** son parámetros de entrada, mientras que los parámetros de la llamada **AddEmp(?, ?, ?)** pueden ser, pero no necesariamente, parámetros de entrada.  
  
     Cuando se ejecuta la instrucción, el controlador envía datos para el parámetro al origen de datos; el \* *parameterValuePtr* búfer debe contener un valor de entrada válido, o el **StrLen_or_IndPtr* búfer debe contener SQL_NULL_DATA, SQL_DATA_AT_EXEC o el resultado de la macro SQL_LEN_DATA_AT_EXEC.  
  
     Si una aplicación no puede determinar el tipo de un parámetro en una llamada a procedimiento, establece *InputOutputType* en SQL_PARAM_INPUT; si el origen de datos devuelve un valor para el parámetro, el controlador lo descarta.  
  
-   SQL_PARAM_INPUT_OUTPUT. El parámetro marca un parámetro de entrada/salida en un procedimiento. Por ejemplo, el parámetro de **la llamada GetEmpDept(?)** es un parámetro de entrada/salida que acepta el nombre de un empleado y devuelve el nombre del departamento del empleado.  
  
     Cuando se ejecuta la instrucción, el controlador envía datos para el parámetro al origen de datos; el \* *ParameterValuePtr* búfer debe contener un \*valor de entrada válido, o el *búfer de StrLen_or_IndPtr* debe contener SQL_NULL_DATA, SQL_DATA_AT_EXEC o el resultado de la macro SQL_LEN_DATA_AT_EXEC. Después de ejecutar la instrucción, el controlador devuelve datos para el parámetro a la aplicación; si el origen de datos no devuelve un valor para un parámetro de entrada/salida, el controlador establece el búfer de*StrLen_or_IndPtr* * en SQL_NULL_DATA.  
  
    > [!NOTE]  
    >  Cuando una aplicación ODBC 1.0 llama a **SQLSetParam** en un controlador ODBC 2.0, el Administrador de controladores convierte esto en una llamada a **SQLBindParameter** en el que el *InputOutputType* argumento está establecido en SQL_PARAM_INPUT_OUTPUT.  
  
-   SQL_PARAM_OUTPUT. El parámetro marca el valor devuelto de un procedimiento o un parámetro de salida en un procedimiento; en cualquier caso, estos se conocen como parámetros de *salida.* Por ejemplo, el parámetro de la dirección de correo electrónico **GetNextEmpID** es un parámetro de salida que devuelve el siguiente identificador de empleado.  
  
     Después de ejecutar la instrucción, el controlador devuelve datos para el parámetro a la aplicación, a menos que el *ParameterValuePtr* y *StrLen_or_IndPtr* argumentos son punteros nulos, en cuyo caso el controlador descarta el valor de salida. Si el origen de datos no devuelve un valor para un parámetro de salida, el controlador establece el búfer de*StrLen_or_IndPtr* * en SQL_NULL_DATA.  
  
-   SQL_PARAM_INPUT_OUTPUT_STREAM. Indica que se debe transmitir un parámetro de entrada/salida. **SQLGetData** puede leer valores de parámetro en partes. *BufferLength* se omite porque la longitud del búfer se determinará a la llamada de **SQLGetData**. El valor del búfer *de StrLen_or_IndPtr* debe contener SQL_NULL_DATA, SQL_DEFAULT_PARAM, SQL_DATA_AT_EXEC o el resultado de la macro SQL_LEN_DATA_AT_EXEC. Un parámetro debe enlazarse como un parámetro de datos en ejecución (DAE) en la entrada si se transmitirá en la salida. *ParameterValuePtr* puede ser cualquier valor de puntero no nulo que **SQLParamData** devolverá como el token definido por el usuario cuyo valor se pasó con *ParameterValuePtr* para la entrada y la salida. Para obtener más información, vea el tema que trata sobre [recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
-   SQL_PARAM_OUTPUT_STREAM. Igual que SQL_PARAM_INPUT_OUTPUT_STREAM, para un parámetro de salida. **StrLen_or_IndPtr* se omite en la entrada.  
  
 En la tabla siguiente se enumeran diferentes combinaciones de *InputOutputType* y **StrLen_or_IndPtr:*  
  
|*InputOutputType*|**StrLen_or_IndPtr*|Resultado|Observación sobre ParameterValuePtr|  
|-----------------------|----------------------------|-------------|---------------------------------|  
|SQL_PARAM_INPUT|SQL_LEN_DATA_AT_EXEC(*len*) o SQL_DATA_AT_EXEC|Entrada en partes|*ParameterValuePtr* puede ser cualquier valor de puntero que **SQLParamData** devolverá como el token definido por el usuario cuyo valor se pasó con *ParameterValuePtr*.|  
|SQL_PARAM_INPUT|No SQL_LEN_DATA_AT_EXEC(*len*) ni SQL_DATA_AT_EXEC|Búfer enlazado a entrada|*ParameterValuePtr* es la dirección del búfer de entrada.|  
|SQL_PARAM_OUTPUT|Ignorado en la entrada.|Búfer enlazado a salida|*ParameterValuePtr* es la dirección del búfer de salida.|  
|SQL_PARAM_OUTPUT_STREAM|Ignorado en la entrada.|Salida transmitida|*ParameterValuePtr* puede ser cualquier valor de puntero, que **SQLParamData** devolverá como el token definido por el usuario cuyo valor se pasó con *ParameterValuePtr*.|  
|SQL_PARAM_INPUT_OUTPUT|SQL_LEN_DATA_AT_EXEC(*len*) o SQL_DATA_AT_EXEC|Entrada en piezas y búfer enlazado a salida|*ParameterValuePtr* es la dirección del búfer de salida, que **SQLParamData** también devolverá como el token definido por el usuario cuyo valor se pasó con *ParameterValuePtr*.|  
|SQL_PARAM_INPUT_OUTPUT|No SQL_LEN_DATA_AT_EXEC(*len*) ni SQL_DATA_AT_EXEC|Búfer enlazado de entrada y búfer enlazado a la salida|*ParameterValuePtr* es la dirección del búfer de entrada/salida compartido.|
|SQL_PARAM_INPUT_OUTPUT_STREAM|SQL_LEN_DATA_AT_EXEC(*len*) o SQL_DATA_AT_EXEC|Entrada en piezas y salida transmitida|*ParameterValuePtr* puede ser cualquier valor de puntero no nulo, que será devuelto por **SQLParamData** como el token definido por el usuario cuyo valor se pasó con *ParameterValuePtr* para la entrada y la salida.|  
  
> [!NOTE]  
>  El controlador debe decidir qué tipos SQL se permiten cuando una aplicación enlaza un parámetro de salida o entrada-salida como transmitido. El administrador de controladores no generará un error para un tipo SQL no válido.  
  
## <a name="valuetype-argument"></a>Argumento ValueType

 El *ValueType* argumento especifica el tipo de datos C del parámetro. Este argumento establece los campos SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE y SQL_DESC_DATETIME_INTERVAL_CODE del APD. Debe ser uno de los valores de la sección Tipos de [datos C](../../../odbc/reference/appendixes/c-data-types.md) del Apéndice D: Tipos de datos.  
  
 Si el argumento *ValueType* es uno de los tipos de datos de intervalo, el campo SQL_DESC_TYPE del registro *ParameterNumber* del APD se establece en SQL_INTERVAL, el campo SQL_DESC_CONCISE_TYPE del APD se establece en el tipo de datos de intervalo conciso y el campo SQL_DESC_DATETIME_INTERVAL_CODE del registro *ParameterNumber* se establece en un subcódigo para el tipo de datos de intervalo específico. (Véase [Apéndice D: Tipos](../../../odbc/reference/appendixes/appendix-d-data-types.md)de datos .) Para los datos se utilizan la precisión inicial del intervalo predeterminado (2) y la precisión de segundos de intervalo predeterminada (6), tal como se establece en los campos SQL_DESC_DATETIME_INTERVAL_PRECISION y SQL_DESC_PRECISION del APD, respectivamente. Si la precisión predeterminada no es adecuada, la aplicación debe establecer explícitamente el campo descriptor mediante una llamada a **SQLSetDescField** o **SQLSetDescRec**.  
  
 Si el argumento *ValueType* es uno de los tipos de datos datetime, el campo SQL_DESC_TYPE del registro *ParameterNumber* del APD se establece en SQL_DATETIME, el campo SQL_DESC_CONCISE_TYPE del registro *ParameterNumber* del APD se establece en el tipo de datos conciso datetime C y el campo SQL_DESC_DATETIME_INTERVAL_CODE del registro *ParameterNumber* se establece en un subcódigo para el tipo de datos datetime específico. (Véase [Apéndice D: Tipos](../../../odbc/reference/appendixes/appendix-d-data-types.md)de datos .)  
  
 Si el *ValueType* argumento es un tipo de datos SQL_C_NUMERIC, la precisión predeterminada (que está definida por el controlador) y la escala predeterminada (0), como se establece en los campos SQL_DESC_PRECISION y SQL_DESC_SCALE del APD, se utilizan para los datos. Si la precisión o escala predeterminada no es adecuada, la aplicación debe establecer explícitamente el campo descriptor mediante una llamada a **SQLSetDescField** o **SQLSetDescRec**.  
  
 SQL_C_DEFAULT especifica que el valor del parámetro se transfiera desde el tipo de datos C predeterminado para el tipo de datos SQL especificado con *ParameterType*.  
  
 También puede especificar un tipo de datos C extendido. Para obtener más información, vea el tema sobre [tipos de datos C en ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 Para obtener más información, vea Tipos de [datos C predeterminados](../../../odbc/reference/appendixes/default-c-data-types.md), [Convertir datos de C a tipos](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md)de datos SQL y Convertir datos de SQL a tipos de [datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) en Apéndice D: Tipos de datos.  
  
## <a name="parametertype-argument"></a>Argumento ParameterType

 Debe ser uno de los valores enumerados en la sección Tipos de [datos SQL](../../../odbc/reference/appendixes/sql-data-types.md) del Apéndice D: Tipos de datos, o debe ser un valor específico del controlador. Este argumento establece los campos SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE y SQL_DESC_DATETIME_INTERVAL_CODE de la IPD.  
  
 Si el *ParameterType* argumento es uno de los identificadores de fecha y hora, el campo de SQL_DESC_TYPE de la IPD se establece en SQL_DATETIME, el campo SQL_DESC_CONCISE_TYPE de la IPD se establece en el tipo de datos SQL datetime conciso y el campo SQL_DESC_DATETIME_INTERVAL_CODE se establece en el valor de subcódigo datetime adecuado.  
  
 Si *ParameterType* es uno de los identificadores de intervalo, el campo SQL_DESC_TYPE de la IPD se establece en SQL_INTERVAL, el campo SQL_DESC_CONCISE_TYPE de la IPD se establece en el tipo de datos de intervalo SQL conciso y el campo SQL_DESC_DATETIME_INTERVAL_CODE de la IPD se establece en el subcódigo de intervalo adecuado. El campo SQL_DESC_DATETIME_INTERVAL_PRECISION del IPD se establece en la precisión inicial del intervalo y el campo SQL_DESC_PRECISION se establece en la precisión de los segundos del intervalo, si procede. Si el valor predeterminado de SQL_DESC_DATETIME_INTERVAL_PRECISION o SQL_DESC_PRECISION no es adecuado, la aplicación debe establecerlo explícitamente llamando a **SQLSetDescField**. Para obtener más información acerca de cualquiera de estos campos, vea [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 Si el *ValueType* argumento es un tipo de datos SQL_NUMERIC, la precisión predeterminada (que está definida por el controlador) y la escala predeterminada (0), como se establece en los campos SQL_DESC_PRECISION y SQL_DESC_SCALE de la IPD, se utilizan para los datos. Si la precisión o escala predeterminada no es adecuada, la aplicación debe establecer explícitamente el campo descriptor mediante una llamada a **SQLSetDescField** o **SQLSetDescRec**.  
  
 Para obtener información sobre cómo se convierten los datos, vea [Convertir datos de C a tipos](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) de datos SQL y Convertir datos de SQL a tipos de datos [C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) en apéndice D: tipos de datos.  
  
## <a name="columnsize-argument"></a>ColumnSize Argument

 El *ColumnSize* argumento especifica el tamaño de la columna o expresión que corresponde al marcador de parámetro, la longitud de esos datos o ambos. Este argumento establece diferentes campos de la IPD, dependiendo del tipo de datos SQL (el *ParameterType* argumento). Las siguientes reglas se aplican a esta asignación:  
  
-   Si *ParameterType* es SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY o uno de los tipos de datos concisos de fecha y hora o intervalo de SQL, el campo SQL_DESC_LENGTH de la IPD se establece en el valor *ColumnSize*. (Para obtener más información, consulte la sección Tamaño de [columna, dígitos decimales, Longitud de octeto de transferencia y Tamaño](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) de visualización en Apéndice D: Tipos de datos.)  
  
-   Si *ParameterType* está SQL_DECIMAL, SQL_NUMERIC, SQL_FLOAT, SQL_REAL o SQL_DOUBLE, el campo SQL_DESC_PRECISION de la IPD se establece en el valor de *ColumnSize*.  
  
-   Para otros tipos de datos, se omite el argumento *ColumnSize.*  
  
 Para obtener más información, consulte "Pasar valores de parámetro" y SQL_DATA_AT_EXEC en "*StrLen_or_IndPtr* Argument."  
  
## <a name="decimaldigits-argument"></a>Argumento DecimalDigits

 Si *ParameterType* es SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP, SQL_INTERVAL_SECOND, SQL_INTERVAL_DAY_TO_SECOND, SQL_INTERVAL_HOUR_TO_SECOND o SQL_INTERVAL_MINUTE_TO_SECOND, el campo SQL_DESC_PRECISION de la IPD se establece en *DecimalDigits*. Si *ParameterType* es SQL_NUMERIC o SQL_DECIMAL, el campo SQL_DESC_SCALE de la IPD se establece en *DecimalDigits*. Para todos los demás tipos de datos, se omite el argumento *DecimalDigits.*  
  
## <a name="parametervalueptr-argument"></a>Argumentación ParameterValuePtr

 El *ParameterValuePtr* argumento apunta a un búfer que, cuando **SQLExecute** o **SQLExecDirect** se llama, contiene los datos reales para el parámetro. Los datos deben tener el formato especificado por el *ValueType* argumento. Este argumento establece el campo SQL_DESC_DATA_PTR del APD. Una aplicación puede establecer el *ParameterValuePtr* argumento a un puntero nulo, siempre que * \*StrLen_or_IndPtr* sea SQL_NULL_DATA o SQL_DATA_AT_EXEC. (Esto solo se aplica a los parámetros de entrada o entrada/salida.)  
  
 Si \* *StrLen_or_IndPtr* es el resultado de la macro o SQL_DATA_AT_EXEC SQL_LEN_DATA_AT_EXEC(*length*), *ParameterValuePtr* es un valor de puntero definido por la aplicación que está asociado con el parámetro. Se devuelve a la aplicación a través de **SQLParamData**. Por ejemplo, *ParameterValuePtr* podría ser un token distinto de cero, como un número de parámetro, un puntero a datos o un puntero a una estructura que la aplicación usó para enlazar parámetros de entrada. Sin embargo, tenga en cuenta que si el parámetro es un parámetro de entrada/salida, *ParameterValuePtr* debe ser un puntero a un búfer donde se almacenará el valor de salida. Si el valor del atributo de instrucción SQL_ATTR_PARAMSET_SIZE es mayor que 1, la aplicación puede usar el valor al que apunta el atributo de instrucción SQL_ATTR_PARAMS_PROCESSED_PTR junto con el *ParameterValuePtr* argumento. Por ejemplo, *ParameterValuePtr* podría apuntar a una matriz de valores y la aplicación podría utilizar el valor señalado por SQL_ATTR_PARAMS_PROCESSED_PTR para recuperar el valor correcto de la matriz. Para obtener más información, consulte "Pasar valores de parámetro" más adelante en esta sección.  
  
 Si el *InputOutputType* argumento es SQL_PARAM_INPUT_OUTPUT o SQL_PARAM_OUTPUT, *ParameterValuePtr* apunta a un búfer en el que el controlador devuelve el valor de salida. Si el procedimiento devuelve uno o \*varios conjuntos de resultados, no se garantiza que se establezca el búfer *ParameterValuePtr* hasta que se hayan procesado todos los conjuntos de resultados o recuentos de filas. Si el búfer no se establece hasta que se completa el procesamiento, los parámetros de salida y los valores devueltos no están disponibles hasta que **SQLMoreResults** devuelve SQL_NO_DATA. Llamar a **SQLCloseCursor** o **SQLFreeStmt** con una opción de SQL_CLOSE hará que se descarten estos valores.  
  
 Si el valor del atributo de instrucción SQL_ATTR_PARAMSET_SIZE es mayor que 1, *ParameterValuePtr* apunta a una matriz. Una sola instrucción SQL procesa la matriz completa de valores de entrada para un parámetro de entrada o entrada/salida y devuelve una matriz de valores de salida para un parámetro de entrada/salida o salida.  
  
## <a name="bufferlength-argument"></a>Argumento BufferLength

 Para los datos de carácter y C binario, \*el *BufferLength* argumento especifica la longitud de la *ParameterValuePtr* búfer (si es un solo elemento) o la longitud de un elemento en el \* *ParameterValuePtr* matriz (si el valor en el SQL_ATTR_PARAMSET_SIZE atributo de instrucción es mayor que 1). Este argumento establece el campo de registro SQL_DESC_OCTET_LENGTH del APD. Si la aplicación especifica varios valores, *BufferLength* se utiliza para determinar la ubicación de los valores en el **ParameterValuePtr* matriz, tanto en la entrada y en la salida. Para los parámetros de entrada/salida y salida, se utiliza para determinar si se truncan los datos de caracteres y C binarios en la salida:  
  
-   Para los datos de carácter C, si el número de bytes disponibles para devolver es mayor o igual que *BufferLength*, los datos de \* *ParameterValuePtr* se truncan en *BufferLength* menos la longitud de un carácter de terminación nula y el controlador termina en null.  
  
-   Para los datos binarios de C, si el número de bytes disponibles para devolver es mayor que *BufferLength*, los datos de \* *ParameterValuePtr* se truncan en bytes *BufferLength.*  
  
 Para todos los demás tipos de datos de C, se omite el argumento *BufferLength.* La longitud \*del búfer *ParameterValuePtr* (si es un único elemento) \*o la longitud de un elemento de la *parameterValuePtr* matriz (si la aplicación llama **a SQLSetStmtAttr** con un *atributo* argumento de SQL_ATTR_PARAMSET_SIZE especificar varios valores para cada parámetro) se supone que es la longitud de la C tipo de datos.  
  
 Para los parámetros de salida o entrada/salida transmitidos por secuencias, se omite el argumento *BufferLength* porque la longitud del búfer se especifica en **SQLGetData**.  
  
> [!NOTE]  
>  Cuando una aplicación ODBC 1.0 llama a **SQLSetParam** en un ODBC 3. *x* controlador, el Administrador de controladores convierte esto en una llamada a **SQLBindParameter** en el que el *BufferLength* argumento siempre está SQL_SETPARAM_VALUE_MAX. Porque el Administrador de controladores devuelve un error si un ODBC 3. *x* aplicación establece *BufferLength* en SQL_SETPARAM_VALUE_MAX, un ODBC 3. *x* controlador puede utilizar esto para determinar cuándo es llamado por una aplicación ODBC 1.0.  
  
> [!NOTE]  
>  En **SQLSetParam**, la forma en que una aplicación especifica la longitud del búfer **ParameterValuePtr* para que el controlador pueda devolver datos binarios o de carácter y la forma en que una aplicación envía una matriz de valores de caracteres o parámetros binarios al controlador, están definidos por el controlador.  
  
## <a name="strlen_or_indptr-argument"></a>StrLen_or_IndPtr Argumento

 El *argumento StrLen_or_IndPtr* apunta a un búfer que, cuando **sqlExecute** o **SQLExecDirect** se llama, contiene uno de los siguientes. (Este argumento establece los campos SQL_DESC_OCTET_LENGTH_PTR y SQL_DESC_INDICATOR_PTR registro de los punteros de parámetro de aplicación.)  
  
-   La longitud del valor del parámetro almacenado en **ParameterValuePtr*. Esto se omite excepto para los datos de carácter o C binarios.  
  
-   SQL_NTS. El valor del parámetro es una cadena terminada en null.  
  
-   SQL_NULL_DATA. El valor del parámetro es NULL.  
  
-   SQL_DEFAULT_PARAM. Un procedimiento consiste en utilizar el valor predeterminado de un parámetro, en lugar de un valor recuperado de la aplicación. Este valor solo es válido en un procedimiento al que se llama en la sintaxis canónica ODBC y, a continuación, solo si el argumento *InputOutputType* es SQL_PARAM_INPUT, SQL_PARAM_INPUT_OUTPUT o SQL_PARAM_INPUT_OUTPUT_STREAM. Cuando \*se *SQL_DEFAULT_PARAM StrLen_or_IndPtr,* los argumentos *ValueType*, *ParameterType*, *ColumnSize*, *DecimalDigits*, *BufferLength*y *ParameterValuePtr* se omiten para los parámetros de entrada y solo se utilizan para definir el valor del parámetro de salida para los parámetros de entrada/salida.  
  
-   El resultado de la macro SQL_LEN_DATA_AT_EXEC(*length*). Los datos del parámetro se enviarán con **SQLPutData**. Si el *ParameterType* argumento es SQL_LONGVARBINARY, SQL_LONGVARCHAR, o un largo, tipo de datos específico del origen de datos y el controlador devuelve "Y" para el tipo de información SQL_NEED_LONG_DATA_LEN en **SQLGetInfo**, *longitud* es el número de bytes de datos que se enviarán para el parámetro; de lo contrario, *la longitud* debe ser un valor no negativo y se omite. Para obtener más información, consulte "Pasar valores de parámetro", más adelante en esta sección.  
  
     Por ejemplo, para especificar que se enviarán 10.000 bytes de datos con **SQLPutData** en una o varias llamadas, para un parámetro SQL_LONGVARCHAR, una aplicación establece **StrLen_or_IndPtr* en SQL_LEN_DATA_AT_EXEC(10000).  
  
-   SQL_DATA_AT_EXEC. Los datos del parámetro se enviarán con **SQLPutData**. Este valor lo usan las aplicaciones ODBC 1.0 cuando llaman a ODBC 3. *x* controladores. Para obtener más información, consulte "Pasar valores de parámetro", más adelante en esta sección.  
  
 Si *StrLen_or_IndPtr* es un puntero nulo, el controlador supone que todos los valores de parámetro de entrada no son NULL y que los datos binarios y caracteres terminan en null. Si *InputOutputType* es SQL_PARAM_OUTPUT o SQL_PARAM_OUTPUT_STREAM y *ParameterValuePtr* y *StrLen_or_IndPtr* son punteros nulos, el controlador descarta el valor de salida.  
  
> [!NOTE]  
>  Se desaconseja encarecidamente a los desarrolladores de aplicaciones que especifiquen un puntero nulo para *StrLen_or_IndPtr* cuando se SQL_C_BINARY el tipo de datos del parámetro. Para asegurarse de que un controlador no trunca inesperadamente SQL_C_BINARY datos, *StrLen_or_IndPtr* debe contener un puntero a un valor de longitud válido.  
  
 Si el *InputOutputType* argumento es SQL_PARAM_INPUT_OUTPUT, SQL_PARAM_OUTPUT, SQL_PARAM_INPUT_OUTPUT_STREAM o SQL_PARAM_OUTPUT_STREAM, *StrLen_or_IndPtr* apunta a un búfer en \*el que el controlador devuelve SQL_NULL_DATA, no se puede determinar el número de bytes disponibles para devolver en *ParameterValuePtr* (excluyendo el byte de terminación nula de datos de caracteres) o SQL_NO_TOTAL (si no se puede determinar el número de bytes disponibles para devolver). Si el procedimiento devuelve uno o varios conjuntos de resultados, no se garantiza que el búfer de*StrLen_or_IndPtr* * se establezca hasta que se hayan capturado todos los resultados.  
  
 Si el valor del atributo de instrucción SQL_ATTR_PARAMSET_SIZE es mayor que 1, *StrLen_or_IndPtr* puntos a una matriz de valores SQLLEN. Estos pueden ser cualquiera de los valores enumerados anteriormente en esta sección y se procesan con una sola instrucción SQL.  
  
## <a name="passing-parameter-values"></a>Pasar valores de parámetros

 Una aplicación puede pasar el valor \*de un parámetro en el búfer *ParameterValuePtr* o con una o varias llamadas a **SQLPutData**. Los parámetros cuyos datos se pasan con **SQLPutData** se conocen como parámetros *de datos en ejecución.* Normalmente se utilizan para enviar datos para SQL_LONGVARBINARY y parámetros SQL_LONGVARCHAR, y se pueden mezclar con otros parámetros.  
  
 Para pasar valores de parámetro, una aplicación realiza la siguiente secuencia de pasos:  
  
1.  Llama a **SQLBindParameter** para cada parámetro para enlazar búferes para el valor del parámetro (*ParameterValuePtr* argumento) y longitud/ indicador (*StrLen_or_IndPtr* argumento). Para los parámetros de datos en ejecución, *ParameterValuePtr* es un valor de puntero definido por la aplicación, como un número de parámetro o un puntero a datos. El valor se devolverá más adelante y se puede utilizar para identificar el parámetro.  
  
2.  Coloca valores para los parámetros \*de entrada y entrada/salida en los búferes *ParameterValuePtr* y **StrLen_or_IndPtr:*  
  
    -   Para los parámetros normales, la \*aplicación coloca el valor del parámetro en el *parameterValuePtr* búfer y la longitud de ese valor en el **StrLen_or_IndPtr* búfer. Para obtener más información, consulte Configuración de valores de [parámetros](../../../odbc/reference/develop-app/setting-parameter-values.md).  
  
    -   Para los parámetros de datos en ejecución, la aplicación coloca el resultado de la macro SQL_LEN_DATA_AT_EXEC(*length*) (cuando se llama a un controlador ODBC 2.0) en el búfer de*StrLen_or_IndPtr* *.  
  
3.  Llama a **SQLExecute** o **SQLExecDirect** para ejecutar la instrucción SQL.  
  
    -   Si no hay parámetros de datos en ejecución, el proceso se ha completado.  
  
    -   Si hay parámetros de datos en ejecución, la función devuelve SQL_NEED_DATA.  
  
4.  Llama a **SQLParamData** para recuperar el valor definido por la aplicación especificado en el *ParameterValuePtr* argumento de **SQLBindParameter** para el primer parámetro de datos en ejecución que se va a procesar. **SQLParamData** devuelve SQL_NEED_DATA.  
  
    > [!NOTE]  
    >  Aunque los parámetros de datos en ejecución se asemejan a las columnas de datos en ejecución, el valor devuelto por **SQLParamData** es diferente para cada una. Los parámetros de datos en ejecución son parámetros de una instrucción SQL para la que se enviarán datos con **SQLPutData** cuando la instrucción se ejecute con **SQLExecDirect** o **SQLExecute**. Están enlazados con **SQLBindParameter**. El valor devuelto por **SQLParamData** es un valor de puntero pasado a **SQLBindParameter** en el *ParameterValuePtr* argumento. Las columnas de datos en ejecución son columnas de un conjunto de filas para el que se enviarán datos con **SQLPutData** cuando se actualice o agregue una fila con **SQLBulkOperations** o se actualice con **SQLSetPos**. Están enlazados con **SQLBindCol**. El valor devuelto por **SQLParamData** es la dirección de la fila en el **TargetValuePtr* búfer (establecido por una llamada a **SQLBindCol**) que se está procesando.  
  
5.  Llama a **SQLPutData** una o varias veces para enviar datos para el parámetro. Se necesita más de una llamada si \*el valor de datos es mayor que el *ParameterValuePtr* búfer especificado en **SQLPutData**; Se permiten varias llamadas a **SQLPutData** para el mismo parámetro solo cuando se envían datos de caracteres C a una columna con un tipo de datos específico de carácter, binario o origen de datos o al enviar datos c binarios a una columna con un tipo de datos de carácter, binario o específico del origen de datos.  
  
6.  Llama a **SQLParamData** de nuevo para indicar que se han enviado todos los datos para el parámetro.  
  
    -   Si hay más parámetros de datos en ejecución, **SQLParamData** devuelve SQL_NEED_DATA y el valor definido por la aplicación para el siguiente parámetro de datos en ejecución que se va a procesar. La aplicación repite los pasos 4 y 5.  
  
    -   Si no hay más parámetros de datos en ejecución, el proceso se ha completado. Si la instrucción se ejecutó correctamente, **SQLParamData** devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO; si se produce un error en la ejecución, devuelve SQL_ERROR. En este momento, **SQLParamData** puede devolver cualquier SQLSTATE que pueda devolver la función que se utiliza para ejecutar la instrucción (**SQLExecDirect** o **SQLExecute**).  
  
         Los valores de salida para cualquier parámetro \*de entrada/salida o salida están disponibles en los búferes *ParameterValuePtr* y **StrLen_or_IndPtr* después de que la aplicación recupere todos los conjuntos de resultados generados por la instrucción.  
  
 Llamar a **SQLExecute** o **SQLExecDirect** coloca la instrucción en un estado SQL_NEED_DATA. En este momento, la aplicación solo puede llamar a **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions**, **SQLParamData**o **SQLPutData** con la instrucción o el identificador de *conexión* asociado a la instrucción. Si llama a cualquier otra función con la instrucción o la conexión asociada a la instrucción, la función devuelve SQLSTATE HY010 (error de secuencia de funciones). La instrucción deja el estado SQL_NEED_DATA cuando **SQLParamData** o **SQLPutData** devuelve un error, **SQLParamData** devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO o se cancela la instrucción.  
  
 Si la aplicación llama a **SQLCancel** mientras el controlador todavía necesita datos para los parámetros de datos en ejecución, el controlador cancela la ejecución de instrucciones; la aplicación puede llamar a **SQLExecute** o **SQLExecDirect** de nuevo.  
  
## <a name="retrieving-streamed-output-parameters"></a>Recuperación de parámetros de salida transmitidos

 Cuando una aplicación establece *InputOutputType* en SQL_PARAM_INPUT_OUTPUT_STREAM o SQL_PARAM_OUTPUT_STREAM, el valor del parámetro de salida debe recuperarse mediante una o varias llamadas a **SQLGetData**. Cuando el controlador tiene un valor de parámetro de salida transmitido para volver a la aplicación, devolverá SQL_PARAM_DATA_AVAILABLE en respuesta a una llamada a las funciones siguientes: **SQLMoreResults**, **SQLExecute**y **SQLExecDirect**. Una aplicación llama a **SQLParamData** para determinar qué valor de parámetro está disponible.  
  
 Para obtener más información acerca de SQL_PARAM_DATA_AVAILABLE y parámetros de salida transmitidos, vea Recuperar parámetros de [salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="using-arrays-of-parameters"></a>Utilizar matrices de parámetros

 Cuando una aplicación prepara una instrucción con marcadores de parámetro y pasa una matriz de parámetros, hay dos maneras diferentes de ejecutar esto. Una forma es que el controlador se base en las capacidades de procesamiento de matrices del back-end, en cuyo caso toda la instrucción con la matriz de parámetros se trata como una unidad atómica. Oracle es un ejemplo de un origen de datos que admite capacidades de procesamiento de matrices. Otra forma de implementar esta característica es que el controlador genere un lote de instrucciones SQL, una instrucción SQL para cada conjunto de parámetros de la matriz de parámetros y ejecute el lote. Las matrices de parámetros no se pueden utilizar con una instrucción **UPDATE WHERE CURRENT OF.**  
  
 Cuando se procesa una matriz de parámetros, los conjuntos de resultados individuales/recuentos de filas (uno para cada conjunto de parámetros) pueden estar disponibles o los recuentos de conjuntos de resultados/filas se pueden acumular en uno. La opción SQL_PARAM_ARRAY_ROW_COUNTS de **SQLGetInfo** indica si los recuentos de filas están disponibles para cada conjunto de parámetros (SQL_PARC_BATCH) o solo un recuento de filas está disponible (SQL_PARC_NO_BATCH).  
  
 La opción SQL_PARAM_ARRAY_SELECTS de **SQLGetInfo** indica si un conjunto de resultados está disponible para cada conjunto de parámetros (SQL_PAS_BATCH) o solo un conjunto de resultados está disponible (SQL_PAS_NO_BATCH). Si el controlador no permite que se ejecute una instrucción de generación de conjuntos de resultados con una matriz de parámetros, SQL_PARAM_ARRAY_SELECTS devuelve SQL_PAS_NO_SELECT.  
  
 Para obtener más información, vea [Función SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
 Para admitir matrices de parámetros, el atributo de instrucción SQL_ATTR_PARAMSET_SIZE se establece para especificar el número de valores para cada parámetro. Si el campo es mayor que 1, los campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR y SQL_DESC_OCTET_LENGTH_PTR del APD deben apuntar a matrices. La cardinalidad de cada matriz es igual al valor de SQL_ATTR_PARAMSET_SIZE.  
  
 El campo SQL_DESC_ROWS_PROCESSED_PTR del APD apunta a un búfer que contiene el número de conjuntos de parámetros que se han procesado, incluidos los conjuntos de errores. A medida que se procesa cada conjunto de parámetros, el controlador almacena un nuevo valor en el búfer. No se devolverá ningún número si se trata de un puntero nulo. Cuando se utilizan matrices de parámetros, el valor señalado por el campo SQL_DESC_ROWS_PROCESSED_PTR del APD se rellena incluso si la función de configuración devuelve SQL_ERROR. Si se devuelve SQL_NEED_DATA, el valor al que apunta el campo SQL_DESC_ROWS_PROCESSED_PTR del APD se establece en el conjunto de parámetros que se está procesando.  
  
 Lo que ocurre cuando se enlaza una matriz de parámetros y se ejecuta una instrucción **UPDATE WHERE CURRENT OF** está definida por el controlador.  
  
## <a name="column-wise-parameter-binding"></a>Encuadernación de parámetros de columna

 En el enlace de columna, la aplicación enlaza matrices de parámetros y longitud/indicador independientes a cada parámetro.  
  
 Para usar el enlace de columna, la aplicación establece primero el atributo de instrucción SQL_ATTR_PARAM_BIND_TYPE en SQL_PARAM_BIND_BY_COLUMN. (Este es el valor predeterminado.) Para cada columna que se va a enlazar, la aplicación realiza los pasos siguientes:  
  
1.  Asigna una matriz de búfer de parámetros.  
  
2.  Asigna una matriz de búferes de longitud/indicador.  
  
    > [!NOTE]  
    >  Si la aplicación escribe directamente en descriptores cuando se utiliza el enlace de columna, se pueden utilizar matrices independientes para los datos de longitud e indicador.  
  
3.  Llama a **SQLBindParameter** con los argumentos siguientes:  
  
    -   *ValueType* es el tipo C de un único elemento en la matriz de búfer de parámetros.  
  
    -   *ParameterType* es el tipo SQL del parámetro.  
  
    -   *ParameterValuePtr* es la dirección de la matriz de búfer de parámetros.  
  
    -   *BufferLength* es el tamaño de un único elemento en la matriz de búfer de parámetros. El *BufferLength* argumento se omite cuando los datos son datos de longitud fija.  
  
    -   *StrLen_or_IndPtr* es la dirección de la matriz de longitud/indicador.  
  
 Para obtener más información acerca de cómo se usa esta información, vea "ParameterValuePtr Argument" en "Comentarios", más adelante en esta sección. Para obtener más información sobre el enlace de parámetros en columna, vea [Binding Arrays of Parameters](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md).  
  
## <a name="row-wise-parameter-binding"></a>Enlace de parámetros Row-Wise

 En el enlace de fila, la aplicación define una estructura que contiene búferes de parámetro y longitud/indicador para cada parámetro que se va a enlazar.  
  
 Para usar el enlace de fila, la aplicación realiza los pasos siguientes:  
  
1.  Define una estructura para contener un único conjunto de parámetros (incluidos los búferes de parámetros y de longitud/indicador) y asigna una matriz de estas estructuras.  
  
    > [!NOTE]  
    >  Si la aplicación escribe directamente en descriptores cuando se utiliza el enlace de fila, se pueden utilizar campos independientes para los datos de longitud e indicador.  
  
2.  Establece el atributo de instrucción SQL_ATTR_PARAM_BIND_TYPE en el tamaño de la estructura que contiene un único conjunto de parámetros o en el tamaño de una instancia de un búfer en el que se enlazarán los parámetros. La longitud debe incluir espacio para todos los parámetros enlazados y cualquier relleno de la estructura o búfer, para asegurarse de que cuando la dirección de un parámetro enlazado se incrementa con la longitud especificada, el resultado apuntará al principio del mismo parámetro en la fila siguiente. Cuando se utiliza el operador *sizeof* en ANSI C, se garantiza este comportamiento.  
  
3.  Llama a **SQLBindParameter** con los argumentos siguientes para cada parámetro que se va a enlazar:  
  
    -   *ValueType* es el tipo del miembro de búfer de parámetro que se va a enlazar a la columna.  
  
    -   *ParameterType* es el tipo SQL del parámetro.  
  
    -   *ParameterValuePtr* es la dirección del miembro de búfer de parámetro en el primer elemento de matriz.  
  
    -   *BufferLength* es el tamaño del miembro de búfer de parámetros.  
  
    -   *StrLen_or_IndPtr* es la dirección del miembro de la longitud/indicador que se va a enlazar.  
  
 Para obtener más información acerca de cómo se usa esta información, vea "*ParameterValuePtr* Argument," más adelante en esta sección. Para obtener más información sobre el enlace de parámetros en cuanto a filas, vea [las matrices de parámetros de enlace](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md).  
  
## <a name="error-information"></a>Información del error

 Si un controlador no implementa matrices de parámetros como lotes (la opción SQL_PARAM_ARRAY_ROW_COUNTS es igual a SQL_PARC_NO_BATCH), las situaciones de error se controlan como si se ejecutara una instrucción. Si el controlador implementa matrices de parámetros como lotes, una aplicación puede usar el campo de encabezado SQL_DESC_ARRAY_STATUS_PTR de la IPD para determinar qué parámetro de una instrucción SQL o qué parámetro de una matriz de parámetros provocó **SQLExecDirect** o **SQLExecute** para devolver un error. Este campo contiene información de estado para cada fila de valores de parámetro. Si el campo indica que se ha producido un error, los campos de la estructura de datos de diagnóstico indicarán la fila y el número de parámetro del parámetro que ha fallado. El número de elementos de la matriz se definirá mediante el campo de encabezado SQL_DESC_ARRAY_SIZE en el APD, que se puede establecer mediante el atributo de instrucción SQL_ATTR_PARAMSET_SIZE.  
  
> [!NOTE]  
>  El campo de encabezado SQL_DESC_ARRAY_STATUS_PTR en el APD se utiliza para ignorar los parámetros. Para obtener más información sobre cómo ignorar parámetros, consulte la siguiente sección, "Ignorar un conjunto de parámetros."  
  
 Cuando **SQLExecute** o **SQLExecDirect** devuelve SQL_ERROR, los elementos de la matriz a la que apunta el campo SQL_DESC_ARRAY_STATUS_PTR de la IPD contendrán SQL_PARAM_ERROR, SQL_PARAM_SUCCESS, SQL_PARAM_SUCCESS_WITH_INFO, SQL_PARAM_UNUSED o SQL_PARAM_DIAG_UNAVAILABLE.  
  
 Para cada elemento de esta matriz, la estructura de datos de diagnóstico contiene uno o varios registros de estado. El campo SQL_DIAG_ROW_NUMBER de la estructura indica el número de fila de los valores de parámetro que causaron el error. Si es posible determinar el parámetro concreto en una fila de parámetros que causó el error, el número de parámetro se introducirá en el campo SQL_DIAG_COLUMN_NUMBER.  
  
 SQL_PARAM_UNUSED se especifica cuando no se ha utilizado un parámetro porque se ha producido un error en un parámetro anterior que obligó a **SQLExecute** o **SQLExecDirect** a anular. Por ejemplo, si hay 50 parámetros y se ha producido un error al ejecutar el conjunto de parámetros tenrigésimo de parámetros que provocó la anulación de **SQLExecute** o **SQLExecDirect,** se especifica SQL_PARAM_UNUSED en la matriz de estado de los parámetros 41 a 50.  
  
 SQL_PARAM_DIAG_UNAVAILABLE se introduce cuando el controlador trata matrices de parámetros como una unidad monolítica, por lo que no genera este nivel de parámetro individual de información de error.  
  
 Algunos errores en el procesamiento de un único conjunto de parámetros hacen que se detenga el procesamiento de los conjuntos posteriores de parámetros de la matriz. Otros errores no afectan al procesamiento de parámetros posteriores. Los errores que detendrán el procesamiento están definidos por el controlador. Si no se detiene el procesamiento, se procesan todos los parámetros de la matriz, SQL_SUCCESS_WITH_INFO se devuelve como resultado del error y el búfer definido por SQL_ATTR_PARAMS_PROCESSED_PTR se establece en el número total de conjuntos de parámetros procesados (según lo definido por el atributo de instrucción SQL_ATTR_PARAMSET_SIZE), que incluye conjuntos de errores.  
  
> [!CAUTION]  
>  El comportamiento de ODBC cuando se produce un error en el procesamiento de una matriz de parámetros es diferente en ODBC 3. *x* que en ODBC 2. *x*. En ODBC 2. *x*, la función devuelta SQL_ERROR y el procesamiento cesó. El búfer al que apunta el argumento *pirow* de **SQLParamOptions** contenía el número de la fila de error. En ODBC 3. *x*, la función devuelve SQL_SUCCESS_WITH_INFO y el procesamiento puede detenerse o continuar. Si continúa, el búfer especificado por SQL_ATTR_PARAMS_PROCESSED_PTR se establecerá en el valor de todos los parámetros procesados, incluidos los que dieron lugar a un error. Este cambio de comportamiento puede causar problemas para las aplicaciones existentes.  
  
 Cuando **SQLExecute** o **SQLExecDirect** devuelve antes de completar el procesamiento de todos los conjuntos de parámetros de una matriz de parámetros, como cuando se devuelve SQL_ERROR o SQL_NEED_DATA, la matriz de estado contiene estados para los parámetros que ya se han procesado. La ubicación señalada por el campo SQL_DESC_ROWS_PROCESSED_PTR en el IPD contiene el número de fila en la matriz de parámetros que causó el SQL_ERROR o SQL_NEED_DATA código de error. Cuando se envía una matriz de parámetros a una instrucción SELECT, la disponibilidad de los valores de matriz de estado está definida por el controlador; pueden estar disponibles después de que se haya ejecutado la instrucción o como se capturan los conjuntos de resultados.  
  
## <a name="ignoring-a-set-of-parameters"></a>Ignorar un conjunto de parámetros

 El campo SQL_DESC_ARRAY_STATUS_PTR de la APD (según lo establecido por el atributo de instrucción SQL_ATTR_PARAM_STATUS_PTR) se puede utilizar para indicar que se debe omitir un conjunto de parámetros enlazados en una instrucción SQL. Para hacer que el controlador ignore uno o más conjuntos de parámetros durante la ejecución, una aplicación debe seguir estos pasos:  
  
1.  Llame a **SQLSetDescField** para establecer el campo de encabezado SQL_DESC_ARRAY_STATUS_PTR de la APD para que apunte a una matriz de SQLUSMALLINT valores para contener información de estado. Este campo también se puede establecer mediante una llamada a **SQLSetStmtAttr** con un *atributo* de SQL_ATTR_PARAM_OPERATION_PTR, que permite a una aplicación establecer el campo sin obtener un identificador de descriptor.  
  
2.  Establezca cada elemento de la matriz definido por el campo SQL_DESC_ARRAY_STATUS_PTR del APD en uno de los dos valores:  
  
    -   SQL_PARAM_IGNORE, para indicar que la fila se excluye de la ejecución de la instrucción.  
  
    -   SQL_PARAM_PROCEED, para indicar que la fila se incluye en la ejecución de la instrucción.  
  
3.  Llame a **SQLExecDirect** o **SQLExecute** para ejecutar la instrucción preparada.  
  
 Las siguientes reglas se aplican a la matriz definida por el campo SQL_DESC_ARRAY_STATUS_PTR del APD:  
  
-   El puntero se establece en null de forma predeterminada.  
  
-   Si el puntero es null, se utilizan todos los conjuntos de parámetros, como si todos los elementos estuvieran establecidos en SQL_ROW_PROCEED.  
  
-   Establecer un elemento en SQL_PARAM_PROCEED no garantiza que la operación utilizará ese conjunto determinado de parámetros.  
  
-   SQL_PARAM_PROCEED se define como 0 en el archivo de encabezado.  
  
 Una aplicación puede establecer el campo de SQL_DESC_ARRAY_STATUS_PTR en el APD para que apunte a la misma matriz que la señalada por el campo SQL_DESC_ARRAY_STATUS_PTR en el IRD. Esto es útil cuando se enlazan parámetros a datos de fila. Los parámetros se pueden ignorar según el estado de los datos de fila. Además de SQL_PARAM_IGNORE, los códigos siguientes hacen que se omita un parámetro de una instrucción SQL: SQL_ROW_DELETED, SQL_ROW_UPDATED y SQL_ROW_ERROR. Además de SQL_PARAM_PROCEED, los códigos siguientes hacen que una instrucción SQL continúe: SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO y SQL_ROW_ADDED.  
  
## <a name="rebinding-parameters"></a>Parámetros de reenlace

 Una aplicación puede realizar cualquiera de las dos operaciones para cambiar un enlace:  
  
-   Llame a **SQLBindParameter** para especificar un nuevo enlace para una columna que ya está enlazada. El controlador sobrescribe el enlace antiguo con el nuevo.  
  
-   Especifique un desplazamiento que se agregará a la dirección de búfer especificada por la llamada de enlace a **SQLBindParameter**. Para obtener más información, consulte la siguiente sección, "Reenlace con desfases."  
  
## <a name="rebinding-with-offsets"></a>Revinculación con desfases

 El reenlace de parámetros es especialmente útil cuando una aplicación tiene una configuración de área de búfer que puede contener muchos parámetros, pero una llamada a **SQLExecDirect** o **SQLExecute** utiliza solo algunos de los parámetros. El espacio restante en el área de búfer se puede utilizar para el siguiente conjunto de parámetros modificando el enlace existente mediante un desplazamiento.  
  
 El campo de encabezado SQL_DESC_BIND_OFFSET_PTR en el APD apunta al desplazamiento de enlace. Si el campo no es null, el controlador desreferencia el puntero y, si ninguno de los valores de los campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR y SQL_DESC_OCTET_LENGTH_PTR es un puntero nulo, agrega el valor desreferenciado a esos campos en los registros descriptores en tiempo de ejecución. Los nuevos valores de puntero se utilizan cuando se ejecutan las instrucciones SQL. El desplazamiento sigue siendo válido después de volver a enlazar. Dado que SQL_DESC_BIND_OFFSET_PTR es un puntero al desplazamiento en lugar del propio desplazamiento, una aplicación puede cambiar el desplazamiento directamente, sin tener que llamar a [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) o [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md) para cambiar el campo descriptor. El puntero se establece en null de forma predeterminada. El SQL_DESC_BIND_OFFSET_PTR campo de la ARD se puede establecer mediante una llamada a [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) o mediante una llamada a [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)con un *fAttribute* de SQL_ATTR_PARAM_BIND_OFFSET_PTR.  
  
 El desplazamiento de enlace siempre se agrega directamente a los valores de los campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR y SQL_DESC_OCTET_LENGTH_PTR. Si el desplazamiento se cambia a un valor diferente, el nuevo valor se sigue agregando directamente al valor en cada campo descriptor. El nuevo desplazamiento no se agrega a la suma del valor del campo y de los desfases anteriores.  
  
## <a name="descriptors"></a>Descriptores de

 La forma en que se enlaza un parámetro viene determinada por los campos de los AD y los IPD. Los argumentos de **SQLBindParameter** se utilizan para establecer esos campos descriptores. Los campos también se pueden establecer mediante las **funciones SQLSetDescField,** aunque **SQLBindParameter** es más eficaz de usar porque la aplicación no tiene que obtener un identificador de descriptor para llamar a **SQLBindParameter**.  
  
> [!CAUTION]  
>  Llamar a **SQLBindParameter** para una instrucción puede afectar a otras instrucciones. Esto ocurre cuando el ARD asociado a la instrucción se asigna explícitamente y también está asociado con otras instrucciones. Dado que **SQLBindParameter** modifica los campos de la APD, las modificaciones se aplican a todas las instrucciones con las que está asociado este descriptor. Si este no es el comportamiento necesario, la aplicación debe disociar este descriptor de las otras instrucciones antes de llamar a **SQLBindParameter**.  
  
 Conceptualmente, **SQLBindParameter** realiza los pasos siguientes en secuencia:  
  
1.  Llama a [SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) para obtener el identificador de APD.  
  
2.  Llama a [SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) para obtener el campo de SQL_DESC_COUNT de APD y si el valor del argumento *ColumnNumber* supera el valor de SQL_DESC_COUNT, llama a **SQLSetDescField** para aumentar el valor de SQL_DESC_COUNT a *ColumnNumber*.  
  
3.  Llama a [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) varias veces para asignar valores a los siguientes campos del APD:  
  
    -   Establece SQL_DESC_TYPE y SQL_DESC_CONCISE_TYPE en el valor de *ValueType*, excepto que si *ValueType* es uno de los identificadores concisos de un subtipo datetime o interval, establece SQL_DESC_TYPE en SQL_DATETIME o SQL_INTERVAL, respectivamente, establece SQL_DESC_CONCISE_TYPE en el identificador conciso y establece SQL_DESC_DATETIME_INTERVAL_CODE en el subcódigo datetime o intervalo correspondiente.  
  
    -   Establece el campo SQL_DESC_OCTET_LENGTH en el valor de *BufferLength*.  
  
    -   Establece el campo SQL_DESC_DATA_PTR en el valor de *ParameterValue*.  
  
    -   Establece el campo SQL_DESC_OCTET_LENGTH_PTR en el valor de *StrLen_or_Ind*.  
  
    -   Establece el campo SQL_DESC_INDICATOR_PTR también en el valor de *StrLen_or_Ind*.  
  
     El parámetro *StrLen_or_Ind* especifica tanto la información del indicador como la longitud del valor del parámetro.  
  
4.  Llama a [SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) para obtener el identificador IPD.  
  
5.  Llama a [SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) para obtener el campo SQL_DESC_COUNT de IPD y, si el valor del argumento *ColumnNumber* supera el valor de SQL_DESC_COUNT, llama a **SQLSetDescField** para aumentar el valor de SQL_DESC_COUNT a *ColumnNumber*.  
  
6.  Llama a [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) varias veces para asignar valores a los siguientes campos de la IPD:  
  
    -   Establece SQL_DESC_TYPE y SQL_DESC_CONCISE_TYPE en el valor de *ParameterType*, excepto que si *ParameterType* es uno de los identificadores concisos de un subtipo datetime o interval, establece SQL_DESC_TYPE en SQL_DATETIME o SQL_INTERVAL, respectivamente, establece SQL_DESC_CONCISE_TYPE en el identificador conciso y establece SQL_DESC_DATETIME_INTERVAL_CODE en el subcódigo datetime o interval correspondiente.  
  
    -   Establece uno o varios de SQL_DESC_LENGTH, SQL_DESC_PRECISION y SQL_DESC_DATETIME_INTERVAL_PRECISION, según corresponda para *ParameterType*.  
  
    -   Establece SQL_DESC_SCALE en el valor de *DecimalDigits*.  
  
 Si se produce un error en la llamada a **SQLBindParameter,** el contenido de los campos descriptores que habría establecido en el APD son indefinidos y el campo SQL_DESC_COUNT del APD no cambia. Además, los campos SQL_DESC_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE y SQL_DESC_TYPE del registro adecuado en el IPD son indefinidos y el campo SQL_DESC_COUNT de la IPD no cambia.  
  
## <a name="conversion-of-calls-to-and-from-sqlsetparam"></a>Conversión de llamadas a y desde SQLSetParam

 Cuando una aplicación ODBC 1.0 llama a **SQLSetParam** en un ODBC 3. *x* controlador, el ODBC 3. *x* El Administrador de controladores asigna la llamada como se muestra en la tabla siguiente.  
  
|Llamada por aplicación ODBC 1.0|Llamada a ODBC 3. *x* conductor|  
|----------------------------------|-------------------------------|  
|SQLSetParam( StatementHandle, ParameterNumber, ValueType, ParameterType, LengthPrecision, ParameterScale, ParameterValuePtr, StrLen_or_IndPtr);|SQLBindParameter( StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, *ColumnSize*, *DecimalDigits*, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX, StrLen_or_IndPtr);|  
  
## <a name="code-example"></a>Ejemplo de código  
 En el ejemplo siguiente, una aplicación prepara una instrucción SQL para insertar datos en la tabla ORDERS. Para cada parámetro de la instrucción, la aplicación llama a **SQLBindParameter** para especificar el tipo de datos ODBC C y el tipo de datos SQL del parámetro y para enlazar un búfer a cada parámetro. Para cada fila de datos, la aplicación asigna valores de datos a cada parámetro y llama a **SQLExecute** para ejecutar la instrucción.  
  
 En el ejemplo siguiente se supone que tiene un origen de datos ODBC en el equipo denominado Northwind que está asociado a la base de datos Northwind.  
  
 Para obtener más ejemplos de código, vea [SQLBulkOperations (Función),](../../../odbc/reference/syntax/sqlbulkoperations-function.md) [SQLProcedures (Función)](../../../odbc/reference/syntax/sqlprocedures-function.md), [SQLPutData (Función)](../../../odbc/reference/syntax/sqlputdata-function.md)y [SQLSetPos (Función) y SQLSetPos (Función).](../../../odbc/reference/syntax/sqlsetpos-function.md)  
  
```cpp
// SQLBindParameter_Function.cpp  
// compile with: ODBC32.lib  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
#define EMPLOYEE_ID_LEN 10  
  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLRETURN retcode;  
SQLHSTMT hstmt = NULL;  
SQLSMALLINT sCustID;  
  
SQLCHAR szEmployeeID[EMPLOYEE_ID_LEN];  
SQL_DATE_STRUCT dsOrderDate;  
SQLINTEGER cbCustID = 0, cbOrderDate = 0, cbEmployeeID = SQL_NTS;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retcode = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, EMPLOYEE_ID_LEN, 0, szEmployeeID, 0, &cbEmployeeID);  
   retcode = SQLBindParameter(hstmt, 2, SQL_PARAM_INPUT, SQL_C_SSHORT, SQL_INTEGER, 0, 0, &sCustID, 0, &cbCustID);  
   retcode = SQLBindParameter(hstmt, 3, SQL_PARAM_INPUT, SQL_C_TYPE_DATE, SQL_TIMESTAMP, sizeof(dsOrderDate), 0, &dsOrderDate, 0, &cbOrderDate);  
  
   retcode = SQLPrepare(hstmt, (SQLCHAR*)"INSERT INTO Orders(CustomerID, EmployeeID, OrderDate) VALUES (?, ?, ?)", SQL_NTS);  
  
   strcpy_s((char*)szEmployeeID, _countof(szEmployeeID), "BERGS");  
   sCustID = 5;  
   dsOrderDate.year = 2006;  
   dsOrderDate.month = 3;  
   dsOrderDate.day = 17;  
  
   retcode = SQLExecute(hstmt);  
}  
```  
  
## <a name="code-example"></a>Ejemplo de código

 En el ejemplo siguiente, una aplicación ejecuta un procedimiento almacenado de SQL Server mediante un parámetro con nombre.  
  
```cpp
// SQLBindParameter_Function_2.cpp  
// compile with: ODBC32.lib  
// sample assumes the following stored procedure:  
// use northwind  
// DROP PROCEDURE SQLBindParameter  
// GO  
//   
// CREATE PROCEDURE SQLBindParameter @quote int  
// AS  
// delete from orders where OrderID >= @quote  
// GO  
#include <windows.h>  
#include <sqltypes.h>  
#include <sqlext.h>  
  
SQLHDESC hIpd = NULL;  
SQLHENV henv = NULL;  
SQLHDBC hdbc = NULL;  
SQLRETURN retcode;  
SQLHSTMT hstmt = NULL;  
SQLCHAR szQuote[50] = "100084";  
SQLINTEGER cbValue = SQL_NTS;  
  
int main() {  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
   retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);   
   retcode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
   retcode = SQLConnect(hdbc, (SQLCHAR*) "Northwind", SQL_NTS, (SQLCHAR*) NULL, 0, NULL, 0);  
   retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   retcode = SQLPrepare(hstmt, (SQLCHAR*)"{call SQLBindParameter(?)}", SQL_NTS);  
   retcode = SQLBindParameter(hstmt, 1, SQL_PARAM_INPUT, SQL_C_CHAR, SQL_CHAR, 50, 0, szQuote, 0, &cbValue);  
   retcode = SQLGetStmtAttr(hstmt, SQL_ATTR_IMP_PARAM_DESC, &hIpd, 0, 0);  
   retcode = SQLSetDescField(hIpd, 1, SQL_DESC_NAME, "@quote", SQL_NTS);  
  
   retcode = SQLExecute(hstmt);  
}  
```  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Devolver información sobre un parámetro en una instrucción|[Función SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|Ejecución de una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecución de una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Liberación de búferes de parámetros en la instrucción|[Función SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Devolver el número de parámetros de la instrucción|[Función SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|Devolver el siguiente parámetro para enviar datos|[Función SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Especificar varios valores de parámetros|[Función SQLParamOptions](../../../odbc/reference/syntax/sqlparamoptions-function.md)|  
|Envío de datos de parámetros en tiempo de ejecución|[Función SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>Consulte también

 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
