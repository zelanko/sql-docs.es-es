---
title: Función SQLGetDescField | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f6762eb4ea9b350a76fc794fa7074af2a107b511
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/11/2018
ms.locfileid: "53204094"
---
# <a name="sqlgetdescfield-function"></a>Función SQLGetDescField
**Conformidad**  
 Versión de introducción: Compatibilidad de ODBC 3.0 estándares: 92 ISO  
  
 **Resumen**  
 **SQLGetDescField** devuelve el valor actual o el valor de un único campo de un registro del descriptor.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
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
 [Entrada] Identificador de descriptor.  
  
 *RecNumber*  
 [Entrada] Indica que el registro de descriptor de la que la aplicación busca información. Registros de descriptor se numeran de 0, con el número de registro 0 es el registro del marcador. Si el *FieldIdentifier* argumento indica un campo de encabezado, *RecNumber* se omite. Si *RecNumber* es menor o igual que SQL_DESC_COUNT pero la fila no contiene datos de una columna o parámetro, una llamada a **SQLGetDescField** devolverá los valores predeterminados de los campos. (Para obtener más información, consulte "Inicialización de campos de Descriptor" en [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).)  
  
 *FieldIdentifier*  
 [Entrada] Indica el campo del descriptor cuyo valor se va a devolver. Para obtener más información, consulte el "*FieldIdentifier* argumento" sección [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md).  
  
 *ValuePtr*  
 [Salida] Puntero a un búfer en el que se va a devolver la información del descriptor. El tipo de datos depende del valor de *FieldIdentifier*.  
  
 Si *ValuePtr* es de tipo entero, las aplicaciones deben utilizar un búfer de SQLULEN e inicializar el valor en 0 antes de llamar a esta función como algunos controladores solo puede escribir el menor de 32 bits o de 16 bits de un búfer y dejar el bit de orden superior sin cambios.  
  
 Si *ValuePtr* es NULL, *StringLengthPtr* devolverá el número total de bytes (excluido el carácter de terminación null para los datos de caracteres) disponibles para devolver en el búfer señalado por  *ValuePtr*.  
  
 *BufferLength*  
 [Entrada] Si *FieldIdentifier* es un campo de ODBC y *ValuePtr* apunta a un búfer binario o una cadena de caracteres, este argumento debe ser la longitud de \* *ValuePtr*. Si *FieldIdentifier* es un campo de ODBC y \* *ValuePtr* es un entero, *BufferLength* se omite. Si el valor de  *\*ValuePtr* es de tipo de datos Unicode (al llamar a **SQLGetDescFieldW**), el *BufferLength* argumento debe ser un número par.  
  
 Si *FieldIdentifier* es un campo definido por el controlador, la aplicación indica la naturaleza del campo para el Administrador de controladores al establecer el *BufferLength* argumento. *BufferLength* puede tener los siguientes valores:  
  
-   Si  *\*ValuePtr* es un puntero a una cadena de caracteres, a continuación, *BufferLength* es la longitud de la cadena o SQL_NTS.  
  
-   Si  *\*ValuePtr* es un puntero a un búfer binario, a continuación, la aplicación, el resultado de la SQL_LEN_BINARY_ATTR (*longitud*) macro en *BufferLength*. Esto coloca un valor negativo en *BufferLength*.  
  
-   Si  *\*ValuePtr* es un puntero a un valor distinto de una cadena de caracteres o una cadena binaria, a continuación, *BufferLength* debe tener el valor SQL_IS_POINTER.  
  
-   Si  *\*ValuePtr* es contiene un tipo de datos de longitud fija, a continuación, *BufferLength* es SQL_IS_INTEGER, SQL_IS_UINTEGER, SQL_IS_SMALLINT o SQL_IS_USMALLINT, según corresponda.  
  
 *StringLengthPtr*  
 [Salida] Puntero al búfer en el que se va a devolver el número total de bytes (sin incluir el número de bytes necesarios para el carácter de terminación null) disponibles para devolver en **ValuePtr*.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR, SQL_NO_DATA o SQL_INVALID_HANDLE.  
  
 Si se devuelve SQL_NO_DATA *RecNumber* es mayor que el número actual de registros de descriptor.  
  
 Si se devuelve SQL_NO_DATA *DescriptorHandle* es un identificador IRD y la instrucción está en estado preparado o ejecutado pero se ha producido ningún cursor abierto asociado con él.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLGetDescField** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLGetDescField** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena derecha truncados|El búfer \* *ValuePtr* no era lo suficientemente grande como para devolver el campo descriptor completo, por lo que el campo se ha truncado. Se devuelve la longitud del campo descriptor sin truncar en **StringLengthPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07009|Índice de descriptor no válido|(DM) el *RecNumber* argumento era igual a 0, el atributo de instrucción SQL_ATTR_USE_BOOKMARK fue SQL_UB_OFF y el *DescriptorHandle* argumento era un identificador IRD. (Este error se puede devolver para un descriptor asignado explícitamente solo si el descriptor está asociado con un identificador de instrucción.)<br /><br /> El *FieldIdentifier* argumento era un campo de registro, el *RecNumber* argumento era 0 y el *DescriptorHandle* argumento era un identificador IPD.<br /><br /> El *RecNumber* argumento era menor que 0.|  
|08S01|Error de vínculo de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos a la que se ha conectado el controlador antes del procesamiento de la función se ha completado.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY007|La instrucción asociada no está preparada|*DescriptorHandle* asoció un *StatementHandle* como un IRD y la instrucción asociada identificador tenía no se ha preparado ni se ejecuta.|  
|HY010|Error de secuencia de función|(DM) *DescriptorHandle* asoció un *StatementHandle* para que se llamó a una función que se ejecuta asincrónicamente (no esta uno) y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) *DescriptorHandle* asoció un *StatementHandle* que **SQLExecute**, **SQLExecDirect**,  **SQLBulkOperations**, o **SQLSetPos** se llamó y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.<br /><br /> (DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *DescriptorHandle*. Aún estaba ejecutando esta función asincrónica cuando el **SQLGetDescField** se llamó a la función.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY021|Información de descriptor incoherente|Los campos SQL_DESC_TYPE y SQL_DESC_DATETIME_INTERVAL_CODE no forman un tipo válido de SQL de ODBC, un tipo válido de SQL específicas del controlador (para los IDP) o un tipo válido de C de ODBC (para APD o en adelante).|  
|HY090|Longitud de búfer o cadena no válida|(DM)  *\*ValuePtr* era una cadena de caracteres, y *BufferLength* era menor que cero.|  
|HY091|Identificador de campo descriptor no válido|*FieldIdentifier* no era un campo de ODBC y no era un valor definido por la implementación.<br /><br /> *FieldIdentifier* no se ha definido para el *DescriptorHandle*.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *DescriptorHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Una aplicación puede llamar a **SQLGetDescField** para devolver el valor de un único campo de un registro del descriptor. Una llamada a **SQLGetDescField** puede devolver el valor de cualquier campo en cualquier tipo de descriptor, incluidos los campos de encabezado, los campos de registros y campos de marcador. Una aplicación puede obtener la configuración de varios campos en los descriptores de iguales o distintos, en orden aleatorio, mediante la realización de llamadas repetidas a **SQLGetDescField**. **SQLGetDescField** también se puede llamar para devolver los campos de descriptor definidos por el controlador.  
  
 Por motivos de rendimiento, una aplicación no debe llamar a **SQLGetDescField** para un IRD antes de ejecutar una instrucción.  
  
 También se pueden recuperar los valores de varios campos que describen el nombre, tipo de datos y almacenamiento de datos de columna o parámetro en una sola llamada a **SQLGetDescRec**. **SQLGetStmtAttr** puede llamarse para devolver el valor de un único campo en el encabezado de descriptor que también es un atributo de instrucción. **SQLColAttribute**, **SQLDescribeCol**, y **SQLDescribeParam** devolver los campos de registro o el marcador.  
  
 Cuando una aplicación llama **SQLGetDescField** para recuperar el valor de un campo que no está definido para un tipo de descriptor determinado, la función devuelve SQL_SUCCESS, pero el valor devuelto para el campo es indefinido. Por ejemplo, al llamar a **SQLGetDescField** para el campo SQL_DESC_NAME o SQL_DESC_NULLABLE de un APD o descartar devuelve SQL_SUCCESS, pero un valor no definido para el campo.  
  
 Cuando una aplicación llama **SQLGetDescField** para recuperar el valor de un campo que se define para un tipo de descriptor concreto pero que no tiene ningún valor predeterminado y no se ha establecido aún, la función devuelve SQL_SUCCESS, pero el valor devuelto para el campo es indefinido. Para obtener más información sobre la inicialización de campos de descriptor y descripciones de los campos, consulte "Inicialización de campos de Descriptor" en [SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md). Para obtener más información sobre los descriptores de, consulte [descriptores](../../../odbc/reference/develop-app/descriptors.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Introducción a varios campos de descriptor|[Función SQLGetDescRec](../../../odbc/reference/syntax/sqlgetdescrec-function.md)|  
|Configuración de un campo único descriptor|[Función SQLSetDescField](../../../odbc/reference/syntax/sqlsetdescfield-function.md)|  
|Configuración de varios campos de descriptor|[Función SQLSetDescRec](../../../odbc/reference/syntax/sqlsetdescrec-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
