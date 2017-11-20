---
title: "Función SQLGetConnectAttr | Documentos de Microsoft"
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
- SQLGetConnectOption
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetConnectAttr
helpviewer_keywords:
- SQLGetConnectAttr function [ODBC]
ms.assetid: 2cb4ffa8-19d3-4664-8c2f-6682cdcc3f33
caps.latest.revision: 32
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fc8f754301b5b0c0d5259cd7613bacdf302a06e7
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlgetconnectattr-function"></a>Función SQLGetConnectAttr
**Conformidad**  
 Versión introdujo: ODBC 3.0 normativas: ISO 92  
  
 **Resumen**  
 **SQLGetConnectAttr** devuelve el valor actual de un atributo de conexión.  
  
> [!NOTE]  
>  Para obtener más información sobre lo que el Administrador de controladores se asigna esta función cuando una aplicación ODBC 3*.x* aplicación está trabajando con una API ODBC 2*.x* controladores, consulte [asignación de funciones de reemplazo para hacia atrás Compatibilidad de las aplicaciones](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
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
 *IdentificadorConexión*  
 [Entrada] Identificador de conexión.  
  
 *Atributo*  
 [Entrada] Atributo para recuperar.  
  
 *ValuePtr*  
 [Salida] Un puntero a la memoria en el que se va a devolver el valor actual del atributo especificado por *atributo*. Para los atributos de tipo entero, algunos controladores pueden escribir solo inferior 32 bits o el bit de orden superior de 16 bits de un búfer y dejar sin cambios. Por lo tanto, las aplicaciones deben usar un búfer de SQLULEN e inicializar el valor en 0 antes de llamar a esta función.  
  
 Si *ValuePtr* es NULL, *StringLengthPtr* devolverá el número total de bytes (sin incluir el carácter de terminación null para los datos de carácter) disponible para devolver en el búfer señalado por  *ValuePtr*.  
  
 *BufferLength*  
 [Entrada] Si *atributo* es un atributo definido en ODBC y *ValuePtr* apunta a una cadena de caracteres o un búfer binario, este argumento debe ser la longitud de \* *ValuePtr*. Si *atributo* es un atributo definido en ODBC y \* *ValuePtr* es un entero, *BufferLength* se omite. Si el valor de  *\*ValuePtr* es una cadena Unicode (cuando se llama a **SQLGetConnectAttrW**), el *BufferLength* el argumento debe ser un número par.  
  
 Si *atributo* es un atributo definido por el controlador, la aplicación indica la naturaleza del atributo para el Administrador de controladores al establecer el *BufferLength* argumento. *BufferLength* puede tener los valores siguientes:  
  
-   Si  *\*ValuePtr* es un puntero a una cadena de caracteres *BufferLength* es la longitud de la cadena.  
  
-   Si  *\*ValuePtr* es un puntero a un búfer binario, los lugares de la aplicación en el resultado de la SQL_LEN_BINARY_ATTR (*longitud*) macro en *BufferLength*. Esto coloca un valor negativo en *BufferLength*.  
  
-   Si  *\*ValuePtr* es un puntero a un valor distinto de una cadena de carácter o cadena binaria, *BufferLength* debería tener el valor SQL_IS_POINTER.  
  
-   Si  *\*ValuePtr* contiene un tipo de datos de longitud fija, *BufferLength* es SQL_IS_INTEGER o SQL_IS_UINTEGER, según corresponda.  
  
 *StringLengthPtr*  
 [Salida] Un puntero a un búfer en el que se va a devolver el número total de bytes (sin incluir el carácter de terminación null) disponible para devolver en \* *ValuePtr*. Si \* *ValuePtr* es un puntero nulo, no se devuelve ninguna longitud. Si el valor del atributo es una cadena de caracteres y el número de bytes disponible para devolver es mayor que *BufferLength* menos la longitud del carácter de terminación null, los datos de  *\*ValuePtr*se trunca a *BufferLength* menos la longitud del carácter de terminación null y termina en null el controlador.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLGetConnectAttr** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado puede obtenerse a partir de la estructura de datos de diagnóstico mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_DBC y un *controlar* de *IdentificadorConexión*. En la tabla siguiente se enumera los valores SQLSTATE suelen ser devueltos por **SQLGetConnectAttr** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores . El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena, delimitado truncados|Los datos devueltos en \* *ValuePtr* se ha truncado para ser *BufferLength* menos la longitud de un carácter de terminación null. Se devuelve la longitud del valor de cadena untruncated en **StringLengthPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08003|Conexión no abierta|(DM) un *atributo* se especificó el valor que requiere una conexión abierta.|  
|08S01|Error de vínculo de comunicación|El vínculo de comunicación entre el controlador y el origen de datos al que se conectó el controlador no pudo antes del procesamiento de la función se ha completado.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. Devuelve el mensaje de error de la estructura de datos de diagnóstico mediante el argumento *MessageText* en **SQLGetDiagField** describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar memoria que es necesario para admitir la ejecución o la finalización de la función.|  
|HY010|Error de secuencia de función|(DM) **SQLBrowseConnect** se llamó para el *IdentificadorConexión* y devuelve SQL_NEED_DATA. Esta función se invoca antes de **SQLBrowseConnect** devuelve SQL_SUCCESS_WITH_INFO o SQL_SUCCESS.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *IdentificadorConexión* devolvió SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM)  *\*ValuePtr* es una cadena de caracteres y BufferLength era menor que cero, pero no es igual a SQL_NTS.|  
|HY092|Identificador de opción o atributo no válido|El valor especificado para el argumento *atributo* no era válido para la versión de ODBC compatible con el controlador.|  
|HY114|Controlador no admite la ejecución de la función de nivel de conexión asincrónica|(DM) una aplicación intentó habilitar la ejecución de la función asincrónica con SQL_ATTR_ASYNC_DBC_FUNCTIONS_ENABLE para un controlador que no admite operaciones de conexión asincrónica.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|El valor especificado para el argumento *atributo* era un atributo de conexión ODBC válido para el controlador es compatible con la versión de ODBC, pero no era compatible con el controlador.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador que se corresponde con el *IdentificadorConexión* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Para obtener información general acerca de los atributos de conexión, vea [atributos de conexión](../../../odbc/reference/develop-app/connection-attributes.md).  
  
 Para obtener una lista de atributos que se pueden establecer, consulte [SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md). Tenga en cuenta que if *atributo* especifica un atributo que devuelve una cadena, *ValuePtr* debe ser un puntero a un búfer para la cadena. La longitud máxima de la cadena devuelta, incluido el carácter de terminación null, será *BufferLength* bytes.  
  
 Según el atributo, una aplicación no tiene que establecer una conexión antes de llamar a **SQLGetConnectAttr**. Sin embargo, si **SQLGetConnectAttr** se llama y el atributo especificado no tiene valor predeterminado y no se ha establecido por una llamada anterior a **SQLSetConnectAttr**, **SQLGetConnectAttr**devuelve SQL_NO_DATA.  
  
 Si *atributo* es SQL_ATTR_ seguimiento o SQL_ATTR_ TRACEFILE, *IdentificadorConexión* no tiene que ser válido, y **SQLGetConnectAttr** no devolverá SQL_ERROR o SQL_ INVALID_HANDLE si *IdentificadorConexión* no es válido. Estos atributos se aplican a todas las conexiones. **SQLGetConnectAttr** devolverá SQL_ERROR o SQL_INVALID_HANDLE si otro argumento no es válido.  
  
 Aunque una aplicación puede establecer los atributos de instrucción mediante **SQLSetConnectAttr**, no se puede usar una aplicación **SQLGetConnectAttr** para recuperar el atributo de instrucción valores; debe llamar a  **SQLGetStmtAttr** para recuperar la configuración de atributos de instrucción.  
  
 Atributos de conexión SQL_ATTR_AUTO_IPD y SQL_ATTR_CONNECTION_DEAD pueden devolver una llamada a **SQLGetConnectAttr** pero no se puede establecer mediante una llamada a **SQLSetConnectAttr**.  
  
> [!NOTE]  
>  No hay ninguna compatibilidad asincrónica para **SQLGetConnectAttr**. Al implementar **SQLGetConnectAttr**, un controlador puede mejorar el rendimiento reduciendo el número de veces que se envía información o se solicita al servidor.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Devolver el valor de un atributo de instrucción|[SQLGetStmtAttr, función](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|Establecer un atributo de conexión|[SQLSetConnectAttr, función](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Establecer un atributo de entorno|[SQLSetEnvAttr, función](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|Establecer un atributo de instrucción|[SQLSetStmtAttr, función](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)

