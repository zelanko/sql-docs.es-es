---
title: FUNción SQLGetDescField ? Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetDescField
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetDescField
helpviewer_keywords:
- SQLGetDescField function [ODBC]
ms.assetid: f09ff660-1e4a-4370-be85-90d4da0487d3
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 89972d7f36b436868cc8e243b03827f095b90492
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285480"
---
# <a name="sqlgetdescfield-function"></a>Función SQLGetDescField
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 3.0: ISO 92  
  
 **Resumen**  
 **SQLGetDescField** devuelve el valor actual de un único campo de un registro descriptor.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLGetDescField(  
     SQLHDESC        DescriptorHandle,  
     SQLSMALLINT     RecNumber,  
     SQLSMALLINT     FieldIdentifier,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *DescriptorHandle*  
 [Entrada] Mango del descriptor.  
  
 *RecNumber*  
 [Entrada] Indica el registro descriptor desde el que la aplicación busca información. Los registros de descriptor se numeran desde 0, siendo el número de registro 0 el registro de marcador. Si el *Argumento FieldIdentifier* indica un campo de encabezado, se omite *RecNumber.* Si *RecNumber* es menor o igual que SQL_DESC_COUNT pero la fila no contiene datos para una columna o parámetro, una llamada a **SQLGetDescField** devolverá los valores predeterminados de los campos. (Para obtener más información, vea "Inicialización de campos [descriptores" en SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 *FieldIdentifier*  
 [Entrada] Indica el campo del descriptor cuyo valor se va a devolver. Para obtener más información, vea la sección "*FieldIdentifier* Argument" en [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 *ValuePtr*  
 [Salida] Puntero a un búfer en el que se va a devolver la información del descriptor. El tipo de datos depende del valor de *FieldIdentifier*.  
  
 Si *ValuePtr* es de tipo entero, las aplicaciones deben usar un búfer de SQLULEN e inicializar el valor en 0 antes de llamar a esta función, ya que algunos controladores solo pueden escribir los 32 bits inferiores o 16 bits de un búfer y dejar el bit de orden superior sin cambios.  
  
 Si *ValuePtr* es NULL, *StringLengthPtr* seguirá devolviendo el número total de bytes (excluyendo el carácter de terminación nula para los datos de caracteres) disponibles para devolver en el búfer señalado por *ValuePtr*.  
  
 *BufferLength*  
 [Entrada] Si *FieldIdentifier* es un campo definido por ODBC y *ValuePtr* apunta a una cadena \*de caracteres o un búfer binario, este argumento debe ser la longitud de *ValuePtr*. Si *FieldIdentifier* es un campo \*definido por ODBC y *ValuePtr* es un entero, *BufferLength* se omite. Si el valor de * \*ValuePtr* es de un tipo de datos Unicode (al llamar a **SQLGetDescFieldW**), el *bufferLength* argumento debe ser un número par.  
  
 Si *FieldIdentifier* es un campo definido por el controlador, la aplicación indica la naturaleza del campo para el Administrador de controladores estableciendo el *BufferLength* argumento. *BufferLength* puede tener los siguientes valores:  
  
-   Si * \*ValuePtr* es un puntero a una cadena de caracteres, *BufferLength* es la longitud de la cadena o SQL_NTS.  
  
-   Si * \*ValuePtr* es un puntero a un búfer binario, la aplicación coloca el resultado de la macro SQL_LEN_BINARY_ATTR(*length*) en *BufferLength*. Esto coloca un valor negativo en *BufferLength*.  
  
-   Si * \*ValuePtr* es un puntero a un valor distinto de una cadena de caracteres o una cadena binaria, *BufferLength* debe tener el valor SQL_IS_POINTER.  
  
-   Si * \*ValuePtr* contiene un tipo de datos de longitud fija, *BufferLength* es SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT o SQL_IS_USMALLINT, según corresponda.  
  
 *StringLengthPtr*  
 [Salida] Puntero al búfer en el que se va a devolver el número total de bytes (excluyendo el número de bytes necesarios para el carácter de terminación nula) disponiblepara devolver en **ValuePtr*.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_NO_DATA o SQL_INVALID_HANDLE.  
  
 SQL_NO_DATA se devuelve si *RecNumber* es mayor que el número actual de registros descriptores.  
  
 SQL_NO_DATA se devuelve si *DescriptorHandle* es un identificador IRD y la instrucción está en estado preparado o ejecutado, pero no había ningún cursor abierto asociado a él.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLGetDescField** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *control* de *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLGetDescField** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01004|Datos de cadena truncados a la derecha|El \*búfer *ValuePtr* no era lo suficientemente grande como para devolver todo el campo descriptor, por lo que el campo se truncó. La longitud del campo descriptor no truncado se devuelve en **StringLengthPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|07009|Indice de descriptor no válido|(DM) el *RecNumber* argumento era igual a 0, el atributo de instrucción SQL_ATTR_USE_BOOKMARK se SQL_UB_OFF y el *DescriptorHandle* argumento era un identificador IRD. (Este error se puede devolver para un descriptor asignado explícitamente solo si el descriptor está asociado a un identificador de instrucción.)<br /><br /> El argumento *FieldIdentifier* era un campo de registro, el argumento *RecNumber* era 0 y el argumento *DescriptorHandle* era un identificador IPD.<br /><br /> El *argumento RecNumber* era menor que 0.|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY007|La declaración asociada no está preparada|*DescriptorHandle* se asoció con un *StatementHandle* como un IRD y el identificador de instrucción asociado no se había preparado o ejecutado.|  
|HY010|Error de secuencia de funciones|DescriptorHandle *DescriptorHandle* se asoció con un *StatementHandle* para el que se llamó a una función de ejecución asincrónica (no a esta) y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> DescriptorHandle *DescriptorHandle* (DM) se asoció a un *StatementHandle* para el que **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó y devolvió SQL_NEED_DATA . Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.<br /><br /> (DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *DescriptorHandle*. Esta función asincrónica todavía se estaba ejecutando cuando se llamó a la función **SQLGetDescField** .|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY021|Información de descriptorina incoherente|Los campos SQL_DESC_TYPE y SQL_DESC_DATETIME_INTERVAL_CODE no forman un tipo SQL ODBC válido, un tipo SQL específico del controlador válido (para IPD) o un tipo ODBC C válido (para ACD o ARD).|  
|HY090|Cadena no válida o longitud de búfer|ValuePtr era una cadena de caracteres y *BufferLength* era menor que cero. * \**|  
|HY091|Identificador de campo descriptor no válido|*FieldIdentifier* no era un campo definido por ODBC y no era un valor definido por la implementación.<br /><br /> *FieldIdentifier* no estaba definido para *descriptorHandle*.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [Función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *DescriptorHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Una aplicación puede llamar a **SQLGetDescField** para devolver el valor de un único campo de un registro descriptor. Una llamada a **SQLGetDescField** puede devolver la configuración de cualquier campo en cualquier tipo de descriptor, incluidos los campos de encabezado, campos de registro y campos de marcador. Una aplicación puede obtener la configuración de varios campos en el mismo o diferentes descriptores, en orden arbitrario, realizando **llamadas repetidas a SQLGetDescField**. **SQLGetDescField** también se puede llamar para devolver campos descriptores definidos por el controlador.  
  
 Por motivos de rendimiento, una aplicación no debe llamar a **SQLGetDescField** para un IRD antes de ejecutar una instrucción.  
  
 La configuración de varios campos que describen el nombre, el tipo de datos y el almacenamiento de datos de columna o parámetro también se pueden recuperar en una sola llamada a **SQLGetDescRec**. **SQLGetStmtAttr** se puede llamar para devolver la configuración de un único campo en el encabezado del descriptor que también es un atributo de instrucción. **SQLColAttribute**, **SQLDescribeCol**y **SQLDescribeParam** devuelven campos de registro o marcador.  
  
 Cuando una aplicación llama a **SQLGetDescField** para recuperar el valor de un campo que no está definido para un tipo de descriptor determinado, la función devuelve SQL_SUCCESS pero el valor devuelto para el campo es indefinido. Por ejemplo, llamar a **SQLGetDescField** para el SQL_DESC_NAME o SQL_DESC_NULLABLE campo de un APD o ARD devolverá SQL_SUCCESS pero un valor indefinido para el campo.  
  
 Cuando una aplicación llama a **SQLGetDescField** para recuperar el valor de un campo que se define para un tipo de descriptor determinado pero que no tiene ningún valor predeterminado y aún no se ha establecido, la función devuelve SQL_SUCCESS pero el valor devuelto para el campo es indefinido. Para obtener más información sobre la inicialización de los campos descriptores y las descripciones de los campos, vea "Inicialización de campos [descriptores" en SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Para obtener más información sobre los descriptores, consulte [Descriptores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Obtención de varios campos descriptores|[Función SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Establecer un único campo descriptor|[Función SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Configuración de varios campos descriptores|[Función SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
