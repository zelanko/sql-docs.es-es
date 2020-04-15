---
title: FUNción SQLGetEnvAttr ? Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetEnvAttr
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLGetEnvAttr
helpviewer_keywords:
- SQLGetEnvAttr function [ODBC]
ms.assetid: 01f4590f-427a-4280-a1c3-18de9f7d86c1
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 77cd24386a8eea6769aee59f3674b681c516d9ed
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285315"
---
# <a name="sqlgetenvattr-function"></a>Función SQLGetEnvAttr
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 3.0: ISO 92  
  
 **Resumen**  
 **SQLGetEnvAttr** devuelve la configuración actual de un atributo de entorno.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLGetEnvAttr(  
     SQLHENV        EnvironmentHandle,  
     SQLINTEGER     Attribute,  
     SQLPOINTER     ValuePtr,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *EnvironmentHandle*  
 [Entrada] Mango de entorno.  
  
 *Atributo*  
 [Entrada] Atributo que se va a recuperar.  
  
 *ValuePtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el valor actual del atributo especificado por *Attribute*.  
  
 Si *ValuePtr* es NULL, *StringLengthPtr* seguirá devolviendo el número total de bytes (excluyendo el carácter de terminación nula para los datos de caracteres) disponibles para devolver en el búfer señalado por *ValuePtr*.  
  
 *BufferLength*  
 [Entrada] Si *ValuePtr* apunta a una cadena de caracteres, este argumento debe ser la longitud de \* *ValuePtr*. Si \* *ValuePtr* es un entero, *BufferLength* se omite. Si * \*ValuePtr* es una cadena Unicode (al llamar a **SQLGetEnvAttrW**), el *BufferLength* argumento debe ser un número par. Si el valor del atributo no es una cadena de caracteres, *BufferLength* no se utiliza.  
  
 *StringLengthPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número total de bytes (excluyendo el carácter de terminación nula) disponiblepara devolver en * \*ValuePtr*. Si *ValuePtr* es un puntero nulo, no se devuelve ninguna longitud. Si el valor del atributo es una cadena de caracteres y el número de bytes disponibles para devolver es mayor o igual que *BufferLength*, los datos de \* *ValuePtr* se truncan en *BufferLength* menos la longitud de un carácter de terminación nula y el controlador termina en null.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLGetEnvAttr** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_ENV y un *control* de *EnvironmentHandle*. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLGetEnvAttr** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01004|Datos de cadena truncados a la derecha|Los datos \*devueltos en *ValuePtr* se truncaron para ser *BufferLength* menos el carácter de terminación nula. La longitud del valor de cadena no truncada se devuelve en **StringLengthPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY010|Error de secuencia de funciones|(DM) **SQL_ATTR_ODBC_VERSION** aún no se ha establecido a través de **SQLSetEnvAttr**. No es necesario establecer **SQL_ATTR_ODBC_VERSION** explícitamente si utiliza **SQLAllocHandleStd**.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY092|Identificador de atributo/opción no válido|El valor especificado para el argumento *Attribute* no era válido para la versión de ODBC admitida por el controlador.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYC00|Característica opcional no implementada|El valor especificado para el argumento *Attribute* era un atributo de entorno ODBC válido para la versión de ODBC admitida por el controlador, pero no era compatible con el controlador.|  
|IM001|El controlador no admite esta función|(DM) El controlador correspondiente a *EnvironmentHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Para obtener una lista de atributos, vea [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md). No hay atributos de entorno específicos del controlador. Si *Attribute* especifica un atributo que devuelve una cadena, *ValuePtr* debe ser un puntero a un búfer en el que devolver la cadena. La longitud máxima de la cadena, incluido el byte de terminación nula, será *BufferLength* bytes.  
  
 **SQLGetEnvAttr** se puede llamar en cualquier momento entre la asignación y la liberación de un identificador de entorno. Todos los atributos de entorno establecidos correctamente por la aplicación para el entorno persisten hasta **SQLFreeHandle** se llama en el *EnvironmentHandle* con un *HandleType* de SQL_HANDLE_ENV. Se puede asignar más de un identificador de entorno simultáneamente en ODBC 3 *.x*. Un atributo de entorno en un entorno no se ve afectado cuando se ha asignado otro entorno.  
  
> [!NOTE]
>  El atributo de entorno SQL_ATTR_OUTPUT_NTS es compatible con las aplicaciones compatibles con estándares. Cuando **SQLGetEnvAttr** se llama, el Administrador de controladores ODBC 3 *.x* siempre devuelve SQL_TRUE para este atributo. SQL_ATTR_OUTPUT_NTS se puede establecer en SQL_TRUE solo mediante una llamada a **SQLSetEnvAttr**.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Devolver la configuración de un atributo de conexión|[Función SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Devolver la configuración de un atributo de instrucción|[Función SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|Establecer un atributo de conexión|[Función SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Establecer un atributo de entorno|[Función SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|Establecer un atributo de instrucción|[Función SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
