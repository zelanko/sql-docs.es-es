---
title: "Función SQLGetCursorName | Documentos de Microsoft"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLGetCursorName
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLGetCursorName
helpviewer_keywords: SQLGetCursorName function [ODBC]
ms.assetid: e6e92199-7bb6-447c-8987-049a4c6ce05d
caps.latest.revision: "24"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 69a0da5196c5724284c2da75dc6c7deb3c3cedcd
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgetcursorname-function"></a>Función SQLGetCursorName
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: ISO 92  
  
 **Resumen**  
 **SQLGetCursorName** devuelve el nombre de cursor asociado con una instrucción especificada.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
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
  
 Si *CursorName* es NULL, *NameLengthPtr* devolverá el número total de caracteres (excepto el carácter de terminación null para los datos de carácter) disponible para devolver en el búfer señalado por *CursorName*.  
  
 *BufferLength*  
 [Entrada] Longitud de \* *CursorName*, en caracteres. Si el valor de  *\*CursorName* es una cadena Unicode (cuando se llama a **SQLGetCursorNameW**), el *BufferLength* el argumento debe ser un número par.  
  
 *NameLengthPtr*  
 [Salida] Puntero a la memoria en el que se va a devolver el número total de caracteres (excepto el carácter de terminación null) disponible para devolver en \* *CursorName*. Si el número de caracteres disponibles para devolver es mayor o igual que *BufferLength*, el nombre del cursor en \* *CursorName* se trunca a *BufferLength*menos la longitud de un carácter de terminación null.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLGetCursorName** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType*de SQL_HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLGetCursorName** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena, delimitado truncados|El búfer \* *CursorName* no era lo suficientemente grande como para devolver el nombre de cursor completo, por lo que el nombre del cursor se ha truncado. Se devuelve la longitud del nombre del cursor untruncated en **NameLengthPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónica aún estaba ejecutando cuando el **SQLGetCursorName** se llamó la función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* devolvió SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY015|Ningún nombre de cursor disponible|(DM) el controlador fue un ODBC 2*.x* controlador, se ha producido ningún cursor abierto en la instrucción y tenía ha establecido ningún nombre de cursor con **SQLSetCursorName**.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el valor especificado en el argumento *BufferLength* era menor que 0.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *StatementHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Nombres de cursor solo se usan en actualización posicionada y eliminar instrucciones (por ejemplo, **actualizar** *nombre de la tabla* ... **WHERE CURRENT OF** *nombre de cursor*). Para obtener más información, consulte [actualización coloca y eliminar instrucciones](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md). Si la aplicación no llama a **SQLSetCursorName** para definir un nombre de cursor, el controlador genera un nombre. Este nombre comienza con las letras SQL_CUR.  
  
> [!NOTE]  
>  En ODBC 2*.x*, cuando se ha producido ningún cursor abierto y ningún nombre hubiera establecido por una llamada a **SQLSetCursorName**, una llamada a **SQLGetCursorName** devuelve SQLSTATE HY015 (ningún nombre de cursor está disponible.) En ODBC 3*.x*, ésta ya no es true; independientemente de cuándo **SQLGetCursorName** es llama, el controlador devuelve el nombre del cursor.  
  
 **SQLGetCursorName** devuelve el nombre de un cursor o no se creó el nombre de forma explícita o implícita. Un nombre de cursor se genera implícitamente si **SQLSetCursorName** no se llama. **SQLSetCursorName** puede llamarse para cambiar el nombre de un cursor en una instrucción mientras el cursor está en un estado asignado o preparado.  
  
 Un nombre de cursor que se establece explícitamente o implícitamente permanece establecido hasta que el *StatementHandle* al que está asociado se quita, con **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_STMT.  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Ejecutar una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecutar una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Preparar una instrucción de ejecución|[Función SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|Establecer un nombre de cursor|[Función SQLSetCursorName](../../../odbc/reference/syntax/sqlsetcursorname-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
