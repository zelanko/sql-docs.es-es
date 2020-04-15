---
title: FUNción SQLSetDescField ( SQLSetDescField) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 122d4b26d1d75811d4a8e252378ce8f81ca2c66b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299555"
---
# <a name="sqlsetdescfield-function"></a>Función SQLSetDescField

**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 3.0: ISO 92  
  
 **Resumen**  
 **SQLSetDescField** establece el valor de un único campo de un registro descriptor.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
SQLRETURN SQLSetDescField(  
     SQLHDESC      DescriptorHandle,  
     SQLSMALLINT   RecNumber,  
     SQLSMALLINT   FieldIdentifier,  
     SQLPOINTER    ValuePtr,  
     SQLINTEGER    BufferLength);  
```  
  
## <a name="arguments"></a>Argumentos  
 *DescriptorHandle*  
 [Entrada] Mango del descriptor.  
  
 *RecNumber*  
 [Entrada] Indica el registro descriptor que contiene el campo que la aplicación busca establecer. Los registros de descriptor se numeran desde 0, siendo el número de registro 0 el registro de marcador. El *Argumento RecNumber* se omite para los campos de encabezado.  
  
 *FieldIdentifier*  
 [Entrada] Indica el campo del descriptor cuyo valor se va a establecer. Para obtener más información, vea *"FieldIdentifier* Argument" en la sección "Comentarios".  
  
 *ValuePtr*  
 [Entrada] Puntero a un búfer que contiene la información del descriptor o un valor entero. El tipo de datos depende del valor de *FieldIdentifier*. Si *ValuePtr* es un valor entero, se puede considerar como 8 bytes (SQLLEN), 4 bytes (SQLINTEGER) o 2 bytes (SQLSMALLINT), dependiendo del valor de la *FieldIdentifier* argumento.  
  
 *BufferLength*  
 [Entrada] Si *FieldIdentifier* es un campo definido por ODBC y *ValuePtr* apunta a una cadena de caracteres o un búfer binario, este argumento debe ser la longitud de **ValuePtr*. Para los datos de cadena de caracteres, este argumento debe contener el número de bytes de la cadena.  
  
 Si *FieldIdentifier* es un campo definido por ODBC y *ValuePtr* es un entero, *BufferLength* se omite.  
  
 Si *FieldIdentifier* es un campo definido por el controlador, la aplicación indica la naturaleza del campo para el Administrador de controladores estableciendo el *BufferLength* argumento. *BufferLength* puede tener los siguientes valores:  
  
-   Si *ValuePtr* es un puntero a una cadena de caracteres, *BufferLength* es la longitud de la cadena o SQL_NTS.  
  
-   Si *ValuePtr* es un puntero a un búfer binario, la aplicación coloca el resultado de la macro SQL_LEN_BINARY_ATTR(*length*) en *BufferLength*. Esto coloca un valor negativo en *BufferLength*.  
  
-   Si *ValuePtr* es un puntero a un valor distinto de una cadena de caracteres o una cadena binaria, *BufferLength* debe tener el valor SQL_IS_POINTER.  
  
-   Si *ValuePtr* contiene un valor de longitud fija, *BufferLength* es SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT o SQL_IS_USMALLINT, según corresponda.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLSetDescField** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_DESC y un *identificador* de *DescriptorHandle*. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLSetDescField** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01S02|Valor de opción cambiado|El controlador no admitía el valor especificado en * \*ValuePtr* (si *ValuePtr* era un puntero) o el valor en *ValuePtr* (si *ValuePtr* era un valor entero), o * \*ValuePtr* no era válido debido a las condiciones de trabajo de implementación, por lo que el controlador sustituyó un valor similar. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|07009|Indice de descriptor no válido|El argumento *FieldIdentifier* era un campo de registro, el argumento *RecNumber* era 0 y el argumento *DescriptorHandle* hacía referencia a un identificador IPD.<br /><br /> El *RecNumber* argumento era menor que 0, y el *DescriptorHandle* argumento hace referencia a un ARD o un APD.<br /><br /> El *RecNumber* argumento era mayor que el número máximo de columnas o parámetros que el origen de datos puede admitir y el *DescriptorHandle* argumento hace referencia a un APD o ARD.<br /><br /> (DM) el *FieldIdentifier* argumento era SQL_DESC_COUNT, y * \*ValuePtr* argumento era menor que 0.<br /><br /> El *RecNumber* argumento era igual a 0, y el *DescriptorHandle* argumento hace referencia a un APD asignado implícitamente. (Este error no se produce con un descriptor de aplicación asignado explícitamente, porque no se sabe si un descriptor de aplicación asignado explícitamente es un APD o ARD hasta el tiempo de ejecución.)|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|22001|Datos de cadena truncados a la derecha|El *FieldIdentifier* argumento se SQL_DESC_NAME y el *BufferLength* argumento era un valor mayor que SQL_MAX_IDENTIFIER_LEN.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY010|Error de secuencia de funciones|(DM) el *DescriptorHandle* se asoció con un *StatementHandle* para el que se llamó a una función de ejecución asincrónica (no esta) y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* con el que el *DescriptorHandle* se asoció y devolvió SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.<br /><br /> (DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *DescriptorHandle*. Esta función asincrónica todavía se estaba ejecutando cuando se llamó a la función **SQLSetDescField** .<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para uno de los identificadores de instrucción asociados con el *DescriptorHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY016|No se puede modificar un descriptor de fila de implementación|El *DescriptorHandle* argumento estaba asociado a un IRD y el *FieldIdentifier* argumento no se SQL_DESC_ARRAY_STATUS_PTR ni SQL_DESC_ROWS_PROCESSED_PTR.|  
|HY021|Información de descriptorina incoherente|Los campos SQL_DESC_TYPE y SQL_DESC_DATETIME_INTERVAL_CODE no forman un tipo SQL ODBC válido o un tipo SQL específico del controlador válido (para IPD) o un tipo ODBC C válido (para ACD o ARD).<br /><br /> La información del descriptor comprobada durante una comprobación de coherencia no era coherente. (Consulte "Comprobación de coherencia" en **SQLSetDescRec**.)|  
|HY090|Cadena no válida o longitud de búfer|(DM) * \*ValuePtr* es una cadena de caracteres y *BufferLength* era menor que cero, pero no era igual a SQL_NTS.<br /><br /> (DM) el controlador era un controlador ODBC 2 *.x,* el descriptor era un ARD, el *ColumnNumber* argumento se estableció en 0, y el valor especificado para el argumento *BufferLength* no era igual a 4.|  
|HY091|Identificador de campo descriptor no válido|El valor especificado para el *FieldIdentifier* argumento no era un campo definido por ODBC y no era un valor definido por la implementación.<br /><br /> El *argumento FieldIdentifier* no era válido para el argumento *DescriptorHandle.*<br /><br /> El *argumento FieldIdentifier* era un campo de solo lectura definido por ODBC.|  
|HY092|Identificador de atributo/opción no válido|El valor de * \*ValuePtr* no era válido para el *Argumento FieldIdentifier.*<br /><br /> El *FieldIdentifier* argumento era SQL_DESC_UNNAMED y *ValuePtr* se SQL_NAMED.|  
|HY105|Tipo de parámetro no válido|(DM) El valor especificado para el campo SQL_DESC_PARAMETER_TYPE no era válido. (Para obtener más información, vea la sección "*InputOutputType* Argument" en **SQLBindParameter**.)|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [Novedades de ODBC 3.8](../../../odbc/reference/what-s-new-in-odbc-3-8.md).|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *DescriptorHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Una aplicación puede llamar a **SQLSetDescField** para establecer cualquier campo descriptor de uno en uno. Una llamada a **SQLSetDescField** establece un único campo en un único descriptor. Esta función se puede llamar para establecer cualquier campo en cualquier tipo de descriptor, siempre que se pueda establecer el campo. (Véase la tabla más adelante en esta sección.)  
  
> [!NOTE]  
>  Si se produce un error en una llamada a **SQLSetDescField,** el contenido del registro descriptor identificado por el *RecNumber* argumento es indefinido.  
  
 Se puede llamar a otras funciones para establecer varios campos descriptores con una sola llamada de la función. La función **SQLSetDescRec** establece una variedad de campos que afectan al tipo de datos y al búfer enlazados a una columna o parámetro (los campos SQL_DESC_TYPE, SQL_DESC_DATETIME_INTERVAL_CODE, SQL_DESC_OCTET_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_DATA_PTR, SQL_DESC_OCTET_LENGTH_PTR y SQL_DESC_INDICATOR_PTR). **SQLBindCol** o **SQLBindParameter** se puede utilizar para realizar una especificación completa para el enlace de una columna o parámetro. Estas funciones establecen un grupo específico de campos descriptores con una llamada de función.  
  
 **SQLSetDescField** se puede llamar para cambiar los búferes de enlace mediante la adición de un desplazamiento a los punteros de enlace (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR o SQL_DESC_OCTET_LENGTH_PTR). Esto cambia los búferes de enlace sin llamar a **SQLBindCol** o **SQLBindParameter**, lo que permite a una aplicación cambiar SQL_DESC_DATA_PTR sin cambiar otros campos, como SQL_DESC_DATA_TYPE.  
  
 Si una aplicación llama a **SQLSetDescField** para establecer cualquier campo distinto de SQL_DESC_COUNT o los campos diferidos SQL_DESC_DATA_PTR, SQL_DESC_OCTET_LENGTH_PTR o SQL_DESC_INDICATOR_PTR, el registro se desenlaza.  
  
 Los campos de encabezado del descriptor se establecen llamando a **SQLSetDescField** con el *FieldIdentifier*adecuado. Muchos campos de encabezado también son atributos de instrucción, por lo que también se pueden establecer mediante una llamada a **SQLSetStmtAttr**. Esto permite a las aplicaciones establecer un campo descriptor sin obtener primero un identificador de descriptor. Cuando **SQLSetDescField** se llama para establecer un campo de encabezado, el *RecNumber* argumento se omite.  
  
 Un *RecNumber* de 0 se utiliza para establecer campos de marcador.  
  
> [!NOTE]  
>  El atributo de instrucción SQL_ATTR_USE_BOOKMARKS siempre debe establecerse antes de llamar a **SQLSetDescField** para establecer campos de marcador. Aunque esto no es obligatorio, se recomienda encarecidamente.  
  
## <a name="sequence-of-setting-descriptor-fields"></a>Secuencia de campos descriptores de configuración  
 Al establecer campos descriptores mediante una llamada a **SQLSetDescField**, la aplicación debe seguir una secuencia específica:  
  
1.  La aplicación debe establecer primero el campo SQL_DESC_TYPE, SQL_DESC_CONCISE_TYPE o SQL_DESC_DATETIME_INTERVAL_CODE.  
  
2.  Una vez establecido uno de estos campos, la aplicación puede establecer un atributo de un tipo de datos y el controlador establece los campos de atributo de tipo de datos en los valores predeterminados adecuados para el tipo de datos. El valor predeterminado automático de los campos de atributo de tipo garantiza que el descriptor siempre esté listo para su uso una vez que la aplicación haya especificado un tipo de datos. Si la aplicación establece explícitamente un atributo de tipo de datos, invalida el atributo predeterminado.  
  
3.  Una vez establecido uno de los campos enumerados en el paso 1 y el establecimiento de atributos de tipo de datos, la aplicación puede establecer SQL_DESC_DATA_PTR. Esto solicita una comprobación de coherencia de los campos descriptores. Si la aplicación cambia el tipo de datos o los atributos después de establecer el campo SQL_DESC_DATA_PTR, el controlador establece SQL_DESC_DATA_PTR en un puntero nulo, desvinculando el registro. Esto obliga a la aplicación a completar los pasos adecuados en secuencia, antes de que se pueda usar el registro descriptor.  
  
## <a name="initialization-of-descriptor-fields"></a>Inicialización de campos de Descriptor  
 Cuando se asigna un descriptor, los campos del descriptor se pueden inicializar en un valor predeterminado, inicializarse sin un valor predeterminado o ser indefinidos para el tipo de descriptor. Las tablas siguientes indican la inicialización de cada campo para cada tipo de descriptor, con "D" que indica que el campo se inicializa con un valor predeterminado y "ND" que indica que el campo se inicializa sin un valor predeterminado. Si se muestra un número, el valor predeterminado del campo es ese número. Las tablas también indican si un campo es de lectura/escritura (R/W) o de solo lectura (R).  
  
 Los campos de un IRD tienen un valor predeterminado solo después de que la instrucción se haya preparado o ejecutado y el IRD se haya rellenado, no cuando se haya asignado el identificador o descriptor de la instrucción. Hasta que el IRD se haya rellenado, cualquier intento de obtener acceso a un campo de un IRD devolverá un error.  
  
 Algunos campos descriptores se definen para uno o más, pero no todos, de los tipos de descriptor (ARD y IRD, y AD e IPD). Cuando un campo no está definido para un tipo de descriptor, ninguna de las funciones que utilizan ese descriptor no lo necesita.  
  
 SQLSetDescField no puede establecer necesariamente los campos a los que puede tener acceso **SQLGetDescField** . **SQLSetDescField** Los campos que se pueden establecer mediante **SQLSetDescField** se enumeran en las tablas siguientes.  
  
 La inicialización de los campos de encabezado se describe en la tabla siguiente.  
  
|Nombre del campo de encabezado|Tipo|L/E|Valor predeterminado|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_ALLOC_TYPE|SQLSMALLINT|ARD: R APD: R IRD: R IPD: R|ARD: SQL_DESC_ALLOC_AUTO para implícitos o SQL_DESC_ALLOC_USER para explícitos<br /><br /> APD: SQL_DESC_ALLOC_AUTO para implícitos o SQL_DESC_ALLOC_USER para explícitos<br /><br /> IRD: SQL_DESC_ALLOC_AUTO<br /><br /> IPD: SQL_DESC_ALLOC_AUTO|  
|SQL_DESC_ARRAY_SIZE|SQLULEN|ARD: R/W APD: R/W IRD: IPD no utilizado: No utilizado|ARD:[1] APD:[1] IRD: IPD no utilizado: No utilizado|  
|SQL_DESC_ARRAY_STATUS_PTR|SQLUSMALLINT*|ARD: R/W APD: R/W IRD: R/W IPD: R/W|ARD: Null ptr APD: Null ptr IRD: Null ptr IPD: Null ptr ptr|  
|SQL_DESC_BIND_OFFSET_PTR|SQLLEN*|ARD: R/W APD: R/W IRD: IPD no utilizado: No utilizado|ARD: Null ptr APD: Null ptr IRD: IPD no utilizado: Sin usar|  
|SQL_DESC_BIND_TYPE|SQLINTEGER|ARD: R/W APD: R/W IRD: IPD no utilizado: No utilizado|ARD: SQL_BIND_BY_COLUMN<br /><br /> APD: SQL_BIND_BY_COLUMN<br /><br /> IRD: Sin usar<br /><br /> IPD: Sin usar|  
|SQL_DESC_COUNT|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: 0 APD: 0 IRD: D IPD: 0|  
|SQL_DESC_ROWS_PROCESSED_PTR|SQLULEN*|ARD: APD no utilizado: IRD no utilizado: R / W IPD: R / W|ARD: APD no utilizado: IRD no utilizado: Null ptr IPD: Null ptr ptr|  
  
 [1] Estos campos se definen solo cuando el controlador rellena automáticamente el IPD. Si no, son indefinidos. Si una aplicación intenta establecer estos campos, se devolverá SQLSTATE HY091 (identificador de campo descriptor no válido).  
  
 La inicialización de los campos de registro es como se muestra en la tabla siguiente.  
  
|Nombre del campo de registro|Tipo|L/E|Valor predeterminado|  
|-----------------------|----------|----------|-------------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQLINTEGER|ARD: APD no utilizado: IRD no utilizado: R IPD: Sin usar|ARD: APD no utilizado: IRD no utilizado: D IPD: Sin usar|  
|SQL_DESC_BASE_COLUMN_NAME|SQLCHAR *|ARD: APD no utilizado: IRD no utilizado: R IPD: Sin usar|ARD: APD no utilizado: IRD no utilizado: D IPD: Sin usar|  
|SQL_DESC_BASE_TABLE_NAME|SQLCHAR *|ARD: APD no utilizado: IRD no utilizado: R IPD: Sin usar|ARD: APD no utilizado: IRD no utilizado: D IPD: Sin usar|  
|SQL_DESC_CASE_SENSITIVE|SQLINTEGER|ARD: APD no utilizado: IRD no utilizado: R IPD: R|ARD: APD no utilizado: IRD no utilizado: D IPD: D[1]|  
|SQL_DESC_CATALOG_NAME|SQLCHAR *|ARD: APD no utilizado: IRD no utilizado: R IPD: Sin usar|ARD: APD no utilizado: IRD no utilizado: D IPD: Sin usar|  
|SQL_DESC_CONCISE_TYPE|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: SQL_C_ APD DEFAULT: SQL_C_ DEFAULT IRD: D IPD: ND|  
|SQL_DESC_DATA_PTR|SQLPOINTER|ARD: R/W APD: R/W IRD: IPD no utilizado: No utilizado|ARD: Null ptr APD: Null ptr IRD: IPD no utilizado: No utilizado[2]|  
|SQL_DESC_DATETIME_INTERVAL_CODE|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_DATETIME_INTERVAL_PRECISION|SQLINTEGER|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_DISPLAY_SIZE|SQLLEN|ARD: APD no utilizado: IRD no utilizado: R IPD: Sin usar|ARD: APD no utilizado: IRD no utilizado: D IPD: Sin usar|  
|SQL_DESC_FIXED_PREC_SCALE|SQLSMALLINT|ARD: APD no utilizado: IRD no utilizado: R IPD: R|ARD: APD no utilizado: IRD no utilizado: D IPD: D[1]|  
|SQL_DESC_INDICATOR_PTR|SQLLEN *|ARD: R/W APD: R/W IRD: IPD no utilizado: No utilizado|ARD: Null ptr APD: Null ptr IRD: IPD no utilizado: Sin usar|  
|SQL_DESC_LABEL|SQLCHAR *|ARD: APD no utilizado: IRD no utilizado: R IPD: Sin usar|ARD: APD no utilizado: IRD no utilizado: D IPD: Sin usar|  
|SQL_DESC_LENGTH|SQLULEN|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_LITERAL_PREFIX|SQLCHAR *|ARD: APD no utilizado: IRD no utilizado: R IPD: Sin usar|ARD: APD no utilizado: IRD no utilizado: D IPD: Sin usar|  
|SQL_DESC_LITERAL_SUFFIX|SQLCHAR *|ARD: APD no utilizado: IRD no utilizado: R IPD: Sin usar|ARD: APD no utilizado: IRD no utilizado: D IPD: Sin usar|  
|SQL_DESC_LOCAL_TYPE_NAME|SQLCHAR *|ARD: APD no utilizado: IRD no utilizado: R IPD: R|ARD: APD no utilizado: IRD no utilizado: D IPD: D[1]|  
|SQL_DESC_NAME|SQLCHAR *|ARD: APD no utilizado: IRD no utilizado: R IPD: R /W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_NULLABLE|SQLSMALLINT|ARD: APD no utilizado: IRD no utilizado: R IPD: R|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_NUM_PREC_RADIX|SQLINTEGER|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_OCTET_LENGTH|SQLLEN|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_OCTET_LENGTH_PTR|SQLLEN *|ARD: R/W APD: R/W IRD: IPD no utilizado: No utilizado|ARD: Null ptr APD: Null ptr IRD: IPD no utilizado: Sin usar|  
|SQL_DESC_PARAMETER_TYPE|SQLSMALLINT|ARD: APD no utilizado: IRD no utilizado: IPD no utilizado: R /W|ARD: APD no utilizado: IRD no utilizado: IPD no utilizado: D-SQL_PARAM_INPUT|  
|SQL_DESC_PRECISION|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_ROWVER|SQLSMALLINT|ARD: Sin usar<br /><br /> APD: Sin usar<br /><br /> IRD: R<br /><br /> IPD: R|ARD: Sin usar<br /><br /> APD: Sin usar<br /><br /> IRD: ND<br /><br /> IPD: ND|  
|SQL_DESC_SCALE|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_SCHEMA_NAME|SQLCHAR *|ARD: APD no utilizado: IRD no utilizado: R IPD: Sin usar|ARD: APD no utilizado: IRD no utilizado: D IPD: Sin usar|  
|SQL_DESC_SEARCHABLE|SQLSMALLINT|ARD: APD no utilizado: IRD no utilizado: R IPD: Sin usar|ARD: APD no utilizado: IRD no utilizado: D IPD: Sin usar|  
|SQL_DESC_TABLE_NAME|SQLCHAR *|ARD: APD no utilizado: IRD no utilizado: R IPD: Sin usar|ARD: APD no utilizado: IRD no utilizado: D IPD: Sin usar|  
|SQL_DESC_TYPE|SQLSMALLINT|ARD: R/W APD: R/W IRD: R IPD: R/W|ARD: SQL_C_DEFAULT APD: SQL_C_DEFAULT IRD: D IPD: ND|  
|SQL_DESC_TYPE_NAME|SQLCHAR *|ARD: APD no utilizado: IRD no utilizado: R IPD: R|ARD: APD no utilizado: IRD no utilizado: D IPD: D[1]|  
|SQL_DESC_UNNAMED|SQLSMALLINT|ARD: APD no utilizado: IRD no utilizado: R IPD: R /W|ARD: ND APD: ND IRD: D IPD: ND|  
|SQL_DESC_UNSIGNED|SQLSMALLINT|ARD: APD no utilizado: IRD no utilizado: R IPD: R|ARD: APD no utilizado: IRD no utilizado: D IPD: D[1]|  
|SQL_DESC_UPDATABLE|SQLSMALLINT|ARD: APD no utilizado: IRD no utilizado: R IPD: Sin usar|ARD: APD no utilizado: IRD no utilizado: D IPD: Sin usar|  
  
 [1] Estos campos se definen solo cuando el controlador rellena automáticamente el IPD. Si no, son indefinidos. Si una aplicación intenta establecer estos campos, se devolverá SQLSTATE HY091 (identificador de campo descriptor no válido).  
  
 [2] El campo SQL_DESC_DATA_PTR en el IPD se puede configurar para forzar una comprobación de coherencia. En una llamada posterior a **SQLGetDescField** o **SQLGetDescRec**, el controlador no es necesario para devolver el valor que SQL_DESC_DATA_PTR se estableció en.  
  
## <a name="fieldidentifier-argument"></a>Argumento FieldIdentifier  
 El argumento *FieldIdentifier* indica el campo descriptor que se va a establecer. Un descriptor contiene el encabezado del *descriptor,* que consta de los campos de encabezado descritos en la sección siguiente, "Campos de encabezado", y cero o más *registros descriptores,* que consisten en los campos de registro descritos en la sección siguiente a la sección "Campos de encabezado".  
  
## <a name="header-fields"></a>Campos de encabezado  
 Cada descriptor tiene un encabezado que consta de los siguientes campos:  
  
 **SQL_DESC_ALLOC_TYPE [Todos]**  
 Este campo de encabezado SQLSMALLINT de solo lectura especifica si el controlador o explícitamente el descriptor lo asignó automáticamente. La aplicación puede obtener, pero no modificar, este campo. El campo se establece en SQL_DESC_ALLOC_AUTO por el controlador si el controlador asignó automáticamente el descriptor. Se establece en SQL_DESC_ALLOC_USER por el controlador si la aplicación asignó explícitamente el descriptor.  
  
 **SQL_DESC_ARRAY_SIZE [Descriptores de aplicación]**  
 En los ARD, este campo de encabezado SQLULEN especifica el número de filas del conjunto de filas. Este es el número de filas que se devolverán mediante una llamada a **SQLFetch** o **SQLFetchScroll** o que se debe utilizar mediante una llamada a **SQLBulkOperations** o **SQLSetPos**.  
  
 En los AMEDIANTE, este campo de encabezado SQLULEN especifica el número de valores para cada parámetro.  
  
 El valor predeterminado de este campo es 1. Si SQL_DESC_ARRAY_SIZE es mayor que 1, SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR y SQL_DESC_OCTET_LENGTH_PTR del punto APD o ARD a matrices. La cardinalidad de cada matriz es igual al valor de este campo.  
  
 Este campo de la ARD también se puede establecer llamando a **SQLSetStmtAttr** con el atributo SQL_ATTR_ROW_ARRAY_SIZE. Este campo en el APD también se puede establecer mediante una llamada a **SQLSetStmtAttr** con el SQL_ATTR_PARAMSET_SIZE atributo.  
  
 **SQL_DESC_ARRAY_STATUS_PTR [Todos]**  
 Para cada tipo de descriptor, este campo de encabezado SQLUSMALLINT * apunta a una matriz de valores SQLUSMALLINT. Estas matrices se denominan de la siguiente manera: matriz de estado de fila (IRD), matriz de estado de parámetros (IPD), matriz de operaciones de fila (ARD) y matriz de operaciones de parámetros (APD).  
  
 En el IRD, este campo de encabezado apunta a una matriz de estado de fila que contiene valores de estado después de una llamada a **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**o **SQLSetPos**. La matriz tiene tantos elementos como filas en el conjunto de filas. La aplicación debe asignar una matriz de SQLUSMALLINTs y establecer este campo para que apunte a la matriz. El campo se establece en un puntero nulo de forma predeterminada. El controlador rellenará la matriz- a menos que el campo SQL_DESC_ARRAY_STATUS_PTR se establezca en un puntero nulo, en cuyo caso no se generan valores de estado y la matriz no se rellena.  
  
> [!CAUTION]  
>  El comportamiento del controlador es indefinido si la aplicación establece los elementos de la matriz de estado de fila a los que apunta el campo SQL_DESC_ARRAY_STATUS_PTR del IRD.  
  
 La matriz se rellena inicialmente mediante una llamada a **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**o **SQLSetPos**. Si la llamada no devolvió SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, el contenido de la matriz señalada por este campo es indefinido. Los elementos de la matriz pueden contener los siguientes valores:  
  
-   SQL_ROW_SUCCESS: La fila se ha capturado correctamente y no ha cambiado desde la última vez que se obtuvo.  
  
-   SQL_ROW_SUCCESS_WITH_INFO: La fila se ha capturado correctamente y no ha cambiado desde la última vez que se obtuvo. Sin embargo, se devolvió una advertencia sobre la fila.  
  
-   SQL_ROW_ERROR: Se ha producido un error al capturar la fila.  
  
-   SQL_ROW_UPDATED: La fila se ha capturado correctamente y se ha actualizado desde la última vez que se obtuvo. Si la fila se vuelve a recuperar, su estado es SQL_ROW_SUCCESS.  
  
-   SQL_ROW_DELETED: La fila se ha eliminado desde la última vez que se obtuvo.  
  
-   SQL_ROW_ADDED: **SQLBulkOperations**insertó la fila. Si la fila se vuelve a recuperar, su estado es SQL_ROW_SUCCESS.  
  
-   SQL_ROW_NOROW: el conjunto de filas superpuso el final del conjunto de resultados y no se devolvió ninguna fila que correspondiera a este elemento de la matriz de estado de fila.  
  
 Este campo en el IRD también se puede establecer llamando a **SQLSetStmtAttr** con el atributo SQL_ATTR_ROW_STATUS_PTR.  
  
 El campo SQL_DESC_ARRAY_STATUS_PTR del IRD solo es válido después de que se haya devuelto SQL_SUCCESS o SQL_SUCCESS_WITH_INFO. Si el código de retorno no es uno de ellos, la ubicación a la que apunta SQL_DESC_ROWS_PROCESSED_PTR es indefinida.  
  
 En el IPD, este campo de encabezado apunta a una matriz de estado de parámetro que contiene información de estado para cada conjunto de valores de parámetro después de una llamada a **SQLExecute** o **SQLExecDirect**. Si la llamada a **SQLExecute** o **SQLExecDirect** no devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, el contenido de la matriz señalada por este campo es indefinido. La aplicación debe asignar una matriz de SQLUSMALLINTs y establecer este campo para que apunte a la matriz. El controlador rellenará la matriz- a menos que el campo SQL_DESC_ARRAY_STATUS_PTR se establezca en un puntero nulo, en cuyo caso no se generan valores de estado y la matriz no se rellena. Los elementos de la matriz pueden contener los siguientes valores:  
  
-   SQL_PARAM_SUCCESS: La instrucción SQL se ejecutó correctamente para este conjunto de parámetros.  
  
-   SQL_PARAM_SUCCESS_WITH_INFO: la instrucción SQL se ejecutó correctamente para este conjunto de parámetros; sin embargo, la información de advertencia está disponible en la estructura de datos de diagnóstico.  
  
-   SQL_PARAM_ERROR: Se ha producido un error al procesar este conjunto de parámetros. Información de error adicional está disponible en la estructura de datos de diagnóstico.  
  
-   SQL_PARAM_UNUSED: Este conjunto de parámetros no se utilizó, posiblemente debido al hecho de que algún conjunto de parámetros anterior causó un error que anuló el procesamiento posterior, o porque SQL_PARAM_IGNORE se estableció para ese conjunto de parámetros en la matriz especificada por el campo SQL_DESC_ARRAY_STATUS_PTR del APD.  
  
-   SQL_PARAM_DIAG_UNAVAILABLE: La información de diagnóstico no está disponible. Un ejemplo de esto es cuando el controlador trata matrices de parámetros como una unidad monolítica y por lo tanto no genera este nivel de información de error.  
  
 Este campo de la IPD también se puede establecer llamando a **SQLSetStmtAttr** con el atributo SQL_ATTR_PARAM_STATUS_PTR.  
  
 En el ARD, este campo de encabezado apunta a una matriz de operaciones de fila de valores que puede establecer la aplicación para indicar si esta fila se debe omitir para las operaciones **SQLSetPos.** Los elementos de la matriz pueden contener los siguientes valores:  
  
-   SQL_ROW_PROCEED: la fila se incluye en la operación masiva mediante **SQLSetPos**. (Esta configuración no garantiza que la operación se producirá en la fila. Si la fila tiene el estado SQL_ROW_ERROR en la matriz de estado de fila IRD, es posible que el controlador no pueda realizar la operación en la fila.)  
  
-   SQL_ROW_IGNORE: la fila se excluye de la operación masiva mediante **SQLSetPos**.  
  
 Si no se establece ningún elemento de la matriz, todas las filas se incluyen en la operación masiva. Si el valor del campo SQL_DESC_ARRAY_STATUS_PTR de la ARD es un puntero nulo, todas las filas se incluyen en la operación masiva; la interpretación es la misma que si el puntero apuntaba a una matriz válida y todos los elementos de la matriz se SQL_ROW_PROCEED. Si un elemento de la matriz se establece en SQL_ROW_IGNORE, no se cambia el valor de la matriz de estado de fila para la fila ignorada.  
  
 Este campo de la ARD también se puede establecer llamando a **SQLSetStmtAttr** con el atributo SQL_ATTR_ROW_OPERATION_PTR.  
  
 En el APD, este campo de encabezado apunta a una matriz de operaciones de parámetro de valores que puede establecer la aplicación para indicar si este conjunto de parámetros debe omitirse cuando **SQLExecute** o **SQLExecDirect** se llama. Los elementos de la matriz pueden contener los siguientes valores:  
  
-   SQL_PARAM_PROCEED: el conjunto de parámetros se incluye en la llamada **sqlExecute** o **SQLExecDirect** .  
  
-   SQL_PARAM_IGNORE: el conjunto de parámetros se excluye de la llamada **SQLExecute** o **SQLExecDirect** .  
  
 Si no se establece ningún elemento de la matriz, todos los conjuntos de parámetros de la matriz se utilizan en las llamadas **SQLExecute** o **SQLExecDirect** . Si el valor del campo SQL_DESC_ARRAY_STATUS_PTR del APD es un puntero nulo, se utilizan todos los conjuntos de parámetros; la interpretación es la misma que si el puntero apuntaba a una matriz válida y todos los elementos de la matriz se SQL_PARAM_PROCEED.  
  
 Este campo en el APD también se puede establecer mediante una llamada a **SQLSetStmtAttr** con el atributo SQL_ATTR_PARAM_OPERATION_PTR.  
  
 **SQL_DESC_BIND_OFFSET_PTR [Descriptores de aplicación]**  
 Este campo de encabezado SQLLEN * apunta al desplazamiento de enlace. Se establece en un puntero nulo de forma predeterminada. Si este campo no es un puntero nulo, el controlador desreferencia el puntero y agrega el valor desreferenciado a cada uno de los campos diferidos que tiene un valor no nulo en el registro descriptor (SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR y SQL_DESC_OCTET_LENGTH_PTR) en el momento de la obtención y utiliza los nuevos valores de puntero al enlazar.  
  
 El desplazamiento de enlace siempre se agrega directamente a los valores de los campos SQL_DESC_DATA_PTR, SQL_DESC_INDICATOR_PTR y SQL_DESC_OCTET_LENGTH_PTR. Si el desplazamiento se cambia a un valor diferente, el nuevo valor se sigue agregando directamente al valor en cada campo descriptor. El nuevo desplazamiento no se agrega al valor del campo más ningún desplazamiento anterior.  
  
 Este campo es un *campo diferido:* no se utiliza en el momento en que se establece, pero el controlador lo utiliza más adelante cuando necesita determinar las direcciones de los búferes de datos.  
  
 Este campo de la ARD también se puede establecer llamando a **SQLSetStmtAttr** con el atributo SQL_ATTR_ROW_BIND_OFFSET_PTR. Este campo de la ARD también se puede establecer llamando a **SQLSetStmtAttr** con el atributo SQL_ATTR_PARAM_BIND_OFFSET_PTR.  
  
 Para obtener más información, vea la descripción del enlace de fila en [SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md) y [SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md).  
  
 **SQL_DESC_BIND_TYPE [Descriptores de aplicación]**  
 Este campo de encabezado SQLUINTEGER establece la orientación de enlace que se usará para enlazar columnas o parámetros.  
  
 En ARD, este campo especifica la orientación de enlace cuando **SQLFetchScroll** o **SQLFetch** se llama en el identificador de instrucción asociado.  
  
 Para seleccionar el enlace de columna para las columnas, este campo se establece en SQL_BIND_BY_COLUMN (valor predeterminado).  
  
 Este campo de la ARD también se puede establecer llamando a **SQLSetStmtAttr** con el *atributo*SQL_ATTR_ROW_BIND_TYPE .  
  
 En los AMEDIANTE, este campo especifica la orientación de enlace que se utilizará para los parámetros dinámicos.  
  
 Para seleccionar el enlace de columna para los parámetros, este campo se establece en SQL_BIND_BY_COLUMN (valor predeterminado).  
  
 Este campo del APD también se puede establecer llamando a **SQLSetStmtAttr** con el *atributo*SQL_ATTR_PARAM_BIND_TYPE .  
  
 **SQL_DESC_COUNT [Todos]**  
 Este campo de encabezado SQLSMALLINT especifica el índice basado en 1 del registro con el número más alto que contiene datos. Cuando el controlador establece la estructura de datos para el descriptor, también debe establecer el campo SQL_DESC_COUNT para mostrar cuántos registros son significativos. Cuando una aplicación asigna una instancia de esta estructura de datos, no tiene que especificar cuántos registros se va a reservar espacio. A medida que la aplicación especifica el contenido de los registros, el controlador realiza cualquier acción necesaria para asegurarse de que el identificador del descriptor hace referencia a una estructura de datos del tamaño adecuado.  
  
 SQL_DESC_COUNT no es un recuento de todas las columnas de datos enlazadas (si el campo está en un ARD) o de todos los parámetros enlazados (si el campo está en un APD), sino el número del registro con el número más alto. Si la columna o parámetro con el número más alto no está enlazado, SQL_DESC_COUNT se cambia al número de la siguiente columna o parámetro con el número más alto. Si una columna o un parámetro con un número menor que el número de la columna con el número más alto no está enlazado (mediante una llamada a **SQLBindCol** con el *TargetValuePtr* argumento establecido en un puntero nulo, o **SQLBindParameter** con el *ParameterValuePtr* argumento establecido en un puntero nulo), no se cambia SQL_DESC_COUNT. Si las columnas o parámetros adicionales se enlazan con números mayores que el registro con el número más alto que contiene datos, el controlador aumenta automáticamente el valor en el campo SQL_DESC_COUNT. Si todas las columnas no están enlazadas llamando a **SQLFreeStmt** con la opción SQL_UNBIND, los campos SQL_DESC_COUNT de ARD e IRD se establecen en 0. Si se llama a **SQLFreeStmt** con la opción SQL_RESET_PARAMS, los campos SQL_DESC_COUNT del APD y el IPD se establecen en 0.  
  
 El valor de SQL_DESC_COUNT se puede establecer explícitamente mediante una aplicación mediante una llamada a **SQLSetDescField**. Si el valor de SQL_DESC_COUNT se reduce explícitamente, todos los registros con números mayores que el nuevo valor en SQL_DESC_COUNT se quitan de forma efectiva. Si el valor de SQL_DESC_COUNT se establece explícitamente en 0 y el campo está en un ARD, se liberan todos los búferes de datos excepto una columna de marcador enlazado.  
  
 El recuento de registros en este campo de un ARD no incluye una columna de marcador enlazada. La única manera de desenlazar una columna de marcador es establecer el campo SQL_DESC_DATA_PTR en un puntero nulo.  
  
 **SQL_DESC_ROWS_PROCESSED_PTR [Descriptores de implementación]**  
 En un IRD, este \* campo de encabezado SQLULEN apunta a un búfer que contiene el número de filas obtenidas después de una llamada a **SQLFetch** o **SQLFetchScroll**, o el número de filas afectadas en una operación masiva realizada por una llamada a **SQLBulkOperations** o **SQLSetPos**, incluidas las filas de error.  
  
 En un IPD, este campo de encabezado SQLUINTEGER * apunta a un búfer que contiene el número de conjuntos de parámetros que se han procesado, incluidos los conjuntos de errores. No se devolverá ningún número si se trata de un puntero nulo.  
  
 SQL_DESC_ROWS_PROCESSED_PTR es válido solo después de SQL_SUCCESS o SQL_SUCCESS_WITH_INFO se ha devuelto después de una llamada a **SQLFetch** o **SQLFetchScroll** (para un campo IRD) o **SQLExecute**, **SQLExecDirect**o **SQLParamData** (para un campo IPD). Si la llamada que rellena el búfer al que apunta este campo no devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, el contenido del búfer es indefinido, a menos que devuelva SQL_NO_DATA, en cuyo caso el valor del búfer se establece en 0.  
  
 Este campo de la ARD también se puede establecer llamando a **SQLSetStmtAttr** con el atributo SQL_ATTR_ROWS_FETCHED_PTR. Este campo en el APD también se puede establecer mediante una llamada a **SQLSetStmtAttr** con el SQL_ATTR_PARAMS_PROCESSED_PTR atributo.  
  
 La aplicación asigna el búfer al que apunta este campo. Es un búfer de salida diferido establecido por el controlador. Se establece en un puntero nulo de forma predeterminada.  
  
## <a name="record-fields"></a>Campos de registro  
 Cada descriptor contiene uno o varios registros que constan de campos que definen datos de columna o parámetros dinámicos, según el tipo de descriptor. Cada registro es una definición completa de una sola columna o parámetro.  
  
 **SQL_DESC_AUTO_UNIQUE_VALUE [IRD]**  
 Este campo de registro SQLINTEGER de solo lectura contiene SQL_TRUE si la columna es una columna de incremento automático o SQL_FALSE si la columna no es una columna de incremento automático. Este campo es de solo lectura, pero la columna de incremento automático subyacente no es necesariamente de solo lectura.  
  
 **SQL_DESC_BASE_COLUMN_NAME [IRD]**  
 Este campo de registro SQLCHAR * de solo lectura contiene el nombre de columna base para la columna del conjunto de resultados. Si no existe un nombre de columna base (como en el caso de las columnas que son expresiones), esta variable contiene una cadena vacía.  
  
 **SQL_DESC_BASE_TABLE_NAME [IRD]**  
 Este campo de registro SQLCHAR * de solo lectura contiene el nombre de la tabla base para la columna del conjunto de resultados. Si no se puede definir un nombre de tabla base o no es aplicable, esta variable contiene una cadena vacía.  
  
 **SQL_DESC_CASE_SENSITIVE [Descriptores de implementación]**  
 Este campo de registro SQLINTEGER de solo lectura contiene SQL_TRUE si la columna o parámetro se trata como que distingue mayúsculas de minúsculas para intercalaciones y comparaciones, o SQL_FALSE si la columna no se trata como que distingue mayúsculas de minúsculas para intercalaciones y comparaciones o si es una columna que no es de caracteres.  
  
 **SQL_DESC_CATALOG_NAME [IRD]**  
 Este campo de registro SQLCHAR * de solo lectura contiene el catálogo de la tabla base que contiene la columna. El valor devuelto depende del controlador si la columna es una expresión o si la columna forma parte de una vista. Si el origen de datos no admite catálogos o no se puede determinar el catálogo, esta variable contiene una cadena vacía.  
  
 **SQL_DESC_CONCISE_TYPE [Todos]**  
 Este campo de encabezado SQLSMALLINT especifica el tipo de datos conciso para todos los tipos de datos, incluidos los tipos de datos datetime e interval.  
  
 Los valores de los campos SQL_DESC_CONCISE_TYPE, SQL_DESC_TYPE y SQL_DESC_DATETIME_INTERVAL_CODE son interdependientes. Cada vez que se establece uno de los campos, también se debe establecer el otro. SQL_DESC_CONCISE_TYPE se puede establecer mediante una llamada a **SQLBindCol** o **SQLBindParameter**, o **SQLSetDescField**. SQL_DESC_TYPE se puede establecer mediante una llamada a **SQLSetDescField** o **SQLSetDescRec**.  
  
 Si SQL_DESC_CONCISE_TYPE se establece en un tipo de datos conciso distinto de un tipo de datos de intervalo o fecha y hora, el campo SQL_DESC_TYPE se establece en el mismo valor y el campo SQL_DESC_DATETIME_INTERVAL_CODE se establece en 0.  
  
 Si SQL_DESC_CONCISE_TYPE se establece en el tipo de datos datetime o interval conciso, el campo SQL_DESC_TYPE se establece en el tipo detallado correspondiente (SQL_DATETIME o SQL_INTERVAL) y el campo SQL_DESC_DATETIME_INTERVAL_CODE se establece en el subcódigo adecuado.  
  
 **SQL_DESC_DATA_PTR [Descriptores de aplicaciones e IPD]**  
 Este campo de registro SQLPOINTER apunta a una variable que contendrá el valor del parámetro (para los AD) o el valor de columna (para ARD). Este campo es un *campo diferido.* No se utiliza en el momento en que se establece, pero el controlador lo utiliza más adelante para recuperar datos.  
  
 La columna especificada por el campo SQL_DESC_DATA_PTR de la ARD no está enlazada si el *TargetValuePtr* argumento en una llamada a **SQLBindCol** es un puntero nulo o si el SQL_DESC_DATA_PTR campo de la ARD se establece mediante una llamada a **SQLSetDescField** o **SQLSetDescRec** a un puntero nulo. Otros campos no se ven afectados si el campo SQL_DESC_DATA_PTR se establece en un puntero nulo.  
  
 Si la llamada a **SQLFetch** o **SQLFetchScroll** que rellena el búfer señalado por este campo no devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, el contenido del búfer es indefinido.  
  
 Siempre que se establece el SQL_DESC_DATA_PTR campo de un APD, ARD o IPD, el controlador comprueba que el valor del campo SQL_DESC_TYPE contiene uno de los tipos de datos ODBC C válidos o un tipo de datos específico del controlador y que todos los demás campos que afectan a los tipos de datos son coherentes. Solicitar una comprobación de coherencia es el único uso del campo SQL_DESC_DATA_PTR de una IPD. En concreto, si una aplicación establece el campo SQL_DESC_DATA_PTR de un IPD y, posteriormente, llama a **SQLGetDescField** en este campo, no se devuelve necesariamente el valor que había establecido. Para obtener más información, vea "Comprobaciones de coherencia" en [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
 **SQL_DESC_DATETIME_INTERVAL_CODE [Todos]**  
 Este campo de registro SQLSMALLINT contiene el subcódigo para el tipo de datos datetime o interval específico cuando el campo SQL_DESC_TYPE está SQL_DATETIME o SQL_INTERVAL. Esto es cierto para los tipos de datos SQL y C. El código consta del nombre de tipo de datos con "CODE" sustituido por "TYPE" o "C_TYPE" (para tipos datetime), o "CODE" sustituido por "INTERVAL" o "C_INTERVAL" (para tipos de intervalo).  
  
 Si SQL_DESC_TYPE y SQL_DESC_CONCISE_TYPE de un descriptor de aplicación se establecen en SQL_C_DEFAULT y el descriptor no está asociado a un identificador de instrucción, el contenido de SQL_DESC_DATETIME_INTERVAL_CODE son indefinidos.  
  
 Este campo se puede establecer para los tipos de datos datetime enumerados en la tabla siguiente.  
  
|Tipos de fecha y hora|DATETIME_INTERVAL_CODE|  
|--------------------|------------------------------|  
|SQL_TYPE_DATE/SQL_C_TYPE_DATE|SQL_CODE_DATE|  
|SQL_TYPE_TIME/SQL_C_TYPE_TIME|SQL_CODE_TIME|  
|SQL_TYPE_TIMESTAMP/SQL_C_TYPE_TIMESTAMP|SQL_CODE_TIMESTAMP|  
  
 Este campo se puede establecer para los tipos de datos de intervalo enumerados en la tabla siguiente.  
  
|Tipo de intervalo|DATETIME_INTERVAL_CODE|  
|-------------------|------------------------------|  
|SQL_INTERVAL_DAY/SQL_C_INTERVAL_DAY|SQL_CODE_DAY|  
|SQL_INTERVAL_DAY_TO_HOUR/SQL_C_INTERVAL_DAY_TO_HOUR|SQL_CODE_DAY_TO_HOUR|  
|SQL_INTERVAL_DAY_TO_MINUTE/SQL_C_INTERVAL_DAY_TO_MINUTE|SQL_CODE_DAY_TO_MINUTE|  
|SQL_INTERVAL_DAY_TO_SECOND/ SQL_C_INTERVAL_DAY_TO_SECOND|SQL_CODE_DAY_TO_SECOND|  
|SQL_INTERVAL_HOUR/SQL_C_INTERVAL_HOUR|SQL_CODE_HOUR|  
|SQL_INTERVAL_HOUR_TO_MINUTE/SQL_C_INTERVAL_HOUR_TO_MINUTE|SQL_CODE_HOUR_TO_MINUTE|  
|SQL_INTERVAL_HOUR_TO_SECOND/ SQL_C_INTERVAL_HOUR_TO_SECOND|SQL_CODE_HOUR_TO_SECOND|  
|SQL_INTERVAL_MINUTE/SQL_C_INTERVAL_MINUTE|SQL_CODE_MINUTE|  
|SQL_INTERVAL_MINUTE_TO_SECOND/SQL_C_INTERVAL_MINUTE_TO_SECOND|SQL_CODE_MINUTE_TO_SECOND|  
|SQL_INTERVAL_MONTH/SQL_C_INTERVAL_MONTH|SQL_CODE_MONTH|  
|SQL_INTERVAL_SECOND/SQL_C_INTERVAL_SECOND|SQL_CODE_SECOND|  
|SQL_INTERVAL_YEAR/ SQL_C_INTERVAL_YEAR|SQL_CODE_YEAR|  
|SQL_INTERVAL_YEAR_TO_MONTH/SQL_C_INTERVAL_YEAR_TO_MONTH|SQL_CODE_YEAR_TO_MONTH|  
  
 Para obtener más información acerca de los intervalos de datos y este campo, vea [Identificadores y descriptores](../../../odbc/reference/appendixes/data-type-identifiers-and-descriptors.md)de tipo de datos .  
  
 **SQL_DESC_DATETIME_INTERVAL_PRECISION [Todos]**  
 Este campo de registro SQLINTEGER contiene la precisión inicial del intervalo si el campo SQL_DESC_TYPE es SQL_INTERVAL. Cuando el campo SQL_DESC_DATETIME_INTERVAL_CODE se establece en un tipo de datos de intervalo, este campo se establece en la precisión inicial del intervalo predeterminado.  
  
 **SQL_DESC_DISPLAY_SIZE [IRD]**  
 Este campo de registro SQLINTEGER de solo lectura contiene el número máximo de caracteres necesarios para mostrar los datos de la columna.  
  
 **SQL_DESC_FIXED_PREC_SCALE [Descriptores de implementación]**  
 Este campo de registro SQLSMALLINT de solo lectura se establece en SQL_TRUE si la columna es una columna numérica exacta y tiene una precisión fija y una escala distinta de cero, o en SQL_FALSE si la columna no es una columna numérica exacta con una precisión y una escala fijas.  
  
 **SQL_DESC_INDICATOR_PTR [Descriptores de aplicación]**  
 En los ARD, este campo de registro SQLLEN * apunta a la variable del indicador. Esta variable contiene SQL_NULL_DATA si el valor de columna es NULL. Para los AD, la variable de indicador se establece en SQL_NULL_DATA para especificar argumentos dinámicos NULL. De lo contrario, la variable es cero (a menos que los valores de SQL_DESC_INDICATOR_PTR y SQL_DESC_OCTET_LENGTH_PTR sean el mismo puntero).  
  
 Si el campo SQL_DESC_INDICATOR_PTR de un ARD es un puntero nulo, se impide que el controlador devuelva información sobre si la columna es NULL o no. Si la columna es NULL y SQL_DESC_INDICATOR_PTR es un puntero nulo, SQLSTATE 22002 (variable de indicador requerida pero no proporcionada) se devuelve cuando el controlador intenta rellenar el búfer después de una llamada a **SQLFetch** o **SQLFetchScroll**. Si la llamada a **SQLFetch** o **SQLFetchScroll** no devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, el contenido del búfer es indefinido.  
  
 El campo SQL_DESC_INDICATOR_PTR determina si se establece el campo al que apunta SQL_DESC_OCTET_LENGTH_PTR. Si el valor de datos de una columna es NULL, el controlador establece la variable de indicador en SQL_NULL_DATA. El campo al que apunta SQL_DESC_OCTET_LENGTH_PTR no se establece. Si no se encuentra un valor NULL durante la captura, el búfer al que apunta SQL_DESC_INDICATOR_PTR se establece en cero y el búfer al que apunta SQL_DESC_OCTET_LENGTH_PTR se establece en la longitud de los datos.  
  
 Si el campo SQL_DESC_INDICATOR_PTR de un APD es un puntero nulo, la aplicación no puede utilizar este registro descriptor para especificar argumentos NULL.  
  
 Este campo es un *campo diferido*: No se utiliza en el momento en que se establece, pero es utilizado en un momento posterior por el controlador para indicar la nulabilidad (para LOS ARD) o para determinar la nulabilidad (para los AED).  
  
 **SQL_DESC_LABEL [IRD]**  
 Este campo de registro SQLCHAR * de solo lectura contiene la etiqueta o el título de la columna. Si la columna no tiene una etiqueta, esta variable contiene el nombre de la columna. Si la columna no tiene nombre y no tiene etiqueta, esta variable contiene una cadena vacía.  
  
 **SQL_DESC_LENGTH [Todos]**  
 Este campo de registro SQLULEN es la longitud máxima o real de una cadena de caracteres en caracteres o un tipo de datos binario en bytes. Es la longitud máxima para un tipo de datos de longitud fija o la longitud real para un tipo de datos de longitud variable. Su valor siempre excluye el carácter de terminación nula que finaliza la cadena de caracteres. Para los valores cuyo tipo es SQL_TYPE_DATE, SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP o uno de los tipos de datos de intervalo SQL, este campo tiene la longitud en caracteres de la representación de cadena de caracteres del valor datetime o interval.  
  
 El valor de este campo puede ser diferente del valor de "length" tal como se define en ODBC 2 *.x*. Para obtener más información, consulte [Apéndice D: Tipos](../../../odbc/reference/appendixes/appendix-d-data-types.md)de datos .  
  
 **SQL_DESC_LITERAL_PREFIX [IRD]**  
 Este campo de registro SQLCHAR * de solo lectura contiene el carácter o caracteres que el controlador reconoce como prefijo para un literal de este tipo de datos. Esta variable contiene una cadena vacía para un tipo de datos para el que no es aplicable un prefijo literal.  
  
 **SQL_DESC_LITERAL_SUFFIX [IRD]**  
 Este campo de registro SQLCHAR * de solo lectura contiene el carácter o caracteres que el controlador reconoce como sufijo para un literal de este tipo de datos. Esta variable contiene una cadena vacía para un tipo de datos para el que no es aplicable un sufijo literal.  
  
 **SQL_DESC_LOCAL_TYPE_NAME [Descriptores de implementación]**  
 Este campo de registro SQLCHAR * de solo lectura contiene cualquier nombre localizado (idioma nativo) para el tipo de datos que puede ser diferente del nombre normal del tipo de datos. Si no hay ningún nombre localizado, se devuelve una cadena vacía. Este campo es solo para fines de visualización.  
  
 **SQL_DESC_NAME [Descriptores de implementación]**  
 Este campo de registro SQLCHAR * en un descriptor de fila contiene el alias de columna, si se aplica. Si el alias de columna no se aplica, se devuelve el nombre de columna. En cualquier caso, el controlador establece el campo SQL_DESC_UNNAMED en SQL_NAMED cuando establece el campo SQL_DESC_NAME. Si no hay ningún nombre de columna o un alias de columna, el controlador devuelve una cadena vacía en el campo SQL_DESC_NAME y establece el campo SQL_DESC_UNNAMED en SQL_UNNAMED.  
  
 Una aplicación puede establecer el campo SQL_DESC_NAME de una IPD en un nombre de parámetro o alias para especificar los parámetros de procedimiento almacenado por nombre. (Para obtener más información, vea Parámetros de [enlace por nombre (parámetros con nombre)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md).) El campo SQL_DESC_NAME de un IRD es un campo de solo lectura; SQLSTATE HY091 (identificador de campo descriptor no válido) se devolverá si una aplicación intenta establecerlo.  
  
 En los IPD, este campo es indefinido si el controlador no admite parámetros con nombre. Si el controlador admite parámetros con nombre y es capaz de describir parámetros, el nombre del parámetro se devuelve en este campo.  
  
 **SQL_DESC_NULLABLE [Descriptores de implementación]**  
 En IRD, este campo de registro SQLSMALLINT de solo lectura se SQL_NULLABLE si la columna puede tener valores NULL, SQL_NO_NULLS si la columna no tiene valores NULL o SQL_NULLABLE_UNKNOWN si no se sabe si la columna acepta valores NULL. Este campo pertenece a la columna del conjunto de resultados, no a la columna base.  
  
 En los IPD, este campo siempre se establece en SQL_NULLABLE porque los parámetros dinámicos siempre aceptan valores NULL y no se pueden establecer mediante una aplicación.  
  
 **SQL_DESC_NUM_PREC_RADIX [Todos]**  
 Este campo SQLINTEGER contiene un valor de 2 si el tipo de datos del campo SQL_DESC_TYPE es un tipo de datos numérico aproximado, porque el campo SQL_DESC_PRECISION contiene el número de bits. Este campo contiene un valor de 10 si el tipo de datos del campo SQL_DESC_TYPE es un tipo de datos numérico exacto, porque el campo SQL_DESC_PRECISION contiene el número de dígitos decimales. Este campo se establece en 0 para todos los tipos de datos no numéricos.  
  
 **SQL_DESC_OCTET_LENGTH [Todos]**  
 Este campo de registro SQLLEN contiene la longitud, en bytes, de una cadena de caracteres o un tipo de datos binario. Para caracteres de longitud fija o tipos binarios, esta es la longitud real en bytes. Para los tipos binarios o de caracteres de longitud variable, esta es la longitud máxima en bytes. Este valor siempre excluye el espacio para el carácter de terminación nula para los descriptores de implementación y siempre incluye espacio para el carácter de terminación nula para los descriptores de aplicación. Para los datos de la aplicación, este campo contiene el tamaño del búfer. Para los ACD, este campo se define solamente para los parámetros de salida o de entrada/salida.  
  
 **SQL_DESC_OCTET_LENGTH_PTR [Descriptores de aplicación]**  
 Este campo de registro SQLLEN * apunta a una variable que contendrá la longitud total en bytes de un argumento dinámico (para descriptores de parámetros) o de un valor de columna enlazado (para descriptores de fila).  
  
 Para un APD, este valor se omite para todos los argumentos excepto la cadena de caracteres y binario; si este campo apunta a SQL_NTS, el argumento dinámico debe estar terminado en null. Para indicar que un parámetro enlazado será un parámetro de datos en ejecución, una aplicación establece este campo en el registro adecuado del APD en una variable que, en tiempo de ejecución, contendrá el valor SQL_DATA_AT_EXEC o el resultado de la macro SQL_LEN_DATA_AT_EXEC. Si hay más de un campo de este tipo, SQL_DESC_DATA_PTR se puede establecer en un valor que identifique de forma exclusiva el parámetro para ayudar a la aplicación a determinar qué parámetro se solicita.  
  
 Si el campo OCTET_LENGTH_PTR de un ARD es un puntero nulo, el controlador no devuelve información de longitud para la columna. Si el campo SQL_DESC_OCTET_LENGTH_PTR de un APD es un puntero nulo, el controlador supone que las cadenas de caracteres y los valores binarios terminan en null. (Los valores binarios no deben terminarse en null, pero se les debe dar una longitud para evitar el truncamiento.)  
  
 Si la llamada a **SQLFetch** o **SQLFetchScroll** que rellena el búfer señalado por este campo no devuelve SQL_SUCCESS o SQL_SUCCESS_WITH_INFO, el contenido del búfer es indefinido. Este campo es un *campo diferido.* No se utiliza en el momento en que se establece, pero se utiliza en un momento posterior por el controlador para determinar o indicar la longitud del octeto de los datos.  
  
 **SQL_DESC_PARAMETER_TYPE [IPDs]**  
 Este campo de registro SQLSMALLINT se establece en SQL_PARAM_INPUT para un parámetro de entrada, SQL_PARAM_INPUT_OUTPUT para un parámetro de entrada/salida, SQL_PARAM_OUTPUT para un parámetro de salida, SQL_PARAM_INPUT_OUTPUT_STREAM para un parámetro transmitido de entrada/salida o SQL_PARAM_OUTPUT_STREAM para un parámetro transmitido de salida. Se establece en SQL_PARAM_INPUT de forma predeterminada.  
  
 Para un IPD, el campo se establece en SQL_PARAM_INPUT de forma predeterminada si el controlador no rellena automáticamente el IPD (el atributo de instrucción SQL_ATTR_ENABLE_AUTO_IPD se SQL_FALSE). Una aplicación debe establecer este campo en el IPD para los parámetros que no son parámetros de entrada.  
  
 **SQL_DESC_PRECISION [Todos]**  
 Este campo de registro SQLSMALLINT contiene el número de dígitos para un tipo numérico exacto, el número de bits de la mantisa (precisión binaria) para un tipo numérico aproximado o el número de dígitos en el componente de fracciones de segundo para el tipo de datos SQL_TYPE_TIME, SQL_TYPE_TIMESTAMP o SQL_INTERVAL_SECOND. Este campo no está definido para todos los demás tipos de datos.  
  
 El valor de este campo puede ser diferente del valor de "precisión" tal como se define en ODBC 2 *.x*. Para obtener más información, consulte [Apéndice D: Tipos](../../../odbc/reference/appendixes/appendix-d-data-types.md)de datos .  
  
 **SQL_DESC_ROWVER [Descriptores de implementación]**  
 Este campo SQLSMALLINTrecord indica si el DBMS modifica automáticamente una columna cuando se actualiza una fila (por ejemplo, una columna del tipo "timestamp" en SQL Server). El valor de este campo de registro se establece en SQL_TRUE si la columna es una columna de control de versiones de fila y en SQL_FALSE lo contrario. Este atributo de columna es similar a llamar a **SQLSpecialColumns** con IdentifierType de SQL_ROWVER para determinar si una columna se actualiza automáticamente.  
  
 **SQL_DESC_SCALE [Todos]**  
 Este campo de registro SQLSMALLINT contiene la escala definida para los tipos de datos decimales y numéricos. El campo no está definido para todos los demás tipos de datos.  
  
 El valor de este campo puede ser diferente del valor de "escala" tal como se define en ODBC 2 *.x*. Para obtener más información, consulte [Apéndice D: Tipos](../../../odbc/reference/appendixes/appendix-d-data-types.md)de datos .  
  
 **SQL_DESC_SCHEMA_NAME [IRD]**  
 Este campo de registro SQLCHAR * de solo lectura contiene el nombre de esquema de la tabla base que contiene la columna. El valor devuelto depende del controlador si la columna es una expresión o si la columna forma parte de una vista. Si el origen de datos no admite esquemas o no se puede determinar el nombre del esquema, esta variable contiene una cadena vacía.  
  
 **SQL_DESC_SEARCHABLE [IRD]**  
 Este campo de registro SQLSMALLINT de solo lectura se establece en uno de los siguientes valores:  
  
-   SQL_PRED_NONE si la columna no se puede utilizar en una cláusula **WHERE.** (Esto es lo mismo que el valor de SQL_UNSEARCHABLE en ODBC 2 *.x*.)  
  
-   SQL_PRED_CHAR si la columna se puede utilizar en una cláusula **WHERE** pero solo con el predicado **LIKE.** (Esto es lo mismo que el valor de SQL_LIKE_ONLY en ODBC 2 *.x*.)  
  
-   SQL_PRED_BASIC si la columna se puede utilizar en una cláusula **WHERE** con todos los operadores de comparación excepto **LIKE**. (Esto es lo mismo que el valor de SQL_EXCEPT_LIKE en ODBC 2 *.x*.)  
  
-   SQL_PRED_SEARCHABLE si la columna se puede utilizar en una cláusula **WHERE** con cualquier operador de comparación.  
  
 **SQL_DESC_TABLE_NAME [IRD]**  
 Este campo de registro SQLCHAR * de solo lectura contiene el nombre de la tabla base que contiene esta columna. El valor devuelto depende del controlador si la columna es una expresión o si la columna forma parte de una vista.  
  
 **SQL_DESC_TYPE [Todos]**  
 Este campo de registro SQLSMALLINT especifica el tipo de datos SQL o C conciso para todos los tipos de datos excepto los tipos de datos datetime e interval. Para los tipos de datos datetime e interval, este campo especifica el tipo de datos detallado, que es SQL_DATETIME o SQL_INTERVAL.  
  
 Siempre que este campo contenga SQL_DATETIME o SQL_INTERVAL, el campo SQL_DESC_DATETIME_INTERVAL_CODE debe contener el subcódigo adecuado para el tipo conciso. Para los tipos de datos datetime, SQL_DESC_TYPE contiene SQL_DATETIME y el campo SQL_DESC_DATETIME_INTERVAL_CODE contiene un subcódigo para el tipo de datos datetime específico. Para los tipos de datos de intervalo, SQL_DESC_TYPE contiene SQL_INTERVAL y el campo SQL_DESC_DATETIME_INTERVAL_CODE contiene un subcódigo para el tipo de datos de intervalo específico.  
  
 Los valores de los campos SQL_DESC_TYPE y SQL_DESC_CONCISE_TYPE son interdependientes. Cada vez que se establece uno de los campos, también se debe establecer el otro. SQL_DESC_TYPE se puede establecer mediante una llamada a **SQLSetDescField** o **SQLSetDescRec**. SQL_DESC_CONCISE_TYPE se puede establecer mediante una llamada a **SQLBindCol** o **SQLBindParameter**, o **SQLSetDescField**.  
  
 Si SQL_DESC_TYPE se establece en un tipo de datos conciso distinto de un tipo de datos de intervalo o fecha y hora, el campo SQL_DESC_CONCISE_TYPE se establece en el mismo valor y el campo SQL_DESC_DATETIME_INTERVAL_CODE se establece en 0.  
  
 Si SQL_DESC_TYPE se establece en el tipo de datos de fecha y hora o intervalo detallado (SQL_DATETIME o SQL_INTERVAL) y el campo SQL_DESC_DATETIME_INTERVAL_CODE se establece en el subcódigo adecuado, el campo SQL_DESC_CONCISE TIPO se establece en el tipo conciso correspondiente. Al intentar establecer SQL_DESC_TYPE en uno de los tipos concisos datetime o interval devolverá SQLSTATE HY021 (información de descriptor incompatible).  
  
 Cuando el SQL_DESC_TYPE campo se establece mediante una llamada a **SQLBindCol**, **SQLBindParameter**o **SQLSetDescField**, los campos siguientes se establecen en los siguientes valores predeterminados, como se muestra en la tabla siguiente. Los valores de los campos restantes del mismo registro son indefinidos.  
  
|Valor de SQL_DESC_TYPE|Otros campos establecidos implícitamente|  
|------------------------------|---------------------------------|  
|SQL_CHAR, SQL_VARCHAR, SQL_C_CHAR, SQL_C_VARCHAR|SQL_DESC_LENGTH se establece en 1. SQL_DESC_PRECISION se establece en 0.|  
|SQL_DATETIME|Cuando SQL_DESC_DATETIME_INTERVAL_CODE se establece en SQL_CODE_DATE o SQL_CODE_TIME, SQL_DESC_PRECISION se establece en 0. Cuando se establece en SQL_DESC_TIMESTAMP, SQL_DESC_PRECISION se establece en 6.|  
|SQL_DECIMAL, SQL_NUMERIC, SQL_C_NUMERIC|SQL_DESC_SCALE se establece en 0. SQL_DESC_PRECISION se establece en la precisión definida por la implementación para el tipo de datos respectivo.<br /><br /> Consulte [SQL a C: numérico](../../../odbc/reference/appendixes/sql-to-c-numeric.md) para obtener información sobre cómo enlazar manualmente un valor de SQL_C_NUMERIC.|  
|SQL_FLOAT, SQL_C_FLOAT|SQL_DESC_PRECISION se establece en la precisión predeterminada definida por la implementación para SQL_FLOAT.|  
|SQL_INTERVAL|Cuando SQL_DESC_DATETIME_INTERVAL_CODE se establece en un tipo de datos de intervalo, SQL_DESC_DATETIME_INTERVAL_PRECISION se establece en 2 (la precisión inicial del intervalo predeterminado). Cuando el intervalo tiene un componente de segundos, SQL_DESC_PRECISION se establece en 6 (la precisión de segundos de intervalo predeterminada).|  
  
 Cuando una aplicación llama a **SQLSetDescField** para establecer campos de un descriptor en lugar de llamar a **SQLSetDescRec**, la aplicación debe declarar primero el tipo de datos. Cuando lo hace, los demás campos indicados en la tabla anterior se establecen implícitamente. Si alguno de los valores establecidos implícitamente son inaceptables, la aplicación puede llamar a **SQLSetDescField** o **SQLSetDescRec** para establecer el valor inaceptable explícitamente.  
  
 **SQL_DESC_TYPE_NAME [Descriptores de implementación]**  
 Este campo de registro SQLCHAR * de solo lectura contiene el nombre de tipo dependiente del origen de datos (por ejemplo, "CHAR", "VARCHAR", etc.). Si el nombre del tipo de datos es desconocido, esta variable contiene una cadena vacía.  
  
 **SQL_DESC_UNNAMED [Descriptores de implementación]**  
 El controlador establece este campo de registro SQLSMALLINT en un descriptor de fila en SQL_NAMED o SQL_UNNAMED cuando establece el campo SQL_DESC_NAME. Si el campo SQL_DESC_NAME contiene un alias de columna o si el alias de columna no se aplica, el controlador establece el campo SQL_DESC_UNNAMED en SQL_NAMED. Si una aplicación establece el campo SQL_DESC_NAME de una IPD en un nombre de parámetro o alias, el controlador establece el campo SQL_DESC_UNNAMED de la IPD en SQL_NAMED. Si no hay ningún nombre de columna o un alias de columna, el controlador establece el campo SQL_DESC_UNNAMED en SQL_UNNAMED.  
  
 Una aplicación puede establecer el campo SQL_DESC_UNNAMED de una IPD en SQL_UNNAMED. Un controlador devuelve SQLSTATE HY091 (identificador de campo descriptor no válido) si una aplicación intenta establecer el campo SQL_DESC_UNNAMED de una IPD en SQL_NAMED. El campo SQL_DESC_UNNAMED de un IRD es de solo lectura; SQLSTATE HY091 (identificador de campo descriptor no válido) se devolverá si una aplicación intenta establecerlo.  
  
 **SQL_DESC_UNSIGNED [Descriptores de implementación]**  
 Este campo de registro SQLSMALLINT de solo lectura se establece en SQL_TRUE si el tipo de columna es sin signo o no numérico, o SQL_FALSE si el tipo de columna está firmado.  
  
 **SQL_DESC_UPDATABLE [IRD]**  
 Este campo de registro SQLSMALLINT de solo lectura se establece en uno de los siguientes valores:  
  
-   SQL_ATTR_READ_ONLY si la columna del conjunto de resultados es de solo lectura.  
  
-   SQL_ATTR_WRITE si la columna del conjunto de resultados es de lectura y escritura.  
  
-   SQL_ATTR_READWRITE_UNKNOWN si no se sabe si la columna del conjunto de resultados es actualizable o no.  
  
 SQL_DESC_UPDATABLE describe la capacidad de actualización de la columna en el conjunto de resultados, no la columna de la tabla base. La capacidad de actualización de la columna de la tabla base en la que se basa esta columna de conjunto de resultados puede ser diferente del valor de este campo. Si una columna es actualizable se puede basar en el tipo de datos, los privilegios de usuario y la definición del propio conjunto de resultados. Si no está claro si una columna es actualizable, se debe devolver SQL_ATTR_READWRITE_UNKNOWN.  
  
## <a name="consistency-checks"></a>Comprobaciones de coherencia  
 El controlador realiza automáticamente una comprobación de coherencia cada vez que una aplicación pasa un valor para el campo SQL_DESC_DATA_PTR de LA ARD, APD o IPD. Si alguno de los campos es incoherente con otros campos, **SQLSetDescField** devolverá SQLSTATE HY021 (información de descriptor incoherente). Para obtener más información, vea "Comprobación de coherencia" en [SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar una columna|[SQLBindCol (función)](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Enlazar un parámetro|[Función SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Obtener un campo descriptor|[Función SQLGetDescField](../../../odbc/reference/syntax/sqlgetdescfield-function.md)|  
|Obtención de varios campos descriptores|[Función SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Configuración de varios campos descriptores|[Función SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Archivos de encabezado ODBC](../../../odbc/reference/install/odbc-header-files.md)   
 [Referencia de API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)
