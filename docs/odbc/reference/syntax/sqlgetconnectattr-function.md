---
title: Función SQLGetConnectAttr | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConnectAttr
helpviewer_keywords:
- SQLGetConnectAttr function [ODBC]
ms.assetid: 2cb4ffa8-19d3-4664-8c2f-6682cdcc3f33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 4a24ccf58a1cd0f6d0f4fb2fd32dbee79feb896b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/23/2019
ms.locfileid: "63259638"
---
# <a name="sqlgetconnectattr-function"></a>Función SQLGetConnectAttr
**Conformidad**  
 Versión de introducción: Compatibilidad de ODBC 3.0 estándares: ISO 92  
  
 **Resumen**  
 **SQLGetConnectAttr** devuelve el valor actual de un atributo de conexión.  
  
> [!NOTE]
>  Para obtener más información sobre lo que el Administrador de controladores se asigna esta función cuando una aplicación ODBC 3 *.x* aplicación funciona con un ODBC 2 *.x* controladores, consulte [asignación de funciones de reemplazo para hacia atrás Compatibilidad de aplicaciones](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLGetConnectAttr(  
     SQLHDBC        ConnectionHandle,  
     SQLINTEGER     Attribute,  
     SQLPOINTER     ValuePtr,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConnectionHandle*  
 [Entrada] Identificador de conexión.  
  
 *Atributo*  
 [Entrada] Atributo para recuperar.  
  
 *ValuePtr*  
 [Salida] Un puntero a la memoria en el que se va a devolver el valor actual del atributo especificado por *atributo*. Para los atributos de tipo entero, algunos controladores pueden escribir solo el 32-bit inferior o el bit de orden superior de 16 bits de un búfer y dejar sin cambios. Por lo tanto, las aplicaciones deben utilizar un búfer de SQLULEN e inicializar el valor a 0 antes de llamar a esta función.  
  
 Si *ValuePtr* es NULL, *StringLengthPtr* devolverá el número total de bytes (excluido el carácter de terminación null para los datos de caracteres) disponibles para devolver en el búfer señalado por  *ValuePtr*.  
  
 *BufferLength*  
 [Entrada] Si *atributo* es un atributo definido por el ODBC y *ValuePtr* apunta a un búfer binario o una cadena de caracteres, este argumento debe ser la longitud de \* *ValuePtr*. Si *atributo* es un atributo definido por el ODBC y \* *ValuePtr* es un entero, *BufferLength* se omite. Si el valor de  *\*ValuePtr* es una cadena Unicode (al llamar a **SQLGetConnectAttrW**), el *BufferLength* argumento debe ser un número par.  
  
 Si *atributo* es un atributo definido por el controlador, la aplicación indica la naturaleza del atributo para el Administrador de controladores al establecer el *BufferLength* argumento. *BufferLength* puede tener los siguientes valores:  
  
-   Si  *\*ValuePtr* es un puntero a una cadena de caracteres, *BufferLength* es la longitud de la cadena.  
  
-   Si  *\*ValuePtr* es un puntero a un búfer binario, los lugares de la aplicación en el resultado de la SQL_LEN_BINARY_ATTR (*longitud*) macro en *BufferLength*. Esto coloca un valor negativo en *BufferLength*.  
  
-   Si  *\*ValuePtr* es un puntero a un valor distinto de una cadena de caracteres o una cadena binaria, *BufferLength* debe tener el valor SQL_IS_POINTER.  
  
-   Si  *\*ValuePtr* contiene un tipo de datos de longitud fija, *BufferLength* es SQL_IS_INTEGER o SQL_IS_UINTEGER, según corresponda.  
  
 *StringLengthPtr*  
 [Salida] Un puntero a un búfer en el que se va a devolver el número total de bytes (excluido el carácter de terminación null) disponibles para devolver en \* *ValuePtr*. Si \* *ValuePtr* es un puntero nulo, no se devuelve ninguna longitud. Si el valor del atributo es una cadena de caracteres y es mayor que el número de bytes disponible para devolver *BufferLength* menos la longitud del carácter de terminación null, los datos de  *\*ValuePtr*se trunca a *BufferLength* menos la longitud del carácter de terminación null y termina en null por el controlador.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLGetConnectAttr** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado puede obtenerse a partir de la estructura de datos de diagnóstico mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_DBC y un *controlar* de *ConnectionHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLGetConnectAttr** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores . El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena derecha truncados|Los datos devueltos en \* *ValuePtr* se ha truncado para ser *BufferLength* menos la longitud de un carácter de terminación null. Se devuelve la longitud del valor de cadena sin truncar en **StringLengthPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08003|Conexión no abierta|(DM) un *atributo* se especificó el valor que requiere una conexión abierta.|  
|08S01|Error de vínculo de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos a la que se ha conectado el controlador antes del procesamiento de la función se ha completado.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. Devuelve el mensaje de error de la estructura de datos de diagnóstico mediante el argumento *MessageText* en **SQLGetDiagField** describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar memoria que es necesario para admitir la ejecución o la finalización de la función.|  
|HY010|Error de secuencia de función|(DM) **SQLBrowseConnect** se llamó para el *ConnectionHandle* y devuelve SQL_NEED_DATA. Se llamó a esta función antes de **SQLBrowseConnect** devuelve SQL_SUCCESS_WITH_INFO o SQL_SUCCESS.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *ConnectionHandle* y devuelven SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM)  *\*ValuePtr* es una cadena de caracteres y BufferLength era menor que cero, pero no es igual a SQL_NTS.|  
|HY092|Identificador de opción o atributo no válido|El valor especificado para el argumento *atributo* no era válido para la versión de ODBC compatible con el controlador.|  
|HY114|Controlador no admite la ejecución de la función de nivel de conexión asincrónica|(DM) ha intentado una aplicación habilitar la ejecución de la función asincrónica con SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE para un controlador que no es compatible con las operaciones de conexión asincrónica.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|El valor especificado para el argumento *atributo* era un atributo de conexión ODBC válido para la versión de ODBC compatibles con el controlador, pero no es compatible con el controlador.|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador que se corresponde con el *ConnectionHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Para obtener información general sobre los atributos de conexión, consulte [los atributos de conexión](../../../odbc/reference/develop-app/connection-attributes.md).  
  
 Para obtener una lista de atributos que se pueden establecer, consulte [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md). Tenga en cuenta que if *atributo* especifica un atributo que se devuelve una cadena, *ValuePtr* debe ser un puntero a un búfer para la cadena. La longitud máxima de la cadena devuelta, incluido el carácter de terminación null, será *BufferLength* bytes.  
  
 Dependiendo del atributo, una aplicación no tiene que establecer una conexión antes de llamar a **SQLGetConnectAttr**. Sin embargo, si **SQLGetConnectAttr** se llama y el atributo especificado no tiene valor predeterminado y no se ha establecido mediante una llamada anterior a **SQLSetConnectAttr**, **SQLGetConnectAttr**devuelve SQL_NO_DATA.  
  
 Si *atributo* es SQL_ATTR_ seguimiento o SQL_ATTR_ TRACEFILE, *ConnectionHandle* no tiene que ser válido, y **SQLGetConnectAttr** no devolverá SQL_ERROR o SQL_ INVALID_HANDLE si *ConnectionHandle* no es válido. Estos atributos se aplican a todas las conexiones. **SQLGetConnectAttr** devolverá SQL_ERROR o SQL_INVALID_HANDLE si otro argumento no es válido.  
  
 Aunque una aplicación puede establecer los atributos de instrucción con **SQLSetConnectAttr**, no se puede usar una aplicación **SQLGetConnectAttr** recuperar el atributo de instrucción valores; debe llamar a  **SQLGetStmtAttr** para recuperar la configuración de atributos de instrucción.  
  
 Atributos de conexión SQL_ATTR_AUTO_IPD y SQL_ATTR_CONNECTION_DEAD pueden devolverse mediante una llamada a **SQLGetConnectAttr** pero no se puede establecer mediante una llamada a **SQLSetConnectAttr**.  
  
> [!NOTE]  
>  No hay ninguna compatibilidad asincrónica para **SQLGetConnectAttr**. Al implementar **SQLGetConnectAttr**, un controlador puede mejorar el rendimiento, ya que minimiza el número de veces que se envía o se solicitan del servidor de información.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Devuelve la configuración de un atributo de instrucción|[Función SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|Establecer un atributo de conexión|[Función SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Establecer un atributo de entorno|[Función SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|Establecer un atributo de instrucción|[Función SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
