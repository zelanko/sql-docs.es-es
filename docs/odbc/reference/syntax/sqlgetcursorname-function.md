---
title: Función SQLGetCursorName | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 33e2d1f4630228d4c59487c2a5f9de891e87ece5
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/11/2019
ms.locfileid: "65537377"
---
# <a name="sqlgetcursorname-function"></a>Función SQLGetCursorName
**Conformidad**  
 Versión de introducción: Cumplimiento de estándares 1.0 de ODBC: ISO 92  
  
 **Resumen**  
 **SQLGetCursorName** devuelve el nombre del cursor asociado con una instrucción especificada.  
  
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
  
 Si *CursorName* es NULL, *NameLengthPtr* devolverá el número total de caracteres (excepto el carácter de terminación null para los datos de caracteres) disponibles para devolver en el búfer señalado por *CursorName*.  
  
 *BufferLength*  
 [Entrada] Longitud de \* *CursorName*, en caracteres. Si el valor de  *\*CursorName* es una cadena Unicode (al llamar a **SQLGetCursorNameW**), el *BufferLength* argumento debe ser un número par.  
  
 *NameLengthPtr*  
 [Salida] Puntero a la memoria en el que se va a devolver el número total de caracteres (excepto el carácter de terminación null) disponibles para devolver en \* *CursorName*. Si el número de caracteres disponibles para devolver es mayor o igual a *BufferLength*, el nombre del cursor en \* *CursorName* se trunca a *BufferLength*menos la longitud de un carácter de terminación null.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLGetCursorName** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType*de SQL_HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLGetCursorName** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena derecha truncados|El búfer \* *CursorName* no era lo suficientemente grande como para devolver el nombre de cursor completo, por lo que el nombre del cursor se ha truncado. Se devuelve la longitud del nombre del cursor sin truncar en **NameLengthPtr*. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Aún estaba ejecutando esta función asincrónica cuando el **SQLGetCursorName** se llamó a la función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* y devuelven SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función que se ejecuta de forma asincrónica para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY015|Nombre de cursor no disponible|(DM) el controlador fue un 2 de ODBC *.x* controlador, se ha producido ningún cursor abierto en la instrucción y se haya establecido ningún nombre de cursor con **SQLSetCursorName**.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el valor especificado en el argumento *BufferLength* era menor que 0.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *StatementHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Los nombres de cursor solo se usan en actualización posicionada y eliminar instrucciones (por ejemplo, **actualizar** _nombre-tabla_ ... **WHERE CURRENT OF** _nombre de cursor_). Para obtener más información, consulte [coloca actualizar y eliminar instrucciones](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md). Si la aplicación no llama a **SQLSetCursorName** para definir un nombre de cursor, el controlador generará un nombre. Este nombre comienza con las letras SQL_CUR.  
  
> [!NOTE]
>  En ODBC 2 *.x*, cuando se ha producido ningún cursor abierto y se haya establecido mediante una llamada a ningún nombre **SQLSetCursorName**, una llamada a **SQLGetCursorName** devuelve SQLSTATE HY015 (ningún nombre de cursor disponible). En ODBC 3 *.x*, esto ya no es true; independientemente de cuándo **SQLGetCursorName** es llama, el controlador devuelve el nombre del cursor.  
  
 **SQLGetCursorName** devuelve el nombre de un cursor o no el nombre se creó explícitamente o implícitamente. Un nombre de cursor se genera de manera implícita si **SQLSetCursorName** no se llama. **SQLSetCursorName** se puede llamar para cambiar el nombre de un cursor en una instrucción siempre y cuando el cursor está en un estado asignado o preparado.  
  
 Un nombre de cursor que se establece explícitamente o implícitamente permanece establecido hasta que el *StatementHandle* con el que está asociado se quita, mediante **SQLFreeHandle** con un *HandleType* de SQL_HANDLE_STMT.  
  
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
