---
title: Función SQLBindParameter | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
apiname:
- SQLBindParameter
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLBindParameter
helpviewer_keywords:
- SQLBindParameter function [ODBC]
ms.assetid: 38349d4b-be03-46f9-9d6a-e50dd144e225
caps.latest.revision: 52
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: On Demand
ms.openlocfilehash: 54a22ecb571f6a6831023ee5c5d6c18149bff575
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sqlbindparameter-function"></a>Función SQLBindParameter
**Conformidad**  
 Versión introdujo: ODBC 2.0 normativas: ODBC  
  
 **Resumen**  
 **SQLBindParameter** enlaza un búfer a un marcador de parámetro en una instrucción SQL. **SQLBindParameter** admite el enlace a un tipo de datos Unicode C, incluso si el controlador subyacente no admite datos Unicode.  
  
> [!NOTE]  
>  Esta función reemplaza la función ODBC 1.0 **SQLSetParam**. Para obtener más información, vea "Comentarios".  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
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
 [Entrada] Número de parámetro, ordenados secuencialmente en orden creciente de los parámetros, comenzando por 1.  
  
 *InputOutputType*  
 [Entrada] El tipo del parámetro. Para obtener más información, vea "*InputOutputType* argumento" en "Comentarios".  
  
 *Tipo de valor*  
 [Entrada] El tipo de datos C del parámetro. Para obtener más información, vea "*ValueType* argumento" en "Comentarios".  
  
 *ParameterType*  
 [Entrada] El tipo de datos SQL del parámetro. Para obtener más información, vea "*ParameterType* argumento" en "Comentarios".  
  
 *ColumnSize*  
 [Entrada] El tamaño de la columna o expresión de marcador de parámetro correspondiente. Para obtener más información, vea "*ColumnSize* argumento" en "Comentarios".  
  
 Si la aplicación se ejecutará en un sistema operativo de Windows de 64 bits, consulte [información ODBC de 64 bits](../../../odbc/reference/odbc-64-bit-information.md).  
  
 *ColumnSize*  
 [Entrada] Los dígitos decimales de la columna o expresión de marcador de parámetro correspondiente. Para obtener más información sobre el tamaño de columna, vea [tamaño de la columna, dígitos decimales, transferencia de longitud de bytes y el tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
 *ParameterValuePtr*  
 [Entrada diferida] Un puntero a un búfer para los datos del parámetro. Para obtener más información, vea "*ParameterValuePtr* argumento" en "Comentarios".  
  
 *BufferLength*  
 [Entrada/salida] Longitud de la *ParameterValuePtr* búfer en bytes. Para obtener más información, vea "*BufferLength* argumento" en "Comentarios".  
  
 Vea [información ODBC de 64 bits](../../../odbc/reference/odbc-64-bit-information.md), si la aplicación se ejecutará en un sistema operativo de 64 bits.  
  
 *StrLen_or_IndPtr*  
 [Entrada diferida] Un puntero a un búfer para la longitud del parámetro. Para obtener más información, vea "*StrLen_or_IndPtr* argumento" en "Comentarios".  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLBindParameter** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE suelen ser devueltos por **SQLBindParameter** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07006|Infracción del atributo de tipo de datos restringido|El tipo de datos identificado por la *ValueType* argumento no se puede convertir al tipo de datos identificado por la *ParameterType* argumento. Tenga en cuenta que puede devolver este error **SQLExecDirect**, **SQLExecute**, o **SQLPutData** en tiempo de ejecución, en lugar de por **SQLBindParameter**.|  
|07009|Índice de descriptor no válido|(DM) el valor especificado para el argumento *ParameterNumber* fue menor que 1.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el **MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar memoria que es necesario para admitir la ejecución o la finalización de la función.|  
|HY003|Tipo de búfer de aplicación no válido|El valor especificado por el argumento *ValueType* no era un tipo de datos válido de C o SQL_C_DEFAULT.|  
|HY004|Tipo de datos SQL no válido|El valor especificado para el argumento *ParameterType* no era un identificador válido de tipo de datos de ODBC SQL ni un identificador de tipo de datos SQL específicas del controlador admitida por el controlador.|  
|HY009|Valor de argumento no válido|(DM) el argumento *ParameterValuePtr* era un puntero nulo, el argumento *StrLen_or_IndPtr* era un puntero nulo y el argumento *InputOutputType* no era SQL_PARAM_ SALIDA.<br /><br /> SQL_PARAM_OUTPUT (DM), donde el argumento *ParameterValuePtr* era un puntero nulo, el tipo de C es el carácter o binario y la BufferLength (*cbValueMax*) es mayor que 0.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónica aún estaba ejecutando cuando **SQLBindParameter** se llamó.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* devolvió SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY021|Información de descriptor incoherente|La información del descriptor comprueba durante una comprobación de coherencia no era coherente. (Vea la sección "Comprobaciones de coherencia" en **SQLSetDescField**.)<br /><br /> El valor especificado para el argumento *ColumnSize* estaba fuera del intervalo de valores admitido por el origen de datos para una columna del tipo de datos SQL especificada por el *ParameterType* argumento.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el valor de *BufferLength* era menor que 0. (Vea la descripción del campo SQL_DESC_DATA_PTR en **SQLSetDescField**.)|  
|HY104|Valor de precisión o escala no válido|El valor especificado para el argumento *ColumnSize* o *ColumnSize* estaba fuera del intervalo de valores admitido por el origen de datos para una columna del tipo de datos SQL especificada por el  *ParameterType* argumento.|  
|HY105|Tipo de parámetro no válido|(DM) el valor especificado para el argumento *InputOutputType* no era válido. (Vea "Comentarios".)|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|El controlador u origen de datos no admite la conversión especificada por la combinación del valor especificado para el argumento *ValueType* y el valor específico del controlador especificado para el argumento *ParameterType*.<br /><br /> El valor especificado para el argumento *ParameterType* era un identificador de tipo de datos de ODBC SQL válido para el controlador es compatible con la versión de ODBC, pero no era compatible con el controlador u origen de datos.<br /><br /> El controlador es compatible con solo 2 de ODBC. *x* y el argumento *ValueType* era una de las siguientes acciones:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> y todos los tipos de datos C de intervalo que aparecen en [tipos de datos C](../../../odbc/reference/appendixes/c-data-types.md) en tipos de datos de apéndice D:.<br /><br /> El controlador solo es compatible con las versiones ODBC anteriores 3.50 y el argumento *ValueType* era SQL_C_GUID.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *StatementHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Una aplicación llama **SQLBindParameter** para enlazar cada marcador de parámetro en una instrucción SQL. Enlaces sigue surtiendo efecto hasta que la aplicación llama **SQLBindParameter** llama de nuevo, **SQLFreeStmt** con la opción de SQL_RESET_PARAMS o llamadas **SQLSetDescField** a Establezca el campo de encabezado SQL_DESC_COUNT de la APD en 0.  
  
 Para obtener más información acerca de los parámetros, vea [parámetros de la instrucción](../../../odbc/reference/develop-app/statement-parameters.md). Para obtener más información sobre los tipos de datos de parámetros y marcadores de parámetros, vea [tipos de datos de parámetro](../../../odbc/reference/appendixes/parameter-data-types.md) y [marcadores de parámetros](../../../odbc/reference/appendixes/parameter-markers.md) en Apéndice C: SQL gramática.  
  
## <a name="parameternumber-argument"></a>Argumento de ParameterNumber  
 Si *ParameterNumber* en la llamada a **SQLBindParameter** es mayor que el valor de SQL_DESC_COUNT, **SQLSetDescField** se llama para aumentar el valor de SQL_DESC_ CONTAR a *ParameterNumber*.  
  
## <a name="inputoutputtype-argument"></a>Argumento de InputOutputType  
 El *InputOutputType* argumento especifica el tipo del parámetro. Este argumento establece el campo SQL_DESC_PARAMETER_TYPE de la IPD. Todos los parámetros en instrucciones SQL que no llame a los procedimientos, como **insertar** instrucciones, son *entrada ** parámetros*. Los parámetros en las llamadas a procedimiento pueden usar como entrados, entrada/salida o parámetros de salida. (Una aplicación llama **SQLProcedureColumns** para determinar el tipo de un parámetro en una llamada a procedimiento; se suponen que los parámetros cuyo tipo no se puede determinar son parámetros de entrada.)  
  
 El *InputOutputType* argumento es uno de los siguientes valores:  
  
-   SQL_PARAM_INPUT. El parámetro de marca un parámetro en una instrucción SQL que no llama a un procedimiento, como un **insertar** instrucción, o se marca un parámetro de entrada en un procedimiento. Por ejemplo, los parámetros de **INSERT INTO empleado VALUES (?,?,?)**  son parámetros de entrada, mientras que los parámetros de **{llamar a AddEmp (?,?,?)}**  puede ser, pero no son necesariamente, parámetros de entrada.  
  
     Cuando se ejecuta la instrucción, el controlador envía los datos para el parámetro para el origen de datos el \* *ParameterValuePtr* búfer debe contener un valor de entrada válido, o el **StrLen_or_IndPtr* búfer debe contener SQL_NULL_DATA, SQL_DATA_AT_EXEC o el resultado de la SQL_LEN_DATA_AT Macro _EXEC.  
  
     Si una aplicación no puede determinar el tipo de un parámetro en una llamada a procedimiento, establece *InputOutputType* a SQL_PARAM_INPUT; si el origen de datos devuelve un valor para el parámetro, el controlador lo descarta.  
  
-   SQL_PARAM_INPUT_OUTPUT. El parámetro marca un parámetro de entrada/salida de un procedimiento. Por ejemplo, el parámetro en **{llamar GetEmpDept(?)}**  es un parámetro de entrada y salida que acepta el nombre de un empleado y devuelve el nombre del departamento del empleado.  
  
     Cuando se ejecuta la instrucción, el controlador envía los datos para el parámetro para el origen de datos el \* *ParameterValuePtr* búfer debe contener un valor de entrada válido, o la \* *StrLen_or_IndPtr* búfer debe contener SQL_NULL_DATA, SQL_DATA_AT_EXEC o el resultado de la macro SQL_LEN_DATA_AT_EXEC. Después de ejecuta la instrucción, el controlador devuelve datos para el parámetro a la aplicación; Si el origen de datos no devuelve un valor para un parámetro de entrada/salida, el controlador establece el **StrLen_or_IndPtr* búfer en SQL_NULL_DATA.  
  
    > [!NOTE]  
    >  Cuando una aplicación ODBC 1.0 llama **SQLSetParam** en un controlador ODBC 2.0, el Administrador de controladores se convierte a una llamada a **SQLBindParameter** en el que el *InputOutputType* argumento está establecido en SQL_PARAM_INPUT_OUTPUT.  
  
-   SQL_PARAM_OUTPUT. El parámetro de marca el valor devuelto de un procedimiento o un parámetro de salida de un procedimiento; en cualquier caso, se conocen como *parámetros de salida*. Por ejemplo, el parámetro en **{? = llamar GetNextEmpID}** es un parámetro de salida que devuelve el siguiente identificador de empleado.  
  
     Después de ejecuta la instrucción, el controlador devuelve datos para el parámetro a la aplicación, a menos que la *ParameterValuePtr* y *StrLen_or_IndPtr* argumentos son ambos punteros nulos, en cuyo caso el controlador descarta el valor de salida. Si el origen de datos no devuelve un valor para un parámetro de salida, el controlador establece el **StrLen_or_IndPtr* búfer en SQL_NULL_DATA.  
  
-   SQL_PARAM_INPUT_OUTPUT_STREAM. Indica que se debe transmitir un parámetro de entrada/salida. **SQLGetData** pueden leer valores de parámetro en partes. *BufferLength* se omite porque la longitud del búfer se determinará en la llamada de **SQLGetData**. El valor de la *StrLen_or_IndPtr* debe contener el búfer SQL_NULL_DATA, SQL_DEFAULT_PARAM, SQL_DATA_AT_EXEC o el resultado de la macro SQL_LEN_DATA_AT_EXEC. Un parámetro debe estar enlazado como un parámetro de datos en ejecución (DAE) en la entrada si se transmitirá en la salida. *ParameterValuePtr* puede ser cualquier valor de puntero null no devolverá **SQLParamData** como definido por el usuario de token cuyo valor se pasaron con *ParameterValuePtr* de entrada y salida. Para obtener más información, consulte [recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
-   SQL_PARAM_OUTPUT_STREAM. Igual que SQL_PARAM_INPUT_OUTPUT_STREAM, para un parámetro de salida. **StrLen_or_IndPtr* se omite en la entrada.  
  
 En la tabla siguiente se enumera diferentes combinaciones de *InputOutputType* y **StrLen_or_IndPtr*:  
  
|*InputOutputType*|**StrLen_or_IndPtr*|Resultado|Comente en ParameterValuePtr|  
|-----------------------|----------------------------|-------------|---------------------------------|  
|SQL_PARAM_INPUT|SQL_LEN_DATA_AT_EXEC (*len*) o SQL_DATA_AT_EXEC|Entrada de elementos|*ParameterValuePtr* puede ser cualquier valor de puntero que se devolverá mediante **SQLParamData** como definido por el usuario de token cuyo valor se pasaron con *ParameterValuePtr*.|  
|SQL_PARAM_INPUT|No SQL_LEN_DATA_AT_EXEC (*len*) o SQL_DATA_AT_EXEC|Búfer de enlazado de entrada|*ParameterValuePtr* es la dirección del búfer de entrada.|  
|SQL_PARAM_OUTPUT|Se omite en la entrada.|Búfer de salida enlazada|*ParameterValuePtr* es la dirección del búfer de salida.|  
|SQL_PARAM_OUTPUT_STREAM|Se omite en la entrada.|Salida transmitidos|*ParameterValuePtr* puede ser cualquier valor de puntero, que se devolverá mediante **SQLParamData** como definido por el usuario de token cuyo valor se pasaron con *ParameterValuePtr*.|  
|SQL_PARAM_INPUT_OUTPUT|SQL_LEN_DATA_AT_EXEC (*len*) o SQL_DATA_AT_EXEC|Entrada de elementos y búfer de salida enlazada|*ParameterValuePtr* es la dirección del búfer de salida, que también se devolverán por **SQLParamData** como definido por el usuario de token cuyo valor se pasaron con *ParameterValuePtr*.|  
|SQL_PARAM_INPUT_OUTPUT|No SQL_LEN_DATA_AT_EXEC (*len*) o SQL_DATA_AT_EXEC|Entrada enlazados búfer y el búfer de salida enlazada|*ParameterValuePtr* es la dirección del búfer de entrada/salida compartido.|  
L_PARAM_INPUT_OUTPUT_STREAM|SQL_LEN_DATA_AT_EXEC (*len*) o SQL_DATA_AT_EXEC|Entrada de partes y salida transmitidos|*ParameterValuePtr* puede ser cualquier valor de puntero no nulo, lo que devolverá **SQLParamData** como definido por el usuario de token cuyo valor se pasaron con *ParameterValuePtr* de entrada y de salida.|  
  
> [!NOTE]  
>  El controlador debe decidir qué tipos SQL se permiten cuando una aplicación enlaza un parámetro de entrada / salida o de salida tal y como se transmite por secuencias. El Administrador de controladores no generará un error para un tipo SQL no válido.  
  
## <a name="valuetype-argument"></a>Argumento de tipo de valor  
 El *ValueType* argumento especifica el tipo de datos de C del parámetro. Este argumento establece los campos SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE y SQL_DESC_DATETIME_INTERVAL_CODE de la APD. Debe ser uno de los valores en el [tipos de datos C](../../../odbc/reference/appendixes/c-data-types.md) sección Apéndice D: de tipos de datos.  
  
 Si el *ValueType* argumento es uno de los tipos de datos de intervalo, el campo SQL_DESC_TYPE de la *ParameterNumber* registro de la APD se establece en SQL_INTERVAL, el campo SQL_DESC_CONCISE_TYPE de la APD está establecido en el tipo de datos de intervalo concisa y el campo SQL_DESC_DATETIME_INTERVAL_CODE de la *ParameterNumber* registro se establece en un subcódigo para el tipo de datos de un intervalo específico. (Consulte [tipos de datos de apéndice D:](../../../odbc/reference/appendixes/appendix-d-data-types.md).) El intervalo predeterminado a la precisión (2) y la precisión de segundos de intervalo predeterminado (6), como se establece en los campos SQL_DESC_DATETIME_INTERVAL_PRECISION y SQL_DESC_PRECISION de APD, respectivamente, se usan para los datos. Si cualquier valor predeterminado de precisión no es adecuado, la aplicación debe establecer explícitamente el campo descriptor mediante una llamada a **SQLSetDescField** o **SQLSetDescRec**.  
  
 Si el *ValueType* argumento es uno de los tipos de datos de fecha y hora, el campo SQL_DESC_TYPE de la *ParameterNumber* registro de la APD se establece en SQL_DATETIME, el campo SQL_DESC_CONCISE_TYPE de la *ParameterNumber* registro de la APD se establece en el tipo de datos datetime concisa C y el campo SQL_DESC_DATETIME_INTERVAL_CODE de la *ParameterNumber* registro se establece en un subcódigo para la fecha y hora específica tipo de datos. (Consulte [tipos de datos de apéndice D:](../../../odbc/reference/appendixes/appendix-d-data-types.md).)  
  
 Si el *ValueType* argumento es un tipo de datos SQL_C_NUMERIC, la precisión predeterminada (que es definido por el controlador) y la escala del valor predeterminado (0), como se establece en los campos SQL_DESC_PRECISION y SQL_DESC_SCALE de APD, se usan para los datos. Si el valor predeterminado de precisión o escala no es adecuada, la aplicación debe establecer explícitamente el campo descriptor mediante una llamada a **SQLSetDescField** o **SQLSetDescRec**.  
  
 SQL_C_DEFAULT especifica que el valor del parámetro se transfieren desde el tipo de datos C predeterminado para el tipo de datos SQL especificado con *ParameterType*.  
  
 También puede especificar un tipo de datos C extendido. Para obtener más información, consulte [tipos de datos C en ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 Para obtener más información, consulte [tipos de datos C predeterminado](../../../odbc/reference/appendixes/default-c-data-types.md), [convertir datos de C a tipos de datos SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md), y [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) en tipos de datos de apéndice D:.  
  
## <a name="parametertype-argument"></a>Argumento de valor ParameterType  
 Debe ser uno de los valores enumerados en la [tipos de datos SQL](../../../odbc/reference/appendixes/sql-data-types.md) sección del apéndice D: tipos de datos, o bien debe ser un valor específico del controlador. Este argumento establece los campos SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE y SQL_DESC_DATETIME_INTERVAL_CODE de la IPD.  
  
 Si el *ParameterType* argumento es uno de los identificadores de fecha y hora, se establece el campo SQL_DESC_TYPE de la IPD en SQL_DATETIME, el campo SQL_DESC_CONCISE_TYPE de la IPD se establece en el tipo de datos SQL concisa de fecha y hora y el SQL_DESC_ Campo DATETIME_INTERVAL_CODE se establece en el valor de subcódigo de datetime adecuado.  
  
 Si *ParameterType* es uno de los identificadores de intervalo, se establece el campo SQL_DESC_TYPE de la IPD en SQL_INTERVAL, el campo SQL_DESC_CONCISE_TYPE de la IPD se establece en el tipo de datos de intervalo SQL conciso y el SQL_DESC_DATETIME_ Campo INTERVAL_CODE de la IPD está establecido para el subcódigo de intervalo adecuado. El campo SQL_DESC_DATETIME_INTERVAL_PRECISION de la IPD está establecido en la precisión de intervalo inicial y el campo SQL_DESC_PRECISION se establece en la precisión de segundos del intervalo, si procede. Si el valor predeterminado de SQL_DESC_DATETIME_INTERVAL_PRECISION o SQL_DESC_PRECISION no es adecuado, la aplicación debe establecer explícitamente, mediante una llamada a **SQLSetDescField**. Para obtener más información acerca de cualquiera de estos campos, vea [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 Si el *ValueType* argumento es un tipo de datos SQL_NUMERIC, la precisión predeterminada (que es definido por el controlador) y la escala del valor predeterminado (0), como se establece en los campos SQL_DESC_PRECISION y SQL_DESC_SCALE de IPD, se usan para los datos. Si el valor predeterminado de precisión o escala no es adecuada, la aplicación debe establecer explícitamente el campo descriptor mediante una llamada a **SQLSetDescField** o **SQLSetDescRec**.  
  
 Para obtener información acerca de cómo se convierten los datos, vea [convertir datos de C a tipos de datos SQL](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md) y [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) en tipos de datos de apéndice D:.  
  
## <a name="columnsize-argument"></a>ColumnSize argumento  
 El *ColumnSize* argumento especifica el tamaño de la columna o expresión que se corresponde con el marcador de parámetro, la longitud de datos, o ambos. Este argumento establece distintos campos de IPD, dependiendo del tipo de datos SQL (el *ParameterType* argumento). Las siguientes reglas se aplican a esta asignación:  
  
-   Si *ParameterType* es SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY o uno de los concisa datetime o intervalo de tipos de datos SQL, el campo SQL_DESC_LENGTH de la IPD se establece en el valor de  *ColumnSize*. (Para obtener más información, consulte el [tamaño de la columna, dígitos decimales, transferencia de longitud de bytes y el tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) sección en tipos de datos de apéndice D:.)  
  
-   Si *ParameterType* es SQL_DECIMAL de ODBC, SQL_NUMERIC, SQL_FLOAT, SQL_REAL o SQL_DOUBLE, el campo SQL_DESC_PRECISION de la IPD se establece en el valor de *ColumnSize*.  
  
-   Para otros tipos de datos, el *ColumnSize* argumento se omite.  
  
 Para obtener más información, vea "Pasar valores de parámetro" y SQL_DATA_AT_EXEC en "*StrLen_or_IndPtr* argumento."  
  
## <a name="decimaldigits-argument"></a>ColumnSize argumento  
 Si *ParameterType* es SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP, SQL_INTERVAL_SECOND, SQL_INTERVAL_DAY_TO_SECOND, SQL_INTERVAL_HOUR_TO_SECOND o SQL_INTERVAL_MINUTE_TO_SECOND, se establece el campo SQL_DESC_PRECISION de la IPD para *ColumnSize*. Si *ParameterType* es SQL_NUMERIC o SQL_DECIMAL de ODBC, el campo SQL_DESC_SCALE de la IPD está establecido en *ColumnSize*. Para los demás tipos de datos, el *ColumnSize* argumento se omite.  
  
## <a name="parametervalueptr-argument"></a>Argumento de ParameterValuePtr  
 El *ParameterValuePtr* argumento apunta a un búfer que, cuando **SQLExecute** o **SQLExecDirect** se llama, contiene los datos reales para el parámetro. Los datos deben tener el formato especificado por el *ValueType* argumento. Este argumento establece el campo SQL_DESC_DATA_PTR de la APD. Una aplicación puede establecer la *ParameterValuePtr* argumento pasado a un puntero nulo, siempre y cuando  *\*StrLen_or_IndPtr* es SQL_NULL_DATA o SQL_DATA_AT_EXEC. (Se aplica solo a entrada/salida parámetros de entrada o).  
  
 Si \* *StrLen_or_IndPtr* es el resultado de la SQL_LEN_DATA_AT_EXEC (*longitud*) macro o SQL_DATA_AT_EXEC, a continuación, *ParameterValuePtr* es un valor de puntero definido por la aplicación que está asociado con el parámetro. Se devuelve a la aplicación a través de **SQLParamData**. Por ejemplo, *ParameterValuePtr* podría ser un token distinto de cero, como un número de parámetro, un puntero a datos o un puntero a una estructura que la aplicación usa para enlazar parámetros de entrada. Sin embargo, tenga en cuenta que si el parámetro es un parámetro de entrada/salida, *ParameterValuePtr* debe ser un puntero a un búfer donde se almacenará el valor de salida. Si el valor del atributo de instrucción de SQL_ATTR_PARAMSET_SIZE es mayor que 1, la aplicación puede utilizar el valor al que señala el atributo de instrucciones SQL_ATTR_PARAMS_PROCESSED_PTR junto con el *ParameterValuePtr* argumento pasado. Por ejemplo, *ParameterValuePtr* puede señalar a una matriz de valores y la aplicación podría usar el valor al que señala SQL_ATTR_PARAMS_PROCESSED_PTR para recuperar el valor correcto de la matriz. Para obtener más información, vea "Pasar valores de parámetro" más adelante en esta sección.  
  
 Si el *InputOutputType* argumento es SQL_PARAM_INPUT_OUTPUT o SQL_PARAM_OUTPUT, *ParameterValuePtr* apunta a un búfer en el que el controlador devuelve el valor de salida. Si el procedimiento devuelve uno o varios conjuntos de resultados, el \* *ParameterValuePtr* búfer no está garantizado que puede establecer hasta que se han procesado todos los recuentos de fila/conjuntos de resultados. Si el búfer no se establece hasta que se complete el procesamiento, los parámetros de salida y valores devueltos no están disponibles hasta que **SQLMoreResults** devuelve SQL_NO_DATA. Al llamar a **SQLCloseCursor** o **SQLFreeStmt** con una opción de SQL_CLOSE hará que estos valores se descarten.  
  
 Si es mayor que 1, el valor del atributo de instrucción de SQL_ATTR_PARAMSET_SIZE *ParameterValuePtr* señala a una matriz. Una sola instrucción SQL procesa la matriz completa de valores de entrada para un parámetro de entrada o de entrada/salida y devuelve una matriz de valores de salida para una entrada/salida o parámetro de salida.  
  
## <a name="bufferlength-argument"></a>Argumento de BufferLength  
 Para datos de caracteres y binarios C, el *BufferLength* argumento especifica la longitud de la \* *ParameterValuePtr* búfer (si es un elemento único) o la longitud de un elemento en el \* *ParameterValuePtr* matriz (si el valor del atributo de instrucción de SQL_ATTR_PARAMSET_SIZE es mayor que 1). Este argumento establece el campo de registro SQL_DESC_OCTET_LENGTH de la APD. Si la aplicación especifica varios valores, *BufferLength* se utiliza para determinar la ubicación de los valores de la **ParameterValuePtr* matriz, tanto de entrada y de salida. Para los parámetros de entrada/salida y salidas, se utiliza para determinar si se debe truncar los datos de caracteres y binarios C en la salida:  
  
-   Para los datos de carácter C, si el número de bytes disponible para devolver es mayor o igual que *BufferLength*, los datos de \* *ParameterValuePtr* se trunca a  *BufferLength* menos la longitud de un carácter de terminación null y termina en null el controlador.  
  
-   Para los datos binarios de C, si es mayor que el número de bytes disponible para devolver *BufferLength*, los datos de \* *ParameterValuePtr* se trunca a *BufferLength*bytes.  
  
 Para los demás tipos de datos de C, el *BufferLength* argumento se omite. La longitud de la \* *ParameterValuePtr* búfer (si es un elemento único) o la longitud de un elemento en el \* *ParameterValuePtr* matriz (si la aplicación llama a  **SQLSetStmtAttr** con una *atributo* argumento de SQL_ATTR_PARAMSET_SIZE para especificar varios valores para cada parámetro) se supone que la longitud del tipo de datos C.  
  
 Para salida transmitidos o los parámetros de entrada/salida por secuencias, el *BufferLength* argumento se omite porque la longitud del búfer se especifica en **SQLGetData**.  
  
> [!NOTE]  
>  Cuando una aplicación ODBC 1.0 llama **SQLSetParam** en una aplicación ODBC 3. *x* controlador, el Administrador de controladores se convierte en una llamada a **SQLBindParameter** en el que el *BufferLength* argumento siempre es SQL_SETPARAM_VALUE_MAX. Dado que el Administrador de controladores devuelve un error si una aplicación ODBC 3. *x* conjuntos de aplicaciones *BufferLength* a SQL_SETPARAM_VALUE_MAX, una aplicación ODBC 3. *x* controlador puede emplear para determinar cuando se llama por una aplicación ODBC 1.0.  
  
> [!NOTE]  
>  En **SQLSetParam**, la forma en que una aplicación especifica la longitud de la **ParameterValuePtr* almacenar en búfer para que el controlador puede devolver caracteres o datos binarios y la manera en que una aplicación envía un matriz de caracteres o valores de parámetro binario para el controlador, se definen por controlador.  
  
## <a name="strlenorindptr-argument"></a>Argumento de StrLen_or_IndPtr  
 El *StrLen_or_IndPtr* argumento apunta a un búfer que, cuando **SQLExecute** o **SQLExecDirect** se llama, contiene uno de los siguientes. (Este argumento establece los campos de registros SQL_DESC_OCTET_LENGTH_PTR y SQL_DESC_INDICATOR_PTR de los punteros de parámetro de la aplicación).  
  
-   La longitud del valor del parámetro almacenado en **ParameterValuePtr*. Esto se omite excepto los datos de caracteres o binarios C.  
  
-   SQL_NTS. El valor del parámetro es una cadena terminada en null.  
  
-   SQL_NULL_DATA. El valor del parámetro es NULL.  
  
-   SQL_DEFAULT_PARAM. Un procedimiento consiste en usar el valor predeterminado de un parámetro, en lugar de un valor recuperado de la aplicación. Este valor solo es válido en un procedimiento llamado en la sintaxis canónica de ODBC y, a continuación, solo si la *InputOutputType* argumento es SQL_PARAM_INPUT_OUTPUT_STREAM, SQL_PARAM_INPUT_OUTPUT o SQL_PARAM_INPUT. Cuando \* *StrLen_or_IndPtr* es SQL_DEFAULT_PARAM, el *ValueType*, *ParameterType*, *ColumnSize*,  *ColumnSize*, *BufferLength*, y *ParameterValuePtr* argumentos se omiten para parámetros de entrada y se utilizan únicamente para definir el valor del parámetro de salida para la entrada / parámetros de salida.  
  
-   El resultado de la SQL_LEN_DATA_AT_EXEC (*longitud*) macro. Los datos para el parámetro se enviará con **SQLPutData**. Si el *ParameterType* argumento es SQL_LONGVARBINARY, SQL_LONGVARCHAR o un valor largo, tipo de datos específico del origen de datos, y el controlador devuelve "Y" para el tipo de información de SQL_NEED_LONG_DATA_LEN en **SQLGetInfo**, *longitud* es el número de bytes de datos que se envía para el parámetro; en caso contrario, *longitud* debe ser un valor no negativo y se omite. Para obtener más información, vea "Pasar valores de parámetro" más adelante en esta sección.  
  
     Por ejemplo, para especificar que se enviarán 10.000 bytes de datos con **SQLPutData** en una o más llamadas, para un parámetro SQL_LONGVARCHAR, una aplicación establece **StrLen_or_IndPtr* en SQL_LEN_DATA_AT_EXEC ( 10000).  
  
-   SQL_DATA_AT_EXEC. Los datos para el parámetro se enviará con **SQLPutData**. Este valor se utiliza en aplicaciones de ODBC 1.0 cuando llama a ODBC 3. *x* controladores. Para obtener más información, vea "Pasar valores de parámetro" más adelante en esta sección.  
  
 Si *StrLen_or_IndPtr* es un puntero nulo, el controlador da por hecho que todos los valores de parámetro de entrada son distintos de NULL y que los datos de caracteres y binarios están terminada en null. Si *InputOutputType* es SQL_PARAM_OUTPUT o SQL_PARAM_OUTPUT_STREAM y *ParameterValuePtr* y *StrLen_or_IndPtr* son ambos punteros nulos, el controlador descarta el valor de salida.  
  
> [!NOTE]  
>  Se recomienda no usar al especificar un puntero nulo para los desarrolladores de aplicaciones *StrLen_or_IndPtr* cuando el tipo de datos del parámetro es SQL_C_BINARY. Para asegurarse de que un controlador de forma inesperada no truncar datos SQL_C_BINARY, *StrLen_or_IndPtr* debe contener un puntero a un valor de longitud válida.  
  
 Si el *InputOutputType* argumento es SQL_PARAM_INPUT_OUTPUT, SQL_PARAM_OUTPUT, SQL_PARAM_INPUT_OUTPUT_STREAM o SQL_PARAM_OUTPUT_STREAM, *StrLen_or_IndPtr* apunta a un búfer en el que el el controlador devuelve SQL_NULL_DATA, el número de bytes disponible para devolver en \* *ParameterValuePtr* (excepto el byte de finalización en null de los datos de caracteres), o SQL_NO_TOTAL (si el número de bytes disponible para valor devuelto no se puede determinar). Si el procedimiento devuelve uno o varios conjuntos de resultados, el **StrLen_or_IndPtr* búfer no está garantizado que puede establecer hasta que todos los resultados se han capturado.  
  
 Si es mayor que 1, el valor del atributo de instrucción de SQL_ATTR_PARAMSET_SIZE *StrLen_or_IndPtr* señala a una matriz de valores SQLLEN. Estos pueden ser cualquiera de los valores enumerados anteriormente en esta sección y se procesan con una sola instrucción SQL.  
  
## <a name="passing-parameter-values"></a>Pasar valores de parámetro  
 Una aplicación puede pasar el valor de un parámetro o en el \* *ParameterValuePtr* búfer o con una o más llamadas a **SQLPutData**. Parámetros cuyos datos se pasan con **SQLPutData** se conocen como *datos en ejecución* parámetros. Estos se utilizan normalmente para enviar datos de parámetros SQL_LONGVARBINARY y SQL_LONGVARCHAR y se pueden combinar con otros parámetros.  
  
 Para pasar valores de parámetro, una aplicación realiza la siguiente secuencia de pasos:  
  
1.  Llamadas **SQLBindParameter** para cada parámetro de enlace de búferes para el valor del parámetro (*ParameterValuePtr* argumento) y longitud/indicador (*StrLen_or_IndPtr* argumento). Para los parámetros de datos en ejecución, *ParameterValuePtr* es un valor de puntero definido por la aplicación como un número de parámetro o un puntero a datos. El valor se devolverá más adelante y puede usarse para identificar el parámetro.  
  
2.  Coloca los valores para parámetros de entrada y de entrada/salida en el \* *ParameterValuePtr* y **StrLen_or_IndPtr* búferes:  
  
    -   Para los parámetros normales, la aplicación coloca el valor del parámetro en el \* *ParameterValuePtr* búfer y la longitud de ese valor en el **StrLen_or_IndPtr* búfer. Para obtener más información, consulte [valores de parámetro de configuración](../../../odbc/reference/develop-app/setting-parameter-values.md).  
  
    -   Para los parámetros de datos en ejecución, la aplicación coloca el resultado de la SQL_LEN_DATA_AT_EXEC (*longitud*) macro (al llamar a un controlador ODBC 2.0) en el **StrLen_or_IndPtr* búfer.  
  
3.  Llamadas **SQLExecute** o **SQLExecDirect** para ejecutar la instrucción SQL.  
  
    -   Si no hay ningún parámetro de datos en ejecución, el proceso es completando.  
  
    -   Si hay algún parámetro de datos en ejecución, la función devuelve SQL_NEED_DATA.  
  
4.  Llamadas **SQLParamData** para recuperar el valor definido por la aplicación especificado en el *ParameterValuePtr* argumento de **SQLBindParameter** para el primer parámetro de datos en ejecución para procesarse. **SQLParamData** devuelve SQL_NEED_DATA.  
  
    > [!NOTE]  
    >  Aunque los parámetros de datos en ejecución son similares a las columnas de datos en ejecución, el valor devuelto por **SQLParamData** es diferente para cada uno de ellos. Parámetros de datos en ejecución son parámetros de una instrucción SQL para que los datos se envían con **SQLPutData** cuando se ejecuta la instrucción con **SQLExecDirect** o **SQLExecute**. Que están enlazados con **SQLBindParameter**. El valor devuelto por **SQLParamData** se pasa un valor de puntero a **SQLBindParameter** en el *ParameterValuePtr* argumento. Columnas de datos en ejecución son columnas de un conjunto de filas para el que los datos se envían con **SQLPutData** cuando una fila se actualiza o se agrega con **SQLBulkOperations** o actualizados con **SQLSetPos**. Que están enlazados con **SQLBindCol**. El valor devuelto por **SQLParamData** es la dirección de la fila en el **TargetValuePtr* búfer (establecido mediante una llamada a **SQLBindCol**) que se está procesando.  
  
5.  Llamadas **SQLPutData** una o más veces para enviar los datos para el parámetro. Se necesita más de una llamada si el valor de datos es mayor que el \* *ParameterValuePtr* especificado en el búfer **SQLPutData**; varias llamadas a **SQLPutData**para el mismo parámetro se permiten solo cuando se envían datos de carácter C a una columna con un tipo de datos de específico del origen de datos, binarios o caracteres o al enviar datos binarios de C a una columna con un carácter, binario, o de tipo de datos específico del origen de datos.  
  
6.  Llamadas **SQLParamData** nuevo para indicar que se han enviado todos los datos para el parámetro.  
  
    -   Si hay más de los parámetros de datos en ejecución, **SQLParamData** devuelve SQL_NEED_DATA y el valor definido por la aplicación para el siguiente parámetro de datos en ejecución para procesarse. La aplicación repite los pasos 4 y 5.  
  
    -   Si no hay nada más parámetros de datos en ejecución, el proceso es completando. Si la instrucción se ejecutó correctamente, **SQLParamData** devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO; si se produce un error en la ejecución, devuelve SQL_ERROR. En este momento, **SQLParamData** puede devolver cualquier SQLSTATE, que puede ser devueltos por la función que se usa para ejecutar la instrucción (**SQLExecDirect** o **SQLExecute**).  
  
         Valores de salida para los parámetros de entrada/salida o de salida están disponibles en la \* *ParameterValuePtr* y **StrLen_or_IndPtr* almacena en búfer después de la aplicación recupera todos los conjuntos de resultados generado por la instrucción.  
  
 Al llamar a **SQLExecute** o **SQLExecDirect** coloca la instrucción en un estado SQL_NEED_DATA. En este punto, la aplicación puede llamar solo **SQLCancel**, **SQLGetDiagField**, **SQLGetDiagRec**, **SQLGetFunctions**, **SQLParamData**, o **SQLPutData** con la instrucción o el *identificador de conexión* asociados con la instrucción. Si llama a cualquier otra función con la instrucción o la conexión asociada con la instrucción, la función devuelve SQLSTATE HY010 (error de secuencia de función). Las hojas de instrucción la SQL_NEED_DATA estado cuando **SQLParamData** o **SQLPutData** devuelve un error, **SQLParamData** devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, o se cancela la instrucción.  
  
 Si la aplicación llama **SQLCancel** mientras el controlador todavía necesita datos para los parámetros de datos en ejecución, el controlador cancela la ejecución de la instrucción; a continuación, puede llamar la aplicación **SQLExecute** o  **SQLExecDirect** nuevo.  
  
## <a name="retrieving-streamed-output-parameters"></a>Recuperar parámetros de salida transmitidos  
 Cuando una aplicación establece *InputOutputType* SQL_PARAM_INPUT_OUTPUT_STREAM o SQL_PARAM_OUTPUT_STREAM, el valor del parámetro de salida se debe recuperar uno o más llamadas a **SQLGetData**. Cuando el controlador tiene un valor de parámetro de salida transmitidos se devuelven a la aplicación, devolverá SQL_PARAM_DATA_AVAILABLE en respuesta a una llamada a las funciones siguientes: **SQLMoreResults**, **SQLExecute**, y **SQLExecDirect**. Una aplicación llama **SQLParamData** para determinar qué valor de parámetro está disponible.  
  
 Para obtener más información sobre SQL_PARAM_DATA_AVAILABLE y los parámetros de salida transmitidos, consulte [recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md).  
  
## <a name="using-arrays-of-parameters"></a>Utilizar matrices de parámetros  
 Cuando una aplicación prepara una instrucción con marcadores de parámetros y pasa una matriz de parámetros, hay dos maneras diferentes, que esto se puede ejecutar. Una manera es el controlador se basan en las capacidades de procesamiento de la matriz del back-end, en el que caso la instrucción con la matriz de parámetros se trata como una unidad atómica. Oracle es un ejemplo de un origen de datos que admite capacidades de procesamiento de la matriz. Otra manera de implementar esta característica es para que el controlador generar un lote de instrucciones SQL, una instrucción SQL para cada conjunto de parámetros de la matriz de parámetros y ejecutar el lote. Las matrices de parámetros no se puede usar con un **WHERE CURRENT OF de actualización** instrucción.  
  
 Cuando se procesa una matriz de parámetros, recuentos de/filas de conjuntos de resultados individuales (uno para cada conjunto de parámetros) pueden estar disponibles o los recuentos de filas/conjuntos de resultados se pueden acumular en uno. Opción el SQL_PARAM_ARRAY_ROW_COUNTS **SQLGetInfo** indica si están disponibles para cada conjunto de parámetros (SQL_PARC_BATCH) de recuentos de filas o recuento de solo filas está disponible (SQL_PARC_NO_BATCH).  
  
 Opción el SQL_PARAM_ARRAY_SELECTS **SQLGetInfo** indica si hay un conjunto de resultados para cada conjunto de parámetros (SQL_PAS_BATCH) o solo un conjunto de resultados está disponible (SQL_PAS_NO_BATCH). Si el controlador no permite una instrucción de generación de conjunto de resultados se puede ejecutar con una matriz de parámetros, SQL_PARAM_ARRAY_SELECTS devuelve SQL_PAS_NO_SELECT.  
  
 Para obtener más información, consulte [función SQLGetInfo](../../../odbc/reference/syntax/sqlgetinfo-function.md).  
  
 Para admitir las matrices de parámetros, se establece el atributo de instrucción de SQL_ATTR_PARAMSET_SIZE para especificar el número de valores para cada parámetro. Si el campo es mayor que 1, los campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR y SQL_DESC_OCTET_LENGTH_PTR de la APD deben apuntar a las matrices. La cardinalidad de cada matriz es igual al valor de SQL_ATTR_PARAMSET_SIZE.  
  
 El campo SQL_DESC_ROWS_PROCESSED_PTR de la APD apunta a un búfer que contiene el número de conjuntos de parámetros que se han procesado, incluidos los juegos de error. Cuando se procesa cada conjunto de parámetros, el controlador almacena un nuevo valor en el búfer. No se devolverá si se trata de un puntero nulo. Cuando se utilizan las matrices de parámetros, se rellena el valor al que señala el campo SQL_DESC_ROWS_PROCESSED_PTR de la APD incluso si se devuelve SQL_ERROR por la función de configuración. Si se devuelve SQL_NEED_DATA, se establece el valor al que señala el campo SQL_DESC_ROWS_PROCESSED_PTR de la APD en el conjunto de parámetros que se está procesando.  
  
 ¿Qué ocurre cuando se enlaza una matriz de parámetros y un **WHERE CURRENT OF de actualización** se ejecuta la instrucción está definida por el controlador.  
  
## <a name="column-wise-parameter-binding"></a>El enlace de parámetro  
 En el enlace, la aplicación enlaza el parámetro independiente y matrices de longitud/indicador para cada parámetro.  
  
 Para utilizar el enlace, la aplicación primero establece el atributo de instrucción SQL_ATTR_PARAM_BIND_TYPE en SQL_PARAM_BIND_BY_COLUMN. (Es el valor predeterminado.) Para que cada columna esté enlazada, la aplicación realiza los pasos siguientes:  
  
1.  Asigna una matriz de búferes de parámetros.  
  
2.  Asigna una matriz de búferes de longitud/indicador.  
  
    > [!NOTE]  
    >  Si la aplicación escribe directamente a descriptores cuando se usa el enlace, matrices independientes pueden usarse para los datos de longitud y el indicador.  
  
3.  Llamadas **SQLBindParameter** con los argumentos siguientes:  
  
    -   *Tipo de valor* es el tipo C de un único elemento de la matriz de búferes de parámetros.  
  
    -   *ParameterType* es el tipo SQL del parámetro.  
  
    -   *ParameterValuePtr* es la dirección de la matriz de búferes de parámetros.  
  
    -   *BufferLength* es el tamaño de un único elemento de la matriz de búferes de parámetros. El *BufferLength* argumento se omite cuando los datos son datos de longitud fija.  
  
    -   *StrLen_or_IndPtr* es la dirección de la matriz de longitud/indicador.  
  
 Para obtener más información sobre cómo se usa esta información, vea "ParameterValuePtr argumento" en "Comentarios" más adelante en esta sección. Para obtener más información sobre el enlace de parámetros, vea [matrices de parámetros de enlace](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md).  
  
## <a name="row-wise-parameter-binding"></a>El enlace de parámetro  
 En el enlace de modo de fila, la aplicación define una estructura que contiene el parámetro y longitud/indicador búferes para cada parámetro que enlazarse.  
  
 Para utilizar el enlace, la aplicación realiza los pasos siguientes:  
  
1.  Define una estructura que contenga un único conjunto de parámetros (incluidos los búferes de parámetro y el indicador de longitud) y asigna una matriz de estas estructuras.  
  
    > [!NOTE]  
    >  Si la aplicación escribe directamente a descriptores cuando se usa el enlace de modo de fila, campos independientes se pueden usar para los datos de longitud y el indicador.  
  
2.  Establece el atributo de instrucción de SQL_ATTR_PARAM_BIND_TYPE en el tamaño de la estructura que contiene un único conjunto de parámetros o hasta el tamaño de una instancia de un búfer en el que se enlazarán los parámetros. La longitud debe incluir el espacio para todos los parámetros enlazados y cualquier relleno de la estructura o el búfer, para asegurarse de que cuando la dirección de un parámetro dependiente se incrementa con la longitud especificada, el resultado señalará al principio del mismo parámetro en el fila siguiente. Cuando se usa el *sizeof* operador en ANSI C, se garantiza que este comportamiento.  
  
3.  Llamadas **SQLBindParameter** con los argumentos siguientes para cada parámetro enlazar:  
  
    -   *Tipo de valor* es el tipo del miembro de búfer de parámetro se puede enlazar a la columna.  
  
    -   *ParameterType* es el tipo SQL del parámetro.  
  
    -   *ParameterValuePtr* es la dirección del miembro de búfer de parámetro en el primer elemento de matriz.  
  
    -   *BufferLength* es el tamaño del miembro de búfer de parámetro.  
  
    -   *StrLen_or_IndPtr* es la dirección del miembro de longitud/indicador esté enlazado.  
  
 Para obtener más información sobre cómo se usa esta información, vea "*ParameterValuePtr* argumento," más adelante en esta sección. Para obtener más información sobre el enlace de parámetros, vea la [matrices de parámetros de enlace](../../../odbc/reference/develop-app/binding-arrays-of-parameters.md).  
  
## <a name="error-information"></a>Información del error  
 Si un controlador no implementa matrices de parámetros como lotes (la opción SQL_PARAM_ARRAY_ROW_COUNTS es igual a SQL_PARC_NO_BATCH), se tratan situaciones de error como si se ejecuta una instrucción. Si el controlador implementa matrices de parámetros como lotes, una aplicación puede usar el campo de encabezado SQL_DESC_ARRAY_STATUS_PTR de la IPD para determinar qué parámetro de una instrucción SQL o qué parámetro en una matriz de parámetros debe  **SQLExecDirect** o **SQLExecute** para devolver un error. Este campo contiene información de estado para cada fila de valores de parámetro. Si el campo indica que se ha producido un error, los campos de la estructura de datos de diagnóstico indicarán el número de fila y los parámetros del parámetro que no se pudo. El número de elementos de la matriz se definirá en el campo de encabezado SQL_DESC_ARRAY_SIZE en el APD, que se puede establecer el atributo de instrucción SQL_ATTR_PARAMSET_SIZE.  
  
> [!NOTE]  
>  El campo de encabezado SQL_DESC_ARRAY_STATUS_PTR en el APD se utiliza para pasar por alto los parámetros. Para obtener más información acerca de la omisión de parámetros, vea la sección siguiente, "Se omitirá un conjunto de parámetros".  
  
 Cuando **SQLExecute** o **SQLExecDirect** devuelve SQL_ERROR, los elementos de la matriz señalada por el campo SQL_DESC_ARRAY_STATUS_PTR en la IPD contendrá SQL_PARAM_ERROR, SQL_PARAM_SUCCESS, SQL_ PARAM_SUCCESS_WITH_INFO, SQL_PARAM_UNUSED o SQL_PARAM_DIAG_UNAVAILABLE.  
  
 Para cada elemento de esta matriz, la estructura de datos de diagnóstico contiene uno o más registros de estado. El campo SQL_DIAG_ROW_NUMBER de la estructura indica el número de fila de los valores de parámetro que provocó el error. Si es posible determinar el parámetro concreto en una fila de parámetros que se produjo el error, debe escribir el número de parámetro en el campo SQL_DIAG_COLUMN_NUMBER.  
  
 SQL_PARAM_UNUSED aparece cuando no se ha utilizado un parámetro porque se produjo un error en un parámetro anterior que fuerza **SQLExecute** o **SQLExecDirect** para anular la operación. Por ejemplo, si no hay parámetros de 50 y un error al ejecutar el conjunto de parámetros que ha causado cuadragésimo **SQLExecute** o **SQLExecDirect** anular, a continuación, se escribe SQL_PARAM_UNUSED en el matriz de Estados para los parámetros 41 a través de 50.  
  
 SQL_PARAM_DIAG_UNAVAILABLE aparece cuando el controlador trata las matrices de parámetros como una unidad monolítica, por lo que no genera este nivel de parámetro individual de información de error.  
  
 Algunos errores en el procesamiento de un único conjunto de parámetros que el procesamiento de los siguientes conjuntos de parámetros de la matriz para detener. Otros errores no influyen en el procesamiento de los parámetros siguientes. Los errores detendrán el procesamiento está definida por el controlador. Si no se detiene el procesamiento, se procesan todos los parámetros de la matriz, se devuelve SQL_SUCCESS_WITH_INFO como resultado el error y el búfer definido por SQL_ATTR_PARAMS_PROCESSED_PTR se establece en el número total de conjuntos de parámetros procesados (tal como se define mediante el Atributo de instrucción SQL_ATTR_PARAMSET_SIZE), que incluye conjuntos de error.  
  
> [!CAUTION]  
>  Comportamiento ODBC cuando se produce un error en el procesamiento de una matriz de parámetros es diferente en ODBC 3. *x* de lo que era en ODBC 2. *x*. En ODBC 2. *x*, la función devuelve SQL_ERROR y procesamiento dejaron. El búfer señalado por el *pirow* argumento de **SQLParamOptions** contiene el número de la fila de error. En ODBC 3. *x*, la función devuelve SQL_SUCCESS_WITH_INFO y procesamiento mayo o detenerse o continuar. Si continúa, el búfer especificado por SQL_ATTR_PARAMS_PROCESSED_PTR se establecerá en el valor de todos los parámetros procesados, los que se generó un error incluidos. Este cambio de comportamiento puede causar problemas a las aplicaciones existentes.  
  
 Cuando **SQLExecute** o **SQLExecDirect** devuelve antes de completar el procesamiento de todos los conjuntos de parámetros en una matriz de parámetros, como cuando se devuelve SQL_ERROR o SQL_NEED_DATA, contiene la matriz de Estados Estados de los parámetros que ya se ha procesado. La ubicación señalada por el campo SQL_DESC_ROWS_PROCESSED_PTR en la IPD contiene el número de fila en la matriz de parámetros que produjo el código de error SQL_ERROR o SQL_NEED_DATA. Cuando se envía una matriz de parámetros a una instrucción SELECT, la disponibilidad de los valores de la matriz de estado está definida por el controlador; pueden estar disponibles después de que se haya ejecutado la instrucción o como resultado se capturan los conjuntos.  
  
## <a name="ignoring-a-set-of-parameters"></a>Se omitirá un conjunto de parámetros  
 El campo SQL_DESC_ARRAY_STATUS_PTR de la APD (según lo establecido por el atributo de instrucciones SQL_ATTR_PARAM_STATUS_PTR) se puede utilizar para indicar que se debe omitir un conjunto de parámetros enlazados en una instrucción SQL. Para dirigir el controlador para pasar por alto uno o varios conjuntos de parámetros durante la ejecución, una aplicación debe seguir estos pasos:  
  
1.  Llame a **SQLSetDescField** para establecer el campo de encabezado SQL_DESC_ARRAY_STATUS_PTR de la APD para que apunte a una matriz de valores SQLUSMALLINT para que contenga información de estado. Este campo también se puede establecer mediante una llamada a **SQLSetStmtAttr** con una *atributo* de SQL_ATTR_PARAM_OPERATION_PTR, que permite a una aplicación establecer el campo sin tener que obtener un identificador de descriptor.  
  
2.  Establezca cada elemento de la matriz que se define en el campo SQL_DESC_ARRAY_STATUS_PTR de la APD en uno de dos valores:  
  
    -   SQL_PARAM_IGNORE, para indicar que la fila está excluida de la ejecución de la instrucción.  
  
    -   SQL_PARAM_PROCEED, para indicar que la fila se incluye en la ejecución de la instrucción.  
  
3.  Llame a **SQLExecDirect** o **SQLExecute** para ejecutar la instrucción preparada.  
  
 Las siguientes reglas se aplican a la matriz que se define en el campo SQL_DESC_ARRAY_STATUS_PTR de la APD:  
  
-   El puntero se establece en null de forma predeterminada.  
  
-   Si el puntero es null, se usan todos los conjuntos de parámetros, como si todos los elementos se han establecido en SQL_ROW_PROCEED.  
  
-   Si se establece un elemento en SQL_PARAM_PROCEED no garantiza que la operación utilizará ese conjunto concreto de parámetros.  
  
-   SQL_PARAM_PROCEED se define como 0 en el archivo de encabezado.  
  
 Una aplicación puede establecer el campo SQL_DESC_ARRAY_STATUS_PTR en el APD para que apunte a la misma matriz como que señala en el campo SQL_DESC_ARRAY_STATUS_PTR en IRD. Esto es útil al enlazar parámetros a los datos de fila. A continuación, se omiten los parámetros según el estado de la fila de datos. Además de SQL_PARAM_IGNORE, los siguientes códigos de provocar un parámetro en una instrucción SQL que se omitan: SQL_ROW_DELETED, SQL_ROW_UPDATED y SQL_ROW_ERROR. Además de SQL_PARAM_PROCEED, los siguientes códigos de que una instrucción SQL continuar: SQL_ROW_SUCCESS, SQL_ROW_SUCCESS_WITH_INFO y SQL_ROW_ADDED.  
  
## <a name="rebinding-parameters"></a>Volver a enlazar parámetros  
 Una aplicación puede realizar cualquiera de las dos operaciones para cambiar un enlace:  
  
-   Llame a **SQLBindParameter** para especificar un nuevo enlace para una columna que ya está enlazado. El controlador sobrescribe el enlace antiguo con uno nuevo.  
  
-   Especifique un desplazamiento que se va a agregar a la dirección de búfer que se especificó en la llamada de enlace a **SQLBindParameter**. Para obtener más información, vea la sección siguiente, "Volver a enlazar con desplazamientos".  
  
## <a name="rebinding-with-offsets"></a>Volver a enlazar con desplazamientos  
 Volver a enlazar de parámetros es especialmente útil cuando una aplicación tiene una configuración de área de búfer que puede contener muchos parámetros pero una llamada a **SQLExecDirect** o **SQLExecute** utiliza solo algunos de los parámetros. El espacio restante en el área del búfer puede usarse para el siguiente conjunto de parámetros modificando el enlace existente por un desplazamiento.  
  
 El campo de encabezado SQL_DESC_BIND_OFFSET_PTR en el APD apunta el desplazamiento de enlace. Si el campo no es null, el controlador desreferencia el puntero y, si ninguno de los valores de los campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR y SQL_DESC_OCTET_LENGTH_PTR es un puntero nulo, agrega el valor sin referencia a esos campos en el descriptor registros en tiempo de ejecución. Los nuevos valores de puntero se utilizan cuando se ejecutan las instrucciones SQL. El desplazamiento sigue siendo válido después de volver a enlazar. Dado que SQL_DESC_BIND_OFFSET_PTR es un puntero a la posición de desplazamiento en lugar de la posición de desplazamiento, una aplicación puede cambiar la posición de desplazamiento directamente, sin tener que llamar [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) o [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md) a cambiar el campo descriptor. El puntero se establece en null de forma predeterminada. El campo SQL_DESC_BIND_OFFSET_PTR de la descartar puede establecerse mediante una llamada a [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) o mediante una llamada a [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)con una *fAttribute* de SQL_ATTR_PARAM_BIND_ OFFSET_PTR.  
  
 El desplazamiento de enlace siempre se agrega directamente a los valores de los campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR y SQL_DESC_OCTET_LENGTH_PTR. Si el desplazamiento se cambia a un valor diferente, el nuevo valor todavía se agrega directamente al valor de cada campo de descriptor. El desplazamiento nuevo no se agrega a la suma de los desplazamientos anteriores y el valor del campo.  
  
## <a name="descriptors"></a>Descriptores de  
 Campos de los APD e IPD determina cómo se enlaza un parámetro. Los argumentos de **SQLBindParameter** se utilizan para establecer los campos de descriptor. Los campos también pueden establecerse mediante el **SQLSetDescField** funciones, aunque **SQLBindParameter** es más eficaz utilizar porque la aplicación no tiene que obtener un identificador de descriptor para llamar a **SQLBindParameter**.  
  
> [!CAUTION]  
>  Al llamar a **SQLBindParameter** para una instrucción puede afectar a otras instrucciones. Esto se produce cuando el descartar asociado con la instrucción se asigna explícitamente y también está asociado con otras instrucciones. Dado que **SQLBindParameter** modifica los campos de APD, las modificaciones se aplican a todas las instrucciones con el que está asociado este descriptor. Si no es el comportamiento requerido, la aplicación debe anular la asociación de este descriptor de las demás instrucciones antes de llamar a **SQLBindParameter**.  
  
 Conceptualmente, **SQLBindParameter** realiza los siguientes pasos de secuencia:  
  
1.  Llamadas [SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) para obtener el identificador APD.  
  
2.  Llamadas [SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) para obtener SQL_DESC_COUNT campo del APD y si el valor de la *ColumnNumber* argumento supera el valor de SQL_DESC_COUNT, llamadas **SQLSetDescField**para aumentar el valor de SQL_DESC_COUNT a *ColumnNumber*.  
  
3.  Llamadas [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) varias veces para asignar valores a los campos siguientes de la APD:  
  
    -   Establece SQL_DESC_TYPE y SQL_DESC_CONCISE_TYPE en el valor de *ValueType*, excepto en que si *ValueType* es uno de los identificadores concisos de un subtipo de intervalo o datetime, Establece SQL_DESC_TYPE en SQL_ Fecha y hora o SQL_INTERVAL, respectivamente, SQL_DESC_CONCISE_TYPE se establece en el identificador conciso y SQL_DESC_DATETIME_INTERVAL_CODE se establece en el valor de datetime correspondiente o el subcódigo de intervalo.  
  
    -   Establece el campo SQL_DESC_OCTET_LENGTH en el valor de *BufferLength*.  
  
    -   Establece el campo SQL_DESC_DATA_PTR en el valor de *ParameterValue*.  
  
    -   Establece el campo SQL_DESC_OCTET_LENGTH_PTR en el valor de *StrLen_or_Ind*.  
  
    -   Establece el campo SQL_DESC_INDICATOR_PTR también en el valor de *StrLen_or_Ind*.  
  
     El *StrLen_or_Ind* parámetro especifica la información de indicador y la longitud del valor de parámetro.  
  
4.  Llamadas [SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md) para obtener el identificador IPD.  
  
5.  Llamadas [SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md) para obtener SQL_DESC_COUNT campo del IPD y si el valor de la *ColumnNumber* argumento supera el valor de SQL_DESC_COUNT, llamadas **SQLSetDescField**para aumentar el valor de SQL_DESC_COUNT a *ColumnNumber*.  
  
6.  Llamadas [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md) varias veces para asignar valores a los campos siguientes de la IPD:  
  
    -   Establece SQL_DESC_TYPE y SQL_DESC_CONCISE_TYPE en el valor de *ParameterType*, excepto en que si *ParameterType* es uno de los identificadores concisos de un subtipo de intervalo o datetime, Establece SQL_DESC_TYPE SQL_DATETIME o SQL_INTERVAL, respectivamente, conjuntos de SQL_DESC_CONCISE_TYPE al identificador concisa y conjuntos de SQL_DESC_DATETIME_INTERVAL_CODE para el valor de datetime correspondiente o el subcódigo de intervalo.  
  
    -   Establece una o varias de SQL_DESC_LENGTH, SQL_DESC_PRECISION y SQL_DESC_DATETIME_INTERVAL_PRECISION, según corresponda para *ParameterType*.  
  
    -   Establece SQL_DESC_SCALE en el valor de *ColumnSize*.  
  
 Si la llamada a **SQLBindParameter** se produce un error, el contenido de los campos de descriptor que habría establecido en el APD no están definidos, y se ha modificado el campo SQL_DESC_COUNT de la APD. Además, los campos SQL_DESC_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE y SQL_DESC_TYPE del registro adecuado en el IPD están definidos y se ha modificado el campo SQL_DESC_COUNT de la IPD.  
  
## <a name="conversion-of-calls-to-and-from-sqlsetparam"></a>Conversión de llamadas a y desde SQLSetParam  
 Cuando una aplicación ODBC 1.0 llama **SQLSetParam** en una aplicación ODBC 3. *x* controlador ODBC 3. *x* el Administrador de controladores se asigna la llamada como se muestra en la tabla siguiente.  
  
|Llamar a la aplicación de ODBC 1.0|La llamada a ODBC 3. *x* controlador|  
|----------------------------------|-------------------------------|  
|SQLSetParam (StatementHandle, ParameterNumber, tipo de valor, ParameterType, LengthPrecision, ParameterScale, ParameterValuePtr, StrLen_or_IndPtr);|SQLBindParameter (StatementHandle, ParameterNumber, SQL_PARAM_INPUT_OUTPUT, tipo de valor, ParameterType, *ColumnSize*, *ColumnSize*, ParameterValuePtr, SQL_SETPARAM_VALUE_MAX,      StrLen_or_IndPtr);|  
  
## <a name="code-example"></a>Ejemplo de código  
 En el siguiente ejemplo, una aplicación prepara una instrucción SQL para insertar datos en la tabla ORDERS. Para cada parámetro en la instrucción, la aplicación llama a **SQLBindParameter** para especificar el tipo de datos C de ODBC y el tipo de datos SQL del parámetro y para enlazar un búfer para cada parámetro. Para cada fila de datos, la aplicación asigna valores de datos para cada parámetro y llama **SQLExecute** para ejecutar la instrucción.  
  
 El ejemplo siguiente se da por supuesto que tiene un origen de datos ODBC en el equipo denominado Northwind que está asociado a la base de datos Northwind.  
  
 Ver más ejemplos de código, consulte [función SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [SQLProcedures, función](../../../odbc/reference/syntax/sqlprocedures-function.md), [función SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md), y [SQLSetPos, función](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```  
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
 En el siguiente ejemplo, una aplicación ejecuta un procedimiento almacenado de SQL Server mediante un parámetro con nombre.  
  
```  
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
|Devolver el número de parámetros de la instrucción|[Función SQLNumParams](../../../odbc/reference/syntax/sqlnumparams-function.md)|  
|Devuelve el siguiente parámetro para enviar datos|[Función SQLParamData](../../../odbc/reference/syntax/sqlparamdata-function.md)|  
|Especificar varios valores de parámetro|[Función SQLParamOptions](../../../odbc/reference/syntax/sqlparamoptions-function.md)|  
|Envío de datos de parámetro en tiempo de ejecución|[Función SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Recuperar parámetros de salida mediante SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
