---
title: "SQLSetCursorName, función | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
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
caps.latest.revision: 18
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 716170dc027cce47b29a11cc9a650cf4fbb3eb29
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetcursorname-function"></a>SQLSetCursorName, función
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: ISO 92  
  
 **Resumen**  
 **SQLSetCursorName** asocia un nombre de cursor con una instrucción activa. Si una aplicación no llama a **SQLSetCursorName**, el controlador genera nombres de cursor según sea necesario para procesar una instrucción SQL.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLSetCursorName(  
     SQLHSTMT      StatementHandle,  
     SQLCHAR *     CursorName,  
     SQLSMALLINT   NameLength);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *CursorName*  
 [Entrada] Nombre del cursor. Para un procesamiento eficaz, el nombre del cursor no debe incluir los espacios iniciales o finales en el nombre del cursor y, si el nombre del cursor incluye un identificador delimitado, el delimitador debe ser posicionado como el primer carácter en el nombre del cursor.  
  
 *Longituddenombre*  
 [Entrada] Longitud en caracteres de **CursorName*.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLSetCursorName** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLSetCursorName** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena, delimitado truncados|El nombre del cursor superó el límite máximo, por lo que se usa solo el número máximo permitido de caracteres.|  
|24000|Estado de cursor no válido|La instrucción correspondiente a *StatementHandle* ya estaba en un estado ejecutado o cursor colocado.|  
|34000|Nombre de cursor no válido|El nombre del cursor especificado en **CursorName* no era válido porque superó la longitud máxima definida por el controlador o inicial "SQLCUR" o "SQL_CUR."|  
|3C000|Nombre de cursor duplicado|El nombre del cursor especificado en **CursorName* ya existe.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY009|Uso no válido del puntero null|(DM) el argumento *CursorName* era un puntero nulo.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónicas aún estaba ejecutando cuando el **SQLSetCursorName** se llamó la función.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el * StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el argumento *longituddenombre* era menor que 0, pero no es igual a SQL_NTS.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *StatementHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Nombres de cursor solo se usan en actualización posicionada y eliminar instrucciones (por ejemplo, **actualizar** *nombre de la tabla* ... **WHERE CURRENT OF** *nombre de cursor*). Para obtener más información, consulte [actualización coloca y eliminar instrucciones](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md). Si la aplicación no llama a **SQLSetCursorName** para definir un nombre de cursor, en la ejecución de una instrucción de consulta el controlador genera un nombre que comienza con las letras SQL_CUR y no superar los 18 caracteres de longitud.  
  
 Todos los nombres de cursor dentro de la conexión deben ser únicos. La longitud máxima de un nombre de cursor se define por el controlador. Para obtener una interoperabilidad máxima, se recomienda que las aplicaciones limitan los nombres de cursor a no más de 18 caracteres. En ODBC 3*.x*, si un nombre de cursor es un identificador entre comillas, se trata de una manera entre mayúsculas y minúsculas y puede contener caracteres que no permitiría la sintaxis de SQL o trataría especial, como espacios en blanco o las palabras clave reservadas. Si un nombre de cursor debe tratarse de una manera entre mayúsculas y minúsculas, se debe pasar como un identificador entre comillas.  
  
 Establecer un nombre de cursor que se establece explícitamente o implícitamente se mantiene hasta que se quite la instrucción con la que está asociado, con **SQLFreeHandle**. **SQLSetCursorName** puede llamarse para cambiar el nombre de un cursor en una instrucción mientras el cursor está en un estado asignado o preparado.  
  
## <a name="code-example"></a>Ejemplo de código  
 En el siguiente ejemplo, una aplicación utiliza **SQLSetCursorName** para establecer un nombre de cursor de una instrucción. A continuación, utiliza esa instrucción para recuperar los resultados de la tabla CUSTOMERS. Por último, realiza una actualización posicionada para cambiar el número de teléfono de John Smith. Tenga en cuenta que la aplicación utiliza identificadores de instrucciones diferente para el **seleccione** y **actualización** instrucciones.  
  
 Para obtener otro ejemplo de código, vea [SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```  
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
|Ejecutar una instrucción SQL|[SQLExecDirect, función](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecutar una instrucción SQL preparada|[SQLExecute, función](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Devolver un nombre de cursor|[Función SQLGetCursorName](../../../odbc/reference/syntax/sqlgetcursorname-function.md)|  
|Establecer opciones de desplazamiento de cursor|[SQLSetScrollOptions (función)](../../../odbc/reference/syntax/sqlsetscrolloptions-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)

