---
title: Función SQLBindParameter | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 65f6145f0cbfbd59fffb71e030f6427ea1f551c0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68036207"
---
# <a name="sqlbindparameter-function"></a>Función SQLBindParameter

**Conformidad**  
 Versión de introducción: Cumplimiento de estándares 2.0 de ODBC: ODBC  
  
 **Resumen**  
 **SQLBindParameter** enlaza un búfer con un marcador de parámetro en una instrucción SQL. **SQLBindParameter** admite el enlace a un tipo de datos Unicode C, incluso si el controlador subyacente no admite datos Unicode.  
  
> [!NOTE]  
>  Esta función reemplaza la función ODBC 1.0 **SQLSetParam**. Para obtener más información, vea "Comentarios".  
  
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
 [Entrada] Número de parámetro, ordenados secuencialmente en orden creciente de los parámetros, empezando por 1.  
  
 *InputOutputType*  
 [Entrada] El tipo del parámetro. Para obtener más información, vea "*InputOutputType* argumento" en "Comentarios".  
  
 *ValueType*  
 [Entrada] El tipo de datos de C del parámetro. Para obtener más información, vea "*ValueType* argumento" en "Comentarios".  
  
 *ParameterType*  
 [Entrada] El tipo de datos SQL del parámetro. Para obtener más información, vea "*ParameterType* argumento" en "Comentarios".  
  
 *ColumnSize*  
 [Entrada] El tamaño de la columna o expresión de marcador de parámetro correspondiente. Para obtener más información, vea "*ColumnSize* argumento" en "Comentarios".  
  
 Si la aplicación se ejecutará en un sistema operativo de Windows de 64 bits, consulte [información ODBC 64-Bit](../../../odbc/reference/odbc-64-bit-information.md).  
  
 *DecimalDigits*  
 [Entrada] Los dígitos decimales de la columna o expresión de marcador de parámetro correspondiente. Para obtener más información sobre el tamaño de columna, vea [tamaño de la columna, dígitos decimales, transferir la longitud en octetos y tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
 *ParameterValuePtr*  
 [Entrada aplazada] Un puntero a un búfer para los datos del parámetro. Para obtener más información, vea "*ParameterValuePtr* argumento" en "Comentarios".  
  
 *BufferLength*  
 [Entrada/salida] Longitud de la *ParameterValuePtr* búfer en bytes. Para obtener más información, vea "*BufferLength* argumento" en "Comentarios".  
  
 Consulte [información ODBC 64-Bit](../../../odbc/reference/odbc-64-bit-information.md), si la aplicación se ejecutará en un sistema operativo de 64 bits.  
  
 *StrLen_or_IndPtr*  
 [Entrada aplazada] Un puntero a un búfer para la longitud del parámetro. Para obtener más información, vea "*StrLen_or_IndPtr* argumento" en "Comentarios".  
  
## <a name="returns"></a>Devuelve

 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico

 Cuando **SQLBindParameter** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLBindParameter** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  

|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07006|Infracción del atributo de tipo de datos restringido|El tipo de datos identificado por el *ValueType* argumento no se puede convertir al tipo de datos identificado por el *ParameterType* argumento. Tenga en cuenta que este error puede devolver **SQLExecDirect**, **SQLExecute**, o **SQLPutData** en tiempo de ejecución, en lugar de por **SQLBindParameter**.|  
|07009|Índice de descriptor no válido|(DM) el valor especificado para el argumento *ParameterNumber* era menor que 1.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el **MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar memoria que es necesario para admitir la ejecución o la finalización de la función.|  
|HY003|Tipo de búfer de aplicación no válido|El valor especificado por el argumento *ValueType* no era un tipo de datos válido de C o SQL_C_DEFAULT.|  
|HY004|Tipo de datos SQL no válido|El valor especificado para el argumento *ParameterType* no era un identificador de tipo de datos de ODBC SQL válido ni un identificador de tipo de datos SQL específicas del controlador admitida por el controlador.|  
|HY009|Valor de argumento no válido|(DM) el argumento *ParameterValuePtr* era un puntero nulo, el argumento *StrLen_or_IndPtr* era un puntero nulo y el argumento *InputOutputType* no era SQL_PARAM_ SALIDA.<br /><br /> SQL_PARAM_OUTPUT (DM), donde el argumento *ParameterValuePtr* era un puntero nulo, el tipo de C era el carácter o binario y el BufferLength (*cbValueMax*) era mayor que 0.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónica aún estaba ejecutando cuando **SQLBindParameter** llamó.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* y devuelven SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función que se ejecuta de forma asincrónica para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY021|Información de descriptor incoherente|La información del descriptor comprobar durante una comprobación de coherencia no era coherente. (Consulte la sección "Comprobaciones de coherencia" en **SQLSetDescField**.)<br /><br /> El valor especificado para el argumento *ColumnSize* estaba fuera del intervalo de valores admitidos por el origen de datos para una columna del tipo de datos SQL especificado por el *ParameterType* argumento.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el valor de *BufferLength* era menor que 0. (Vea la descripción del campo SQL_DESC_DATA_PTR en **SQLSetDescField**.)|  
|HY104|Valor de precisión o escala no válido|El valor especificado para el argumento *ColumnSize* o *ColumnSize* estaba fuera del intervalo de valores admitidos por el origen de datos para una columna del tipo de datos SQL especificado por el  *ParameterType* argumento.|  
|HY105|Tipo de parámetro no válido|(DM) el valor especificado para el argumento *InputOutputType* no era válido. (Vea "Comentarios".)|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|El controlador u origen de datos no admite la conversión especificada por la combinación del valor especificado para el argumento *ValueType* y el valor específico del controlador especificado para el argumento *ParameterType*.<br /><br /> El valor especificado para el argumento *ParameterType* era un identificador válido de tipo de datos de SQL de ODBC para la versión de ODBC compatibles con el controlador, pero no es compatible con el controlador u origen de datos.<br /><br /> El controlador admite solo ODBC 2. *x* y el argumento *ValueType* fue uno de los siguientes:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> y todos los tipos de datos de intervalo de C que aparecen en [tipos de datos C](../../../odbc/reference/appendixes/c-data-types.md) en el apéndice D: Tipos de datos.<br /><br /> El controlador sólo es compatible con versiones ODBC antes de 3,50 y el argumento *ValueType* era SQL_C_GUID.|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *StatementHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios

 Una aplicación llama a **SQLBindParameter** para enlazar cada marcador de parámetro en una instrucción SQL. Los enlaces permanecen activas hasta que la aplicación llama a **SQLBindParameter** llama de nuevo, **SQLFreeStmt** con la opción SQL_RESET_PARAMS o llamadas **SQLSetDescField** a Establezca el campo de encabezado SQL_DESC_COUNT del APD en 0.  
  
 Para obtener más información acerca de los parámetros, vea [parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md). Para obtener más información sobre los tipos de datos de parámetro y marcadores de parámetros, vea [tipos de datos de parámetro](../../../odbc/reference/appendixes/parameter-data-types.md) y [marcadores de parámetros](../../../odbc/reference/appendixes/parameter-markers.md) en el apéndice C: Gramática de SQL.  
  
## <a name="parameternumber-argument"></a>Argumento ParameterNumber  
 Si *ParameterNumber* en la llamada a **SQLBindParameter** es mayor que el valor de SQL_DESC_COUNT, **SQLSetDescField** se llama para aumentar el valor de SQL_DESC_ CONTAR al *ParameterNumber*.  
  
## <a name="inputoutputtype-argument"></a>Argumento InputOutputType  
 El *InputOutputType* argumento especifica el tipo del parámetro. Este argumento establece el campo SQL_DESC_PARAMETER_TYPE de la IPD. Todos los parámetros en instrucciones SQL que no llame a los procedimientos, como **insertar** son instrucciones, *entrada ** parámetros*. Parámetros en las llamadas a procedimiento pueden ser de entrada, entrada/salida o los parámetros de salida. (Una aplicación llama a **SQLProcedureColumns** para determinar el tipo de un parámetro en una llamada a procedimiento; se supone parámetros cuyo tipo no se puede determinar los parámetros de entrada.)  
  
 El *InputOutputType* argumento es uno de los valores siguientes:  
  
-   SQL_PARAM_INPUT. El parámetro marca un parámetro en una instrucción SQL que no llama a un procedimiento, como un **insertar** instrucción, o se marca un parámetro de entrada en un procedimiento. Por ejemplo, los parámetros de **INSERT INTO empleado VALUES (?,?,?)**  son parámetros de entrada, mientras que los parámetros de **{llamar AddEmp (?,?,?)}**  puede ser, pero no son necesariamente, parámetros de entrada.  
  
     Cuando se ejecuta la instrucción, el controlador envía los datos para el parámetro para el origen de datos el \* *ParameterValuePtr* búfer debe contener un valor de entrada válido, o el **StrLen_or_IndPtr* debe contener el búfer SQL_NULL_DATA, SQL_DATA_AT_EXEC o el resultado de la SQL_LEN_DATA_AT Macro _EXEC.  
  
     Si una aplicación no puede determinar el tipo de un parámetro en una llamada a procedimiento, establece *InputOutputType* a SQL_PARAM_INPUT; si el origen de datos devuelve un valor para el parámetro, el controlador lo descarta.  
  
-   SQL_PARAM_INPUT_OUTPUT. El parámetro marca un parámetro de entrada/salida en un procedimiento. Por ejemplo, el parámetro en **{llamar GetEmpDept(?)}**  es un parámetro de entrada y salida que acepta el nombre del empleado y devuelve el nombre del departamento del empleado.  
  
     Cuando se ejecuta la instrucción, el controlador envía los datos para el parámetro para el origen de datos el \* *ParameterValuePtr* búfer debe contener un valor de entrada válido, o el \* *StrLen_or_IndPtr* debe contener el búfer SQL_NULL_DATA, SQL_DATA_AT_EXEC o el resultado de la macro SQL_LEN_DATA_AT_EXEC. Después de ejecutar la instrucción, el controlador devuelve datos para el parámetro a la aplicación; Si el origen de datos no devuelve un valor para un parámetro de entrada/salida, el controlador establece el **StrLen_or_IndPtr* búfer en SQL_NULL_DATA.  
  
    > [!NOTE]  
    >  Cuando llama una aplicación ODBC 1.0 **SQLSetParam** en un controlador ODBC 2.0, el Administrador de controladores Esto convierte a una llamada a **SQLBindParameter** en el que el *InputOutputType* argumento está establecido en SQL_PARAM_INPUT_OUTPUT.  
  
-   SQL_PARAM_OUTPUT. El parámetro marca el valor devuelto de un procedimiento o un parámetro de salida en un procedimiento; en cualquier caso, estos se conocen como *parámetros de salida*. Por ejemplo, el parámetro en **{? = llamar GetNextEmpID}** es un parámetro de salida que devuelve el siguiente identificador de empleado.  
  
     Después de ejecutar la instrucción, el controlador devuelve datos para el parámetro a la aplicación, a menos que el *ParameterValuePtr* y *StrLen_or_IndPtr* argumentos son ambos punteros nulos, en cuyo caso el controlador descarta el valor de salida. Si el origen de datos no devuelve un valor para un parámetro de salida, el controlador establece el **StrLen_or_IndPtr* búfer en SQL_NULL_DATA.  
  
-   SQL_PARAM_INPUT_OUTPUT_STREAM. Indica que se debe transmitir un parámetro de entrada/salida. **SQLGetData** puede leer los valores de parámetro de elementos. *BufferLength* se omite porque la longitud del búfer se determinará de la llamada de **SQLGetData**. El valor de la *StrLen_or_IndPtr* búfer debe contener el resultado de la macro SQL_LEN_DATA_AT_EXEC, SQL_DATA_AT_EXEC, SQL_DEFAULT_PARAM o SQL_NULL_DATA. Un parámetro debe estar enlazado como un parámetro de datos en ejecución (DAE) en la entrada si se transmitirá al resultado. *ParameterValuePtr* puede ser cualquier valor de puntero no null que se devolverán por **SQLParamData** como definido por el usuario de token cuyo valor se ha pasado con *ParameterValuePtr* para entrada y salida. Para obtener más información, vea el tema que trata sobre [recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
-   SQL_PARAM_OUTPUT_STREAM. Igual que SQL_PARAM_INPUT_OUTPUT_STREAM, para un parámetro de salida. **StrLen_or_IndPtr* se omite en la entrada.  
  
 En la tabla siguiente se enumera combinaciones diferentes de *InputOutputType* y **StrLen_or_IndPtr*:  
  
|*InputOutputType*|**StrLen_or_IndPtr*|Resultado|Comentario en ParameterValuePtr|  
|-----------------------|----------------------------|-------------|---------------------------------|  
|SQL_PARAM_INPUT|SQL_LEN_DATA_AT_EXEC (*len*) o SQL_DATA_AT_EXEC|Entrada en partes|*ParameterValuePtr* puede ser cualquier valor de puntero que se devolverán por **SQLParamData** como definido por el usuario de token cuyo valor se ha pasado con *ParameterValuePtr*.|  
|SQL_PARAM_INPUT|No SQL_LEN_DATA_AT_EXEC (*len*) o SQL_DATA_AT_EXEC|Búfer de entrada puede enlazar|*ParameterValuePtr* es la dirección del búfer de entrada.|  
|SQL_PARAM_OUTPUT|Se omite en la entrada.|Búfer de salida enlazada|*ParameterValuePtr* es la dirección del búfer de salida.|  
|SQL_PARAM_OUTPUT_STREAM|Se omite en la entrada.|Salida transmitidos|*ParameterValuePtr* puede ser cualquier valor de puntero, que se devolverán por **SQLParamData** como definido por el usuario de token cuyo valor se ha pasado con *ParameterValuePtr*.|  
|SQL_PARAM_INPUT_OUTPUT|SQL_LEN_DATA_AT_EXEC (*len*) o SQL_DATA_AT_EXEC|Entrada en partes y búfer de salida enlazadas|*ParameterValuePtr* es la dirección del búfer de salida, que también se devolverán por **SQLParamData** como definido por el usuario de token cuyo valor se ha pasado con *ParameterValuePtr*.|  
|SQL_PARAM_INPUT_OUTPUT|No SQL_LEN_DATA_AT_EXEC (*len*) o SQL_DATA_AT_EXEC|Entrada enlazar el búfer y salida enlazada|*ParameterValuePtr* es la dirección del búfer de entrada/salida compartido.|
|SQL_PARAM_INPUT_OUTPUT_STREAM|SQL_LEN_DATA_AT_EXEC (*len*) o SQL_DATA_AT_EXEC|Entrada en partes y salida transmitidos|*ParameterValuePtr* puede ser cualquier valor de puntero no null, que se devolverán por **SQLParamData** como definido por el usuario de token cuyo valor se ha pasado con *ParameterValuePtr* de entrada y de salida.|  
  
> [!NOTE]  
>  El controlador debe decidir qué tipos SQL se permiten cuando una aplicación enlaza un parámetro de entrada y salida o de salida como transmitido. El Administrador de controladores no generará un error para un tipo SQL no válido.  
  
## <a name="valuetype-argument"></a>Argumento de tipo de valor

 El *ValueType* argumento especifica el tipo de datos de C del parámetro. Este argumento establece los campos SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE y SQL_DESC_DATETIME_INTERVAL_CODE del APD. Debe ser uno de los valores de la [tipos de datos C](../../../odbc/reference/appendixes/c-data-types.md) sección del apéndice D: Tipos de datos.  
  
 Si el *ValueType* argumento es uno de los tipos de datos de intervalo, el campo SQL_DESC_TYPE de la *ParameterNumber* registro de la APD está establecido en SQL_INTERVAL, el campo SQL_DESC_CONCISE_TYPE del APD se establece en el tipo de datos de intervalo concisa y el campo SQL_DESC_DATETIME_INTERVAL_CODE de la *ParameterNumber* registro está establecido en un subcódigo para el tipo de datos de un intervalo específico. (Consulte [apéndice D: Tipos de datos](../../../odbc/reference/appendixes/appendix-d-data-types.md).) El intervalo predeterminado iniciales precisión (2) y la precisión de segundos de intervalo predeterminado (6), como se establece en los campos SQL_DESC_DATETIME_INTERVAL_PRECISION y SQL_DESC_PRECISION del APD, respectivamente, se usan para los datos. Si la precisión predeterminada no es adecuada, la aplicación debe establecer explícitamente el campo descriptor mediante una llamada a **SQLSetDescField** o **SQLSetDescRec**.  
  
 Si el *ValueType* argumento es uno de los tipos de datos de fecha y hora, el campo SQL_DESC_TYPE de la *ParameterNumber* registro de la APD está establecido en SQL_DATETIME, el campo SQL_DESC_CONCISE_TYPE de la *ParameterNumber* registro de la APD se establece en el tipo de datos datetime concisa C y el campo SQL_DESC_DATETIME_INTERVAL_CODE de la *ParameterNumber* registro está establecido en un subcódigo para la fecha y hora específicas tipo de datos. (Consulte [apéndice D: Tipos de datos](../../../odbc/reference/appendixes/appendix-d-data-types.md).)  
  
 Si el *ValueType* argumento es un tipo de datos SQL_C_NUMERIC, la precisión predeterminada (que es definido por el controlador) y la escala predeterminada (0), como se establece en los campos SQL_DESC_PRECISION y SQL_DESC_SCALE del APD, se usan para los datos. Si el valor predeterminado de precisión o la escala no es adecuado, la aplicación debe establecer explícitamente el campo descriptor mediante una llamada a **SQLSetDescField** o **SQLSetDescRec**.  
  
 SQL_C_DEFAULT especifica que el valor del parámetro se transfieren desde el tipo de datos C predeterminado para el tipo de datos SQL especificado con *ParameterType*.  
  
 También puede especificar un tipo de datos C extendido. Para obtener más información, vea el tema sobre [tipos de datos C en ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 Para obtener más información, consulte [tipos de datos C predeterminado](../../../odbc/reference/appendixes/default-c-data-types.md), [convertir datos de C a tipos de datos SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md), y [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) en el apéndice D: Tipos de datos.  
  
## <a name="parametertype-argument"></a>Argumento ParameterType

 Esto debe ser uno de los valores enumerados en la [tipos de datos SQL](../../../odbc/reference/appendixes/sql-data-types.md) sección del apéndice D: Tipos de datos, o debe ser un valor específico del controlador. Este argumento establece los campos SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE y SQL_DESC_DATETIME_INTERVAL_CODE de la IPD.  
  
 Si el *ParameterType* argumento es uno de los identificadores de fecha y hora, el campo SQL_DESC_TYPE de la IPD es SQL_DATETIME, se establece el campo SQL_DESC_CONCISE_TYPE de la IPD para el tipo de datos SQL concisa y el SQL_DESC_ Campo DATETIME_INTERVAL_CODE se establece en el valor de subcódigo de datetime adecuado.  
  
 Si *ParameterType* es uno de los identificadores del intervalo, se establece el campo SQL_DESC_TYPE de la IPD para SQL_INTERVAL, el campo SQL_DESC_CONCISE_TYPE de la IPD se establece en el tipo de datos de intervalo SQL conciso y el SQL_DESC_DATETIME_ Campo INTERVAL_CODE de la IPD se establece en el subcódigo de intervalo apropiado. El campo SQL_DESC_DATETIME_INTERVAL_PRECISION de la IPD se establece en la precisión de intervalo inicial y el campo SQL_DESC_PRECISION se establece en la precisión de segundos del intervalo, si procede. Si el valor predeterminado de SQL_DESC_DATETIME_INTERVAL_PRECISION o SQL_DESC_PRECISION no es adecuado, la aplicación debe establecer explícitamente, mediante una llamada a **SQLSetDescField**. Para obtener más información acerca de cualquiera de estos campos, consulte [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 Si el *ValueType* argumento es un tipo de datos SQL_NUMERIC, la precisión predeterminada (que es definido por el controlador) y la escala predeterminada (0), como se establece en los campos SQL_DESC_PRECISION y SQL_DESC_SCALE de la IPD, se usan para los datos. Si el valor predeterminado de precisión o la escala no es adecuado, la aplicación debe establecer explícitamente el campo descriptor mediante una llamada a **SQLSetDescField** o **SQLSetDescRec**.  
  
 Para obtener información acerca de cómo se convierten los datos, vea [convertir datos de C a tipos de datos SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) y [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) en el apéndice D: Tipos de datos.  
  
## <a name="columnsize-argument"></a>Argumento ColumnSize

 El *ColumnSize* argumento especifica el tamaño de la columna o expresión que se corresponde con el marcador de parámetro, la longitud de datos, o ambos. Este argumento establece distintos campos de la IPD, según el tipo de datos SQL (el *ParameterType* argumento). Las siguientes reglas se aplican a esta asignación:  
  
-   Si *ParameterType* es SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY, o uno de los concisa datetime o intervalo de tipos de datos SQL, el campo SQL_DESC_LENGTH de la IPD está establecida en el valor de  *ColumnSize*. (Para obtener más información, consulte el [tamaño de la columna, dígitos decimales, transferir la longitud en octetos y tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) sección en el apéndice D: Tipos de datos).  
  
-   Si *ParameterType* es SQL_DECIMAL, SQL_NUMERIC, SQL_FLOAT, SQL_REAL o SQL_DOUBLE, el campo SQL_DESC_PRECISION de la IPD se establece en el valor de *ColumnSize*.  
  
-   Para otros tipos de datos, el *ColumnSize* argumento se omite.  
  
 Para obtener más información, vea "Pasar valores de parámetro" y SQL_DATA_AT_EXEC en "*StrLen_or_IndPtr* argumento."  
  
## <a name="decimaldigits-argument"></a>Argumento ColumnSize

 Si *ParameterType* es SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP, SQL_INTERVAL_SECOND, SQL_INTERVAL_DAY_TO_SECOND, SQL_INTERVAL_HOUR_TO_SECOND o SQL_INTERVAL_MINUTE_TO_SECOND, se establece el campo SQL_DESC_PRECISION de la IPD para *ColumnSize*. Si *ParameterType* es SQL_NUMERIC o SQL_DECIMAL, se establece el campo SQL_DESC_SCALE de la IPD *ColumnSize*. Para los demás tipos de datos, el *ColumnSize* argumento se omite.  
  
## <a name="parametervalueptr-argument"></a>Argumento ParameterValuePtr

 El *ParameterValuePtr* argumento apunta a un búfer que, cuando **SQLExecute** o **SQLExecDirect** se llama, que contiene los datos reales para el parámetro. Los datos deben estar en la forma especificada por el *ValueType* argumento. Este argumento establece el campo SQL_DESC_DATA_PTR del APD. Una aplicación puede establecer la *ParameterValuePtr* argumento a un puntero nulo, siempre y cuando  *\*StrLen_or_IndPtr* es a SQL_NULL_DATA o SQL_DATA_AT_EXEC. (Se aplica solo a entrada/salida parámetros de entrada o).  
  
 Si \* *StrLen_or_IndPtr* es el resultado de la SQL_LEN_DATA_AT_EXEC (*longitud*) macro o SQL_DATA_AT_EXEC, a continuación, *ParameterValuePtr* es un valor de puntero definido por la aplicación que está asociado con el parámetro. Se devuelve a la aplicación a través de **SQLParamData**. Por ejemplo, *ParameterValuePtr* podría ser un token distinto de cero como un número de parámetro, un puntero a datos o un puntero a una estructura que la aplicación se usa para enlazar parámetros de entrada. Sin embargo, tenga en cuenta que si el parámetro es un parámetro de entrada/salida, *ParameterValuePtr* debe ser un puntero a un búfer donde se almacenará el valor de salida. Si el valor del atributo de instrucción SQL_ATTR_PARAMSET_SIZE es mayor que 1, la aplicación puede usar el valor señalado por el atributo de instrucciones SQL_ATTR_PARAMS_PROCESSED_PTR junto con el *ParameterValuePtr* argumento. Por ejemplo, *ParameterValuePtr* puede señalar a una matriz de valores y la aplicación podría usar el valor señalado por SQL_ATTR_PARAMS_PROCESSED_PTR para recuperar el valor correcto de la matriz. Para obtener más información, vea "Pasar valores de parámetro" más adelante en esta sección.  
  
 Si el *InputOutputType* argumento es SQL_PARAM_INPUT_OUTPUT o SQL_PARAM_OUTPUT, *ParameterValuePtr* apunta a un búfer en el que el controlador devuelve el valor de salida. Si el procedimiento devuelve uno o varios conjuntos de resultados, el \* *ParameterValuePtr* no se garantiza que el búfer debe establecerse hasta que se han procesado todos los recuentos de fila/conjuntos de resultados. Si no se establece el búfer hasta que se complete el procesamiento, los parámetros de salida y valores devueltos no estarán disponibles hasta que **SQLMoreResults** devuelve SQL_NO_DATA. Una llamada a **SQLCloseCursor** o **SQLFreeStmt** con una opción de SQL_CLOSE hará que estos valores se descarten.  
  
 Si es mayor que 1, el valor del atributo de instrucción SQL_ATTR_PARAMSET_SIZE *ParameterValuePtr* señala a una matriz. Una única instrucción SQL procesa la matriz completa de los valores de entrada para un parámetro de entrada o de entrada/salida y devuelve una matriz de valores de salida para una entrada y salida o parámetro de salida.  
  
## <a name="bufferlength-argument"></a>Argumento BufferLength

 Para los datos de caracteres y binarios C, la *BufferLength* argumento especifica la longitud de la \* *ParameterValuePtr* búfer (si es un elemento único) o la longitud de un elemento en el \* *ParameterValuePtr* matriz (si el valor del atributo de instrucción SQL_ATTR_PARAMSET_SIZE es mayor que 1). Este argumento establece el campo de registro SQL_DESC_OCTET_LENGTH del APD. Si la aplicación especifica varios valores, *BufferLength* se usa para determinar la ubicación de los valores de la **ParameterValuePtr* de matriz, en la entrada y salida. Para los parámetros de entrada/salida y salidos, se usa para determinar si se debe truncar los datos de caracteres y binarios C en la salida:  
  
-   Para los datos de carácter C, si el número de bytes disponible para devolver es mayor o igual a *BufferLength*, los datos de \* *ParameterValuePtr* se trunca a  *BufferLength* menos la longitud de un carácter de terminación null y termina en null por el controlador.  
  
-   Para los datos binarios de C, si es mayor que el número de bytes disponible para devolver *BufferLength*, los datos de \* *ParameterValuePtr* se trunca a *BufferLength*bytes.  
  
 Para los demás tipos de datos de C, la *BufferLength* argumento se omite. La longitud de la \* *ParameterValuePtr* búfer (si es un elemento único) o la longitud de un elemento en el \* *ParameterValuePtr* (si la aplicación llama a dematriz **SQLSetStmtAttr** con un *atributo* argumento de SQL_ATTR_PARAMSET_SIZE para especificar varios valores para cada parámetro) se supone que la longitud del tipo de datos C.  
  
 Para salida transmitidos o los parámetros de entrada/salida por secuencias, el *BufferLength* argumento se omite porque la longitud del búfer se especifica en **SQLGetData**.  
  
> [!NOTE]  
>  Cuando llama una aplicación ODBC 1.0 **SQLSetParam** en una aplicación ODBC 3. *x* controlador, el Administrador de controladores Esto convierte a una llamada a **SQLBindParameter** en el que el *BufferLength* argumento siempre es SQL_SETPARAM_VALUE_MAX. Dado que el Administrador de controladores devuelve un error si una aplicación ODBC 3. *x* aplicación establece *BufferLength* a SQL_SETPARAM_VALUE_MAX, una aplicación ODBC 3. *x* controlador puede emplear para determinar cuando se llama a una aplicación ODBC 1.0.  
  
> [!NOTE]  
>  En **SQLSetParam**, la forma en que una aplicación especifica la longitud de la **ParameterValuePtr* almacenar en búfer para que el controlador puede devolver caracteres o datos binarios y la manera en que una aplicación envía una matriz de caracteres o valores de parámetro binario para el controlador, se definen por controlador.  
  
## <a name="strlenorindptr-argument"></a>Argumento StrLen_or_IndPtr

 El *StrLen_or_IndPtr* argumento apunta a un búfer que, cuando **SQLExecute** o **SQLExecDirect** se denomina, contiene uno de los siguientes. (Este argumento establece los campos de registro SQL_DESC_OCTET_LENGTH_PTR y SQL_DESC_INDICATOR_PTR de los punteros de parámetro de la aplicación).  
  
-   La longitud del valor del parámetro almacenado en **ParameterValuePtr*. Se omite, excepto los caracteres o datos binarios de C.  
  
-   SQL_NTS. El valor del parámetro es una cadena terminada en null.  
  
-   SQL_NULL_DATA. El valor del parámetro es NULL.  
  
-   SQL_DEFAULT_PARAM. Un procedimiento consiste en usar el valor predeterminado de un parámetro, en lugar de un valor recuperado de la aplicación. Este valor solo es válido en un procedimiento llamado en la sintaxis canónica de ODBC y, a continuación, solo si el *InputOutputType* argumento es SQL_PARAM_INPUT_OUTPUT_STREAM, SQL_PARAM_INPUT_OUTPUT o SQL_PARAM_INPUT. Cuando \* *StrLen_or_IndPtr* es SQL_DEFAULT_PARAM el *ValueType*, *ParameterType*, *ColumnSize*,  *ColumnSize*, *BufferLength*, y *ParameterValuePtr* argumentos se omiten los parámetros de entrada y se usan únicamente para definir el valor del parámetro de salida para la entrada / parámetros de salida.  
  
-   El resultado de la SQL_LEN_DATA_AT_EXEC (*longitud*) macro. Los datos para el parámetro se enviarán con **SQLPutData**. Si el *ParameterType* argumento es SQL_LONGVARBINARY, SQL_LONGVARCHAR o long, tipo de datos específico del origen de datos, y el controlador devuelve "Y" para el tipo de información SQL_NEED_LONG_DATA_LEN en **SQLGetInfo**, *longitud* es el número de bytes de datos que se enviarán para el parámetro; en caso contrario, *longitud* debe ser un valor no negativo y se omite. Para obtener más información, vea "Pasar valores de parámetro" más adelante en esta sección.  
  
     Por ejemplo, para especificar que se enviará con 10 000 bytes de datos **SQLPutData** en una o varias llamadas para un parámetro SQL_LONGVARCHAR, una aplicación establece **StrLen_or_IndPtr* en SQL_LEN_DATA_AT_EXEC ( 10000).  
  
-   SQL_DATA_AT_EXEC. Los datos para el parámetro se enviarán con **SQLPutData**. Este valor se utiliza por las aplicaciones ODBC 1.0 cuando llaman a ODBC 3. *x* controladores. Para obtener más información, vea "Pasar valores de parámetro" más adelante en esta sección.  
  
 Si *StrLen_or_IndPtr* es un puntero nulo, el controlador se da por supuesto que todos los valores de parámetro de entrada son no NULL y que los datos binarios y de carácter están terminada en null. Si *InputOutputType* es SQL_PARAM_OUTPUT o SQL_PARAM_OUTPUT_STREAM y *ParameterValuePtr* y *StrLen_or_IndPtr* son ambos punteros nulos, los descartes de controlador el valor de salida.  
  
> [!NOTE]  
>  Se recomienda encarecidamente no especifique un puntero nulo para los desarrolladores de aplicaciones *StrLen_or_IndPtr* cuando el tipo de datos del parámetro es SQL_C_BINARY. Para asegurarse de que un controlador inesperado no truncar datos SQL_C_BINARY, *StrLen_or_IndPtr* debe contener un puntero a un valor de longitud válida.  
  
 Si el *InputOutputType* argumento es SQL_PARAM_OUTPUT_STREAM, SQL_PARAM_INPUT_OUTPUT_STREAM, SQL_PARAM_OUTPUT o SQL_PARAM_INPUT_OUTPUT *StrLen_or_IndPtr* apunta a un búfer en el que el el controlador devuelve el número de bytes disponible para devolver en SQL_NULL_DATA \* *ParameterValuePtr* (excepto el byte de una terminación null de los datos de caracteres), o SQL_NO_TOTAL (si el número de bytes disponible para valor devuelto no puede determinarse). Si el procedimiento devuelve uno o varios conjuntos de resultados, el **StrLen_or_IndPtr* no se garantiza que el búfer debe establecerse hasta que todos los resultados se han capturado.  
  
 Si es mayor que 1, el valor del atributo de instrucción SQL_ATTR_PARAMSET_SIZE *StrLen_or_IndPtr* apunta a una matriz de valores SQLLEN. Estos pueden ser cualquiera de los valores enumerados anteriormente en esta sección y se procesan con una única instrucción SQL.  
  
## <a name="passing-parameter-values"></a>Pasar valores de parámetro

 Una aplicación puede pasar el valor de parámetro ya sea en el \* *ParameterValuePtr* búfer o con uno o más llamadas a **SQLPutData**. Los parámetros cuyos datos se pasan con **SQLPutData** se conocen como *datos en ejecución* parámetros. Estos se usan normalmente para enviar datos de parámetros SQL_LONGVARBINARY y SQL_LONGVARCHAR y se pueden combinar con otros parámetros.  
  
 Para pasar valores de parámetro, una aplicación realiza la siguiente secuencia de pasos:  
  
1.  Las llamadas **SQLBindParameter** para cada parámetro para enlazar los búferes para el valor del parámetro (*ParameterValuePtr* argumento) y el indicador de longitud (*StrLen_or_IndPtr* argumento). Para los parámetros de datos en ejecución, *ParameterValuePtr* es un valor de puntero definido por la aplicación como un número de parámetro o un puntero a datos. El valor se devolverá más adelante y se puede usar para identificar el parámetro.  
  
2.  Coloca los valores para parámetros de entrada y de entrada/salida en el \* *ParameterValuePtr* y **StrLen_or_IndPtr* búferes:  
  
    -   Para los parámetros normales, la aplicación coloca el valor del parámetro en el \* *ParameterValuePtr* búfer y la longitud de ese valor en el **StrLen_or_IndPtr* búfer. Para obtener más información, consulte [valores de parámetro de configuración](../../../odbc/reference/develop-app/setting-parameter-values.md).  
  
    -   Para los parámetros de datos en ejecución, la aplicación coloca el resultado de la SQL_LEN_DATA_AT_EXEC (*longitud*) macro (al llamar a un controlador ODBC 2.0) en el **StrLen_or_IndPtr* búfer.  
  
3.  Las llamadas **SQLExecute** o **SQLExecDirect** para ejecutar la instrucción SQL.  
  
    -   Si no hay ningún parámetro de datos en ejecución, el proceso está completado.  
  
    -   Si hay algún parámetro de datos en ejecución, la función devuelve SQL_NEED_DATA.  
  
4.  Las llamadas **SQLParamData** para recuperar el valor definido por la aplicación especificado en el *ParameterValuePtr* argumento de **SQLBindParameter** para la primera parámetro de datos en ejecución para procesarse. **SQLParamData** devuelve SQL_NEED_DATA.  
  
    > [!NOTE]  
    >  Aunque los parámetros de datos en ejecución son similares a las columnas de datos en ejecución, el valor devuelto por **SQLParamData** es diferente para cada uno. Parámetros de datos en ejecución son parámetros en una instrucción SQL para el que se enviarán los datos con **SQLPutData** cuando se ejecuta la instrucción con **SQLExecDirect** o **SQLExecute**. Se enlazan con **SQLBindParameter**. El valor devuelto por **SQLParamData** se pasa un valor de puntero a **SQLBindParameter** en el *ParameterValuePtr* argumento. Columnas de datos en ejecución son columnas de un conjunto de filas para el que se enviarán los datos con **SQLPutData** cuando una fila se actualiza o agrega con **SQLBulkOperations** o actualizados con **SQLSetPos**. Se enlazan con **SQLBindCol**. El valor devuelto por **SQLParamData** es la dirección de la fila en el **TargetValuePtr* búfer (establecido mediante una llamada a **SQLBindCol**) que se está procesando.  
  
5.  Las llamadas **SQLPutData** uno o más veces para enviar datos para el parámetro. Se necesita más de una llamada si el valor de datos es mayor que el \* *ParameterValuePtr* especificado en el búfer **SQLPutData**; varias llamadas a **SQLPutData**para el mismo parámetro que se permiten solo al enviar datos de carácter C a una columna con un tipo de carácter, binario o datos específicos del origen de datos o al enviar datos binarios de C a una columna con un carácter, binario, o tipo de datos específico del origen de datos.  
  
6.  Las llamadas **SQLParamData** nuevo para indicar que se han enviado todos los datos para el parámetro.  
  
    -   Si hay más de los parámetros de datos en ejecución, **SQLParamData** devuelve SQL_NEED_DATA y el valor definido por la aplicación para el siguiente parámetro de datos en ejecución al procesarse. La aplicación repite los pasos 4 y 5.  
  
    -   Si no hay nada más parámetros de datos en ejecución, el proceso está completado. Si la instrucción se ejecutó correctamente, **SQLParamData** devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO; si se produjo un error en la ejecución, devuelve SQL_ERROR. En este momento, **SQLParamData** puede devolver cualquier SQLSTATE que puede ser devueltos por la función que se usa para ejecutar la instrucción (**SQLExecDirect** o **SQLExecute**).  
  
         Los valores de salida para los parámetros de entrada y salida o de salida están disponibles en el \* *ParameterValuePtr* y **StrLen_or_IndPtr* almacena en búfer después de la aplicación recupera todos los conjuntos de resultados generado por la instrucción.  
  
 Una llamada a **SQLExecute** o **SQLExecDirect** coloca la instrucción en un estado SQL_NEED_DATA. En este momento, la aplicación puede llamar solo **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions**, **SQLParamData**, o **SQLPutData** con la instrucción o el *identificador de conexión* asociados con la instrucción. Si llama a cualquier otra función con la instrucción o la conexión asociada con la instrucción, la función devuelve SQLSTATE HY010 (función de error de secuencia). Las hojas de instrucción el SQL_NEED_DATA estado cuando **SQLParamData** o **SQLPutData** devuelve un error, **SQLParamData** devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, o se cancela la instrucción.  
  
 Si la aplicación llama a **SQLCancel** mientras el controlador sigue necesitando los datos para los parámetros de datos en ejecución, el controlador cancela la ejecución de la instrucción; a continuación, puede llamar la aplicación **SQLExecute** o  **SQLExecDirect** nuevo.  
  
## <a name="retrieving-streamed-output-parameters"></a>Recuperar parámetros de salida transmitidos

 Cuando una aplicación establece *InputOutputType* SQL_PARAM_INPUT_OUTPUT_STREAM o SQL_PARAM_OUTPUT_STREAM, se debe recuperar el valor del parámetro de salida mediante una o varias llamadas a **SQLGetData**. Cuando el controlador tiene un valor de parámetro de salida transmitidos para volver a la aplicación, devolverá SQL_PARAM_DATA_AVAILABLE en respuesta a una llamada a las funciones siguientes: **SQLMoreResults**, **SQLExecute**, y **SQLExecDirect**. Una aplicación llama a **SQLParamData** para determinar qué valor del parámetro está disponible.  
  
 Para obtener más información acerca de los parámetros de salida transmitidos y SQL_PARAM_DATA_AVAILABLE, consulte [recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="using-arrays-of-parameters"></a>Utilizar matrices de parámetros

 Cuando una aplicación prepara una instrucción con marcadores de parámetros y pasa una matriz de parámetros, hay dos maneras diferentes, que esto se puede ejecutar. Es una manera para que el controlador se basan en las capacidades de procesamiento de la matriz del back-end, en el que caso la instrucción completa con la matriz de parámetros se trata como una unidad atómica. Oracle es un ejemplo de un origen de datos que admite capacidades de procesamiento de la matriz. Otra manera de implementar esta característica es para que el controlador generar un lote de instrucciones SQL, una instrucción SQL para cada conjunto de parámetros en la matriz de parámetros y ejecutar el lote. Matrices de parámetros no se puede usar con un **UPDATE WHERE CURRENT OF** instrucción.  
  
 Cuando se procesa una matriz de parámetros, recuentos de fila o conjuntos de resultados individuales (uno para cada conjunto de parámetros) pueden estar disponibles o recuentos de filas o conjuntos de resultados se pueden acumular en uno. Opción el SQL_PARAM_ARRAY_ROW_COUNTS **SQLGetInfo** indica si están disponibles para cada conjunto de parámetros (SQL_PARC_BATCH) recuentos de filas o recuento de filas de un solo está disponible (SQL_PARC_NO_BATCH).  
  
 Opción el SQL_PARAM_ARRAY_SELECTS **SQLGetInfo** indica si un conjunto de resultados está disponible para cada conjunto de parámetros (SQL_PAS_BATCH) o solo un conjunto de resultados está disponible (SQL_PAS_NO_BATCH). Si el controlador no permite una instrucción generadora de conjunto de resultados que se ejecutará con una matriz de parámetros, SQL_PARAM_ARRAY_SELECTS devuelve SQL_PAS_NO_SELECT.  
  
 Para obtener más información, consulte [función SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
 Para admitir matrices de parámetros, se establece el atributo de instrucción SQL_ATTR_PARAMSET_SIZE para especificar el número de valores para cada parámetro. Si el campo es mayor que 1, los campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR y SQL_DESC_OCTET_LENGTH_PTR del APD deben apuntar a las matrices. La cardinalidad de cada matriz es igual al valor de SQL_ATTR_PARAMSET_SIZE.  
  
 El campo SQL_DESC_ROWS_PROCESSED_PTR del APD apunta a un búfer que contiene el número de conjuntos de parámetros que se han procesado, incluidos los conjuntos de error. Cuando se procesa cada conjunto de parámetros, el controlador almacena un nuevo valor en el búfer. Si se trata de un puntero nulo, no se devolverá ningún número. Cuando se utilizan matrices de parámetros, se rellena el valor señalado por el campo SQL_DESC_ROWS_PROCESSED_PTR del APD incluso si se devuelve SQL_ERROR por la función de configuración. Si se devuelve SQL_NEED_DATA, se establece el valor al que apunta el campo SQL_DESC_ROWS_PROCESSED_PTR del APD al conjunto de parámetros que se está procesando.  
  
 Lo que ocurre cuando se enlaza a una matriz de parámetros y un **UPDATE WHERE CURRENT OF** se ejecuta la instrucción está definido por el controlador.  
  
## <a name="column-wise-parameter-binding"></a>El enlace de parámetro

 En el enlace, la aplicación enlaza el parámetro independiente y matrices de longitud/indicador para cada parámetro.  
  
 Para usar el enlace, la aplicación primero establece el atributo de instrucción SQL_ATTR_PARAM_BIND_TYPE en SQL_PARAM_BIND_BY_COLUMN. (Esto es el valor predeterminado). Para que enlazar cada columna, la aplicación realiza los pasos siguientes:  
  
1.  Asigna una matriz de búferes de parámetros.  
  
2.  Asigna una matriz de búferes de longitud/indicador.  
  
    > [!NOTE]  
    >  Si la aplicación escribe directamente en los descriptores de cuando se usa el enlace, matrices independientes pueden usarse para datos de longitud y el indicador.  
  
3.  Las llamadas **SQLBindParameter** con los argumentos siguientes:  
  
    -   *ValueType* es el tipo C de un único elemento de la matriz del búfer de parámetro.  
  
    -   *ParameterType* es el tipo SQL del parámetro.  
  
    -   *ParameterValuePtr* es la dirección de la matriz de búferes de parámetros.  
  
    -   *BufferLength* es el tamaño de un único elemento de la matriz del búfer de parámetro. El *BufferLength* argumento se omite cuando los datos son datos de longitud fija.  
  
    -   *StrLen_or_IndPtr* es la dirección de la matriz de longitud/indicador.  
  
 Para obtener más información sobre cómo se usa esta información, vea "ParameterValuePtr argumento" en "Comentarios" más adelante en esta sección. Para obtener más información sobre el enlace de parámetros, vea [matrices de parámetros de enlace](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md).  
  
## <a name="row-wise-parameter-binding"></a>El enlace de parámetro

 En el enlace, la aplicación define una estructura que contiene el parámetro y el indicador de longitud búferes para cada parámetro que se enlazará.  
  
 Para usar el enlace, la aplicación lleva a cabo los pasos siguientes:  
  
1.  Define una estructura que contenga un único conjunto de parámetros (incluidos los búferes de parámetros y de longitud/indicador) y asigna una matriz de estas estructuras.  
  
    > [!NOTE]  
    >  Si la aplicación escribe directamente en los descriptores de cuando se usa el enlace, campos independientes se pueden usar para los datos de longitud y el indicador.  
  
2.  Establece el atributo de instrucción SQL_ATTR_PARAM_BIND_TYPE en el tamaño de la estructura que contiene un único conjunto de parámetros o hasta el tamaño de una instancia de un búfer en el que se enlazará los parámetros. La longitud debe incluir el espacio para todos los parámetros enlazados y cualquier relleno de la estructura o búfer, para asegurarse de que cuando la dirección de un parámetro dependiente se incrementa con la longitud especificada, el resultado señalará al principio del mismo parámetro en el fila siguiente. Cuando se usa el *sizeof* operador en ANSI C, se garantiza que este comportamiento.  
  
3.  Las llamadas **SQLBindParameter** con los argumentos siguientes para cada parámetro enlazar:  
  
    -   *ValueType* es el tipo del miembro de búfer de parámetro para enlazarse a la columna.  
  
    -   *ParameterType* es el tipo SQL del parámetro.  
  
    -   *ParameterValuePtr* es la dirección del miembro de búfer de parámetro en el primer elemento de matriz.  
  
    -   *BufferLength* es el tamaño del miembro de búfer del parámetro.  
  
    -   *StrLen_or_IndPtr* es la dirección del miembro de longitud/indicador enlazar.  
  
 Para obtener más información sobre cómo se usa esta información, vea "*ParameterValuePtr* argumento," más adelante en esta sección. Para obtener más información sobre el enlace de parámetros, vea el [matrices de parámetros de enlace](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md).  
  
## <a name="error-information"></a>Información del error

 Si un controlador no implementa las matrices de parámetros como lotes (la opción SQL_PARAM_ARRAY_ROW_COUNTS es igual a SQL_PARC_NO_BATCH), las situaciones de error se tratan como si se ejecuta una instrucción. Si el controlador implementa las matrices de parámetros como lotes, una aplicación puede usar el campo de encabezado SQL_DESC_ARRAY_STATUS_PTR de la IPD para determinar qué parámetro de una instrucción SQL o qué hizo en una matriz de parámetros  **SQLExecDirect** o **SQLExecute** para devolver un error. Este campo contiene información de estado para cada fila de valores de parámetro. Si el campo indica que se ha producido un error, los campos de la estructura de datos de diagnóstico le indicará el número de fila y los parámetros del parámetro que no se pudo. El número de elementos de la matriz se definirá en el campo de encabezado SQL_DESC_ARRAY_SIZE en el APD, que se puede establecer el atributo de instrucción SQL_ATTR_PARAMSET_SIZE.  
  
> [!NOTE]  
>  El campo de encabezado SQL_DESC_ARRAY_STATUS_PTR en el APD se usa para omitir los parámetros. Para obtener más información acerca de la omisión de los parámetros, vea la sección siguiente, "Se omitirá un conjunto de parámetros".  
  
 Cuando **SQLExecute** o **SQLExecDirect** devuelve SQL_ERROR, los elementos de la matriz señalada por el campo SQL_DESC_ARRAY_STATUS_PTR en la IPD contendrá SQL_ SQL_PARAM_ERROR, SQL_PARAM_SUCCESS, PARAM_SUCCESS_WITH_INFO, SQL_PARAM_UNUSED o SQL_PARAM_DIAG_UNAVAILABLE.  
  
 Para cada elemento de esta matriz, la estructura de datos de diagnóstico contiene uno o más registros de estado. El campo SQL_DIAG_ROW_NUMBER de la estructura indica el número de fila de los valores de parámetro que produjo el error. Si es posible determinar el parámetro concreto en una fila de parámetros que se produjo el error, el número de parámetro se escribirán en el campo SQL_DIAG_COLUMN_NUMBER.  
  
 SQL_PARAM_UNUSED se escribe cuando no se ha utilizado un parámetro porque se produjo un error en un parámetro anterior que obligan a **SQLExecute** o **SQLExecDirect** para anular la operación. Por ejemplo, si hay 50 parámetros y un error al ejecutar el conjunto de parámetros que ha provocado cuadragésimo **SQLExecute** o **SQLExecDirect** anular, a continuación, SQL_PARAM_UNUSED se escribe en el matriz de Estados para los parámetros de 41 a través de 50.  
  
 SQL_PARAM_DIAG_UNAVAILABLE se especifica cuando el controlador trata a las matrices de parámetros como una unidad monolítica, por lo que no genera este nivel de parámetro individual de información de error.  
  
 Algunos errores en el procesamiento de un único conjunto de parámetros que el procesamiento de los siguientes conjuntos de parámetros en la matriz a detener. Otros errores no afectan el procesamiento de los parámetros siguientes. Qué errores detendrá el procesamiento es definido por el controlador. Si no se ha detenido el procesamiento, se procesan todos los parámetros de la matriz, se devuelve SQL_SUCCESS_WITH_INFO como resultado el error y el búfer definido por SQL_ATTR_PARAMS_PROCESSED_PTR se establece en el número total de conjuntos de parámetros procesados (según se define en el Atributo de instrucción SQL_ATTR_PARAMSET_SIZE), que incluye los conjuntos de error.  
  
> [!CAUTION]  
>  Comportamiento ODBC cuando se produce un error en el procesamiento de una matriz de parámetros es diferente en ODBC 3. *x* de lo que era en ODBC 2. *x*. En ODBC 2. *x*, la función devuelve SQL_ERROR y el procesamiento si dejaron de serlo. El búfer señalado por el *pirow* argumento de **SQLParamOptions** contiene el número de la fila de error. En ODBC 3. *x*, la función devuelve SQL_SUCCESS_WITH_INFO y mayo de procesamiento o detenerse o continuar. Si continúa, el búfer especificado por SQL_ATTR_PARAMS_PROCESSED_PTR se establecerá en el valor de todos los parámetros procesados, las que dieron lugar a un error incluidas. Este cambio de comportamiento puede causar problemas para las aplicaciones existentes.  
  
 Cuando **SQLExecute** o **SQLExecDirect** devuelve antes de completar el procesamiento de todos los conjuntos de parámetros en una matriz de parámetros, como cuando se devuelve SQL_ERROR o SQL_NEED_DATA, contiene la matriz de Estados Estados para los parámetros que ya se han procesado. La ubicación señalada por el campo SQL_DESC_ROWS_PROCESSED_PTR la IPD contiene el número de fila en la matriz de parámetros que produjo el código de error SQL_ERROR o SQL_NEED_DATA. Cuando se envía una matriz de parámetros a una instrucción SELECT, la disponibilidad de la matriz de valores de estado está definido por el controlador; pueden estar disponibles después de haber ejecutado la instrucción o como resultado conjuntos se capturan.  
  
## <a name="ignoring-a-set-of-parameters"></a>Se omitirá un conjunto de parámetros

 El campo SQL_DESC_ARRAY_STATUS_PTR del APD (según lo establecido por el atributo de instrucciones SQL_ATTR_PARAM_STATUS_PTR) se puede utilizar para indicar que debe omitirse un conjunto de parámetros enlazados en una instrucción SQL. Para indicar que el controlador para pasar por alto uno o varios conjuntos de parámetros durante la ejecución, una aplicación debe seguir estos pasos:  
  
1.  Llame a **SQLSetDescField** para establecer el campo de encabezado SQL_DESC_ARRAY_STATUS_PTR del APD para que apunte a una matriz de valores SQLUSMALLINT que contienen información de estado. Este campo también se puede establecer mediante una llamada a **SQLSetStmtAttr** con un *atributo* de SQL_ATTR_PARAM_OPERATION_PTR, lo que permite a una aplicación establecer el campo sin obtener un identificador de descriptor.  
  
2.  Establezca cada elemento de la matriz que se define en el campo SQL_DESC_ARRAY_STATUS_PTR del APD en uno de dos valores:  
  
    -   SQL_PARAM_IGNORE, para indicar que la fila se excluye de la ejecución de la instrucción.  
  
    -   SQL_PARAM_PROCEED, para indicar que la fila se incluye en la ejecución de la instrucción.  
  
3.  Llame a **SQLExecDirect** o **SQLExecute** para ejecutar la instrucción preparada.  
  
 Las siguientes reglas se aplican a la matriz que se define en el campo SQL_DESC_ARRAY_STATUS_PTR del APD:  
  
-   El puntero se establece en null de forma predeterminada.  
  
-   Si el puntero es null, se usan todos los conjuntos de parámetros, como si todos los elementos se han establecido en SQL_ROW_PROCEED.  
  
-   Establecimiento de un elemento a SQL_PARAM_PROCEED no garantiza que la operación usará ese conjunto concreto de parámetros.  
  
-   SQL_PARAM_PROCEED se define como 0 en el archivo de encabezado.  
  
 Una aplicación puede establecer el campo SQL_DESC_ARRAY_STATUS_PTR en el APD para que apunte a la misma matriz como que ha señalado por el campo SQL_DESC_ARRAY_STATUS_PTR en IRD. Esto es útil al enlazar parámetros a los datos de fila. A continuación, se omiten los parámetros según el estado de la fila de datos. SQL_PARAM_IGNORE, además de los siguientes códigos de provocar un parámetro en una instrucción SQL que se pasen por alto: SQL_ROW_DELETED, SQL_ROW_UPDATED y SQL_ROW_ERROR. SQL_PARAM_PROCEED, además de los siguientes códigos de producen una instrucción SQL continuar: SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO y SQL_ROW_ADDED.  
  
## <a name="rebinding-parameters"></a>Volver a enlazar parámetros

 Una aplicación puede realizar cualquiera de las dos operaciones para cambiar un enlace:  
  
-   Llame a **SQLBindParameter** para especificar un nuevo enlace para una columna que ya está enlazado. El controlador sobrescribe los enlaces antiguos con uno nuevo.  
  
-   Especifique un desplazamiento que se agregarán a la dirección del búfer que se especificó en la llamada de enlace a **SQLBindParameter**. Para obtener más información, consulte la sección siguiente, "Volver a enlazar con los desplazamientos".  
  
## <a name="rebinding-with-offsets"></a>Volver a enlazar con desplazamientos

 Este nuevo enlace de parámetros es especialmente útil cuando una aplicación tiene una configuración de área de búfer que puede contener muchos parámetros, pero una llamada a **SQLExecDirect** o **SQLExecute** usa sólo algunos de los parámetros. El espacio restante en el área del búfer se puede usar para el siguiente conjunto de parámetros modificando el enlace existente por un desplazamiento.  
  
 El campo de encabezado SQL_DESC_BIND_OFFSET_PTR en el APD señala el desplazamiento de enlace. Si el campo es distinto de null, el controlador desreferencia el puntero y, si ninguno de los valores de los campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR y SQL_DESC_OCTET_LENGTH_PTR es un puntero nulo, agrega el valor sin referencia a esos campos en el descriptor registros en tiempo de ejecución. Los nuevos valores de puntero se utilizan cuando se ejecutan las instrucciones SQL. El desplazamiento sigue siendo válido después de volver a enlazar. Dado que SQL_DESC_BIND_OFFSET_PTR es un puntero para el desplazamiento en lugar de con el desplazamiento de sí misma, una aplicación puede cambiar el desplazamiento directamente, sin tener que llamar [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) o [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md) a Cambie el campo descriptor. El puntero se establece en null de forma predeterminada. Se puede establecer el campo SQL_DESC_BIND_OFFSET_PTR de la descartar mediante una llamada a [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) o mediante una llamada a [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)con un *fAttribute* de SQL_ATTR_PARAM_BIND_ OFFSET_PTR.  
  
 El desplazamiento de enlace siempre se agrega directamente a los valores de los campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR y SQL_DESC_OCTET_LENGTH_PTR. Si el desplazamiento se cambia a un valor diferente, el nuevo valor todavía se agrega directamente al valor de cada campo descriptor. El desplazamiento nuevo no se agrega a la suma del valor de campo y los desplazamientos anteriores.  
  
## <a name="descriptors"></a>Descriptores de

 ¿Cómo se enlaza un parámetro viene determinada por los campos de los IDP y APD. Los argumentos de **SQLBindParameter** se utilizan para establecer los campos de descriptor. También se pueden establecer los campos los **SQLSetDescField** funciones, aunque **SQLBindParameter** es más eficaz utilizar porque la aplicación no tiene que obtener un identificador de descriptor para llamar a **SQLBindParameter**.  
  
> [!CAUTION]  
>  Una llamada a **SQLBindParameter** para una instrucción puede afectar a otras instrucciones. Esto ocurre cuando el descartar asociado con la instrucción se asigna explícitamente y también está asociado con otras instrucciones. Dado que **SQLBindParameter** modifica los campos de la APD, las modificaciones se aplicarán a todas las instrucciones que está asociada este descriptor. Si esto no es el comportamiento necesario, la aplicación debe desasociar este descriptor de las demás instrucciones antes de llamar a **SQLBindParameter**.  
  
 Conceptualmente, **SQLBindParameter** realiza los siguientes pasos en secuencia:  
  
1.  Las llamadas [SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) para obtener el identificador APD.  
  
2.  Las llamadas [SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) para obtener SQL_DESC_COUNT campo del APD y si el valor de la *ColumnNumber* argumento supera el valor de SQL_DESC_COUNT, llamadas **SQLSetDescField**para aumentar el valor de SQL_DESC_COUNT a *ColumnNumber*.  
  
3.  Las llamadas [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) varias veces para asignar valores a los campos siguientes de la APD:  
  
    -   Establece SQL_DESC_TYPE y SQL_DESC_CONCISE_TYPE en el valor de *ValueType*, salvo que si *ValueType* es uno de los identificadores concisos de un subtipo de intervalo o datetime, Establece SQL_DESC_TYPE en SQL_ Fecha y hora o SQL_INTERVAL, respectivamente, SQL_DESC_CONCISE_TYPE se establece en el identificador conciso y SQL_DESC_DATETIME_INTERVAL_CODE se establece en el valor de datetime correspondiente o el subcódigo de intervalo.  
  
    -   Establece el campo SQL_DESC_OCTET_LENGTH en el valor de *BufferLength*.  
  
    -   El campo SQL_DESC_DATA_PTR se establece en el valor de *ParameterValue*.  
  
    -   Establece el campo SQL_DESC_OCTET_LENGTH_PTR en el valor de *StrLen_or_Ind*.  
  
    -   Establece el campo SQL_DESC_INDICATOR_PTR también en el valor de *StrLen_or_Ind*.  
  
     El *StrLen_or_Ind* parámetro especifica la información de indicador y la longitud del valor de parámetro.  
  
4.  Las llamadas [SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) para obtener el identificador IPD.  
  
5.  Las llamadas [SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) para obtener SQL_DESC_COUNT campo de IPD y si el valor de la *ColumnNumber* argumento supera el valor de SQL_DESC_COUNT, llamadas **SQLSetDescField**para aumentar el valor de SQL_DESC_COUNT a *ColumnNumber*.  
  
6.  Las llamadas [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) varias veces para asignar valores a los campos siguientes de la IPD:  
  
    -   Establece SQL_DESC_TYPE y SQL_DESC_CONCISE_TYPE en el valor de *ParameterType*, salvo que si *ParameterType* es uno de los identificadores concisos de un subtipo de intervalo o datetime, Establece SQL_DESC_TYPE SQL_DATETIME o SQL_INTERVAL, respectivamente, Establece SQL_DESC_CONCISE_TYPE en el identificador concisa y establece SQL_DESC_DATETIME_INTERVAL_CODE para el valor de datetime correspondiente o el subcódigo de intervalo.  
  
    -   Establece uno o varios de SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_PRECISION y SQL_DESC_LENGTH según corresponda para *ParameterType*.  
  
    -   Establece el valor de SQL_DESC_SCALE *ColumnSize*.  
  
 Si la llamada a **SQLBindParameter** se produce un error, el contenido de los campos de descriptor que se habría establecido en el APD están definidos y no se modifica el campo SQL_DESC_COUNT del APD. Además, los campos SQL_DESC_TYPE, SQL_DESC_SCALE, SQL_DESC_PRECISION y SQL_DESC_LENGTH del registro adecuado de la IPD están definidos y no se modifica el campo SQL_DESC_COUNT de la IPD.  
  
## <a name="conversion-of-calls-to-and-from-sqlsetparam"></a>Conversión de las llamadas a y desde SQLSetParam

 Cuando llama una aplicación ODBC 1.0 **SQLSetParam** en una aplicación ODBC 3. *x* controlador, el ODBC 3. *x* Administrador de controladores se asigna la llamada como se muestra en la tabla siguiente.  
  
|Llamar a la aplicación ODBC 1.0|La llamada a ODBC 3. *x* controlador|  
|----------------------------------|-------------------------------|  
|SQLSetParam(      StatementHandle,      ParameterNumber,      ValueType,      ParameterType,      LengthPrecision,      ParameterScale,      ParameterValuePtr,      StrLen_or_IndPtr);|SQLBindParameter (StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, ValueType, ParameterType, *ColumnSize*, *ColumnSize*, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX,      StrLen_or_IndPtr);|  
  
## <a name="code-example"></a>Ejemplo de código  
 En el ejemplo siguiente, una aplicación prepara una instrucción SQL para insertar datos en la tabla ORDERS. Para cada parámetro en la instrucción, la aplicación llama a **SQLBindParameter** para especificar el tipo de datos ODBC C y el tipo de datos SQL del parámetro y para enlazar un búfer para cada parámetro. Para cada fila de datos, la aplicación asigna valores de datos para cada parámetro y llama a **SQLExecute** para ejecutar la instrucción.  
  
 El ejemplo siguiente se da por supuesto que tiene un origen de datos ODBC en el equipo denominado Northwind que está asociado con la base de datos Northwind.  
  
 Para obtener más ejemplos de código, vea [función SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [función SQLProcedures](../../../odbc/reference/syntax/sqlprocedures-function.md), [función SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md), y [función SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
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
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Devolver información acerca de un parámetro en una instrucción|[Función SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
|Ejecutar una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecutar una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Liberar los búferes de parámetros en la instrucción|[Función SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Devuelve el número de parámetros de la instrucción|[Función SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|Devuelve el siguiente parámetro para enviar datos|[Función SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Especificar varios valores de parámetro|[Función SQLParamOptions](../../../odbc/reference/syntax/sqlparamoptions-function.md)|  
|Envío de datos de parámetro en tiempo de ejecución|[Función SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>Vea también

 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
