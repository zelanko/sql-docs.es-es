---
title: Función SQLGetConnectAttr ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e6076f14ff0c33fec38b99e9c43b8a688970a7a9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285635"
---
# <a name="sqlgetconnectattr-function"></a>Función SQLGetConnectAttr
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 3.0: ISO 92  
  
 **Resumen**  
 **SQLGetConnectAttr** devuelve la configuración actual de un atributo de conexión.  
  
> [!NOTE]
>  Para obtener más información acerca de a qué asigna el Administrador de controladores esta función cuando una aplicación ODBC 3 *.x* está trabajando con un controlador ODBC 2 *.x,* vea Asignación de funciones de [reemplazo para la compatibilidad con versiones anteriores de aplicaciones](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
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
 [Entrada] Atributo que se va a recuperar.  
  
 *ValuePtr*  
 [Salida] Puntero a la memoria en el que se va a devolver el valor actual del atributo especificado por *Attribute*. Para los atributos de tipo entero, algunos controladores solo pueden escribir los 32 bits inferiores o 16 bits de un búfer y dejar el bit de orden superior sin cambios. Por lo tanto, las aplicaciones deben usar un búfer de SQLULEN e inicializar el valor en 0 antes de llamar a esta función.  
  
 Si *ValuePtr* es NULL, *StringLengthPtr* seguirá devolviendo el número total de bytes (excluyendo el carácter de terminación nula para los datos de caracteres) disponibles para devolver en el búfer señalado por *ValuePtr*.  
  
 *BufferLength*  
 [Entrada] Si *Attribute* es un atributo definido por ODBC y *ValuePtr* apunta a una cadena \*de caracteres o un búfer binario, este argumento debe ser la longitud de *ValuePtr*. Si *Attribute* es un atributo \*definido por ODBC y *ValuePtr* es un entero, *BufferLength* se omite. Si el valor de * \*ValuePtr* es una cadena Unicode (al llamar a **SQLGetConnectAttrW**), el argumento *BufferLength* debe ser un número par.  
  
 Si *Attribute* es un atributo definido por el controlador, la aplicación indica la naturaleza del atributo para el Administrador de controladores estableciendo el *BufferLength* argumento. *BufferLength* puede tener los siguientes valores:  
  
-   Si * \*ValuePtr* es un puntero a una cadena de caracteres, *BufferLength* es la longitud de la cadena.  
  
-   Si * \*ValuePtr* es un puntero a un búfer binario, la aplicación coloca el resultado de la macro SQL_LEN_BINARY_ATTR(*length*) en *BufferLength*. Esto coloca un valor negativo en *BufferLength*.  
  
-   Si * \*ValuePtr* es un puntero a un valor distinto de una cadena de caracteres o una cadena binaria, *BufferLength* debe tener el valor SQL_IS_POINTER.  
  
-   Si * \*ValuePtr* contiene un tipo de datos de longitud fija, *BufferLength* es SQL_IS_INTEGER o SQL_IS_UINTEGER, según corresponda.  
  
 *StringLengthPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número total \*de bytes (excluyendo el carácter de terminación nula) disponiblepara devolver en *ValuePtr*. Si \* *ValuePtr* es un puntero nulo, no se devuelve ninguna longitud. Si el valor del atributo es una cadena de caracteres y el número de bytes disponibles para devolver es mayor que *BufferLength* menos la longitud del carácter de terminación nula, los datos de * \*ValuePtr* se truncan en *BufferLength* menos la longitud del carácter de terminación nula y el controlador termina en null.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLGetConnectAttr** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado de la estructura de datos de diagnóstico llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_DBC y un *control* de *ConnectionHandle*. En la tabla siguiente se enumeran los valores SQLSTATE normalmente devueltos por **SQLGetConnectAttr** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01004|Datos de cadena truncados a la derecha|Los datos \*devueltos en *ValuePtr* se truncaron para ser *BufferLength* menos la longitud de un carácter de terminación nula. La longitud del valor de cadena no truncada se devuelve en **StringLengthPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexión no abierta|(DM) Se especificó un valor *de atributo* que requería una conexión abierta.|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto desde la estructura de datos de diagnóstico por el argumento *MessageText* en **SQLGetDiagField** describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY010|Error de secuencia de funciones|(DM) **SQLBrowseConnect** se llamó para el *ConnectionHandle* y devuelto SQL_NEED_DATA. Esta función se llamó antes de **SQLBrowseConnect** devuelto SQL_SUCCESS_WITH_INFO o SQL_SUCCESS.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *ConnectionHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY090|Cadena no válida o longitud de búfer|(DM) * \*ValuePtr* es una cadena de caracteres y BufferLength era menor que cero, pero no igual a SQL_NTS.|  
|HY092|Identificador de atributo/opción no válido|El valor especificado para el argumento *Attribute* no era válido para la versión de ODBC admitida por el controlador.|  
|HY114|El controlador no admite la ejecución de funciones asincrónicas a nivel de conexión|(DM) Una aplicación intentó habilitar la ejecución de funciones asincrónicas con SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE para un controlador que no admite operaciones de conexión asincrónicas.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYC00|Característica opcional no implementada|El valor especificado para el argumento *Attribute* era un atributo de conexión ODBC válido para la versión de ODBC admitida por el controlador, pero no lo admitía el controlador.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador que corresponde a *ConnectionHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Para obtener información general sobre los atributos de conexión, consulte [Atributos](../../../odbc/reference/develop-app/connection-attributes.md)de conexión .  
  
 Para obtener una lista de atributos que se pueden establecer, vea [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md). Tenga en cuenta que si *Attribute* especifica un atributo que devuelve una cadena, *ValuePtr* debe ser un puntero a un búfer para la cadena. La longitud máxima de la cadena devuelta, incluido el carácter de terminación nula, será *BufferLength* bytes.  
  
 Según el atributo, una aplicación no tiene que establecer una conexión antes de llamar a **SQLGetConnectAttr**. Sin embargo, si se llama a **SQLGetConnectAttr** y el atributo especificado no tiene un valor predeterminado y no se ha establecido mediante una llamada anterior a **SQLSetConnectAttr**, **SQLGetConnectAttr** devolverá SQL_NO_DATA.  
  
 Si *Attribute* es SQL_ATTR_ TRACE o SQL_ATTR_ TRACEFILE, *ConnectionHandle* no tiene que ser válido y **SQLGetConnectAttr** no devolverá SQL_ERROR o SQL_INVALID_HANDLE si *ConnectionHandle* no es válido. Estos atributos se aplican a todas las conexiones. **SQLGetConnectAttr** devolverá SQL_ERROR o SQL_INVALID_HANDLE si otro argumento no es válido.  
  
 Aunque una aplicación puede establecer atributos de instrucción mediante **SQLSetConnectAttr**, una aplicación no puede usar **SQLGetConnectAttr** para recuperar valores de atributo de instrucción; debe llamar a **SQLGetStmtAttr** para recuperar la configuración de los atributos de instrucción.  
  
 Los atributos de conexión SQL_ATTR_AUTO_IPD y SQL_ATTR_CONNECTION_DEAD se pueden devolver mediante una llamada a **SQLGetConnectAttr,** pero no se puede establecer mediante una llamada a **SQLSetConnectAttr**.  
  
> [!NOTE]  
>  No hay compatibilidad asincrónica con **SQLGetConnectAttr**. Al implementar **SQLGetConnectAttr**, un controlador puede mejorar el rendimiento minimizando el número de veces que se envía o solicita esa información desde el servidor.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Devolver la configuración de un atributo de instrucción|[Función SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|Establecer un atributo de conexión|[Función SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Establecer un atributo de entorno|[Función SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|Establecer un atributo de instrucción|[Función SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
