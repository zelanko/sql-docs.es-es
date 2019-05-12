---
title: Función SQLNumParams | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLNumParams
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLNumParams
helpviewer_keywords:
- SQLNumParams function [ODBC]
ms.assetid: dbf2da44-253b-4094-bd6b-29bafc23c7a3
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 05e65eac94cffa0e31e3ec71179f18704a7e8b71
ms.sourcegitcommit: 7a3243c45830cb3f49a7fa71c2991a9454fd6f5a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/11/2019
ms.locfileid: "65536588"
---
# <a name="sqlnumparams-function"></a>Función SQLNumParams
**Conformidad**  
 Versión de introducción: Cumplimiento de estándares 1.0 de ODBC: ISO 92  
  
 **Resumen**  
 **SQLNumParams** devuelve el número de parámetros en una instrucción SQL.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
SQLRETURN SQLNumParams(  
     SQLHSTMT        StatementHandle,  
     SQLSMALLINT *   ParameterCountPtr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *ParameterCountPtr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número de parámetros en la instrucción.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLNumParams** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLNumParams** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08S01|Error de vínculo de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos a la que se ha conectado el controlador antes del procesamiento de la función se ha completado.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. El **SQLNumParams** se llamó a la función y, antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle* ; el **SQLNumParams** función, a continuación, se llamó de nuevo en el *StatementHandle*.<br /><br /> O bien, el **SQLNumParams** se llamó a la función y, antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle*  desde un subproceso diferente en una aplicación multiproceso.|  
|HY010|Error de secuencia de función|(DM) que se llamó la función antes de llamar a **SQLPrepare** o **SQLExecDirect** para el *StatementHandle*.<br /><br /> (DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Aún estaba ejecutando esta función asincrónica cuando el **SQLNumParams** se llamó a la función.<br /><br /> (DM) se llamó a una función que se ejecuta asincrónicamente (no ésta) para el *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|Sondeo se deshabilita en modo de notificación asincrónica|Cada vez que se usa el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 **SQLNumParams** se puede llamar solo después **SQLPrepare** se ha llamado.  
  
 Si la instrucción asociada *StatementHandle* no contiene parámetros, **SQLNumParams** establece **ParameterCountPtr* en 0.  
  
 El número de parámetros devueltos por **SQLNumParams** es el mismo valor que el campo SQL_DESC_COUNT de la IPD.  
  
 Para obtener más información, consulte [que describe parámetros](../../../odbc/reference/develop-app/describing-parameters.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con un parámetro|[Función SQLBindParameter](../../../odbc/reference/syntax/sqlbindparameter-function.md)|  
|Devolver información acerca de un parámetro en una instrucción|[Función SQLDescribeParam](../../../odbc/reference/syntax/sqldescribeparam-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
