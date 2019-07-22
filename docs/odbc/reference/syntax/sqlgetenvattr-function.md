---
title: Función SQLGetEnvAttr | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 0940a5a2c70a7b670ca6a81521759fd08e60461e
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/19/2019
ms.locfileid: "68345630"
---
# <a name="sqlgetenvattr-function"></a>Función SQLGetEnvAttr
**Conformidad**  
 Versión introducida: Compatibilidad con los estándares de ODBC 3,0: ISO 92  
  
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
 Entradas Identificador de entorno.  
  
 *Atributo*  
 Entradas Atributo que se va a recuperar.  
  
 *ValuePtr*  
 Genere Puntero a un búfer en el que se va a devolver el valor actual del atributo especificado por el *atributo*.  
  
 Si *ValuePtr* es null, *StringLengthPtr* devolverá el número total de bytes (sin incluir el carácter de terminación null para los datos de caracteres) disponible para devolver en el búfer señalado por *ValuePtr*.  
  
 *BufferLength*  
 Entradas Si *ValuePtr* apunta a una cadena de caracteres, este argumento debe ser la longitud \*de *ValuePtr*. Si \* *ValuePtr* es un entero, *BufferLength* se omite. *Si\*ValuePtr* es una cadena Unicode (al llamar a **SQLGetEnvAttrW**), el argumento *BufferLength* debe ser un número par. Si el valor del atributo no es una cadena de caracteres, *BufferLength* no se utiliza.  
  
 *StringLengthPtr*  
 Genere Un puntero a un búfer en el que se va a devolver el número total de bytes (sin incluir el carácter de terminación de NULL) disponible para devolver en  *\*ValuePtr*. Si *ValuePtr* es un puntero nulo, no se devuelve ninguna longitud. Si el valor del atributo es una cadena de caracteres y el número de bytes disponibles para devolver es mayor o igual que *BufferLength*, los datos \*de *ValuePtr* se truncan en *BufferLength* menos la longitud de una terminación nula. y el controlador termina en NULL.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLGetEnvAttr** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_ENV y un *identificador* de *EnvironmentHandle*. En la tabla siguiente se enumeran los valores de SQLSTATE que devuelve normalmente **SQLGetEnvAttr** y se explica cada uno de ellos en el contexto de esta función. la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|ADVERTENCIA general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena, truncados a la derecha|Los datos devueltos en \* *ValuePtr* se truncaron para *BufferLength* menos el carácter de terminación null. La longitud del valor de cadena no truncado se devuelve en **StringLengthPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|HY000|Error general|Se produjo un error para el que no había ningún SQLSTATE específico y para el que no se definió ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*búfer MessageText* describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY010|Error de secuencia de función|(DM) **SQL_ATTR_ODBC_VERSION** todavía no se ha establecido a través de **SQLSetEnvAttr**. No es necesario establecer **SQL_ATTR_ODBC_VERSION** explícitamente si se usa **SQLAllocHandleStd**.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de memoria insuficientes.|  
|HY092|Identificador de opción/atributo no válido|El valor especificado para el *atributo* argument no era válido para la versión de ODBC admitida por el controlador.|  
|HY117|La conexión se suspendió debido a un estado de transacción desconocido. Solo se permiten las funciones de desconexión y de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|El valor especificado para el *atributo* argument era un atributo de entorno ODBC válido para la versión de ODBC admitida por el controlador, pero no era compatible con el controlador.|  
|IM001|El controlador no admite esta función|(DM) el controlador correspondiente a *EnvironmentHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Para obtener una lista de atributos, vea [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md). No hay ningún atributo de entorno específico del controlador. Si el *atributo* especifica un atributo que devuelve una cadena, *ValuePtr* debe ser un puntero a un búfer en el que se va a devolver la cadena. La longitud máxima de la cadena, incluido el byte de terminación de NULL, será *BufferLength* bytes.  
  
 Se puede llamar a **SQLGetEnvAttr** en cualquier momento entre la asignación y la liberación de un identificador de entorno. Todos los atributos de entorno establecidos correctamente por la aplicación para el entorno se conservan hasta que se llama a **SQLFreeHandle** en *EnvironmentHandle* con *HandleType* de SQL_HANDLE_ENV. Se puede asignar más de un identificador de entorno simultáneamente en ODBC 3 *. x*. Un atributo de entorno en un entorno no se ve afectado cuando se ha asignado otro entorno.  
  
> [!NOTE]
>  El atributo de entorno SQL_ATTR_OUTPUT_NTS es compatible con las aplicaciones compatibles con los estándares. Cuando se llama a **SQLGetEnvAttr** , el administrador de controladores ODBC 3 *. x* siempre devuelve SQL_TRUE para este atributo. SQL_ATTR_OUTPUT_NTS solo se puede establecer en SQL_TRUE mediante una llamada a **SQLSetEnvAttr**.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Devolver el valor de un atributo de conexión|[Función SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Devolver el valor de un atributo de instrucción|[Función SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|Establecer un atributo de conexión|[Función SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Establecer un atributo de entorno|[Función SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|Establecer un atributo de instrucción|[Función SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
