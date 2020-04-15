---
title: Función SQLColAttribute (SQLColAttribute) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLColAttribute
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColAttribute
helpviewer_keywords:
- SQLColAttribute function [ODBC]
ms.assetid: 8c45c598-cb01-4789-a571-e93619a18ed9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c94de3dfc7036277f8be56c401326cdab07a9606
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301295"
---
# <a name="sqlcolattribute-function"></a>Función SQLColAttribute
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 3.0: ISO 92  
  
 **Resumen**  
 **SQLColAttribute** devuelve información de descriptor para una columna en un conjunto de resultados. La información del descriptor se devuelve como una cadena de caracteres, un valor dependiente del descriptor o un valor entero.  
  
> [!NOTE]  
>  Para obtener más información acerca de lo que el Administrador de controladores asigna esta función a cuando un ODBC 3. *x* aplicación está trabajando con un ODBC 2. *x* driver, consulte Asignación de [funciones de reemplazo para compatibilidad con versiones anteriores de aplicaciones](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLColAttribute (  
      SQLHSTMT        StatementHandle,  
      SQLUSMALLINT    ColumnNumber,  
      SQLUSMALLINT    FieldIdentifier,  
      SQLPOINTER      CharacterAttributePtr,  
      SQLSMALLINT     BufferLength,  
      SQLSMALLINT *   StringLengthPtr,  
      SQLLEN *        NumericAttributePtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *ColumnNumber*  
 [Entrada] El número del registro en el IRD del que se va a recuperar el valor del campo. Este argumento corresponde al número de columna de datos de resultados, ordenados secuencialmente en el orden de las columnas crecientes, comenzando en 1. Las columnas se pueden describir en cualquier orden.  
  
 La columna 0 se puede especificar en este argumento, pero todos los valores excepto SQL_DESC_TYPE y SQL_DESC_OCTET_LENGTH devolverán valores indefinidos.  
  
 *FieldIdentifier*  
 [Entrada] El identificador del descriptor. Este identificador define qué campo del IRD se debe consultar (por ejemplo, SQL_COLUMN_TABLE_NAME).  
  
 *CharacterAttributePtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el valor en el campo *FieldIdentifier* de la fila *ColumnNumber* del IRD, si el campo es una cadena de caracteres. De lo contrario, el campo no se utiliza.  
  
 Si *CharacterAttributePtr* es NULL, *StringLengthPtr* seguirá devolviendo el número total de bytes (excluyendo el carácter de terminación nula para los datos de caracteres) disponibles para devolver en el búfer señalado por *CharacterAttributePtr*.  
  
 *BufferLength*  
 [Entrada] Si *FieldIdentifier* es un campo definido por ODBC y *CharacterAttributePtr* apunta a una \*cadena de caracteres o búfer binario, este argumento debe ser la longitud de *CharacterAttributePtr*. Si *FieldIdentifier* es un campo \*definido por ODBC y *CharacterAttribute*Ptr es un entero, se omite este campo. Si el * \*CharacterAttributePtr* es una cadena Unicode (cuando se llama a **SQLColAttributeW**), el *BufferLength* argumento debe ser un número par. Si *FieldIdentifier* es un campo definido por el controlador, la aplicación indica la naturaleza del campo para el Administrador de controladores estableciendo el *BufferLength* argumento. *BufferLength* puede tener los siguientes valores:  
  
-   Si *CharacterAttributePtr* es un puntero a un puntero, *BufferLength* debe tener el valor SQL_IS_POINTER.  
  
-   Si *CharacterAttributePtr* es un puntero a una cadena de caracteres, *BufferLength* es la longitud del búfer.  
  
-   Si *CharacterAttributePtr* es un puntero a un búfer binario, la aplicación coloca el resultado de la macro SQL_LEN_BINARY_ATTR(*length*) en *BufferLength*. Esto coloca un valor negativo en *BufferLength*.  
  
-   Si *CharacterAttributePtr* es un puntero a un tipo de datos de longitud fija, *BufferLength* debe ser uno de los siguientes: SQL_IS_INTEGER, SQL_IS_UNINTEGER, SQL_SMALLINT o SQLUSMALLINT.  
  
 *StringLengthPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número total de bytes (excluyendo el byte de terminación nula para los datos de caracteres) disponible para devolver en **CharacterAttributePtr*.  
  
 Para los datos de caracteres, si el número de bytes disponibles \*para devolver es mayor o igual que *BufferLength*, la información del descriptor en *CharacterAttributePtr* se trunca en *BufferLength* menos la longitud de un carácter de terminación nula y está terminada en null por el controlador.  
  
 Para todos los demás tipos de datos, se omite el valor de *BufferLength* y el controlador asume que el tamaño de **CharacterAttributePtr* es de 32 bits.  
  
 *NumericAttributePtr*  
 [Salida] Puntero a un búfer entero en el que se va a devolver el valor en el campo *FieldIdentifier* de la fila *ColumnNumber* del IRD, si el campo es un tipo de descriptor numérico, como SQL_DESC_COLUMN_LENGTH. De lo contrario, el campo no se utiliza. Tenga en cuenta que algunos controladores solo pueden escribir los 32 bits o 16 bits inferiores de un búfer y dejar el bit de orden superior sin cambios. Por lo tanto, las aplicaciones deben inicializar el valor en 0 antes de llamar a esta función.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLColAttribute** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *Control* de *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLColAttribute** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01004|Datos de cadena truncados a la derecha|El \*búfer *CharacterAttributePtr* no era lo suficientemente grande como para devolver todo el valor de cadena, por lo que el valor de cadena se truncó. La longitud del valor de cadena no truncada se devuelve en **StringLengthPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|07005|Declaración preparada no una *especificación de cursor*|La instrucción asociada con el *StatementHandle* no devolvió un conjunto de resultados y *FieldIdentifier* no se SQL_DESC_COUNT. No había columnas que describir.|  
|07009|Indice de descriptor no válido|(DM) el valor especificado para *ColumnNumber* era igual a 0 y el atributo de instrucción SQL_ATTR_USE_BOOKMARKS se SQL_UB_OFF.<br /><br /> El valor especificado para el argumento *ColumnNumber* era mayor que el número de columnas del conjunto de resultados.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagField** desde la estructura de datos de diagnóstico describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY008|Operación cancelada|El procesamiento asincrónico se ha habilitado para *StatementHandle*. Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle*. A continuación, se volvió a llamar a la función en *StatementHandle*.<br /><br /> Se llamó a la función y antes de completar la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en el *StatementHandle* desde un subproceso diferente en una aplicación multiproceso.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función anócrona todavía se estaba ejecutando cuando SQLColAttribute se llamó.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *StatementHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.<br /><br /> (DM) Se llamó a la función antes de llamar a **SQLPrepare**, **SQLExecDirect**o a una función de catálogo para *StatementHandle*.<br /><br /> (DM) se llamó a una función de ejecución asincrónica (no esta) para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY090|Cadena no válida o longitud de búfer|(DM) * \*CharacterAttributePtr* es una cadena de caracteres y *BufferLength* era menor que 0 pero no igual a SQL_NTS.|  
|HY091|Identificador de campo descriptor no válido|El valor especificado para el argumento *FieldIdentifier* no era uno de los valores definidos y no era un valor definido por la implementación.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYC00|Conductor no capaz|El controlador no admite el valor especificado para el argumento *FieldIdentifier.*|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|El sondeo está deshabilitado en el modo de notificación asincrónica|Siempre que se utiliza el modelo de notificación, el sondeo está deshabilitado.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el identificador devuelve SQL_STILL_EXECUTING y si el modo de notificación está habilitado, **sqlCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
 Cuando se llama después de **SQLPrepare** y antes de **SQLExecute**, **SQLColAttribute** puede devolver cualquier SQLSTATE que **SQLPrepare** o **SQLExecute**puedan devolver, dependiendo de cuándo el origen de datos evalúe la instrucción SQL asociada a *StatementHandle*.  
  
 Por motivos de rendimiento, una aplicación no debe llamar a **SQLColAttribute** antes de ejecutar una instrucción.  
  
## <a name="comments"></a>Comentarios  
 Para obtener información sobre cómo las aplicaciones usan la información devuelta por **SQLColAttribute**, vea Metadatos del conjunto de [resultados](../../../odbc/reference/develop-app/result-set-metadata.md).  
  
 **SQLColAttribute** devuelve información \*en *NumericAttributePtr* o en \* *CharacterAttributePtr*. La información de \*enteros se devuelve en *NumericAttributePtr* como un valor SQLLEN; todos los demás formatos de información se devuelven en \* *CharacterAttributePtr*. Cuando se devuelve \*información en *NumericAttributePtr*, el controlador omite *CharacterAttributePtr*, *BufferLength*y *StringLengthPtr*. Cuando se devuelve \*información en *CharacterAttributePtr*, el controlador omite *NumericAttributePtr*.  
  
 **SQLColAttribute** devuelve valores de los campos descriptores del IRD. Se llama a la función con un identificador de instrucción en lugar de un identificador de descriptor. Los valores devueltos por **SQLColAttribute** para el *FieldIdentifier* valores enumerados más adelante en esta sección también se pueden recuperar mediante una llamada a **SQLGetDescField** con el identificador IRD adecuado.  
  
 Los campos descriptores definidos actualmente, la versión de ODBC en la que se introdujeron y los argumentos en los que se devuelve información para ellos se muestran más adelante en esta sección; más tipos de descriptores pueden ser definidos por los controladores para aprovechar los diferentes orígenes de datos.  
  
 Un ODBC 3. *x* controlador debe devolver un valor para cada uno de los campos descriptores. Si un campo descriptor no se aplica a un controlador o origen \*de datos y, a menos que se indique lo contrario, el controlador devuelve 0 en *StringLengthPtr* o una cadena vacía en **CharacterAttributePtr*.  
  
## <a name="backward-compatibility"></a>Backward Compatibility  
 El ODBC 3. *x* función **SQLColAttribute** reemplaza el ODBC 2 en desuso. *x* función **SQLColAttributes**. Al asignar **SQLColAttributes** a **SQLColAttribute** (cuando un ODBC 2.* x* aplicación está trabajando con un ODBC 3. *x* controlador) o la asignación de **SQLColAttribute** a **SQLColAttributes** (cuando un ODBC 3.* x* aplicación está trabajando con un ODBC 2. *x* driver), el Administrador de controladores pasa el valor de *FieldIdentifier* a través, lo asigna a un nuevo valor o devuelve un error, como se indica a continuación:  
  
> [!NOTE]  
>  Prefijo utilizado en los valores *FieldIdentifier* en ODBC 3. *x* se ha cambiado de la utilizada en ODBC 2. *x*. El nuevo prefijo es "SQL_DESC"; el prefijo antiguo era "SQL_COLUMN".  
  
-   Si el **valor #define** de ODBC 2. *x* *FieldIdentifier* es el mismo que el valor **#define** de ODBC 3. *x* *FieldIdentifier*, el valor de la llamada de función se acaba de pasar.  
  
-   Los **valores #define** de ODBC 2. *x* *FieldIdentifiers* SQL_COLUMN_LENGTH, SQL_COLUMN_PRECISION y SQL_COLUMN_SCALE son diferentes de los valores **#define** de ODBC 3. *x* *FieldIdentifiers* SQL_DESC_PRECISION, SQL_DESC_SCALE y SQL_DESC_LENGTH. Un ODBC 2. *x* controlador sólo necesita admitir el ODBC 2. *x* valores. Un ODBC 3. *x* controlador debe admitir los valores "SQL_COLUMN" y "SQL_DESC" para estos tres *FieldIdentifiers*. Estos valores son diferentes porque la precisión, la escala y la longitud se definen de forma diferente en ODBC 3. *x* que en ODBC 2. *x*. Para obtener más información, consulte [Tamaño de columna, Dígitos decimales, Transferir longitud de octeto y Tamaño](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md)de visualización .  
  
-   Si el **valor #define** de ODBC 2. *x* *FieldIdentifier* es diferente del valor **#define** de ODBC 3. *x* *FieldIdentifier*, como ocurre con los valores COUNT, NAME y NULLABLE, el valor de la llamada de función se asigna al valor correspondiente. Por ejemplo, SQL_COLUMN_COUNT se asigna a SQL_DESC_COUNT y SQL_DESC_COUNT se asigna a SQL_COLUMN_COUNT, dependiendo de la dirección de la asignación.  
  
-   Si *FieldIdentifier* es un nuevo valor en ODBC 3. *x*, para el que no había ningún valor correspondiente en ODBC 2. *x*, no se asignará cuando un ODBC 3. *x* aplicación lo utiliza en una llamada a **SQLColAttribute** en un ODBC 2. *x* controlador y la llamada devolverá SQLSTATE HY091 (identificador de campo descriptor no válido).  
  
 En la tabla siguiente se enumeran los tipos de descriptor devueltos por **SQLColAttribute**. El tipo de los valores *NumericAttributePtr* es ** \*SQLLEN **.  
  
|*FieldIdentifier*|Information<br /><br /> regresó en|Descripción|  
|-----------------------|---------------------------------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE si la columna es una columna de incremento automático.<br /><br /> SQL_FALSE si la columna no es una columna de incremento automático o no es numérica.<br /><br /> Este campo solo es válido para columnas de tipo de datos numéricos. Una aplicación puede insertar valores en una fila que contenga una columna de incremento automático, pero normalmente no puede actualizar valores en la columna.<br /><br /> Cuando se realiza una inserción en una columna de incremento automático, se inserta un valor único en la columna en el momento de la inserción. El incremento no está definido, pero es específico del origen de datos. Una aplicación no debe suponer que una columna de incremento automático comienza en un punto determinado o incrementos por cualquier valor determinado.|  
|SQL_DESC_BASE_COLUMN_NAME (ODBC 3.0)|*CharacterAttributePtr*|El nombre de columna base de la columna del conjunto de resultados. Si no existe un nombre de columna base (como en el caso de las columnas que son expresiones), esta variable contiene una cadena vacía.<br /><br /> Esta información se devuelve desde el campo de registro SQL_DESC_BASE_COLUMN_NAME del IRD, que es un campo de solo lectura.|  
|SQL_DESC_BASE_TABLE_NAME (ODBC 3.0)|*CharacterAttributePtr*|El nombre de la tabla base que contiene la columna. Si el nombre de la tabla base no se puede definir o no es aplicable, esta variable contiene una cadena vacía.<br /><br /> Esta información se devuelve desde el campo de registro SQL_DESC_BASE_TABLE_NAME del IRD, que es un campo de solo lectura.|  
|SQL_DESC_CASE_SENSITIVE (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE si la columna se trata como que distingue mayúsculas de minúsculas para intercalaciones y comparaciones.<br /><br /> SQL_FALSE si la columna no se trata como sensible a mayúsculas y minúsculas para intercalaciones y comparaciones o no es de carácter.|  
|SQL_DESC_CATALOG_NAME (ODBC 2.0)|*CharacterAttributePtr*|El catálogo de la tabla que contiene la columna. El valor devuelto es definido por la implementación si la columna es una expresión o si la columna forma parte de una vista. Si el origen de datos no admite catálogos o no se puede determinar el nombre del catálogo, se devuelve una cadena vacía. Este campo de registro VARCHAR no está limitado a 128 caracteres.|  
|SQL_DESC_CONCISE_TYPE (ODBC 1.0)|*NumericAttributePtr*|El tipo de datos conciso.<br /><br /> Para los tipos de datos datetime e interval, este campo devuelve el tipo de datos conciso; por ejemplo, SQL_TYPE_TIME o SQL_INTERVAL_YEAR. (Para obtener más información, consulte [Identificadores y descriptores](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) de tipos de datos en apéndice D: tipos de datos.)<br /><br /> Esta información se devuelve desde el campo de registro SQL_DESC_CONCISE_TYPE del IRD.|  
|SQL_DESC_COUNT (ODBC 1.0)|*NumericAttributePtr*|El número de columnas disponibles en el conjunto de resultados. Esto devuelve 0 si no hay columnas en el conjunto de resultados. Se omite el valor del argumento *ColumnNumber.*<br /><br /> Esta información se devuelve desde el campo de encabezado SQL_DESC_COUNT del IRD.|  
|SQL_DESC_DISPLAY_SIZE (ODBC 1.0)|*NumericAttributePtr*|Número máximo de caracteres necesarios para mostrar los datos de la columna. Para obtener más información sobre el tamaño de visualización, consulte Tamaño de [columna, Dígitos decimales, Transferir longitud de octeto y Tamaño](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) de visualización en apéndice D: tipos de datos.|  
|SQL_DESC_FIXED_PREC_SCALE (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE si la columna tiene una precisión fija y una escala distinta de cero que son específicas del origen de datos.<br /><br /> SQL_FALSE si la columna no tiene una precisión fija y una escala distinta de cero que sean específicas del origen de datos.|  
|SQL_DESC_LABEL (ODBC 2.0)|*CharacterAttributePtr*|La etiqueta o el título de la columna. Por ejemplo, una columna denominada EmpName podría etiquetarse como Nombre del empleado o puede etiquetarse con un alias.<br /><br /> Si una columna no tiene una etiqueta, se devuelve el nombre de la columna. Si la columna no tiene etiqueta y no tiene nombre, se devuelve una cadena vacía.|  
|SQL_DESC_LENGTH (ODBC 3.0)|*NumericAttributePtr*|Valor numérico que es la longitud de caracteres máxima o real de una cadena de caracteres o un tipo de datos binario. Es la longitud máxima de caracteres para un tipo de datos de longitud fija o la longitud de carácter real para un tipo de datos de longitud variable. Su valor siempre excluye el byte de terminación nula que finaliza la cadena de caracteres.<br /><br /> Esta información se devuelve desde el campo de registro SQL_DESC_LENGTH del IRD.<br /><br /> Para obtener más información acerca de la longitud, consulte Tamaño de [columna, Dígitos decimales, Transferir longitud de octeto y Tamaño](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) de visualización en apéndice D: tipos de datos.|  
|SQL_DESC_LITERAL_PREFIX (ODBC 3.0)|*CharacterAttributePtr*|Este campo de registro VARCHAR(128) contiene el carácter o caracteres que el controlador reconoce como prefijo para un literal de este tipo de datos. Este campo contiene una cadena vacía para un tipo de datos para el que no es aplicable un prefijo literal. Para obtener más información, consulte [Prefijos y sufijos literales](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md).|  
|SQL_DESC_LITERAL_SUFFIX (ODBC 3.0)|*CharacterAttributePtr*|Este campo de registro VARCHAR(128) contiene el carácter o caracteres que el controlador reconoce como sufijo para un literal de este tipo de datos. Este campo contiene una cadena vacía para un tipo de datos para el que no es aplicable un sufijo literal. Para obtener más información, consulte [Prefijos y sufijos literales](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md).|  
|SQL_DESC_LOCAL_TYPE_NAME (ODBC 3.0)|*CharacterAttributePtr*|Este campo de registro VARCHAR(128) contiene cualquier nombre localizado (idioma nativo) para el tipo de datos que puede ser diferente del nombre normal del tipo de datos. Si no hay ningún nombre localizado, se devuelve una cadena vacía. Este campo es solo para fines de visualización. El juego de caracteres de la cadena depende de la configuración regional y suele ser el juego de caracteres predeterminado del servidor.|  
|SQL_DESC_NAME (ODBC 3.0)|*CharacterAttributePtr*|El alias de columna, si se aplica. Si el alias de columna no se aplica, se devuelve el nombre de columna. En cualquier caso, SQL_DESC_UNNAMED se establece en SQL_NAMED. Si no hay ningún nombre de columna o un alias de columna, se devuelve una cadena vacía y SQL_DESC_UNNAMED se establece en SQL_UNNAMED.<br /><br /> Esta información se devuelve desde el campo de registro SQL_DESC_NAME del IRD.|  
|SQL_DESC_NULLABLE (ODBC 3.0)|*NumericAttributePtr*|SQL_ NULLABLE si la columna puede tener valores NULL; SQL_NO_NULLS si la columna no tiene valores NULL; o SQL_NULLABLE_UNKNOWN si no se sabe si la columna acepta valores NULL.<br /><br /> Esta información se devuelve desde el campo de registro SQL_DESC_NULLABLE del IRD.|  
|SQL_DESC_NUM_PREC_RADIX (ODBC 3.0)|*NumericAttributePtr*|Si el tipo de datos del campo SQL_DESC_TYPE es un tipo de datos numérico aproximado, este campo SQLINTEGER contiene un valor de 2 porque el campo SQL_DESC_PRECISION contiene el número de bits. Si el tipo de datos del campo SQL_DESC_TYPE es un tipo de datos numérico exacto, este campo contiene un valor de 10 porque el campo SQL_DESC_PRECISION contiene el número de dígitos decimales. Este campo se establece en 0 para todos los tipos de datos no numéricos.|  
|SQL_DESC_OCTET_LENGTH (ODBC 3.0)|*NumericAttributePtr*|La longitud, en bytes, de una cadena de caracteres o un tipo de datos binario. Para caracteres de longitud fija o tipos binarios, esta es la longitud real en bytes. Para los tipos binarios o de caracteres de longitud variable, esta es la longitud máxima en bytes. Este valor no incluye el terminador nulo.<br /><br /> Esta información se devuelve desde el campo de registro SQL_DESC_OCTET_LENGTH del IRD.<br /><br /> Para obtener más información acerca de la longitud, consulte Tamaño de [columna, Dígitos decimales, Transferir longitud de octeto y Tamaño](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) de visualización en apéndice D: tipos de datos.|  
|SQL_DESC_PRECISION (ODBC 3.0)|*NumericAttributePtr*|Un valor numérico que para un tipo de datos numérico denota la precisión aplicable. Para los tipos de datos SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP y todos los tipos de datos de intervalo que representan un intervalo de tiempo, su valor es la precisión aplicable del componente de fracciones de segundo.<br /><br /> Esta información se devuelve desde el campo de registro SQL_DESC_PRECISION del IRD.|  
|SQL_DESC_SCALE (ODBC 3.0)|*NumericAttributePtr*|Valor numérico que es la escala aplicable para un tipo de datos numérico. Para los tipos de datos DECIMAL y NUMERIC, esta es la escala definida. No está definido para todos los demás tipos de datos.<br /><br /> Esta información se devuelve desde el campo de registro SCALE del IRD.|  
|SQL_DESC_SCHEMA_NAME (ODBC 2.0)|*CharacterAttributePtr*|El esquema de la tabla que contiene la columna. El valor devuelto es definido por la implementación si la columna es una expresión o si la columna forma parte de una vista. Si el origen de datos no admite esquemas o no se puede determinar el nombre del esquema, se devuelve una cadena vacía. Este campo de registro VARCHAR no está limitado a 128 caracteres.|  
|SQL_DESC_SEARCHABLE (ODBC 1.0)|*NumericAttributePtr*|SQL_PRED_NONE si la columna no se puede utilizar en una cláusula WHERE. (Esto es lo mismo que el valor de SQL_UNSEARCHABLE en ODBC 2. *x*.)<br /><br /> SQL_PRED_CHAR si la columna se puede utilizar en una cláusula WHERE pero solo con el predicado LIKE. (Esto es lo mismo que el valor de SQL_LIKE_ONLY en ODBC 2. *x*.)<br /><br /> SQL_PRED_BASIC si la columna se puede utilizar en una cláusula WHERE con todos los operadores de comparación excepto LIKE. (Esto es lo mismo que el valor de SQL_EXCEPT_LIKE en ODBC 2. *x*.)<br /><br /> SQL_PRED_SEARCHABLE si la columna se puede utilizar en una cláusula WHERE con cualquier operador de comparación.<br /><br /> Las columnas de tipo SQL_LONGVARCHAR y SQL_LONGVARBINARY suelen devolver SQL_PRED_CHAR.|  
|SQL_DESC_TABLE_NAME (ODBC 2.0)|*CharacterAttributePtr*|El nombre de la tabla que contiene la columna. El valor devuelto es definido por la implementación si la columna es una expresión o si la columna forma parte de una vista.<br /><br /> Si no se puede determinar el nombre de la tabla, se devuelve una cadena vacía.|  
|SQL_DESC_TYPE (ODBC 3.0)|*NumericAttributePtr*|Valor numérico que especifica el tipo de datos SQL.<br /><br /> Cuando *ColumnNumber* es igual a 0, se devuelve SQL_BINARY para los marcadores de longitud variable y SQL_INTEGER se devuelve para los marcadores de longitud fija.<br /><br /> Para los tipos de datos datetime e interval, este campo devuelve el tipo de datos detallado: SQL_DATETIME o SQL_INTERVAL. (Para obtener más información, consulte [Identificadores y descriptores](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) de tipos de datos en apéndice D: tipos de datos.<br /><br /> Esta información se devuelve desde el campo de registro SQL_DESC_TYPE del IRD. **Nota:**  Para trabajar con ODBC 2. *x* controladores, utilice SQL_DESC_CONCISE_TYPE en su lugar.|  
|SQL_DESC_TYPE_NAME (ODBC 1.0)|*CharacterAttributePtr*|Nombre de tipo de datos dependiente del origen de datos; por ejemplo, "CHAR", "VARCHAR", "MONEY", "LONG VARBINARY" o "CHAR ( ) FOR BIT DATA".<br /><br /> Si el tipo es desconocido, se devuelve una cadena vacía.|  
|SQL_DESC_UNNAMED (ODBC 3.0)|*NumericAttributePtr*|SQL_NAMED o SQL_UNNAMED. Si el campo SQL_DESC_NAME del IRD contiene un alias de columna o un nombre de columna, se devuelve SQL_NAMED. Si no hay ningún nombre de columna o alias de columna, se devuelve SQL_UNNAMED.<br /><br /> Esta información se devuelve desde el campo de registro SQL_DESC_UNNAMED del IRD.|  
|SQL_DESC_UNSIGNED (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE si la columna no está firmada (o no es numérica).<br /><br /> SQL_FALSE si la columna está firmada.|  
|SQL_DESC_UPDATABLE (ODBC 1.0)|*NumericAttributePtr*|La columna se describe mediante los valores de las constantes definidas:<br /><br /> SQL_ATTR_READONLY SQL_ATTR_WRITE SQL_ATTR_READWRITE_UNKNOWN<br /><br /> SQL_DESC_UPDATABLE describe la capacidad de actualización de la columna en el conjunto de resultados, no la columna de la tabla base. La capacidad de actualización de la columna base en la que se basa la columna del conjunto de resultados puede ser diferente del valor de este campo. Si una columna es actualizable se puede basar en el tipo de datos, los privilegios de usuario y la definición del propio conjunto de resultados. Si no está claro si una columna es actualizable, se debe devolver SQL_ATTR_READWRITE_UNKNOWN.|  
  
 **SQLColAttribute** es una alternativa extensible a **SQLDescribeCol**. **SQLDescribeCol** devuelve un conjunto fijo de información de descriptor basado en ANSI-89 SQL. **SQLColAttribute** permite el acceso al conjunto más amplio de información de descriptor disponible en las extensiones de proveedor ANSI SQL-92 y DBMS.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer a una columna en un conjunto de resultados|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelación del procesamiento de extractos|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devolver información sobre una columna en un conjunto de resultados|[SQLDescribeCol (función)](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Obtención de un bloque de datos o desplazamiento por un conjunto de resultados|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Obtención de varias filas de datos|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
  
## <a name="example"></a>Ejemplo  
 El siguiente código de ejemplo no libera identificadores y conexiones. Vea [SQLFreeHandle (Función),](../../../odbc/reference/syntax/sqlfreehandle-function.md) [Programa ODBC](../../../odbc/reference/sample-odbc-program.md)de ejemplo y [Función SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md) para obtener ejemplos de código para liberar identificadores e instrucciones.  
  
```cpp  
// SQLColAttibute.cpp  
// compile with: user32.lib odbc32.lib  
  
#define UNICODE  
  
#include <windows.h>  
#include <sqlext.h>  
#include <strsafe.h>  
  
struct DataBinding {  
   SQLSMALLINT TargetType;  
   SQLPOINTER TargetValuePtr;  
   SQLINTEGER BufferLength;  
   SQLLEN StrLen_or_Ind;  
};  
  
void printStatementResult(SQLHSTMT hstmt) {  
   int bufferSize = 1024, i;  
   SQLRETURN retCode;  
   SQLSMALLINT numColumn = 0, bufferLenUsed;
   
   retCode = SQLNumResultCols(hstmt, &numColumn);  
   
   SQLPOINTER* columnLabels = (SQLPOINTER *)malloc( numColumn * sizeof(SQLPOINTER*) );  
   struct DataBinding* columnData = (struct DataBinding*)malloc( numColumn * sizeof(struct DataBinding) );  
  
   printf( "Columns from that table:\n" );  
   for ( i = 0 ; i < numColumn ; i++ ) {  
      columnLabels[i] = (SQLPOINTER)malloc( bufferSize*sizeof(char) );  
  
      retCode = SQLColAttribute(hstmt, (SQLUSMALLINT)i + 1, SQL_DESC_LABEL, columnLabels[i], (SQLSMALLINT)bufferSize, &bufferLenUsed, NULL);  
      wprintf( L"Column %d: %s\n", i, (wchar_t*)columnLabels[i] );  
   }  
  
   // allocate memory for the binding  
   for ( i = 0 ; i < numColumn ; i++ ) {  
      columnData[i].TargetType = SQL_C_CHAR;  
      columnData[i].BufferLength = (bufferSize+1);  
      columnData[i].TargetValuePtr = malloc( sizeof(unsigned char)*columnData[i].BufferLength );  
   }  
  
   // setup the binding   
   for ( i = 0 ; i < numColumn ; i++ ) {  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, columnData[i].TargetType,   
         columnData[i].TargetValuePtr, columnData[i].BufferLength, &(columnData[i].StrLen_or_Ind));  
   }  
  
   printf( "Data from that table:\n" );  
   // fetch the data and print out the data  
   for ( retCode = SQLFetch(hstmt) ; retCode == SQL_SUCCESS || retCode == SQL_SUCCESS_WITH_INFO ; retCode = SQLFetch(hstmt) ) {  
      int j;  
      for ( j = 0 ; j < numColumn ; j++ )  
         wprintf( L"%s: %hs\n", columnLabels[j], columnData[j].TargetValuePtr );  
      printf( "\n" );  
   }  
   printf( "\n" );   
}  
  
int main() {  
   int bufferSize = 1024, i, count = 1, numCols = 5;  
   wchar_t firstTableName[1024], * dbName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize ), * userName = (wchar_t *)malloc( sizeof(wchar_t)*bufferSize );  
   HWND desktopHandle = GetDesktopWindow();   // desktop's window handle  
   SQLWCHAR connStrbuffer[1024];  
   SQLSMALLINT connStrBufferLen, bufferLen;  
   SQLRETURN retCode;  
  
   SQLHENV henv = NULL;   // Environment     
   SQLHDBC hdbc = NULL;   // Connection handle  
   SQLHSTMT hstmt = NULL;   // Statement handle  
  
   struct DataBinding* catalogResult = (struct DataBinding*) malloc( numCols * sizeof(struct DataBinding) );  
   SQLWCHAR* selectAllQuery = (SQLWCHAR *)malloc( sizeof(SQLWCHAR) * bufferSize );  
  
   // connect to database  
   retCode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
   retCode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLCHAR *)(void*)SQL_OV_ODBC3, -1);  
   retCode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
   retCode = SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)10, 0);  
   retCode = SQLDriverConnect(hdbc, desktopHandle, L"Driver={SQL Server}", SQL_NTS, connStrbuffer, 1025, &connStrBufferLen, SQL_DRIVER_PROMPT);  
   retCode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);  
  
   // display the database information  
   retCode = SQLGetInfo(hdbc, SQL_DATABASE_NAME, dbName, (SQLSMALLINT)bufferSize, (SQLSMALLINT *)&bufferLen);  
   retCode = SQLGetInfo(hdbc, SQL_USER_NAME, userName, (SQLSMALLINT)bufferSize, &bufferLen);  
  
   for ( i = 0 ; i < numCols ; i++ ) {  
      catalogResult[i].TargetType = SQL_C_CHAR;  
      catalogResult[i].BufferLength = (bufferSize + 1);  
      catalogResult[i].TargetValuePtr = malloc( sizeof(unsigned char)*catalogResult[i].BufferLength );  
   }  
  
   // Set up the binding. This can be used even if the statement is closed by closeStatementHandle  
   for ( i = 0 ; i < numCols ; i++ )  
      retCode = SQLBindCol(hstmt, (SQLUSMALLINT)i + 1, catalogResult[i].TargetType, catalogResult[i].TargetValuePtr, catalogResult[i].BufferLength, &(catalogResult[i].StrLen_or_Ind));  
  
   retCode = SQLTables( hstmt, (SQLWCHAR*)SQL_ALL_CATALOGS, SQL_NTS, L"", SQL_NTS, L"", SQL_NTS, L"", SQL_NTS );  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
  
   retCode = SQLTables( hstmt, dbName, SQL_NTS, userName, SQL_NTS, L"%", SQL_NTS, L"TABLE", SQL_NTS );  
  
   for ( retCode = SQLFetch(hstmt) ; retCode == SQL_SUCCESS || retCode == SQL_SUCCESS_WITH_INFO ; retCode = SQLFetch(hstmt), ++count )  
      if ( count == 1 )  
         StringCchPrintfW( firstTableName, 1024, L"%hs", catalogResult[2].TargetValuePtr );  
   retCode = SQLFreeStmt(hstmt, SQL_CLOSE);  
  
   wprintf( L"Select all data from the first table (%s)\n", firstTableName );  
   StringCchPrintfW( selectAllQuery, bufferSize, L"SELECT * FROM %s", firstTableName );  
  
   retCode = SQLExecDirect(hstmt, selectAllQuery, SQL_NTS);  
   printStatementResult(hstmt);  
}  
```  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Programa de ejemplo de ODBC](../../../odbc/reference/sample-odbc-program.md)
