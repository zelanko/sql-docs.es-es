---
title: Función SQLColAttribute | Documentos de Microsoft
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
- SQLColAttribute
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLColAttribute
helpviewer_keywords:
- SQLColAttribute function [ODBC]
ms.assetid: 8c45c598-cb01-4789-a571-e93619a18ed9
caps.latest.revision: 42
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5afbe6bbea4e1c50e3b16742bf5d0fa1b3c16a9d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="sqlcolattribute-function"></a>Función SQLColAttribute
**Conformidad**  
 Versión introdujo: ODBC 3.0 normativas: ISO 92  
  
 **Resumen**  
 **SQLColAttribute** devuelve información del descriptor para una columna de un conjunto de resultados. Información del descriptor se devuelve como una cadena de caracteres, un valor de descriptor dependiente o un valor entero.  
  
> [!NOTE]  
>  Para obtener más información acerca de qué el Administrador de controladores asigna esta función cuando una aplicación ODBC 3. *x* aplicación está trabajando con una API ODBC 2. *x* controladores, consulte [asignación de funciones de reemplazo para compatibilidad con versiones anteriores de aplicaciones](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
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
 [Entrada] El número del registro en IRD desde el que el valor del campo es va a recuperar. Este argumento se corresponde con el número de columna de datos de resultados, ordenados de forma secuencial en orden creciente de columna, comenzando por 1. Las columnas se pueden describir en cualquier orden.  
  
 En este argumento, se puede especificar la columna 0, pero todos los valores excepto SQL_DESC_TYPE y SQL_DESC_OCTET_LENGTH devolverá valores sin definir.  
  
 *FieldIdentifier*  
 [Entrada] El identificador de descriptor. Este identificador define qué campo IRD se debe consultar (por ejemplo, SQL_COLUMN_TABLE_NAME).  
  
 *CharacterAttributePtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el valor de la *FieldIdentifier* campo de la *ColumnNumber* fila de IRD, si el campo es una cadena de caracteres. En caso contrario, el campo no se utiliza.  
  
 Si *CharacterAttributePtr* es NULL, *StringLengthPtr* devolverá el número total de bytes (sin incluir el carácter de terminación null para los datos de carácter) disponible para devolver en el búfer que señala *CharacterAttributePtr*.  
  
 *BufferLength*  
 [Entrada] Si *FieldIdentifier* es un campo definido en ODBC y *CharacterAttributePtr* apunta a una cadena de caracteres o el búfer binario, este argumento debe ser la longitud de \*  *CharacterAttributePtr*. Si *FieldIdentifier* es un campo definido en ODBC y \* *CharacterAttribute*Ptr es un entero, se omite este campo. Si el  *\*CharacterAttributePtr* es una cadena Unicode (cuando se llama a **SQLColAttributeW**), el *BufferLength* el argumento debe ser un número par. Si *FieldIdentifier* es un campo definido por el controlador, la aplicación indica la naturaleza del campo para el Administrador de controladores al establecer el *BufferLength* argumento. *BufferLength* puede tener los valores siguientes:  
  
-   Si *CharacterAttributePtr* es un puntero a un puntero, *BufferLength* debería tener el valor SQL_IS_POINTER.  
  
-   Si *CharacterAttributePtr* es un puntero a una cadena de caracteres, el *BufferLength* es la longitud del búfer.  
  
-   Si *CharacterAttributePtr* es un puntero a un búfer binario, los lugares de la aplicación en el resultado de la SQL_LEN_BINARY_ATTR (*longitud*) macro en *BufferLength*. Esto coloca un valor negativo en *BufferLength*.  
  
-   Si *CharacterAttributePtr* es un puntero a un tipo de datos de longitud fija, *BufferLength* debe ser uno de los siguientes: SQL_IS_INTEGER, SQL_IS_UNINTEGER, SQL_SMALLINT o SQLUSMALLINT.  
  
 *StringLengthPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número total de bytes (excepto el byte de finalización en null para los datos de carácter) disponible para devolver en **CharacterAttributePtr*.  
  
 Para datos de caracteres, si el número de bytes disponible para devolver es mayor o igual que *BufferLength*, la información del descriptor de \* *CharacterAttributePtr* se trunca a  *BufferLength* menos la longitud de un carácter de terminación null y termina en null el controlador.  
  
 Para los demás tipos de datos, el valor de *BufferLength* se omite y el controlador se supone que el tamaño de **CharacterAttributePtr* es de 32 bits.  
  
 *NumericAttributePtr*  
 [Salida] Puntero a un búfer de entero en el que se va a devolver el valor de la *FieldIdentifier* campo de la *ColumnNumber* fila de IRD, si el campo es un tipo de descriptor numérico, como SQL_DESC_COLUMN_LENGTH. En caso contrario, el campo no se utiliza. Tenga en cuenta que algunos controladores pueden escribir solo inferior 32 bits o el bit de orden superior de 16 bits de un búfer y dejar sin cambios. Por lo tanto, las aplicaciones deben inicializar el valor en 0 antes de llamar a esta función.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLColAttribute** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType*de SQL_HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLColAttribute** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena, delimitado truncados|El búfer \* *CharacterAttributePtr* no era lo suficientemente grande como para devolver el valor de cadena completa, por lo que el valor de cadena se ha truncado. Se devuelve la longitud del valor de cadena untruncated en **StringLengthPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07005|Instrucción preparada no un *especificación de cursor*|La instrucción asociada con el *StatementHandle* no devolvió un conjunto de resultados y *FieldIdentifier* no era SQL_DESC_COUNT. No hay ninguna columna para describir.|  
|07009|Índice de descriptor no válido|(DM) el valor especificado para *ColumnNumber* era igual a 0, mientras que el atributo de instrucción de SQL_ATTR_USE_BOOKMARKS fue SQL_UB_OFF.<br /><br /> El valor especificado para el argumento *ColumnNumber* era mayor que el número de columnas del conjunto de resultados.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagField** de los datos de diagnóstico estructura describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle*. A continuación, se llama a la función nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se llamó en la *StatementHandle* desde un subproceso distinto en un aplicaciones multiproceso.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónicas aún se estaba ejecutando cuando se llamó a SQLColAttribute.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* devolvió SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llama a la función antes de llamar a **SQLPrepare**, **SQLExecDirect**, o una función de catálogo para el *StatementHandle*.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica (no esta uno) para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM)  *\*CharacterAttributePtr* es una cadena de caracteres y *BufferLength* era menor que 0, pero no es igual a SQL_NTS.|  
|HY091|Identificador de campo descriptor no válido|El valor especificado para el argumento *FieldIdentifier* no era uno de los valores definidos y no era un valor definido por la implementación.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Controlador no capaz.|El valor especificado para el argumento *FieldIdentifier* no era compatible con el controlador.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *StatementHandle* no admite la función.|  
|IM017|Sondeo está deshabilitado en el modo de notificación asincrónica|Cada vez que se utiliza el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** se debe llamar en el identificador para realizar el procesamiento posterior a la y completar la operación.|  
  
 Cuando se llama después **SQLPrepare** y antes de **SQLExecute**, **SQLColAttribute** puede devolver cualquier SQLSTATE, que puede ser devueltos por **SQLPrepare**o **SQLExecute**, dependiendo de si el origen de datos se evalúa como la instrucción SQL asociada con el *StatementHandle*.  
  
 Por motivos de rendimiento, una aplicación no debe llamar a **SQLColAttribute** antes de ejecutar una instrucción.  
  
## <a name="comments"></a>Comentarios  
 Para obtener información sobre cómo las aplicaciones utilizan la información devuelta por **SQLColAttribute**, consulte [metadatos del conjunto de resultados](../../../odbc/reference/develop-app/result-set-metadata.md).  
  
 **SQLColAttribute** devuelve información ya sea en \* *NumericAttributePtr* o en \* *CharacterAttributePtr*. Información de entero se devuelve en \* *NumericAttributePtr* como un valor SQLLEN; se devuelven todos los demás formatos de información en \* *CharacterAttributePtr*. Cuando se devuelve información de \* *NumericAttributePtr*, el controlador omite *CharacterAttributePtr*, *BufferLength*, y  *StringLengthPtr*. Cuando se devuelve información de \* *CharacterAttributePtr*, el controlador omite *NumericAttributePtr*.  
  
 **SQLColAttribute** devuelve valores de los campos de descriptor de IRD. Se llama a la función con un identificador de instrucción en lugar de un identificador de descriptor. Los valores devueltos por **SQLColAttribute** para el *FieldIdentifier* valores que se indican más adelante en esta sección también se pueden recuperar mediante una llamada a **SQLGetDescField** con el identificador IRD apropiado.  
  
 Campos de descriptor definido actualmente, la versión de ODBC en el que se introdujeron y los argumentos en el que se devuelve información sobre ellos se muestran más adelante en esta sección; más tipos de descriptor pueden definirse mediante controladores para aprovechar las ventajas de diferentes orígenes de datos.  
  
 Un ODBC 3. *x* controlador debe devolver un valor para cada uno de los campos de descriptor. Si un campo de descriptor no se aplica a un controlador u origen de datos y, a menos que se indique lo contrario, el controlador devuelve 0 en \* *StringLengthPtr* o una cadena vacía en **CharacterAttributePtr*.  
  
## <a name="backward-compatibility"></a>Compatibilidad con versiones anteriores  
 ODBC 3. *x* función **SQLColAttribute** reemplaza el 2 de ODBC en desuso. *x* función **SQLColAttributes**. Al asignar **SQLColAttributes** a **SQLColAttribute** (cuando una API ODBC 2. *x* aplicación está trabajando con una aplicación ODBC 3. *x* controlador), o asignación **SQLColAttribute** a **SQLColAttributes** (cuando una aplicación ODBC 3. *x* aplicación está trabajando con una API ODBC 2. *x* controlador), el Administrador de controladores o pasa el valor de *FieldIdentifier* a través de, lo asigna a un nuevo valor o devuelve un error, como se indica a continuación:  
  
> [!NOTE]  
>  El prefijo usado en *FieldIdentifier* valores en ODBC 3. *x* cambió desde que usa en ODBC 2. *x*. El nuevo prefijo es "SQL_DESC"; el prefijo anterior era "SQL_COLUMN".  
  
-   Si el **#define** valor de la API ODBC 2. *x* *FieldIdentifier* es el mismo que el **#define** valor de ODBC 3. *x* *FieldIdentifier*, solo se pasa el valor de la llamada de función.  
  
-   El **#define** valores de la API ODBC 2. *x* *FieldIdentifiers* SQL_COLUMN_LENGTH, SQL_COLUMN_PRECISION y SQL_COLUMN_SCALE son diferentes de los **#define** valores de ODBC 3. *x* *FieldIdentifiers* SQL_DESC_PRECISION, SQL_DESC_SCALE y SQL_DESC_LENGTH. Un ODBC 2. *x* controlador sólo necesita admitir la API ODBC 2. *x* valores. Un ODBC 3. *x* controlador debe admitir valores "SQL_COLUMN" y "SQL_DESC" para estos tres *FieldIdentifiers*. Estos valores son diferentes porque precisión, escala y longitud se definen de manera diferente en ODBC 3. *x* que estuvieran en ODBC 2. *x*. Para obtener más información, consulte [tamaño de la columna, dígitos decimales, transferencia de longitud de bytes y el tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md).  
  
-   Si el **#define** valor de la API ODBC 2. *x* *FieldIdentifier* es diferente de la **#define** valor de ODBC 3. *x* *FieldIdentifier*, al igual que ocurre con el recuento, nombre, y que aceptan valores NULL, el valor de la llamada de función se asigna al valor correspondiente. Por ejemplo, SQL_COLUMN_COUNT se asigna a SQL_DESC_COUNT, y SQL_DESC_COUNT se asigna a SQL_COLUMN_COUNT, dependiendo de la dirección de la asignación.  
  
-   Si *FieldIdentifier* es un nuevo valor en ODBC 3. *x*, para que no había ningún valor correspondiente en ODBC 2. *x*, no se asignarán cuando una aplicación ODBC 3. *x* aplicación utiliza en una llamada a **SQLColAttribute** en una API ODBC 2. *x* controlador y la llamada devolverá SQLSTATE HY091 (identificador de campo descriptor no válido).  
  
 En la tabla siguiente se enumera los tipos de descriptor devueltos por **SQLColAttribute**. El tipo de *NumericAttributePtr* valores es **SQLLEN \*** .  
  
|*FieldIdentifier*|Información<br /><br /> devuelto en|Description|  
|-----------------------|---------------------------------|-----------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE si la columna es una columna de incremento automático.<br /><br /> SQL_FALSE si la columna no es una columna de incremento automático o no es numérica.<br /><br /> Este campo es válido para solo las columnas de tipo de datos numéricos. Una aplicación puede insertar valores en una fila que contiene una columna de incremento automático, pero normalmente no puede actualizar valores de la columna.<br /><br /> Cuando se realiza una inserción en una columna de incremento automático, se inserta un valor único en la columna en el momento de la inserción. El incremento no está definido, pero es específico del origen de datos. Una aplicación no debe suponer que una columna de incremento automático comienza en cualquier momento determinado o incrementos en cualquier valor determinado.|  
|SQL_DESC_BASE_COLUMN_NAME (ODBC 3.0)|*CharacterAttributePtr*|El nombre de columna base para el resultado de establece la columna. Si no existe un nombre de columna base (como en el caso de las columnas que son expresiones), esta variable contiene una cadena vacía.<br /><br /> Esta información se devuelve del campo de registro SQL_DESC_BASE_COLUMN_NAME de IRD, que es un campo de solo lectura.|  
|SQL_DESC_BASE_TABLE_NAME (ODBC 3.0)|*CharacterAttributePtr*|El nombre de la tabla base que contiene la columna. Si el nombre de tabla base no se puede definir o no es aplicable, a continuación, esta variable contiene una cadena vacía.<br /><br /> Esta información se devuelve del campo de registro SQL_DESC_BASE_TABLE_NAME de IRD, que es un campo de solo lectura.|  
|SQL_DESC_CASE_SENSITIVE (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE si la columna se trata como entre mayúsculas y minúsculas para intercalaciones y comparaciones.<br /><br /> SQL_FALSE si la columna no se trata como entre mayúsculas y minúsculas para intercalaciones y comparaciones o es que no son caracteres.|  
|SQL_DESC_CATALOG_NAME (ODBC 2.0)|*CharacterAttributePtr*|El catálogo de la tabla que contiene la columna. El valor devuelto es la implementación define si la columna es una expresión o si la columna forma parte de una vista. Si el origen de datos no admite catálogos o no se puede determinar el nombre del catálogo, se devuelve una cadena vacía. Este campo de registro VARCHAR no está limitado a 128 caracteres.|  
|SQL_DESC_CONCISE_TYPE (ODBC 1.0)|*NumericAttributePtr*|El tipo de datos concisa.<br /><br /> Para los tipos de datos datetime e interval, este campo devuelve el tipo de datos concisa; Por ejemplo, SQL_TYPE_TIME o SQL_INTERVAL_YEAR. (Para obtener más información, consulte [identificadores de tipo de datos y los descriptores de](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) en tipos de datos de apéndice D:.)<br /><br /> Esta información se devuelve del campo de registro SQL_DESC_CONCISE_TYPE de IRD.|  
|SQL_DESC_COUNT (ODBC 1.0)|*NumericAttributePtr*|El número de columnas disponibles en el conjunto de resultados. Esto devuelve 0 si no hay ninguna columna del conjunto de resultados. El valor de la *ColumnNumber* argumento se omite.<br /><br /> Esta información se devuelve desde el campo de encabezado SQL_DESC_COUNT de IRD.|  
|SQL_DESC_DISPLAY_SIZE (ODBC 1.0)|*NumericAttributePtr*|Número máximo de caracteres necesarios para mostrar los datos de la columna. Para obtener más información sobre el tamaño de presentación, consulte [tamaño de la columna, dígitos decimales, transferir la longitud en octetos y mostrar tamaño](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) en tipos de datos de apéndice D:.|  
|SQL_DESC_FIXED_PREC_SCALE (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE si la columna tiene una precisión fija y una escala es distinto de cero que son específicos del origen de datos.<br /><br /> SQL_FALSE si la columna no tiene una precisión fija y una escala es distinto de cero que son específicos del origen de datos.|  
|SQL_DESC_LABEL (ODBC 2.0)|*CharacterAttributePtr*|La etiqueta de la columna o del título. Por ejemplo, una columna denominada EmpName podría etiquetarse como nombre de empleado o podría estar etiquetada con un alias.<br /><br /> Si una columna no tiene una etiqueta, se devuelve el nombre de columna. Si la columna es sin ninguna etiqueta y sin nombre, se devuelve una cadena vacía.|  
|SQL_DESC_LENGTH (ODBC 3.0)|*NumericAttributePtr*|Un valor numérico que es la longitud de caracteres máximo o real de los datos de cadena o binario de carácter tipo. Es la longitud máxima de caracteres para un tipo de datos de longitud fija o la longitud real de caracteres para un tipo de datos de longitud variable. Su valor siempre excluye el byte de finalización en null que finaliza la cadena de caracteres.<br /><br /> Esta información se devuelve del campo de registro SQL_DESC_LENGTH de IRD.<br /><br /> Para obtener más información acerca de longitud, vea [tamaño de la columna, dígitos decimales, transferencia de longitud de bytes y el tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) en tipos de datos de apéndice D:.|  
|SQL_DESC_LITERAL_PREFIX (ODBC 3.0)|*CharacterAttributePtr*|Este campo de registro varchar (128) contiene el carácter o caracteres que el controlador se reconoce como un prefijo para un literal de este tipo de datos. Este campo contiene una cadena vacía para un tipo de datos para el que no es aplicable un prefijo de literal. Para obtener más información, consulte [Literal prefijos y sufijos](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md).|  
|SQL_DESC_LITERAL_SUFFIX (ODBC 3.0)|*CharacterAttributePtr*|Este campo de registro varchar (128) contiene el carácter o caracteres que el controlador se reconoce como un sufijo para un literal de este tipo de datos. Este campo contiene una cadena vacía para un tipo de datos para el que no es aplicable un sufijo literal. Para obtener más información, consulte [Literal prefijos y sufijos](../../../odbc/reference/develop-app/literal-prefixes-and-suffixes.md).|  
|SQL_DESC_LOCAL_TYPE_NAME (ODBC 3.0)|*CharacterAttributePtr*|Este campo de registro varchar (128) contiene cualquier nombre localizado (idioma nativo) para el tipo de datos que puede ser distinto del nombre del tipo de datos normal. Si no hay ningún nombre localizado, se devuelve una cadena vacía. Este campo es de solo con fines de visualización. El juego de caracteres de la cadena depende de la configuración regional y normalmente es el juego de caracteres predeterminado del servidor.|  
|SQL_DESC_NAME (ODBC 3.0)|*CharacterAttributePtr*|El alias de columna, si corresponde. Si no se aplica el alias de columna, se devuelve el nombre de columna. En cualquier caso, se establece SQL_DESC_UNNAMED en SQL_NAMED. Si no hay ningún nombre de columna o un alias de columna, se devuelve una cadena vacía y SQL_DESC_UNNAMED se establece en SQL_UNNAMED.<br /><br /> Esta información se devuelve del campo de registro SQL_DESC_NAME de IRD.|  
|SQL_DESC_NULLABLE (ODBC 3.0)|*NumericAttributePtr*|SQL_ que acepta valores NULL si la columna puede tener valores NULL; SQL_NO_NULLS si la columna no tiene valores NULL; o SQL_NULLABLE_UNKNOWN si no se sabe si la columna acepta valores NULL.<br /><br /> Esta información se devuelve del campo de registro SQL_DESC_NULLABLE de IRD.|  
|SQL_DESC_NUM_PREC_RADIX (ODBC 3.0)|*NumericAttributePtr*|Si el tipo de datos en el campo SQL_DESC_TYPE es un tipo de datos numéricos aproximados, este campo SQLINTEGER contiene un valor de 2 porque el campo SQL_DESC_PRECISION contiene el número de bits. Si el tipo de datos en el campo SQL_DESC_TYPE es un tipo de datos numéricos exactos, este campo contiene un valor de 10 porque el campo SQL_DESC_PRECISION contiene el número de dígitos decimales. Este campo se establece en 0 para todos los tipos de datos no numéricos.|  
|SQL_DESC_OCTET_LENGTH (ODBC 3.0)|*NumericAttributePtr*|La longitud, en bytes, de un tipo de datos binario o de cadena de caracteres. Para caracteres de longitud fija o tipos binarios, se trata de la longitud real en bytes. Para caracteres de longitud variable o tipos binarios, se trata de la longitud máxima en bytes. Este valor no incluye el terminador nulo.<br /><br /> Esta información se devuelve del campo de registro SQL_DESC_OCTET_LENGTH de IRD.<br /><br /> Para obtener más información acerca de longitud, vea [tamaño de la columna, dígitos decimales, transferencia de longitud de bytes y el tamaño de presentación](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) en tipos de datos de apéndice D:.|  
|SQL_DESC_PRECISION (ODBC 3.0)|*NumericAttributePtr*|Un valor numérico que, para un tipo de datos numéricos, indica la precisión es aplicable. Para tipos de datos SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP, y todos los tipos de datos de intervalo que representan un intervalo de tiempo, su valor es la precisión del componente de fracciones de segundo es aplicable.<br /><br /> Esta información se devuelve del campo de registro SQL_DESC_PRECISION de IRD.|  
|SQL_DESC_SCALE (ODBC 3.0)|*NumericAttributePtr*|Un valor numérico que es la escala es aplicable para un tipo de datos numéricos. Para los tipos de datos DECIMAL y NUMERIC, se trata de la escala definida. No se define para todos los demás tipos de datos.<br /><br /> Esta información se devuelve del campo de registro de escala de IRD.|  
|SQL_DESC_SCHEMA_NAME (ODBC 2.0)|*CharacterAttributePtr*|El esquema de la tabla que contiene la columna. El valor devuelto es la implementación define si la columna es una expresión o si la columna forma parte de una vista. Si el origen de datos no admite esquemas o no se puede determinar el nombre del esquema, se devuelve una cadena vacía. Este campo de registro VARCHAR no está limitado a 128 caracteres.|  
|SQL_DESC_SEARCHABLE (ODBC 1.0)|*NumericAttributePtr*|SQL_PRED_NONE si la columna no se puede usar en una cláusula WHERE. (Este es el mismo que el valor SQL_UNSEARCHABLE en ODBC 2. *x*.)<br /><br /> SQL_PRED_CHAR si la columna se puede utilizar en una cláusula WHERE, pero solo con el predicado LIKE. (Este es el mismo que el valor SQL_LIKE_ONLY en ODBC 2. *x*.)<br /><br /> SQL_PRED_BASIC si la columna se puede utilizar en una cláusula WHERE con todos los operadores de comparación excepto similar. (Este es el mismo que el valor SQL_EXCEPT_LIKE en ODBC 2. *x*.)<br /><br /> SQL_PRED_SEARCHABLE si la columna se puede utilizar en una cláusula WHERE con cualquier operador de comparación.<br /><br /> Las columnas del tipo SQL_LONGVARCHAR y SQL_LONGVARBINARY normalmente devuelto SQL_PRED_CHAR.|  
|SQL_DESC_TABLE_NAME (ODBC 2.0)|*CharacterAttributePtr*|El nombre de la tabla que contiene la columna. El valor devuelto es la implementación define si la columna es una expresión o si la columna forma parte de una vista.<br /><br /> Si no se puede determinar el nombre de tabla, se devuelve una cadena vacía.|  
|SQL_DESC_TYPE (ODBC 3.0)|*NumericAttributePtr*|Un valor numérico que especifica el tipo de datos SQL.<br /><br /> Cuando *ColumnNumber* es igual a 0, se devuelve SQL_BINARY marcadores de longitud variable y se devuelve SQL_INTEGER marcadores de longitud fija.<br /><br /> Para los tipos de datos datetime e interval, este campo devuelve el tipo de datos detallados: SQL_DATETIME o SQL_INTERVAL. (Para obtener más información, consulte [identificadores de tipo de datos y los descriptores de](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md) en tipos de datos de apéndice D:.<br /><br /> Esta información se devuelve del campo de registro SQL_DESC_TYPE de IRD. **Nota:** para trabajar con ODBC 2. *x* controladores, utilice SQL_DESC_CONCISE_TYPE en su lugar.|  
|SQL_DESC_TYPE_NAME (ODBC 1.0)|*CharacterAttributePtr*|Nombre de tipo de datos depende del origen de datos; "Por ejemplo,"CHAR", VARCHAR", "MONEY", "LONG VARBINARY" o "CHAR () para datos de bits".<br /><br /> Si el tipo es desconocido, se devuelve una cadena vacía.|  
|SQL_DESC_UNNAMED (ODBC 3.0)|*NumericAttributePtr*|SQL_NAMED o SQL_UNNAMED. Si el campo SQL_DESC_NAME de IRD contiene un alias de columna o un nombre de columna, se devuelve SQL_NAMED. Si no hay ningún nombre de columna o alias de columna, se devuelve SQL_UNNAMED.<br /><br /> Esta información se devuelve del campo de registro SQL_DESC_UNNAMED de IRD.|  
|SQL_DESC_UNSIGNED (ODBC 1.0)|*NumericAttributePtr*|SQL_TRUE si la columna es sin signo (o no numérico).<br /><br /> SQL_FALSE si la columna está firmada.|  
|SQL_DESC_UPDATABLE (ODBC 1.0)|*NumericAttributePtr*|Columna se describe por los valores de las constantes definidas:<br /><br /> SQL_ATTR_READONLY SQL_ATTR_WRITE SQL_ATTR_READWRITE_UNKNOWN<br /><br /> SQL_DESC_UPDATABLE describe la posibilidad de actualización de la columna del conjunto de resultados, no la columna de la tabla base. La posibilidad de actualización de la columna de base en el que se basa la columna de conjunto de resultados puede ser diferente del valor de este campo. Si una columna es actualizable pueden basarse en el tipo de datos, privilegios de usuario y la definición del propio conjunto de resultados. Si no está claro si una columna es actualizable, debería mostrarse SQL_ATTR_READWRITE_UNKNOWN.|  
  
 **SQLColAttribute** es una alternativa a extensible **SQLDescribeCol**. **SQLDescribeCol** devuelve un conjunto fijo de información del descriptor basado en ANSI-89 SQL. **SQLColAttribute** permite el acceso al conjunto más amplio de información del descriptor disponible en las extensiones de proveedor de ANSI SQL-92 y DBMS.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con una columna en un conjunto de resultados|[Función SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Cancelar el procesamiento de una instrucción|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devolver información acerca de una columna en un conjunto de resultados|[Función SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Captura un bloque de datos o desplazarse a través de un resultado de conjunto|[Función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Recopilación de varias filas de datos|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
  
## <a name="example"></a>Ejemplo  
 El siguiente código de ejemplo no libera identificadores y conexiones. Vea [SQLFreeHandle, función](../../../odbc/reference/syntax/sqlfreehandle-function.md), [ejemplo ODBC programa](../../../odbc/reference/sample-odbc-program.md), y [SQLFreeStmt, función](../../../odbc/reference/syntax/sqlfreestmt-function.md) para obtener ejemplos de código liberar los identificadores y las instrucciones.  
  
```  
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
   SQLPOINTER* columnLabels = (SQLPOINTER *)malloc( numColumn * sizeof(SQLPOINTER*) );  
   struct DataBinding* columnData = (struct DataBinding*)malloc( numColumn * sizeof(struct DataBinding) );  
  
   retCode = SQLNumResultCols(hstmt, &numColumn);  
  
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
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Programa de ejemplo de ODBC](../../../odbc/reference/sample-odbc-program.md)
