---
title: SQLGetCursorName (Función) Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetCursorName
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetCursorName
helpviewer_keywords:
- SQLGetCursorName function [ODBC]
ms.assetid: e6e92199-7bb6-447c-8987-049a4c6ce05d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d3ac65dc07897ddc789ee03b06b1bc1f71d37c3c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285553"
---
# <a name="sqlgetcursorname-function"></a>Función SQLGetCursorName
**Conformidad**  
 Versión introducida: Cumplimiento de normas ODBC 1.0: ISO 92  
  
 **Resumen**  
 **SQLGetCursorName** devuelve el nombre del cursor asociado a una instrucción especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLGetCursorName(  
     SQLHSTMT        StatementHandle,  
     SQLCHAR *       CursorName,  
     SQLSMALLINT     BufferLength,  
     SQLSMALLINT *   NameLengthPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *CursorName*  
 [Salida] Puntero a un búfer en el que se va a devolver el nombre del cursor.  
  
 Si *CursorName* es NULL, *NameLengthPtr* seguirá devolviendo el número total de caracteres (excluyendo el carácter de terminación nula para los datos de caracteres) disponibles para devolver en el búfer señalado por *CursorName*.  
  
 *BufferLength*  
 [Entrada] Longitud \*de *CursorName*, en caracteres. Si el valor de * \*CursorName* es una cadena Unicode (al llamar a **SQLGetCursorNameW**), el argumento *BufferLength* debe ser un número par.  
  
 *NameLengthPtr*  
 [Salida] Puntero a la memoria en la que se va a devolver el número \*total de caracteres (excluyendo el carácter de terminación nula) disponibles para devolver en *CursorName*. Si el número de caracteres disponibles para devolver es mayor \*o igual que *BufferLength*, el nombre del cursor en *CursorName* se trunca en *BufferLength* menos la longitud de un carácter de terminación nula.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLGetCursorName** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *control* de *StatementHandle*. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLGetCursorName** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01004|Datos de cadena truncados a la derecha|El \*búfer *CursorName* no era lo suficientemente grande como para devolver el nombre completo del cursor, por lo que el nombre del cursor se truncó. La longitud del nombre del cursor no truncado se devuelve en **NameLengthPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para el identificador de conexión asociado a *StatementHandle*. Esta función asincrónica todavía se estaba ejecutando cuando se llamó a la función **SQLGetCursorName** .<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**o **SQLMoreResults** se llamó para el *StatementHandle* y devuelto SQL_PARAM_DATA_AVAILABLE. Se llamó a esta función antes de recuperar los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función de ejecución asincrónica para el *StatementHandle* y todavía se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el *StatementHandle* y devuelto SQL_NEED_DATA. Se llamó a esta función antes de que se enviaran datos para todos los parámetros o columnas de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY015|No hay nombre de cursor disponible|(DM) El controlador era un controlador ODBC 2 *.x,* no había ningún cursor abierto en la instrucción y no se había establecido ningún nombre de cursor con **SQLSetCursorName**.|  
|HY090|Cadena no válida o longitud de búfer|(DM) el valor especificado en el argumento *BufferLength* era menor que 0.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado con el *StatementHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Los nombres de cursor solo se utilizan en instrucciones de actualización y eliminación posicionadas (por ejemplo, **UPDATE** _nombre-tabla_ ... **DONDE ACTUAL DE** _nombre-cursor_). Para obtener más información, consulte [Instrucciones de actualización y eliminación posicionadas](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md). Si la aplicación no llama a **SQLSetCursorName** para definir un nombre de cursor, el controlador genera un nombre. Este nombre comienza con las letras SQL_CUR.  
  
> [!NOTE]
>  En ODBC 2 *.x*, cuando no había ningún cursor abierto y no se había establecido ningún nombre mediante una llamada a **SQLSetCursorName**, una llamada a **SQLGetCursorName** devolvió SQLSTATE HY015 (no hay nombre de cursor disponible). En ODBC 3 *.x*, esto ya no es cierto; Independientemente de cuando **SQLGetCursorName** se llama, el controlador devuelve el nombre del cursor.  
  
 **SQLGetCursorName** devuelve el nombre de un cursor independientemente de si el nombre se creó explícita o implícitamente. Un nombre de cursor se genera implícitamente si **SQLSetCursorName** no se llama. **SQLSetCursorName** se puede llamar para cambiar el nombre de un cursor en una instrucción siempre que el cursor está en un estado asignado o preparado.  
  
 Un nombre de cursor que se establece explícita o implícitamente permanece establecido hasta el *StatementHandle* con el que está asociado se quita, mediante **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_STMT.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para información acerca de|Vea|  
|---------------------------|---------|  
|Ejecución de una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecución de una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Preparación de una declaración para la ejecución|[Función SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|Establecer un nombre de cursor|[Función SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
