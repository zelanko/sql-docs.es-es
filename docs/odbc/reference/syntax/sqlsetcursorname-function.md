---
title: Función SQLSetCursorName | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLSetCursorName
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLSetCursorName
helpviewer_keywords:
- SQLSetCursorName function [ODBC]
ms.assetid: 4e055946-12d4-4589-9891-41617a50f34e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 842d21bc36b9360826b4b85aa7da2798782995c6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/15/2019
ms.locfileid: "68092988"
---
# <a name="sqlsetcursorname-function"></a>Función SQLSetCursorName
**Conformidad**  
 Versión de introducción: Cumplimiento de estándares 1.0 de ODBC: ISO 92  
  
 **Resumen**  
 **SQLSetCursorName** asocia un nombre de cursor con una instrucción activa. Si una aplicación no llama a **SQLSetCursorName**, el controlador generará los nombres de cursor según sea necesario para procesar una instrucción SQL.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLSetCursorName(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CursorName,  
     SQLSMALLINT   NameLength);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *cursorName*  
 [Entrada] Nombre del cursor. Para un procesamiento eficaz, el nombre del cursor no debe incluir los espacios iniciales o finales en el nombre del cursor y, si el nombre del cursor incluye un identificador delimitado, debe colocarse el delimitador como primer carácter en el nombre del cursor.  
  
 *NameLength*  
 [Entrada] Longitud en caracteres de **CursorName*.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLSetCursorName** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLSetCursorName** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena derecha truncados|El nombre del cursor superó el límite máximo, por lo que se usa solo el número máximo permitido de caracteres.|  
|24000|Estado de cursor no válido|La instrucción correspondiente a *StatementHandle* ya estaba en un estado ejecutado o una posición de cursor.|  
|34000|Nombre de cursor no válido|El nombre de cursor especificado en **CursorName* no era válido porque superó la longitud máxima definida por el controlador o inicial "SQLCUR" o "SQL_CUR."|  
|3C000|Nombre de cursor duplicado|El nombre de cursor especificado en **CursorName* ya existe.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY009|Uso no válido del puntero nulo|(DM) el argumento *CursorName* era un puntero nulo.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónicas aún estaba ejecutando cuando el **SQLSetCursorName** se llamó a la función.<br /><br /> (DM) se llamó a una función que se ejecuta de forma asincrónica para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el argumento *longituddenombre* era menor que 0 pero no es igual a SQL_NTS.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *StatementHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Los nombres de cursor solo se usan en actualización posicionada y eliminar instrucciones (por ejemplo, **actualizar** _nombre-tabla_ ... **WHERE CURRENT OF** _nombre de cursor_). Para obtener más información, consulte [coloca actualizar y eliminar instrucciones](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md). Si la aplicación no llama a **SQLSetCursorName** para definir un nombre de cursor, en la ejecución de una instrucción de consulta el controlador generará un nombre que comienza con las letras SQL_CUR y no más de 18 caracteres de longitud.  
  
 Todos los nombres de cursor dentro de la conexión deben ser únicos. La longitud máxima de un nombre de cursor se define por el controlador. Para obtener la máxima interoperatividad, se recomienda que las aplicaciones limitar los nombres de cursor a no más de 18 caracteres. En ODBC 3 *.x*, si un nombre de cursor es un identificador entre comillas, se trata de una manera distingue mayúsculas de minúsculas y que puede contener caracteres que no permitiría la sintaxis de SQL o trataría especial, como espacios en blanco o palabras clave reservadas. Si un nombre de cursor debe tratarse de una manera de mayúsculas y minúsculas, se debe pasar como un identificador entre comillas.  
  
 Un nombre de cursor que se establece explícitamente o implícitamente permanece establecido hasta que se quite la instrucción que está asociado, utilizando **SQLFreeHandle**. **SQLSetCursorName** se puede llamar para cambiar el nombre de un cursor en una instrucción siempre y cuando el cursor está en un estado asignado o preparado.  
  
## <a name="code-example"></a>Ejemplo de código  
 En el ejemplo siguiente, una aplicación utiliza **SQLSetCursorName** para establecer un nombre de cursor para una instrucción. A continuación, se usa esa instrucción para recuperar los resultados de la tabla CUSTOMERS. Por último, realiza una actualización posicionada para cambiar el número de teléfono de John Smith. Tenga en cuenta que la aplicación utiliza identificadores de instrucciones diferentes para el **seleccione** y **actualización** instrucciones.  
  
 Para obtener otro ejemplo de código, vea [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```cpp  
#define NAME_LEN 50  
#define PHONE_LEN 10  
  
SQLHSTMT     hstmtSelect,  
SQLHSTMT     hstmtUpdate;  
SQLRETURN    retcode;  
SQLHDBC      hdbc;  
SQLCHAR      szName[NAME_LEN], szPhone[PHONE_LEN];  
SQLINTEGER   cbName, cbPhone;  
  
/* Allocate the statements and set the cursor name. */  
  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmtSelect);  
SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmtUpdate);  
SQLSetCursorName(hstmtSelect, "C1", SQL_NTS);  
  
/* SELECT the result set and bind its columns to local buffers. */  
  
SQLExecDirect(hstmtSelect,  
      "SELECT NAME, PHONE FROM CUSTOMERS",  
      SQL_NTS);  
SQLBindCol(hstmtSelect, 1, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
SQLBindCol(hstmtSelect, 2, SQL_C_CHAR, szPhone, PHONE_LEN, &cbPhone);  
  
/* Read through the result set until the cursor is */  
/* positioned on the row for John Smith. */  
  
do  
 retcode = SQLFetch(hstmtSelect);  
while ((retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) &&  
   (strcmp(szName, "Smith, John") != 0));  
  
/* Perform a positioned update of John Smith's name. */  
  
if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
   SQLExecDirect(hstmtUpdate,  
   "UPDATE EMPLOYEE SET PHONE=\"2064890154\" WHERE CURRENT OF C1",  
   SQL_NTS);  
}  
```  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Ejecutar una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecutar una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Devuelve un nombre de cursor|[Función SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|Establecer opciones de desplazamiento de cursor|[Función SQLSetScrollOptions](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
