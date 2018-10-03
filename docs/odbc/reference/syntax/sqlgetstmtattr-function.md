---
title: Función SQLGetStmtAttr | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetStmtAttr
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetStmtAttr
helpviewer_keywords:
- SQLGetStmtAttr function [ODBC]
ms.assetid: e321d460-e997-4527-aee6-207cf5a498e9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d2df20e27949b82a9f2e827984f0c2fb77a3814b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47731993"
---
# <a name="sqlgetstmtattr-function"></a>Función SQLGetStmtAttr
**Conformidad**  
 Versión introdujo: ODBC 3.0 normativo: 92 ISO  
  
 **Resumen**  
 **SQLGetStmtAttr** devuelve el valor actual de un atributo de instrucción.  
  
> [!NOTE]  
>  Para obtener más información sobre lo que el Administrador de controladores asigna esta función cuando una aplicación ODBC 3. *x* aplicación funciona con un ODBC 2. *x* controladores, consulte [asignación de funciones de reemplazo para compatibilidad con versiones anteriores de aplicaciones](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLGetStmtAttr(  
     SQLHSTMT        StatementHandle,  
     SQLINTEGER      Attribute,  
     SQLPOINTER      ValuePtr,  
     SQLINTEGER      BufferLength,  
     SQLINTEGER *    StringLengthPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *Atributo*  
 [Entrada] Atributo para recuperar.  
  
 *ValuePtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el valor del atributo especificado en *atributo*.  
  
 Si *ValuePtr* es NULL, *StringLengthPtr* devolverá el número total de bytes (excluido el carácter de terminación null para los datos de caracteres) disponibles para devolver en el búfer señalado por  *ValuePtr*.  
  
 *BufferLength*  
 [Entrada] Si *atributo* es un atributo definido por el ODBC y *ValuePtr* apunta a un búfer binario o una cadena de caracteres, este argumento debe ser la longitud de \* *ValuePtr*. Si *atributo* es un atributo definido por el ODBC y \* *ValuePtr* es un entero, *BufferLength* se omite. Si el valor devuelto en  *\*ValuePtr* es una cadena Unicode (al llamar a **SQLGetStmtAttrW**), el *BufferLength* argumento debe ser un número par.  
  
 Si *atributo* es un atributo definido por el controlador, la aplicación indica la naturaleza del atributo para el Administrador de controladores al establecer el *BufferLength* argumento. *BufferLength* puede tener los siguientes valores:  
  
-   Si  *\*ValuePtr* es un puntero a una cadena de caracteres, a continuación, *BufferLength* es la longitud de la cadena o SQL_NTS.  
  
-   Si  *\*ValuePtr* es un puntero a un búfer binario, a continuación, la aplicación, el resultado de la SQL_LEN_BINARY_ATTR (*longitud*) macro en *BufferLength*. Esto coloca un valor negativo en *BufferLength*.  
  
-   Si  *\*ValuePtr* es un puntero a un valor distinto de una cadena de caracteres o una cadena binaria, a continuación, *BufferLength* debe tener el valor SQL_IS_POINTER.  
  
-   Si  *\*ValuePtr* es contiene un tipo de datos de longitud fija, a continuación, *BufferLength* es SQL_IS_INTEGER o SQL_IS_UINTEGER, según corresponda.  
  
 *StringLengthPtr*  
 [Salida] Un puntero a un búfer en el que se va a devolver el número total de bytes (excluido el carácter de terminación null) disponibles para devolver en  *\*ValuePtr*. Si *ValuePtr* es un puntero nulo, no se devuelve ninguna longitud. Si el valor del atributo es una cadena de caracteres y el número de bytes disponible para devolver es mayor o igual a *BufferLength*, los datos de  *\*ValuePtr* se trunca a *BufferLength* menos la longitud de un carácter de terminación null y termina en null por el controlador.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLGetStmtAttr** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL _HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLGetStmtAttr** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena derecha truncados|Los datos devueltos en  *\*ValuePtr* se ha truncado para ser *BufferLength* menos la longitud de un carácter de terminación null. Se devuelve la longitud del valor de cadena sin truncar en **StringLengthPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|24000|Estado de cursor no válido|El argumento *atributo* era SQL_ATTR_ROW_NUMBER y el cursor no estaba abierto o el cursor se coloca antes del inicio del conjunto de resultados o después del final del conjunto de resultados.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el argumento *MessageText* describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Aún estaba ejecutando esta función asincrónica cuando el **SQLGetStmtAttr** se llamó a la función.<br /><br /> (DM) se llamó a una función que se ejecuta de forma asincrónica para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|*(DM) \*ValuePtr* es una cadena de caracteres y BufferLength era menor que cero, pero no es igual a SQL_NTS.|  
|HY092|Identificador de opción o atributo no válido|El valor especificado para el argumento *atributo* no era válido para la versión de ODBC compatible con el controlador.|  
|HY109|Posición del cursor no válido|El *atributo* argumento era SQL_ATTR_ROW_NUMBER y había eliminada o no se pudo obtener la fila.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|El valor especificado para el argumento *atributo* era un atributo de instrucción ODBC válido para la versión de ODBC compatibles con el controlador, pero no es compatible con el controlador.|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador correspondiente a la *StatementHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Para obtener información general acerca de los atributos de instrucción, consulte [atributos de instrucción](../../../odbc/reference/develop-app/statement-attributes.md).  
  
 Una llamada a **SQLGetStmtAttr** devuelve  *\*ValuePtr* el valor del atributo de instrucción especificado en *atributo*. Ese valor puede ser un valor SQLULEN o una cadena de caracteres terminada en null. Si el valor es un valor SQLULEN, algunos controladores pueden escribir solo el 32-bit inferior o el bit de orden superior de 16 bits de un búfer y dejar sin cambios. Por lo tanto, las aplicaciones deben utilizar un búfer de SQLULEN e inicializar el valor a 0 antes de llamar a esta función. Además, el *BufferLength* y *StringLengthPtr* no se usan argumentos. Si el valor es una cadena terminada en null, la aplicación especifica la longitud máxima de esa cadena en el *BufferLength* argumento y el controlador devuelve la longitud de esa cadena en el  *\* StringLengthPtr* búfer.  
  
 Para permitir que aplicaciones que llaman a **SQLGetStmtAttr** para trabajar con ODBC 2. *x* controladores, una llamada a **SQLGetStmtAttr** se asigna en el Administrador de controladores a **SQLGetStmtOption**.  
  
 Los siguientes atributos de instrucción son de solo lectura, por lo que se puede recuperar **SQLGetStmtAttr**, pero no la establece **SQLSetStmtAttr**:  
  
-   SQL_ATTR_IMP_PARAM_DESC  
  
-   SQL_ATTR_IMP_ROW_DESC  
  
-   SQL_ATTR_ROW_NUMBER  
  
 Para obtener una lista de atributos que se pueden establecer y recuperar, vea [SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Devuelve el valor de un atributo de conexión|[Función SQLGetConnectAttr](../../../odbc/reference/syntax/sqlgetconnectattr-function.md)|  
|Establecer un atributo de conexión|[Función SQLSetConnectAttr](../../../odbc/reference/syntax/sqlsetconnectattr-function.md)|  
|Establecer un atributo de instrucción|[Función SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
