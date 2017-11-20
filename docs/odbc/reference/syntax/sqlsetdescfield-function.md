---
title: "Sqlsetdescfield, función | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname:
- SQLSetDescField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetDescField
helpviewer_keywords:
- SQLSetDescField function [ODBC]
ms.assetid: 8c544388-fe9d-4f94-a0ac-fa0b9c9c88a5
caps.latest.revision: 28
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 3a67508ad9e676e679f0458eef8e46960cc72737
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetdescfield-function"></a>Sqlsetdescfield, función
**Conformidad**  
 Versión introdujo: ODBC 3.0 normativas: ISO 92  
  
 **Resumen**  
 **SQLSetDescField** establece el valor de un único campo de un registro del descriptor.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLSetDescField(  
     SQLHDESC      DescriptorHandle,  
     SQLSMALLINT   RecNumber,  
     SQLSMALLINT   FieldIdentifier,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    BufferLength);  
```  
  
## <a name="arguments"></a>Argumentos  
 *DescriptorHandle*  
 [Entrada] Identificador de descriptor.  
  
 *RecNumber*  
 [Entrada] Indica que el registro de descriptor que contiene el campo que intente establecer la aplicación. Registros del descriptor se numeran de 0, con el número de registro 0 es el registro de marcador. El *RecNumber* argumento se omite para los campos de encabezado.  
  
 *FieldIdentifier*  
 [Entrada] Indica el campo del descriptor cuyo valor se va a establecer. Para obtener más información, vea "*FieldIdentifier* argumento" en la sección "Comentarios".  
  
 *ValuePtr*  
 [Entrada] Puntero a un búfer que contiene la información del descriptor o un valor entero. El tipo de datos depende del valor de *FieldIdentifier*. Si *ValuePtr* es un valor entero, puede considerarse como 8 bytes (SQLLEN), 4 bytes (SQLINTEGER) o 2 bytes (SQLSMALLINT), dependiendo del valor de la *FieldIdentifier* argumento.  
  
 *BufferLength*  
 [Entrada] Si *FieldIdentifier* es un campo definido en ODBC y *ValuePtr* apunta a una cadena de caracteres o un búfer binario, este argumento debe ser la longitud de **ValuePtr*. Para los datos de cadena de caracteres, este argumento debe contener el número de bytes en la cadena.  
  
 Si *FieldIdentifier* es un campo definido en ODBC y *ValuePtr* es un entero, *BufferLength* se omite.  
  
 Si *FieldIdentifier* es un campo definido por el controlador, la aplicación indica la naturaleza del campo para el Administrador de controladores al establecer el *BufferLength* argumento. *BufferLength* puede tener los valores siguientes:  
  
-   Si *ValuePtr* es un puntero a una cadena de caracteres, a continuación, *BufferLength* es la longitud de la cadena o SQL_NTS.  
  
-   Si *ValuePtr* es un puntero a un búfer binario, a continuación, la aplicación coloca el resultado de la SQL_LEN_BINARY_ATTR (*longitud*) macro en *BufferLength*. Esto coloca un valor negativo en *BufferLength*.  
  
-   Si *ValuePtr* es un puntero a un valor distinto de una cadena de caracteres o una cadena binaria, a continuación, *BufferLength* debería tener el valor SQL_IS_POINTER.  
  
-   Si *ValuePtr* contiene un valor de longitud fija, a continuación, *BufferLength* es SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT o SQL_IS_USMALLINT, según corresponda.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLSetDescField** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_DESC y un *controlar* de *DescriptorHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLSetDescField** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S02 DE SQLSTATE|Ha cambiado el valor de opción|El controlador no admitía el valor especificado en  *\*ValuePtr* (si *ValuePtr* era un puntero) o el valor en *ValuePtr* (si *ValuePtr*  era un valor entero), o  *\*ValuePtr* no era válido debido a las condiciones de trabajo de implementación, por lo que el controlador sustituye un valor similar. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07009|Índice de descriptor no válido|El *FieldIdentifier* argumento era un campo de registro, el *RecNumber* argumento era 0 y el *DescriptorHandle* argumento hace referencia a un identificador de IPD.<br /><br /> El *RecNumber* argumento era menor que 0 y el *DescriptorHandle* argumento hace referencia a un descartar o un APD.<br /><br /> El *RecNumber* argumento era mayor que el número máximo de columnas o parámetros que el origen de datos puede admitir, y el *DescriptorHandle* argumento hace referencia a un APD o descartar.<br /><br /> (DM) la *FieldIdentifier* argumento era SQL_DESC_COUNT, y  *\*ValuePtr* argumento era menor que 0.<br /><br /> El *RecNumber* argumento era igual a 0 y el *DescriptorHandle* argumento hace referencia a un APD implícitamente asignado. (Este error no se produce con un descriptor de aplicación asignado explícitamente, porque no se sabe si un descriptor de aplicación asignado explícitamente es un APD o descartar hasta que ejecute tiempo.)|  
|08S01|Error de vínculo de comunicación|El vínculo de comunicación entre el controlador y el origen de datos al que se conectó el controlador no pudo antes del procesamiento de la función se ha completado.|  
|22001|Datos de cadena, delimitado truncados|El *FieldIdentifier* argumento era SQL_DESC_NAME y el *BufferLength* argumento era un valor mayor que SQL_MAX_IDENTIFIER_LEN.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY010|Error de secuencia de función|(DM) la *DescriptorHandle* se asoció una *StatementHandle* para que se llamó a una función que se ejecuta asincrónicamente (no esta uno) y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* con la que el *DescriptorHandle* se ha asociado y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión que está asociado el *DescriptorHandle*. Esta función asincrónica aún estaba ejecutando cuando el **SQLSetDescField** se llamó la función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llama para uno de los identificadores de instrucción asociados a la *DescriptorHandle* y devuelve SQL_PARAM_DATA_AVAILABLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY016|No se puede modificar un descriptor de fila de implementación|El *DescriptorHandle* argumento estaba asociado con un IRD y el *FieldIdentifier* argumento no era SQL_DESC_ARRAY_STATUS_PTR o SQL_DESC_ROWS_PROCESSED_PTR.|  
|HY021|Información de descriptor incoherente|Los campos SQL_DESC_TYPE y SQL_DESC_DATETIME_INTERVAL_CODE no forman un tipo válido de SQL de ODBC o un tipo válido de SQL específicas del controlador (para IPD) o un tipo válido de C de ODBC (para APD o en adelante).<br /><br /> Información del descriptor de comprobarse durante una comprobación de coherencia no era coherente. (Consulte "Comprobación de coherencia" en **SQLSetDescRec**.)|  
|HY090|Longitud de búfer o cadena no válida|(DM)  *\*ValuePtr* es una cadena de caracteres y *BufferLength* era menor que cero pero no igual a SQL_NTS.<br /><br /> (DM) el controlador fue un ODBC 2*.x* controlador, el descriptor fue un descartar la *ColumnNumber* argumento se establece en 0 y el valor especificado para el argumento *BufferLength* era no es igual a 4.|  
|HY091|Identificador de campo descriptor no válido|El valor especificado para la *FieldIdentifier* argumento no es un campo definida por ODBC y no era un valor definido por la implementación.<br /><br /> El *FieldIdentifier* argumento no era válido para el *DescriptorHandle* argumento.<br /><br /> El *FieldIdentifier* argumento era un campo de solo lectura, definida por ODBC.|  
|HY092|Identificador de opción o atributo no válido|El valor de  *\*ValuePtr* no era válido para el *FieldIdentifier* argumento.<br /><br /> El *FieldIdentifier* argumento era SQL_DESC_UNNAMED, y *ValuePtr* era SQL_NAMED.|  
|HY105|Tipo de parámetro no válido|(DM) el valor especificado para el campo SQL_DESC_PARAMETER_TYPE no era válido. (Para obtener más información, consulte la "*InputOutputType* argumento" sección **SQLBindParameter**.)|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [What's New en ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *DescriptorHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Una aplicación puede llamar a **SQLSetDescField** para establecer cualquier campo del descriptor de uno en uno. Una llamada a **SQLSetDescField** establece un único campo en un único descriptor. Esta función se puede llamar para establecer cualquier campo de cualquier tipo de descriptor, proporciona que el campo se puede establecer. (Vea la tabla más adelante en esta sección).  
  
> [!NOTE]  
>  Si una llamada a **SQLSetDescField** se produce un error, el contenido del registro de descriptor identificado por la *RecNumber* argumento son indefinidos.  
  
 Puede llamar a otras funciones para establecer varios campos de descriptor con una sola llamada de la función. El **SQLSetDescRec** función establece una serie de campos que afectan al búfer y el tipo de datos enlazados a una columna o parámetro (el SQL_DESC_TYPE, SQL_DESC_DATETIME_INTERVAL_CODE, SQL_DESC_OCTET_LENGTH, SQL_DESC_PRECISION, SQL_ Campos DESC_SCALE, SQL_DESC_DATA_PTR, SQL_DESC_OCTET_LENGTH_PTR y SQL_DESC_INDICATOR_PTR). **SQLBindCol** o **SQLBindParameter** puede utilizarse para realizar una especificación completa para el enlace de una columna o parámetro. Estas funciones establecen un grupo específico de campos de descriptor con una llamada a función.  
  
 **SQLSetDescField** puede llamarse para cambiar los búferes de enlace mediante la adición de un desplazamiento para los punteros de enlace (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR y SQL_DESC_OCTET_LENGTH_PTR). Esto cambia los búferes de enlace sin llamar a **SQLBindCol** o **SQLBindParameter**, que permite que una aplicación cambiar SQL_DESC_DATA_PTR sin cambiar otros campos, como SQL_DESC_DATA_ TIPO.  
  
 Si una aplicación llama **SQLSetDescField** para establecer cualquier campo que no sea SQL_DESC_COUNT o los campos aplazados SQL_DESC_DATA_PTR, SQL_DESC_OCTET_LENGTH_PTR o SQL_DESC_INDICATOR_PTR, en el registro se convierte en independiente.  
  
 Campos de encabezado de descriptor se establecen mediante una llamada a **SQLSetDescField** con el adecuado *FieldIdentifier*. Muchos de los campos de encabezado también son atributos de instrucción, por lo que también se pueden establecer mediante una llamada a **SQLSetStmtAttr**. Esto permite a las aplicaciones establecer un campo descriptor sin obtener primero un identificador de descriptor. Cuando **SQLSetDescField** se llama para establecer un campo de encabezado, el *RecNumber* argumento se omite.  
  
 A *RecNumber* 0 se usa para establecer campos de marcador.  
  
> [!NOTE]  
>  El atributo de instrucción SQL_ATTR_USE_BOOKMARKS siempre se debe establecer antes de llamar a **SQLSetDescField** para establecer campos de marcador. Aunque esto no es obligatorio, se recomienda encarecidamente.  
  
## <a name="sequence-of-setting-descriptor-fields"></a>Secuencia de campos de Descriptor de configuración  
 Al establecer campos de descriptor mediante una llamada a **SQLSetDescField**, la aplicación debe seguir una secuencia específica:  
  
1.  La aplicación debe establecer primero el campo SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE o SQL_DESC_DATETIME_INTERVAL_CODE.  
  
2.  Una vez se ha establecido uno de estos campos, la aplicación puede establecer un atributo de un tipo de datos y el controlador establece los campos de atributos de tipo de datos a los valores predeterminados adecuados para el tipo de datos. Automática toma como valor predeterminado de campos de atributo de tipo garantiza que el descriptor de siempre esté listo para su uso una vez que la aplicación ha especificado un tipo de datos. Si la aplicación establece explícitamente un atributo de tipo de datos, que reemplaza el atributo predeterminado.  
  
3.  Después de que se ha establecido uno de los campos enumerados en el paso 1, y se han establecido los atributos de tipo de datos, la aplicación puede establecer SQL_DESC_DATA_PTR. Esto provoca una comprobación de coherencia de campos de descriptor. Si la aplicación cambia el tipo de datos o los atributos después de establecer el campo SQL_DESC_DATA_PTR, el controlador establece SQL_DESC_DATA_PTR en un puntero nulo, desenlaza el registro. Esto obliga a la aplicación para completar los pasos adecuados en secuencia, antes de que se puede usar el registro del descriptor.  
  
## <a name="initialization-of-descriptor-fields"></a>Inicialización de campos de Descriptor  
 Cuando se asigna un descriptor, los campos del descriptor de pueden inicializarse con un valor predeterminado, se pueden inicializar sin un valor predeterminado o se define para el tipo de descriptor. Las tablas siguientes indican la inicialización de cada campo para cada tipo de descriptor con "D", que indica que el campo se inicializa con un valor predeterminado y "ND" que indica que el campo se inicializa sin valor predeterminado. Si se muestra un número, el valor predeterminado del campo es ese número. Las tablas también indican si un campo es de lectura/escritura (lectura/escritura) o solo lectura (R).  
  
 Los campos de un IRD tienen un valor predeterminado una vez se ha preparado la instrucción o se ha ejecutado y se ha rellenado IRD, no cuando se ha asignado el identificador de instrucción o descriptor. Hasta que se haya rellenado IRD, cualquier intento de obtener acceso a un campo de un IRD devolverá un error.  
  
 Algunos campos del descriptor se definen para uno o más, pero no todos, de los tipos de descriptor (en adelante y IRDs y APD e IPD). Cuando un campo no está definido para un tipo de descriptor, no es necesario por cualquiera de las funciones que usan ese descriptor.  
  
 Los campos que pueden tener acceso a **SQLGetDescField** necesariamente no se puede establecer **SQLSetDescField**. Campos que se pueden establecer por **SQLSetDescField** se enumeran en las tablas siguientes.  
  
 La inicialización de campos de encabezado se describe en la tabla siguiente.  
  
|Nombre del campo de encabezado|Tipo|L/E|Predeterminado|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_ALLOC_TYPE|SQLSMALLINT|DESCARTAR: R APD: R IRD: R IPD: R|Descartar: SQL_DESC_ALLOC_AUTO para implícita o SQL_DESC_ALLOC_USER para explícita<br /><br /> APD: SQL_DESC_ALLOC_AUTO para implícita o SQL_DESC_ALLOC_USER para explícita<br /><br /> IRD: SQL_DESC_ALLOC_AUTO<br /><br /> IPD: SQL_DESC_ALLOC_AUTO|  
|SQL_DESC_ARRAY_SIZE|SQLULEN|Descartar: Lectura/escritura APD: lectura/escritura IRD: sin usar IPD: sin usar|Descartar: APD [1]: [1] IRD: sin usar IPD: sin usar|  
|SQL_DESC_ARRAY_STATUS_PTR|SQLUSMALLINT *|DESCARTAR: LECTURA/ESCRITURA APD: LECTURA/ESCRITURA IRD: IPD DE LECTURA/ESCRITURA: LECTURA/ESCRITURA|Descartar: Null ptr APD: Null ptr IRD: Null ptr IPD: Null ptr|  
|SQL_DESC_BIND_OFFSET_PTR|SQLLEN *|Descartar: Lectura/escritura APD: lectura/escritura IRD: sin usar IPD: sin usar|Descartar: Null ptr APD: Null ptr IRD: sin usar IPD: sin usar|  
|SQL_DESC_BIND_TYPE|SQLINTEGER|Descartar: Lectura/escritura APD: lectura/escritura IRD: sin usar IPD: sin usar|DESCARTAR: SQL_BIND_BY_COLUMN<br /><br /> APD: SQL_BIND_BY_COLUMN<br /><br /> IRD: sin usar<br /><br /> IPD: sin usar|  
SQL_DESC_COUNT|SQLSMALLINT|DESCARTAR: LECTURA/ESCRITURA APD: LECTURA/ESCRITURA IRD: R IPD: LECTURA/ESCRITURA|DESCARTAR: 0 APD: IRD 0: D IPD: 0|  
|SQL_DESC_ROWS_PROCESSED_PTR|SQLULEN *|Descartar: Sin usar APD: sin usar IRD: lectura/escritura IPD: lectura/escritura|Descartar: Sin usar APD: sin usar IRD: Null ptr IPD: Null ptr|  
  
 [1] estos campos se definen solo cuando el IPD se rellena automáticamente con el controlador. Si no es así, no están definidos. Si una aplicación intenta establecer estos campos, SQLSTATE HY091 devolverá (identificador de campo descriptor no válido).  
  
 La inicialización de campos de registro es como se muestra en la tabla siguiente.  
  
|Nombre del campo de registro|Tipo|L/E|Predeterminado|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|Descartar: Sin usar APD: sin usar IRD: R IPD: sin usar|Descartar: Sin usar APD: sin usar IRD: D IPD: sin usar|  
|SQL_DESC_BASE_COLUMN_NAME|SQLCHAR *|Descartar: Sin usar APD: sin usar IRD: R IPD: sin usar|Descartar: Sin usar APD: sin usar IRD: D IPD: sin usar|  
|SQL_DESC_BASE_TABLE_NAME|SQLCHAR *|Descartar: Sin usar APD: sin usar IRD: R IPD: sin usar|Descartar: Sin usar APD: sin usar IRD: D IPD: sin usar|  
|SQL_DESC_CASE_SENSITIVE|SQLINTEGER|Descartar: Sin usar APD: sin usar IRD: R IPD: R|Descartar: Sin usar APD: sin usar IRD: D IPD: D. [1]|  
|SQL_DESC_CATALOG_NAME|SQLCHAR *|Descartar: Sin usar APD: sin usar IRD: R IPD: sin usar|Descartar: Sin usar APD: sin usar IRD: D IPD: sin usar|  
|SQL_DESC_CONCISE_TYPE|SQLSMALLINT|DESCARTAR: LECTURA/ESCRITURA APD: LECTURA/ESCRITURA IRD: R IPD: LECTURA/ESCRITURA|DESCARTAR: SQL_C_ PREDETERMINADO APD: SQL_C_ PREDETERMINADO IRD: D IPD: ND|  
|SQL_DESC_DATA_PTR|SQLPOINTER|Descartar: Lectura/escritura APD: lectura/escritura IRD: sin usar IPD: sin usar|Descartar: Null ptr APD: Null ptr IRD: sin usar IPD: [2] no utilizadas|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQLSMALLINT|DESCARTAR: LECTURA/ESCRITURA APD: LECTURA/ESCRITURA IRD: R IPD: LECTURA/ESCRITURA|DESCARTAR: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|SQLINTEGER|DESCARTAR: LECTURA/ESCRITURA APD: LECTURA/ESCRITURA IRD: R IPD: LECTURA/ESCRITURA|DESCARTAR: ND APD: ND IRD: D IPD: ND|  
SQL_DESC_DISPLAY_SIZE|SQLLEN|Descartar: Sin usar APD: sin usar IRD: R IPD: sin usar|Descartar: Sin usar APD: sin usar IRD: D IPD: sin usar|  
|SQL_DESC_FIXED_PREC_SCALE|SQLSMALLINT|Descartar: Sin usar APD: sin usar IRD: R IPD: R|Descartar: Sin usar APD: sin usar IRD: D IPD: D. [1]|  
|SQL_DESC_INDICATOR_PTR|SQLLEN *|Descartar: Lectura/escritura APD: lectura/escritura IRD: sin usar IPD: sin usar|Descartar: Null ptr APD: Null ptr IRD: sin usar IPD: sin usar|  
|SQL_DESC_LABEL|SQLCHAR *|Descartar: Sin usar APD: sin usar IRD: R IPD: sin usar|Descartar: Sin usar APD: sin usar IRD: D IPD: sin usar|  
|SQL_DESC_LENGTH|SQLULEN|DESCARTAR: LECTURA/ESCRITURA APD: LECTURA/ESCRITURA IRD: R IPD: LECTURA/ESCRITURA|DESCARTAR: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_LITERAL_PREFIX|SQLCHAR *|Descartar: Sin usar APD: sin usar IRD: R IPD: sin usar|Descartar: Sin usar APD: sin usar IRD: D IPD: sin usar|  
|SQL_DESC_LITERAL_SUFFIX|SQLCHAR *|Descartar: Sin usar APD: sin usar IRD: R IPD: sin usar|Descartar: Sin usar APD: sin usar IRD: D IPD: sin usar|  
|SQL_DESC_LOCAL_TYPE_NAME|SQLCHAR *|Descartar: Sin usar APD: sin usar IRD: R IPD: R|Descartar: Sin usar APD: sin usar IRD: D IPD: D. [1]|  
|SQL_DESC_NAME|SQLCHAR *|Descartar: Sin usar APD: sin usar IRD: R IPD: lectura/escritura|DESCARTAR: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_NULLABLE|SQLSMALLINT|Descartar: Sin usar APD: sin usar IRD: R IPD: R|DESCARTAR: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_NUM_PREC_RADIX|SQLINTEGER|DESCARTAR: LECTURA/ESCRITURA APD: LECTURA/ESCRITURA IRD: R IPD: LECTURA/ESCRITURA|DESCARTAR: ND APD: ND IRD: D IPD: ND|  
SQL_DESC_OCTET_LENGTH|SQLLEN|DESCARTAR: LECTURA/ESCRITURA APD: LECTURA/ESCRITURA IRD: R IPD: LECTURA/ESCRITURA|DESCARTAR: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_OCTET_LENGTH_PTR|SQLLEN *|Descartar: Lectura/escritura APD: lectura/escritura IRD: sin usar IPD: sin usar|Descartar: Null ptr APD: Null ptr IRD: sin usar IPD: sin usar|  
|SQL_DESC_PARAMETER_TYPE|SQLSMALLINT|Descartar: Sin usar APD: sin usar IRD: IPD sin usar: lectura/escritura|Descartar: Sin usar APD: sin usar IRD: sin usar IPD: D. = SQL_PARAM_INPUT|  
|SQL_DESC_PRECISION|SQLSMALLINT|DESCARTAR: LECTURA/ESCRITURA APD: LECTURA/ESCRITURA IRD: R IPD: LECTURA/ESCRITURA|DESCARTAR: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_ROWVER|SQLSMALLINT|Descartar: sin usar<br /><br /> APD: sin usar<br /><br /> IRD: R<br /><br /> IPD: R|Descartar: sin usar<br /><br /> APD: sin usar<br /><br /> IRD: ND<br /><br /> IPD: ND|  
|SQL_DESC_SCALE|SQLSMALLINT|DESCARTAR: LECTURA/ESCRITURA APD: LECTURA/ESCRITURA IRD: R IPD: LECTURA/ESCRITURA|DESCARTAR: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_SCHEMA_NAME|SQLCHAR *|Descartar: Sin usar APD: sin usar IRD: R IPD: sin usar|Descartar: Sin usar APD: sin usar IRD: D IPD: sin usar|  
|SQL_DESC_SEARCHABLE|SQLSMALLINT|Descartar: Sin usar APD: sin usar IRD: R IPD: sin usar|Descartar: Sin usar APD: sin usar IRD: D IPD: sin usar|  
|SQL_DESC_TABLE_NAME|SQLCHAR *|Descartar: Sin usar APD: sin usar IRD: R IPD: sin usar|Descartar: Sin usar APD: sin usar IRD: D IPD: sin usar|  
|SQL_DESC_TYPE|SQLSMALLINT|DESCARTAR: LECTURA/ESCRITURA APD: LECTURA/ESCRITURA IRD: R IPD: LECTURA/ESCRITURA|DESCARTAR: SQL_C_DEFAULT APD: SQL_C_DEFAULT IRD: D IPD: ND|  
SQL_DESC_TYPE_NAME|SQLCHAR *|Descartar: Sin usar APD: sin usar IRD: R IPD: R|Descartar: Sin usar APD: sin usar IRD: D IPD: D. [1]|  
|SQL_DESC_UNNAMED|SQLSMALLINT|Descartar: Sin usar APD: sin usar IRD: R IPD: lectura/escritura|DESCARTAR: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_UNSIGNED|SQLSMALLINT|Descartar: Sin usar APD: sin usar IRD: R IPD: R|Descartar: Sin usar APD: sin usar IRD: D IPD: D. [1]|  
|SQL_DESC_UPDATABLE|SQLSMALLINT|Descartar: Sin usar APD: sin usar IRD: R IPD: sin usar|Descartar: Sin usar APD: sin usar IRD: D IPD: sin usar|  
  
 [1] estos campos se definen solo cuando el IPD se rellena automáticamente con el controlador. Si no es así, no están definidos. Si una aplicación intenta establecer estos campos, SQLSTATE HY091 devolverá (identificador de campo descriptor no válido).  
  
 [2], el campo SQL_DESC_DATA_PTR en la IPD puede establecerse para forzar una comprobación de coherencia. En una llamada subsiguiente a **SQLGetDescField** o **SQLGetDescRec**, el controlador no tiene que devolver el valor que SQL_DESC_DATA_PTR se estableció en.  
  
## <a name="fieldidentifier-argument"></a>Argumento de FieldIdentifier  
 El *FieldIdentifier* argumento indica el campo descriptor establecerse. Contiene un descriptor de la *encabezado de descriptor,* que consta de los campos de encabezado se describe en la siguiente sección, "Campos de encabezado" y cero o más *registros descriptores,* que consta de los campos de registro se describe en la sección siguiente de la sección "Campos de encabezado".  
  
## <a name="header-fields"></a>Campos de encabezado  
 Cada descriptor tiene un encabezado que consta de los siguientes campos:  
  
 **SQL_DESC_ALLOC_TYPE [All]**  
 Este campo de encabezado SQLSMALLINT de solo lectura especifica si el descriptor de se asigna automáticamente el controlador o explícitamente mediante la aplicación. La aplicación puede obtener, pero no modificar, este campo. El campo se establece en SQL_DESC_ALLOC_AUTO el controlador si el descriptor de se asigna automáticamente el controlador. Si el descriptor de se asigna explícitamente por la aplicación se establece en SQL_DESC_ALLOC_USER por el controlador.  
  
 **SQL_DESC_ARRAY_SIZE [descriptores de aplicación]**  
 En adelante, este campo de encabezado SQLULEN especifica el número de filas del conjunto de filas. Este es el número de filas que se devuelven mediante una llamada a **SQLFetch** o **SQLFetchScroll** o para funcionar con una llamada a **SQLBulkOperations** o **SQLSetPos** .  
  
 En APD, este campo de encabezado SQLULEN especifica el número de valores para cada parámetro.  
  
 El valor predeterminado de este campo es 1. Si SQL_DESC_ARRAY_SIZE es mayor que 1, SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR y SQL_DESC_OCTET_LENGTH_PTR del APD o descartar apuntan a las matrices. La cardinalidad de cada matriz es igual al valor de este campo.  
  
 También puede establecerse mediante una llamada a este campo en el descartar **SQLSetStmtAttr** con el atributo SQL_ATTR_ROW_ARRAY_SIZE. También puede establecerse mediante una llamada a este campo en el APD **SQLSetStmtAttr** con el atributo SQL_ATTR_PARAMSET_SIZE.  
  
 **SQL_DESC_ARRAY_STATUS_PTR [All]**  
 Para cada tipo de descriptor, este SQLUSMALLINT * puntos del campo de encabezado en una matriz de valores SQLUSMALLINT. Estas matrices se denominan como sigue: matriz de Estados (IRD), matriz de Estados de parámetro (IPD), matriz de operación de fila (descartar) y matriz de operación de parámetro (APD) de la fila.  
  
 En IRD, este campo de encabezado señala a una matriz de estado de la fila que contiene los valores de estado después de llamar a **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**, o **SQLSetPos**. La matriz tiene tantos elementos como filas en el conjunto de filas. La aplicación debe asignar una matriz de SQLUSMALLINTs y establezca este campo para que apunte a la matriz. El campo se establece en un puntero null de forma predeterminada. El controlador llenará la matriz, a menos que el campo SQL_DESC_ARRAY_STATUS_PTR se establece en un puntero nulo, en cuyo caso no se genera ningún valor de estado y no se rellena la matriz.  
  
> [!CAUTION]  
>  Comportamiento del controlador es indefinido si la aplicación establece los elementos de la matriz de Estados de fila que apunta el campo SQL_DESC_ARRAY_STATUS_PTR de IRD.  
  
 La matriz se rellena inicialmente con una llamada a **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**, o **SQLSetPos**. Si la llamada no devolvió SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, el contenido de la matriz señalada por este campo es indefinido. Los elementos de la matriz pueden contener los siguientes valores:  
  
-   SQL_ROW_SUCCESS: La fila se ha obtenido correctamente y no ha cambiado desde que se capturó en último lugar.  
  
-   SQL_ROW_SUCCESS_WITH_INFO: La fila se ha obtenido correctamente y no ha cambiado desde que se capturó en último lugar. Sin embargo, se devuelve una advertencia acerca de la fila.  
  
-   SQL_ROW_ERROR: Se produjo un error al capturar la fila.  
  
-   SQL_ROW_UPDATED: La fila se ha obtenido correctamente y se ha actualizado desde que se capturó en último lugar. Si la fila se vuelve a recopilar, su estado es SQL_ROW_SUCCESS.  
  
-   SQL_ROW_DELETED: Se eliminó la fila desde la última vez se recopiló.  
  
-   SQL_ROW_ADDED: La fila se ha insertado por **SQLBulkOperations**. Si la fila se vuelve a recopilar, su estado es SQL_ROW_SUCCESS.  
  
-   SQL_ROW_NOROW: El conjunto de filas había superpuesta al final del conjunto de resultados y se devuelve ninguna fila que correspondía a este elemento de la matriz de estado de fila.  
  
 Este campo en IRD también puede establecerse mediante una llamada a **SQLSetStmtAttr** con el atributo SQL_ATTR_ROW_STATUS_PTR.  
  
 El campo SQL_DESC_ARRAY_STATUS_PTR de IRD es válido solo después de que se haya devuelto SQL_SUCCESS o SQL_SUCCESS_WITH_INFO. Si el código de retorno no es uno de ellos, la ubicación señalada por SQL_DESC_ROWS_PROCESSED_PTR es indefinida.  
  
 En IPD, este campo de encabezado apunta a una matriz de estado de parámetro que contiene información de estado para cada conjunto de valores de parámetro después de llamar a **SQLExecute** o **SQLExecDirect**. Si la llamada a **SQLExecute** o **SQLExecDirect** no devolvió SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, el contenido de la matriz señalada por este campo son indefinidos. La aplicación debe asignar una matriz de SQLUSMALLINTs y establezca este campo para que apunte a la matriz. El controlador llenará la matriz, a menos que el campo SQL_DESC_ARRAY_STATUS_PTR se establece en un puntero nulo, en cuyo caso no se genera ningún valor de estado y no se rellena la matriz. Los elementos de la matriz pueden contener los siguientes valores:  
  
-   SQL_PARAM_SUCCESS: La instrucción SQL se ha ejecutado correctamente para este conjunto de parámetros.  
  
-   SQL_PARAM_SUCCESS_WITH_INFO: La instrucción SQL se ha ejecutado correctamente para este conjunto de parámetros; Sin embargo, la información sobre la advertencia está disponible en la estructura de datos de diagnóstico.  
  
-   SQL_PARAM_ERROR: Se produjo un error en el procesamiento de este conjunto de parámetros. Información de error adicional está disponible en la estructura de datos de diagnóstico.  
  
-   SQL_PARAM_UNUSED: Este conjunto de parámetros se sin usar, posiblemente debido al hecho de que algún conjunto anterior de parámetro ha producido un error que se ha anulado el procesamiento adicional, o porque se estableció SQL_PARAM_IGNORE para ese conjunto de parámetros en la matriz especificada por el SQL_DESC_ARRAY_ Campo STATUS_PTR de la APD.  
  
-   SQL_PARAM_DIAG_UNAVAILABLE: La información de diagnóstico no está disponible. Un ejemplo de esto es cuando el controlador trata a las matrices de parámetros como una unidad monolítica de modo que no genera este nivel de información de error.  
  
 Este campo en el IPD también puede establecerse mediante una llamada a **SQLSetStmtAttr** con el atributo SQL_ATTR_PARAM_STATUS_PTR.  
  
 En el descartar, este campo de encabezado señala a una matriz de operación de fila de valores que se puede establecer la aplicación para indicar si esta fila es omitir **SQLSetPos** operaciones. Los elementos de la matriz pueden contener los siguientes valores:  
  
-   SQL_ROW_PROCEED: La fila se incluye en la operación masiva utilizando **SQLSetPos**. (Esta opción no garantiza que se realizará la operación en la fila. Si la fila tiene el estado SQL_ROW_ERROR en la matriz de Estados de fila IRD, el controlador podría no ser capaz de realizar la operación en la fila.)  
  
-   SQL_ROW_IGNORE: La fila se excluye de la operación masiva utilizando **SQLSetPos**.  
  
 Si no hay elementos de la matriz se establecen, se incluyen todas las filas de la operación masiva. Si el valor del campo SQL_DESC_ARRAY_STATUS_PTR de la descartar es un puntero nulo, se incluyen todas las filas en la operación masiva; la interpretación es el mismo que si el puntero que señala a una matriz válida y para todos los elementos de la matriz son SQL_ROW_PROCEED. Si un elemento de la matriz se establece en SQL_ROW_IGNORE, no se cambia el valor de la matriz de estado de fila para la fila omitida.  
  
 También puede establecerse mediante una llamada a este campo en el descartar **SQLSetStmtAttr** con el atributo SQL_ATTR_ROW_OPERATION_PTR.  
  
 En el APD, este campo de encabezado apunta a una matriz de operación de parámetros de valores que se pueden establecer por la aplicación para indicar si este conjunto de parámetros se omiten cuando **SQLExecute** o **SQLExecDirect**se llama. Los elementos de la matriz pueden contener los siguientes valores:  
  
-   SQL_PARAM_PROCEED: El conjunto de parámetros se incluye en el **SQLExecute** o **SQLExecDirect** llamar.  
  
-   SQL_PARAM_IGNORE: El conjunto de parámetros está excluido de la **SQLExecute** o **SQLExecDirect** llamar.  
  
 Si no hay elementos de la matriz se establecen, se usan todos los conjuntos de parámetros de la matriz en la **SQLExecute** o **SQLExecDirect** llamadas. Si el valor del campo SQL_DESC_ARRAY_STATUS_PTR de la APD es un puntero nulo, se utilizarán todos los conjuntos de parámetros. la interpretación es el mismo que si el puntero que señala a una matriz válida y para todos los elementos de la matriz son SQL_PARAM_PROCEED.  
  
 También puede establecerse mediante una llamada a este campo en el APD **SQLSetStmtAttr** con el atributo SQL_ATTR_PARAM_OPERATION_PTR.  
  
 **SQL_DESC_BIND_OFFSET_PTR [descriptores de aplicación]**  
 Este SQLLEN * puntos del campo de encabezado para el desplazamiento de enlace. Se establece en un puntero null de forma predeterminada. Si este campo no es un puntero nulo, el controlador desreferencia el puntero y agrega el valor sin referencia a cada uno de los campos aplazados que tiene un valor distinto de null en el registro del descriptor (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR y SQL_DESC_OCTET_LENGTH_PTR) al capturar tiempo y utiliza los nuevos valores de puntero al enlazar.  
  
 El desplazamiento de enlace siempre se agrega directamente a los valores de los campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR y SQL_DESC_OCTET_LENGTH_PTR. Si el desplazamiento se cambia a un valor diferente, el nuevo valor todavía se agrega directamente al valor de cada campo de descriptor. El desplazamiento nuevo no se agrega a cualquier desplazamiento anterior junto con el valor del campo.  
  
 Este campo es un *campo diferida*: no se utiliza en el momento en que se establece, pero se usa en un momento posterior con el controlador cuando sea necesario determinar las direcciones para los búferes de datos.  
  
 También puede establecerse mediante una llamada a este campo en el descartar **SQLSetStmtAttr** con el atributo SQL_ATTR_ROW_BIND_OFFSET_PTR. También puede establecerse mediante una llamada a este campo en el descartar **SQLSetStmtAttr** con el atributo SQL_ATTR_PARAM_BIND_OFFSET_PTR.  
  
 Para obtener más información, vea la descripción del enlace de modo de fila en [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) y [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 **SQL_DESC_BIND_TYPE [descriptores de aplicación]**  
 Este campo de encabezado SQLUINTEGER establece la orientación de enlace que se usará para columnas o parámetros de enlace.  
  
 En adelante, este campo especifica la orientación de enlace cuando **SQLFetchScroll** o **SQLFetch** se llama en el identificador de instrucción asociado.  
  
 Para seleccionar el enlace para las columnas, este campo está establecido en SQL_BIND_BY_COLUMN (valor predeterminado).  
  
 También puede establecerse mediante una llamada a este campo en el descartar **SQLSetStmtAttr** con el SQL_ATTR_ROW_BIND_TYPE *atributo*.  
  
 En APD, este campo especifica la orientación de enlace que se usará para los parámetros dinámicos.  
  
 Para seleccionar el enlace de parámetros, este campo está establecido en SQL_BIND_BY_COLUMN (valor predeterminado).  
  
 También puede establecerse mediante una llamada a este campo en el APD **SQLSetStmtAttr** con el SQL_ATTR_PARAM_BIND_TYPE *atributo*.  
  
 **SQL_DESC_COUNT [All]**  
 Este campo de encabezado SQLSMALLINT especifica el índice basado en 1 del registro con el número mayor que contiene los datos. Cuando el controlador establece el descriptor de la estructura de datos, también se debe establecer el campo SQL_DESC_COUNT para mostrar el número de registros es significativo. Cuando una aplicación asigna una instancia de esta estructura de datos, no tiene que especificar el número de registros para reservar espacio para. Como la aplicación especifica el contenido de los registros, el controlador toma las medidas necesarias para asegurarse de que el identificador de descriptor hace referencia a una estructura de datos del tamaño adecuado.  
  
 SQL_DESC_COUNT no es un recuento de todas las columnas de datos que están enlazadas (si el campo está en un descartar) o de todos los parámetros que están enlazados (si el campo está en un APD), pero el número del registro con el número mayor. Si la columna con el número mayor o parámetro no está enlazada, SQL_DESC_COUNT se cambia el número de la columna siguiente con el número mayor o parámetro. Si una columna o un parámetro con un número que es menor que el número de la columna con el número mayor es independiente (mediante una llamada a **SQLBindCol** con el *TargetValuePtr* establecido en un puntero nulo, o **SQLBindParameter** con el *ParameterValuePtr* establecido en un puntero nulo), no se cambia SQL_DESC_COUNT. Si las demás columnas o parámetros se enlazan con un número mayor que el registro con el número mayor que contiene datos, el controlador aumenta automáticamente el valor en el campo SQL_DESC_COUNT. Si todas las columnas que no están enlazadas mediante una llamada a **SQLFreeStmt** con la opción SQL_UNBIND, los campos SQL_DESC_COUNT descartar y IRD se establecen en 0. Si **SQLFreeStmt** se llama con la opción SQL_RESET_PARAMS, los campos SQL_DESC_COUNT en el APD e IPD se establecen en 0.  
  
 El valor de SQL_DESC_COUNT puede establecerse de forma explícita por una aplicación mediante una llamada a **SQLSetDescField**. Si el valor de SQL_DESC_COUNT explícitamente se reduce, eficazmente se quitan todos los registros con números mayores que el nuevo valor en SQL_DESC_COUNT. Si el valor de SQL_DESC_COUNT se establece explícitamente en 0 y el campo está en un descartar, se liberan todos los búferes de datos excepto una columna de marcador enlazado.  
  
 El número de registros en este campo de un descartar no incluye una columna de marcador enlazado. La única manera de deshacer el enlace de una columna de marcador es establecer el campo SQL_DESC_DATA_PTR en un puntero nulo.  
  
 **SQL_DESC_ROWS_PROCESSED_PTR [descriptores de implementación]**  
 En un IRD, este SQLULEN \* puntos del campo de encabezado en un búfer que contiene el número de filas recuperadas después de llamar a **SQLFetch** o **SQLFetchScroll**, o el número de filas afectadas en una operación masiva realiza una llamada a **SQLBulkOperations** o **SQLSetPos**, incluidas las filas de error.  
  
 En un IPD, este SQLUINTEGER * puntos del campo de encabezado en un búfer que contiene el número de conjuntos de parámetros que se han procesado, incluidos los juegos de error. No se devolverá si se trata de un puntero nulo.  
  
 SQL_DESC_ROWS_PROCESSED_PTR sólo es válido después SQL_SUCCESS o SQL_SUCCESS_WITH_INFO ha devuelto después de llamar a **SQLFetch** o **SQLFetchScroll** (para un campo IRD) o **SQLExecute** , **SQLExecDirect**, o **SQLParamData** (para un campo IPD). Si la llamada que se llena el búfer señalado por este campo no devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, el contenido del búfer es indefinido, a menos que devuelva SQL_NO_DATA, en el que caso el valor en el búfer se establece en 0.  
  
 También puede establecerse mediante una llamada a este campo en el descartar **SQLSetStmtAttr** con el atributo SQL_ATTR_ROWS_FETCHED_PTR. También puede establecerse mediante una llamada a este campo en el APD **SQLSetStmtAttr** con el atributo SQL_ATTR_PARAMS_PROCESSED_PTR.  
  
 El búfer señalado por este campo está asignado por la aplicación. Es un búfer de salida diferida establecido por el controlador. Se establece en un puntero null de forma predeterminada.  
  
## <a name="record-fields"></a>Campos de registro  
 Cada descriptor contiene uno o más registros que se compone de campos que definen los datos de las columnas o los parámetros dinámicos, según el tipo de descriptor. Cada registro es una definición completa de una sola columna o parámetro.  
  
 **SQL_DESC_AUTO_UNIQUE_VALUE [IRDs]**  
 Este campo de registro de solo lectura SQLINTEGER contiene SQL_TRUE si la columna es una columna de incremento automático o SQL_FALSE si la columna no es una columna de incremento automático. Este campo es de solo lectura, pero la columna subyacente de incremento automático no es necesariamente de solo lectura.  
  
 **SQL_DESC_BASE_COLUMN_NAME [IRDs]**  
 Este SQLCHAR de solo lectura * campo de registro contiene el nombre de columna base para el resultado de la columna del conjunto. Si no existe un nombre de columna base (como en el caso de las columnas que son expresiones), esta variable contiene una cadena vacía.  
  
 **SQL_DESC_BASE_TABLE_NAME [IRDs]**  
 Este SQLCHAR de solo lectura * campo de registro contiene el nombre de la tabla base para el resultado de la columna del conjunto. Si un nombre de tabla base no se puede definir o no es aplicable, esta variable contiene una cadena vacía.  
  
 **SQL_DESC_CASE_SENSITIVE [descriptores de implementación]**  
 Este campo de registro de solo lectura SQLINTEGER contiene SQL_TRUE si la columna o parámetro se trata como entre mayúsculas y minúsculas para intercalaciones y realizar comparaciones o SQL_FALSE si la columna no se trata como entre mayúsculas y minúsculas para intercalaciones y comparaciones o, si es un caracteres columna.  
  
 **SQL_DESC_CATALOG_NAME [IRDs]**  
 Este SQLCHAR de solo lectura * campo de registro contiene el catálogo de la tabla base que contiene la columna. El valor devuelto es dependiente del controlador si la columna es una expresión o si la columna forma parte de una vista. Si el origen de datos no admite catálogos o no se puede determinar el catálogo, esta variable contiene una cadena vacía.  
  
 **SQL_DESC_CONCISE_TYPE [All]**  
 Este campo de encabezado SQLSMALLINT especifica el tipo de datos concisa para todos los tipos de datos, incluidos los tipos de datos datetime e interval.  
  
 Los valores de los campos SQL_DESC_CONCISE_TYPE, SQL_DESC_TYPE y SQL_DESC_DATETIME_INTERVAL_CODE son interdependientes. Se establece cada vez que uno de los campos, también se debe establecer el otro. SQL_DESC_CONCISE_TYPE se puede establecer mediante una llamada a **SQLBindCol** o **SQLBindParameter**, o **SQLSetDescField**. SQL_DESC_TYPE se puede establecer mediante una llamada a **SQLSetDescField** o **SQLSetDescRec**.  
  
 Si SQL_DESC_CONCISE_TYPE se establece en un tipo de datos conciso que no sea un tipo de datos de fecha y hora o de intervalo, el campo SQL_DESC_TYPE está establecido en el mismo valor y el campo SQL_DESC_DATETIME_INTERVAL_CODE se establece en 0.  
  
 Si SQL_DESC_CONCISE_TYPE se establece en el tipo de datos de fecha y hora o intervalo conciso, el campo SQL_DESC_TYPE está establecido en el tipo detallado correspondiente (SQL_DATETIME o SQL_INTERVAL) y el campo SQL_DESC_DATETIME_INTERVAL_CODE está establecido para el subcódigo adecuado.  
  
 **SQL_DESC_DATA_PTR [descriptores de aplicación e IPD]**  
 Este campo de registro de SQLPOINTER señala a una variable que contendrá el valor del parámetro (APD) o el valor de columna (por en adelante). Este campo es un *campo diferida*. No se utiliza en el momento en que se establece, pero se utiliza para recuperar datos en un momento posterior con el controlador.  
  
 La columna especificada por el campo SQL_DESC_DATA_PTR de la descartar es independiente de si la *TargetValuePtr* argumento en una llamada a **SQLBindCol** es un puntero nulo o si el SQL_DESC_DATA_PTR del campo en el descartar está establecido un la llamada a **SQLSetDescField** o **SQLSetDescRec** a un puntero null. Otros campos no afecta a si el campo SQL_DESC_DATA_PTR se establece en un puntero nulo.  
  
 Si la llamada a **SQLFetch** o **SQLFetchScroll** que rellena el búfer señalado por este campo no devolvió SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, el contenido del búfer es indefinido.  
  
 Cada vez que se establece el campo SQL_DESC_DATA_PTR de APD, descartar o IPD, el controlador comprueba que el valor en el campo SQL_DESC_TYPE contiene uno de los tipos de datos ODBC C válidos o un tipo de datos específico del controlador, y que todos los demás campos que afectan a los tipos de datos son coherentes. Solicite una comprobación de coherencia es el uso único del campo SQL_DESC_DATA_PTR de una IPD. En concreto, si una aplicación establece el campo SQL_DESC_DATA_PTR de una IPD y las llamadas posteriores **SQLGetDescField** en este campo, no se necesariamente devuelve el valor que hubiera establecido. Para obtener más información, consulte "Comprobaciones de coherencia" en [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
 **SQL_DESC_DATETIME_INTERVAL_CODE [All]**  
 Este campo SQLSMALLINT de registro contiene el subcódigo para el tipo de datos datetime o intervalo específico cuando el campo SQL_DESC_TYPE es SQL_DATETIME o SQL_INTERVAL. Esto es cierto para tipos de datos SQL y C. El código está compuesto del nombre del tipo de datos con "Código" que se sustituye por "Tipo" o "C_TYPE" (para tipos de fecha y hora) o "Código" que se sustituye por "Intervalo" o "C_INTERVAL" (para tipos de intervalo).  
  
 Si SQL_DESC_TYPE y SQL_DESC_CONCISE_TYPE en un descriptor de la aplicación se establecen en SQL_C_DEFAULT y el descriptor no está asociado con un identificador de instrucción, el contenido de SQL_DESC_DATETIME_INTERVAL_CODE es indefinido.  
  
 Este campo puede establecerse para los tipos de datos de fecha y hora que aparecen en la tabla siguiente.  
  
|Tipos de fecha y hora|DATETIME_INTERVAL_CODE|  
|--------------------|------------------------------|  
|SQL_TYPE_DATE/SQL_C_TYPE_DATE|SQL_CODE_DATE|  
|SQL_TYPE_TIME/SQL_C_TYPE_TIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP / SQL_C_TYPE_TIMESTAMP|SQL_CODE_TIMESTAMP|  
  
 Este campo puede establecerse para los tipos de datos de intervalo que aparecen en la tabla siguiente.  
  
|Tipo de intervalo|DATETIME_INTERVAL_CODE|  
|-------------------|------------------------------|  
|SQL_INTERVAL_DAY / SQL_C_INTERVAL_DAY|SQL_CODE_DAY|  
|SQL_INTERVAL_DAY_TO_HOUR / SQL_C_INTERVAL_DAY_TO_HOUR|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE / SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_CODE_DAY_TO_MINUTE|  
|SQL_INTERVAL_DAY_TO_SECOND / SQL_C_INTERVAL_DAY_TO_SECOND|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR / SQL_C_INTERVAL_HOUR|SQL_CODE_HOUR|  
QL_INTERVAL_HOUR_TO_MINUTE / SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND / SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE / SQL_C_INTERVAL_MINUTE|SQL_CODE_MINUTE|  
|SQL_INTERVAL_MINUTE_TO_SECOND / SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_CODE_MINUTE_TO_SECOND|  
|SQL_INTERVAL_MONTH / SQL_C_INTERVAL_MONTH|SQL_CODE_MONTH|  
QL_INTERVAL_SECOND / SQL_C_INTERVAL_SECOND|SQL_CODE_SECOND|  
|SQL_INTERVAL_YEAR / SQL_C_INTERVAL_YEAR|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH / SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_CODE_YEAR_TO_MONTH|  
  
 Para obtener más información acerca de los intervalos de datos y este campo, consulte [identificadores de tipo de datos y los descriptores de](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md).  
  
 **SQL_DESC_DATETIME_INTERVAL_PRECISION [All]**  
 Este campo de registro SQLINTEGER contiene el intervalo de precisión del principio si el campo SQL_DESC_TYPE es SQL_INTERVAL. Cuando el campo SQL_DESC_DATETIME_INTERVAL_CODE se establece en un tipo de datos de intervalo, este campo se establece en el intervalo predeterminado de precisión del principio.  
  
 **SQL_DESC_DISPLAY_SIZE [IRDs]**  
 Este campo de registro de solo lectura SQLINTEGER contiene el número máximo de caracteres necesarios para mostrar los datos de la columna.  
  
 **SQL_DESC_FIXED_PREC_SCALE [descriptores de implementación]**  
 Este campo de registro SQLSMALLINT de solo lectura se establece en SQL_TRUE si la columna es una columna numérica exacta y tiene una precisión fija y la escala es distinto de cero, o para SQL_FALSE si la columna no es una columna numérica exacta con una precisión y escala fijas.  
  
 **SQL_DESC_INDICATOR_PTR [descriptores de aplicación]**  
 En adelante, este SQLLEN * grabar campo señala a la variable de indicador. Esta variable contiene SQL_NULL_DATA si el valor de columna es un valor NULL. Para APD, la variable de indicador se establece en SQL_NULL_DATA para especificar los argumentos dinámicos es NULL. En caso contrario, la variable es cero (a menos que los valores de SQL_DESC_INDICATOR_PTR y SQL_DESC_OCTET_LENGTH_PTR son el mismo puntero).  
  
 Si el campo SQL_DESC_INDICATOR_PTR en un descartar es un puntero nulo, el controlador no puede devolver información acerca de si la columna es NULL o no. Si la columna es NULL y SQL_DESC_INDICATOR_PTR es un puntero nulo, se devuelve SQLSTATE 22002 (variable de indicador necesaria, pero no se ha suministrado) cuando el controlador intenta rellenar el búfer después de llamar a **SQLFetch** o  **SQLFetchScroll**. Si la llamada a **SQLFetch** o **SQLFetchScroll** no devolvió SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, el contenido del búfer son indefinidos.  
  
 El campo SQL_DESC_INDICATOR_PTR determina si se ha establecido el campo apuntado a SQL_DESC_OCTET_LENGTH_PTR. Si el valor de datos para una columna es NULL, el controlador establece la variable de indicador en SQL_NULL_DATA. El campo que señala SQL_DESC_OCTET_LENGTH_PTR no está establecido, a continuación. Si no se encuentra un valor NULL durante la operación de captura, el búfer señalado por SQL_DESC_INDICATOR_PTR se establece en cero y el búfer señalado por SQL_DESC_OCTET_LENGTH_PTR se establece en la longitud de los datos.  
  
 Si el campo SQL_DESC_INDICATOR_PTR en un APD es un puntero nulo, la aplicación no puede usar este registro de descriptor para especificar los argumentos es NULL.  
  
 Este campo es un *campo diferida*: no se utiliza en el momento en que se establece, pero se utiliza en un momento posterior con el controlador que indica la nulabilidad (para en adelante) o para determinar la nulabilidad (para APD).  
  
 **SQL_DESC_LABEL [IRDs]**  
 Este SQLCHAR de solo lectura * campo de registro contiene la etiqueta de la columna o del título. Si la columna no tiene una etiqueta, esta variable contiene el nombre de columna. Si la columna sin nombre y sin ninguna etiqueta, esta variable contiene una cadena vacía.  
  
 **SQL_DESC_LENGTH [All]**  
 Este campo de registro SQLULEN es la longitud máxima o real de una cadena de caracteres en caracteres o un tipo de datos binarios en bytes. Es la longitud máxima para un tipo de datos de longitud fija o la longitud real de un tipo de datos de longitud variable. Su valor siempre excluye el carácter de terminación null que finaliza la cadena de caracteres. Para los valores cuyo tipo sea SQL_TYPE_DATE, SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP o uno de los tipos de datos interval SQL, este campo tiene la longitud en caracteres de la representación de cadena de caracteres del valor de fecha y hora o intervalo.  
  
 El valor de este campo puede ser diferente del valor de "longitud" como definida en ODBC 2*.x*. Para obtener más información, consulte [tipos de datos de apéndice D:](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 **SQL_DESC_LITERAL_PREFIX [IRDs]**  
 Este SQLCHAR de solo lectura * campo de registro contiene el carácter o caracteres que el controlador se reconoce como un prefijo para un literal de este tipo de datos. Esta variable contiene una cadena vacía para un tipo de datos para el que no es aplicable un prefijo de literal.  
  
 **SQL_DESC_LITERAL_SUFFIX [IRDs]**  
 Este SQLCHAR de solo lectura * campo de registro contiene el carácter o caracteres que el controlador se reconoce como un sufijo para un literal de este tipo de datos. Esta variable contiene una cadena vacía para un tipo de datos para el que no es aplicable un sufijo literal.  
  
 **SQL_DESC_LOCAL_TYPE_NAME [descriptores de implementación]**  
 Este SQLCHAR de solo lectura * campo de registro contiene cualquier nombre localizado (idioma nativo) para el tipo de datos que puede ser distinto del nombre del tipo de datos normal. Si no hay ningún nombre localizado, se devuelve una cadena vacía. Este campo es de solo con fines de visualización.  
  
 **SQL_DESC_NAME [descriptores de implementación]**  
 Este SQLCHAR * el campo de registro en un descriptor de fila contiene el alias de columna, si corresponde. Si no se aplica el alias de columna, se devuelve el nombre de columna. En cualquier caso, el controlador establece el campo SQL_DESC_UNNAMED en SQL_NAMED cuando establece el campo SQL_DESC_NAME. Si no hay ningún nombre de columna o un alias de columna, el controlador devuelve una cadena vacía en el campo SQL_DESC_NAME y establece el campo SQL_DESC_UNNAMED en SQL_UNNAMED.  
  
 Una aplicación puede establecer el campo SQL_DESC_NAME de una IPD a un nombre de parámetro o un alias para especificar parámetros de procedimiento almacenado por su nombre. (Para obtener más información, consulte [enlazar parámetros por nombre (parámetros con nombre)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md).) El campo SQL_DESC_NAME de un IRD es un campo de solo lectura; SQLSTATE HY091 (identificador de campo descriptor no válido) se devolverá si una aplicación intenta establecerla.  
  
 En IPD, este campo es indefinido si el controlador no admite parámetros con nombre. Si el controlador admite parámetros con nombre y es capaz de describir los parámetros, se devuelve el nombre del parámetro en este campo.  
  
 **SQL_DESC_NULLABLE [descriptores de implementación]**  
 En IRDs, este campo de registro SQLSMALLINT de solo lectura es SQL_NULLABLE si la columna puede tener valores NULL, SQL_NO_NULLS si la columna no tiene valores NULL o SQL_NULLABLE_UNKNOWN si no se sabe si la columna acepta valores NULL. Este campo pertenece a la columna de conjunto de resultados, no la columna base.  
  
 En IPD, este campo siempre se establece en SQL_NULLABLE porque los parámetros dinámicos siempre admiten valores NULL y no se puede establecer por una aplicación.  
  
 **SQL_DESC_NUM_PREC_RADIX [All]**  
 Este campo SQLINTEGER contiene un valor de 2 si el tipo de datos en el campo SQL_DESC_TYPE es un tipo de datos numéricos aproximados, porque el campo SQL_DESC_PRECISION contiene el número de bits. Este campo contiene un valor de 10 si el tipo de datos en el campo SQL_DESC_TYPE es un tipo de datos numéricos exactos, porque el campo SQL_DESC_PRECISION contiene el número de dígitos decimales. Este campo se establece en 0 para todos los tipos de datos no numéricos.  
  
 **SQL_DESC_OCTET_LENGTH [All]**  
 Este campo de registro SQLLEN contiene la longitud, en bytes, de una cadena de caracteres o tipo de datos binario. Para caracteres de longitud fija o tipos binarios, se trata de la longitud real en bytes. Para caracteres de longitud variable o tipos binarios, se trata de la longitud máxima en bytes. Este valor siempre excluye espacio para el carácter de terminación null para los descriptores de implementación de y siempre incluye espacio para el carácter de terminación null para los descriptores de aplicación. Para los datos de aplicación, este campo contiene el tamaño del búfer. Para APD, este campo está definido solo para salida o parámetros de entrada/salida.  
  
 **SQL_DESC_OCTET_LENGTH_PTR [descriptores de aplicación]**  
 Este SQLLEN * grabar campo señala a una variable que va a contener la longitud total en bytes de un argumento dinámico (para los descriptores de parámetros) o de un valor de columna enlazada (para los descriptores de fila).  
  
 Para una APD, este valor se omite para todos los argumentos excepto la cadena de caracteres y binarios; Si este campo apunta a SQL_NTS, el argumento dinámico debe ser terminada en null. Para indicar que un parámetro dependiente será un parámetro de datos en ejecución, una aplicación establece este campo en el registro adecuado de la APD a una variable que, al ejecutar el tiempo, contendrá el valor SQL_DATA_AT_EXEC o el resultado de la macro SQL_LEN_DATA_AT_EXEC . Si hay más de uno de esos campos, SQL_DESC_DATA_PTR puede establecerse en un valor que identifica de forma única el parámetro para la aplicación determinar qué parámetros se solicita.  
  
 Si el campo OCTET_LENGTH_PTR de una descartar es un puntero nulo, el controlador no devuelve información sobre la longitud de la columna. Si el campo SQL_DESC_OCTET_LENGTH_PTR de un APD es un puntero nulo, el controlador se da por supuesto que las cadenas de caracteres y valores binarios son terminada en null. (Los valores binarios no deben estar terminada en null pero deberían contar con una longitud para evitar el truncamiento).  
  
 Si la llamada a **SQLFetch** o **SQLFetchScroll** que rellena el búfer señalado por este campo no devolvió SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, el contenido del búfer es indefinido. Este campo es un *campo diferida*. No se utiliza en el momento en que se establece, pero se usa en un momento posterior con el controlador para determinar o indicar la longitud de bytes de los datos.  
  
 **SQL_DESC_PARAMETER_TYPE [IPD]**  
 Este campo SQLSMALLINT de registro se establece en SQL_PARAM_INPUT para un parámetro de entrada, SQL_PARAM_INPUT_OUTPUT para un parámetro de entrada/salida, SQL_PARAM_OUTPUT para un parámetro de salida, SQL_PARAM_INPUT_OUTPUT_STREAM para un parámetro de transmisión por secuencias de entrada/salida o SQL_ PARAM_OUTPUT_STREAM para un parámetro de salida que se transmite por secuencias. Se establece en SQL_PARAM_INPUT de forma predeterminada.  
  
 Para un IPD, el campo se establece en SQL_PARAM_INPUT de forma predeterminada si el IPD no se rellena automáticamente con el controlador (el atributo de instrucción de SQL_ATTR_ENABLE_AUTO_IPD es SQL_FALSE). Una aplicación debe establecer este campo en el IPD para los parámetros que no son parámetros de entrada.  
  
 **SQL_DESC_PRECISION [All]**  
 Este campo SQLSMALLINT de registro contiene el número de dígitos para un tipo numérico exacto, el número de bits de la mantisa (precisión binaria) para un tipo numérico aproximado, o el número de dígitos en el componente de fracciones de segundo para la SQL_TYPE_TIME, SQL_TYPE Sql_c_type_timestamp o tipo de datos SQL_INTERVAL_SECOND. Este campo está definido para los demás tipos de datos.  
  
 El valor de este campo puede ser diferente del valor de "precisión" como definido en ODBC 2*.x*. Para obtener más información, consulte [tipos de datos de apéndice D:](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 **SQL_DESC_ROWVER [descriptores de implementación]**  
 Este campo SQLSMALLINTrecord indica si una columna se modifica automáticamente por el sistema DBMS cuando se actualiza una fila (por ejemplo, una columna del tipo "timestamp" en SQL Server). El valor de este campo de registro se establece en SQL_TRUE si la columna es una columna de control de versiones de fila y en SQL_FALSE en caso contrario. Este atributo de columna es similar a llamar a **SQLSpecialColumns** con IdentifierType de SQL_ROWVER para determinar si una columna se actualiza automáticamente.  
  
 **SQL_DESC_SCALE [All]**  
 Este campo SQLSMALLINT de registro contiene la escala definida para los tipos de datos decimal y numeric. El campo está definido para los demás tipos de datos.  
  
 El valor de este campo puede ser diferente del valor de "escala", tal como se define en ODBC 2*.x*. Para obtener más información, consulte [tipos de datos de apéndice D:](../../../odbc/reference/appendixes/appendix-d-data-types.md).  
  
 **SQL_DESC_SCHEMA_NAME [IRDs]**  
 Este SQLCHAR de solo lectura * campo de registro contiene el nombre del esquema de la tabla base que contiene la columna. El valor devuelto es dependiente del controlador si la columna es una expresión o si la columna forma parte de una vista. Si el origen de datos no admite los esquemas o no se puede determinar el nombre del esquema, esta variable contiene una cadena vacía.  
  
 **SQL_DESC_SEARCHABLE [IRDs]**  
 Este campo de registro SQLSMALLINT de solo lectura se establece en uno de los siguientes valores:  
  
-   SQL_PRED_NONE si la columna no se puede usar en un **donde** cláusula. (Este es el mismo que el valor SQL_UNSEARCHABLE en ODBC 2*.x*.)  
  
-   SQL_PRED_CHAR si la columna se puede utilizar en una **donde** cláusula pero solo con el **como** predicado. (Este es el mismo que el valor SQL_LIKE_ONLY en ODBC 2*.x*.)  
  
-   SQL_PRED_BASIC si la columna se puede utilizar en una **donde** cláusula con todos los operadores de comparación excepto **como**. (Este es el mismo que el valor SQL_EXCEPT_LIKE en ODBC 2*.x*.)  
  
-   SQL_PRED_SEARCHABLE si la columna se puede utilizar en una **donde** cláusula con cualquier operador de comparación.  
  
 **SQL_DESC_TABLE_NAME [IRDs]**  
 Este SQLCHAR de solo lectura * campo de registro contiene el nombre de la tabla base que contiene esta columna. El valor devuelto es dependiente del controlador si la columna es una expresión o si la columna forma parte de una vista.  
  
 **SQL_DESC_TYPE [All]**  
 Este campo SQLSMALLINT de registro especifica el tipo de datos SQL o C conciso para todos los tipos de datos excepto los tipos de datos datetime e interval. Para los tipos de datos datetime e interval, este campo especifica el tipo de datos detallados, que es SQL_DATETIME o SQL_INTERVAL.  
  
 Siempre que este campo contenga SQL_DATETIME o SQL_INTERVAL, el campo SQL_DESC_DATETIME_INTERVAL_CODE debe contener el subcódigo adecuado para el tipo conciso. Para los tipos de datos de fecha y hora, SQL_DESC_TYPE contiene SQL_DATETIME y el campo SQL_DESC_DATETIME_INTERVAL_CODE contiene un subcódigo para el tipo de datos específicos de fecha y hora. Para los tipos de datos interval, SQL_DESC_TYPE contiene SQL_INTERVAL y el campo SQL_DESC_DATETIME_INTERVAL_CODE contiene un subcódigo para el tipo de datos de un intervalo específico.  
  
 Los valores de los campos SQL_DESC_TYPE y SQL_DESC_CONCISE_TYPE son interdependientes. Se establece cada vez que uno de los campos, también se debe establecer el otro. SQL_DESC_TYPE se puede establecer mediante una llamada a **SQLSetDescField** o **SQLSetDescRec**. SQL_DESC_CONCISE_TYPE se puede establecer mediante una llamada a **SQLBindCol** o **SQLBindParameter**, o **SQLSetDescField**.  
  
 Si SQL_DESC_TYPE está establecido en un tipo de datos conciso que no sea un tipo de datos de fecha y hora o de intervalo, el campo SQL_DESC_CONCISE_TYPE está establecido en el mismo valor y el campo SQL_DESC_DATETIME_INTERVAL_CODE se establece en 0.  
  
 Si SQL_DESC_TYPE está establecido en el valor de datetime detallado o el tipo de datos de intervalo (SQL_DATETIME o SQL_INTERVAL) y el campo SQL_DESC_DATETIME_INTERVAL_CODE está establecido para el subcódigo adecuado, el campo de tipo SQL_DESC_CONCISE se establece en el tipo conciso correspondiente. Al intentar establecer SQL_DESC_TYPE en uno de los tipos de fecha y hora o intervalo concisos devolverá SQLSTATE HY021 (información de descriptor incoherente).  
  
 Cuando se establece el campo SQL_DESC_TYPE mediante una llamada a **SQLBindCol**, **SQLBindParameter**, o **SQLSetDescField**, los siguientes campos se establecen en los siguientes valores predeterminados, como se muestra en la tabla siguiente. Los valores de los campos restantes del mismo registro son indefinidos.  
  
|Valor de SQL_DESC_TYPE|Otros campos se establecen implícitamente|  
|------------------------------|---------------------------------|  
|SQL_CHAR, SQL_VARCHAR, SQL_C_CHAR, SQL_C_VARCHAR|SQL_DESC_LENGTH se establece en 1. SQL_DESC_PRECISION se establece en 0.|  
|SQL_DATETIME|Cuando se establece SQL_DESC_DATETIME_INTERVAL_CODE en SQL_CODE_DATE o SQL_CODE_TIME, SQL_DESC_PRECISION se establece en 0. Cuando se establece en SQL_DESC_TIMESTAMP, SQL_DESC_PRECISION está establecida en 6.|  
|SQL_DECIMAL DE ODBC, SQL_NUMERIC, SQL_C_NUMERIC|SQL_DESC_SCALE se establece en 0. SQL_DESC_PRECISION se establece en la precisión definido por la implementación del tipo de datos correspondiente.<br /><br /> Vea [SQL a C: numérico](../../../odbc/reference/appendixes/sql-to-c-numeric.md) para obtener información sobre cómo enlazar manualmente un valor SQL_C_NUMERIC.|  
|SQL_FLOAT, SQL_C_FLOAT|SQL_DESC_PRECISION se establece en la precisión definido por la implementación predeterminada para SQL_FLOAT.|  
|SQL_INTERVAL|Cuando SQL_DESC_DATETIME_INTERVAL_CODE se establece en un tipo de datos de intervalo, SQL_DESC_DATETIME_INTERVAL_PRECISION está establecido en 2 (el intervalo inicial precisión predeterminada). Cuando el intervalo tiene un componente de segundos, SQL_DESC_PRECISION está establecida en 6 (la precisión de segundos de intervalo predeterminado).|  
  
 Cuando una aplicación llama **SQLSetDescField** para establecer los campos de un descriptor en lugar de llamar a **SQLSetDescRec**, la aplicación en primer lugar debe declarar el tipo de datos. Cuando lo hace, se establece implícitamente el resto de los campos indicado en la tabla anterior. Si alguno de los valores implícitamente conjunto es aceptable, la aplicación, a continuación, puede llamar a **SQLSetDescField** o **SQLSetDescRec** para establecer explícitamente el valor inaceptable.  
  
 **SQL_DESC_TYPE_NAME [descriptores de implementación]**  
 Este SQLCHAR de solo lectura * campo de registro contiene el nombre de tipo depende del origen de datos (por ejemplo, "CHAR", "VARCHAR" y así sucesivamente). Si se desconoce el nombre de tipo de datos, esta variable contiene una cadena vacía.  
  
 **SQL_DESC_UNNAMED [descriptores de implementación]**  
 Este campo SQLSMALLINT de registro en un descriptor de fila se establece mediante el controlador SQL_NAMED o SQL_UNNAMED cuando establece el campo SQL_DESC_NAME. Si el campo SQL_DESC_NAME contiene un alias de columna o el alias de columna no se aplica, el controlador establece el campo SQL_DESC_UNNAMED en SQL_NAMED. Si una aplicación establece el campo SQL_DESC_NAME de una IPD a un nombre de parámetro o el alias, el controlador establece el campo SQL_DESC_UNNAMED de la IPD para SQL_NAMED. Si no hay ningún nombre de columna o un alias de columna, el controlador establece el campo SQL_DESC_UNNAMED en SQL_UNNAMED.  
  
 Una aplicación puede establecer el campo SQL_DESC_UNNAMED de una IPD para SQL_UNNAMED. Un controlador devuelve SQLSTATE HY091 (identificador de campo descriptor no válido) si una aplicación intenta establecer el campo SQL_DESC_UNNAMED de una IPD para SQL_NAMED. El campo SQL_DESC_UNNAMED de un IRD es de solo lectura; SQLSTATE HY091 (identificador de campo descriptor no válido) se devolverá si una aplicación intenta establecerla.  
  
 **SQL_DESC_UNSIGNED [descriptores de implementación]**  
 Este campo de registro SQLSMALLINT de solo lectura se establece en SQL_TRUE si el tipo de columna es sin signo o no numéricos, o SQL_FALSE si el tipo de columna está firmado.  
  
 **SQL_DESC_UPDATABLE [IRDs]**  
 Este campo de registro SQLSMALLINT de solo lectura se establece en uno de los siguientes valores:  
  
-   SQL_ATTR_READ_ONLY si el resultado de la columna del conjunto es de solo lectura.  
  
-   SQL_ATTR_WRITE si el resultado de la columna del conjunto es de lectura y escritura.  
  
-   SQL_ATTR_READWRITE_UNKNOWN si no se conoce si el conjunto de resultados columna es actualizable o no.  
  
 SQL_DESC_UPDATABLE describe la posibilidad de actualización de la columna del conjunto de resultados, no la columna de la tabla base. La posibilidad de actualización de la columna en la tabla base en el que se basa esta columna del conjunto de resultados puede ser diferente del valor de este campo. Si una columna es actualizable pueden basarse en el tipo de datos, privilegios de usuario y la definición del propio conjunto de resultados. Si no está claro si una columna es actualizable, debería mostrarse SQL_ATTR_READWRITE_UNKNOWN.  
  
## <a name="consistency-checks"></a>Comprobaciones de coherencia  
 Se realiza una comprobación de coherencia con el controlador automáticamente cada vez que una aplicación pasa un valor para el campo SQL_DESC_DATA_PTR del descartar, APD o IPD. Si cualquiera de los campos no es coherente con otros campos, **SQLSetDescField** devolverá SQLSTATE HY021 (información de descriptor incoherente). Para obtener más información, vea "Comprobación de coherencia" en [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar una columna|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Enlazar un parámetro|[SQLBindParameter, función](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Obtención de un campo de descriptor|[Sqlgetdescfield, función](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Obtener varios campos de descriptor|[Sqlgetdescrec, función](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Configuración de varios campos de descriptor|[Sqlsetdescrec, función](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)

