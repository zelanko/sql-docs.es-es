---
title: Función SQLGetEnvAttr | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 11c2b83057291f04e7476abddc63c0ccb9954b85
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="sqlgetenvattr-function"></a>SQLGetEnvAttr (función)
**Conformidad**  
 Versión introdujo: ODBC 3.0 normativas: ISO 92  
  
 **Resumen**  
 **SQLGetEnvAttr** devuelve el valor actual de un atributo de entorno.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
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
  
 Si *ValuePtr* es NULL, *StringLengthPtr* devolverá el número total de bytes (sin incluir el carácter de terminación null para los datos de carácter) disponible para devolver en el búfer señalado por  *ValuePtr*.  
  
 *BufferLength*  
 [Entrada] Si *ValuePtr* apunta a una cadena de caracteres, este argumento debe ser la longitud de \* *ValuePtr*. Si \* *ValuePtr* es un entero, *BufferLength* se omite. Si  *\*ValuePtr* es una cadena Unicode (cuando se llama a **SQLGetEnvAttrW**), el *BufferLength* el argumento debe ser un número par. Si el valor de atributo no es una cadena de caracteres *BufferLength* no se utiliza.  
  
 *StringLengthPtr*  
 [Salida] Un puntero a un búfer en el que se va a devolver el número total de bytes (sin incluir el carácter de terminación null) disponible para devolver en  *\*ValuePtr*. Si *ValuePtr* es un puntero nulo, no se devuelve ninguna longitud. Si el valor del atributo es una cadena de caracteres y el número de bytes disponible para devolver es mayor o igual que *BufferLength*, los datos de \* *ValuePtr* se trunca a  *BufferLength* menos la longitud de un carácter de terminación null y termina en null el controlador.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLGetEnvAttr** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_ENV y un *controlar* de *EnvironmentHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLGetEnvAttr** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena, delimitado truncados|Los datos devueltos en \* *ValuePtr* se ha truncado para ser *BufferLength* menos el carácter de terminación null. Se devuelve la longitud del valor de cadena untruncated en **StringLengthPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY010|Error de secuencia de función|(DM) **SQL_ATTR_ODBC_VERSION** aún no se ha establecido a través de **SQLSetEnvAttr**. No es necesario establecer **SQL_ATTR_ODBC_VERSION** explícitamente si utilizas **SQLAllocHandleStd**.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY092|Identificador de opción o atributo no válido|El valor especificado para el argumento *atributo* no era válido para la versión de ODBC compatible con el controlador.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|El valor especificado para el argumento *atributo* era un atributo válido de entorno de ODBC para el controlador es compatible con la versión de ODBC, pero no era compatible con el controlador.|  
|IM001|Controlador no admite esta función|(DM) el controlador correspondiente a la *EnvironmentHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Para obtener una lista de atributos, vea [SQLSetEnvAttr](../../../odbc/reference/syntax/sqlsetenvattr-function.md). No hay ningún atributo de entorno específicas del controlador. Si *atributo* especifica un atributo que devuelve una cadena, *ValuePtr* debe ser un puntero a un búfer en el que se va a devolver la cadena. La longitud máxima de la cadena, incluido el byte de finalización en null, será *BufferLength* bytes.  
  
 **SQLGetEnvAttr** se puede llamar en cualquier momento entre la asignación y liberación de un identificador de entorno. Todos los atributos de entorno definidos correctamente para la aplicación para el entorno se conservan hasta que **SQLFreeHandle** se llama en el *EnvironmentHandle* con un *HandleType*de SQL_HANDLE_ENV. Se puede asignar más de un identificador de entorno al mismo tiempo en ODBC 3*.x*. Un atributo de entorno en un entorno no se ve afectado cuando se ha asignado otro entorno.  
  
> [!NOTE]  
>  El atributo de entorno SQL_ATTR_OUTPUT_NTS es compatible con aplicaciones compatibles con los estándares. Cuando **SQLGetEnvAttr** se denomina ODBC 3*.x* siempre el Administrador de controladores devuelve SQL_TRUE para este atributo. Se puede establecer SQL_ATTR_OUTPUT_NTS en SQL_TRUE sólo mediante una llamada a **SQLSetEnvAttr**.  
  
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
