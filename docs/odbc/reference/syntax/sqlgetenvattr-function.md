---
title: Función SQLGetEnvAttr | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetEnvAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetEnvAttr
helpviewer_keywords:
- SQLGetEnvAttr function [ODBC]
ms.assetid: 01f4590f-427a-4280-a1c3-18de9f7d86c1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9d09182bc39d99a99f3d03957e296c91101b0fe5
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/11/2019
ms.locfileid: "65538135"
---
# <a name="sqlgetenvattr-function"></a>Función SQLGetEnvAttr
**Conformidad**  
 Versión de introducción: Compatibilidad de ODBC 3.0 estándares: ISO 92  
  
 **Resumen**  
 **SQLGetEnvAttr** devuelve el valor actual de un atributo de entorno.  
  
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
 [Entrada] Identificador de entorno.  
  
 *Atributo*  
 [Entrada] Atributo para recuperar.  
  
 *ValuePtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el valor actual del atributo especificado por *atributo*.  
  
 Si *ValuePtr* es NULL, *StringLengthPtr* devolverá el número total de bytes (excluido el carácter de terminación null para los datos de caracteres) disponibles para devolver en el búfer señalado por  *ValuePtr*.  
  
 *BufferLength*  
 [Entrada] Si *ValuePtr* apunta a una cadena de caracteres, este argumento debe ser la longitud de \* *ValuePtr*. Si \* *ValuePtr* es un entero, *BufferLength* se omite. Si  *\*ValuePtr* es una cadena Unicode (al llamar a **SQLGetEnvAttrW**), el *BufferLength* argumento debe ser un número par. Si el valor del atributo no es una cadena de caracteres, *BufferLength* no se utiliza.  
  
 *StringLengthPtr*  
 [Salida] Un puntero a un búfer en el que se va a devolver el número total de bytes (excluido el carácter de terminación null) disponibles para devolver en  *\*ValuePtr*. Si *ValuePtr* es un puntero nulo, no se devuelve ninguna longitud. Si el valor del atributo es una cadena de caracteres y el número de bytes disponible para devolver es mayor o igual a *BufferLength*, los datos de \* *ValuePtr* se trunca a  *BufferLength* menos la longitud de un carácter de terminación null y termina en null por el controlador.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLGetEnvAttr** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_ENV y un *controlar* de *EnvironmentHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLGetEnvAttr** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena derecha truncados|Los datos devueltos en \* *ValuePtr* se ha truncado para ser *BufferLength* menos el carácter de terminación null. Se devuelve la longitud del valor de cadena sin truncar en **StringLengthPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY010|Error de secuencia de función|(DM) **SQL_ATTR_ODBC_VERSION** aún no se ha establecido a través de **SQLSetEnvAttr**. No es necesario establecer **SQL_ATTR_ODBC_VERSION** explícitamente si usas **SQLAllocHandleStd**.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY092|Identificador de opción o atributo no válido|El valor especificado para el argumento *atributo* no era válido para la versión de ODBC compatible con el controlador.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|El valor especificado para el argumento *atributo* era un atributo de entorno ODBC válido para la versión de ODBC compatibles con el controlador, pero no es compatible con el controlador.|  
|IM001|Controlador no admite esta función|(DM) el controlador correspondiente a la *EnvironmentHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Para obtener una lista de atributos, vea [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md). No hay ningún atributo de entorno específicas del controlador. Si *atributo* especifica un atributo que se devuelve una cadena, *ValuePtr* debe ser un puntero a un búfer en el que se va a devolver la cadena. La longitud máxima de la cadena, incluido el byte de una terminación null, será *BufferLength* bytes.  
  
 **SQLGetEnvAttr** puede llamarse en cualquier momento entre la asignación y la liberación de un identificador de entorno. Se conservan hasta que todos los atributos de entorno se estableció correctamente la aplicación para el entorno **SQLFreeHandle** se llama en el *EnvironmentHandle* con un *HandleType*de SQL_HANDLE_ENV. Se puede asignar más de un identificador de entorno al mismo tiempo en ODBC 3 *.x*. Un atributo de entorno en un entorno no se ve afectado cuando se ha asignado otro entorno.  
  
> [!NOTE]
>  El atributo de entorno SQL_ATTR_OUTPUT_NTS es compatible con aplicaciones compatibles con los estándares. Cuando **SQLGetEnvAttr** se denomina el ODBC 3 *.x* Administrador de controladores siempre devuelve SQL_TRUE para este atributo. Se puede establecer en SQL_TRUE SQL_ATTR_OUTPUT_NTS solo mediante una llamada a **SQLSetEnvAttr**.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Devuelve el valor de un atributo de conexión|[Función SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Devuelve la configuración de un atributo de instrucción|[Función SQLGetStmtAttr](../../../odbc/reference/syntax/sqlgetstmtattr-function.md)|  
|Establecer un atributo de conexión|[Función SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Establecer un atributo de entorno|[Función SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md)|  
|Establecer un atributo de instrucción|[Función SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
