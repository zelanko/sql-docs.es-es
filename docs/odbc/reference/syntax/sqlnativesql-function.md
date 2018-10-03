---
title: Función SQLNativeSql | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLNativeSql
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLNativeSql
helpviewer_keywords:
- SQLNativeSql function [ODBC]
ms.assetid: b8efc247-27ab-4a00-92b6-1400785783fe
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d2e5596948a9e764ca0005d6cc41e62d65421866
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47692305"
---
# <a name="sqlnativesql-function"></a>Función SQLNativeSql
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: ODBC  
  
 **Resumen**  
 **SQLNativeSql** devuelve la cadena SQL como modificada por el controlador. **SQLNativeSql** no se ejecuta la instrucción SQL.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLNativeSql(  
     SQLHDBC        ConnectionHandle,  
     SQLCHAR *      InStatementText,  
     SQLINTEGER     TextLength1,  
     SQLCHAR *      OutStatementText,  
     SQLINTEGER     BufferLength,  
     SQLINTEGER *   TextLength2Ptr);  
```  
  
## <a name="arguments"></a>Argumentos  
 *ConnectionHandle*  
 [Entrada] Identificador de conexión.  
  
 *InStatementText*  
 [Entrada] Cadena de texto SQL que se deben traducir.  
  
 *TextLength1*  
 [Entrada] Longitud en caracteres de **InStatementText* cadena de texto.  
  
 *OutStatementText*  
 [Salida] Puntero a un búfer en el que se va a devolver la cadena traducida de SQL.  
  
 Si *OutStatementText* es NULL, *TextLength2Ptr* devolverá el número total de caracteres (excepto el carácter de terminación null para los datos de caracteres) disponibles para devolver en el búfer apunta a *OutStatementText*.  
  
 *BufferLength*  
 [Entrada] Número de caracteres de la \* *OutStatementText* búfer. Si el valor devuelto en  *\*InStatementText* es una cadena Unicode (al llamar a **SQLNativeSqlW**), el *BufferLength* argumento debe ser un número par.  
  
 *TextLength2Ptr*  
 [Salida] Puntero a un búfer en el que se va a devolver el número total de caracteres (excluyendo-finalización en null) disponibles para devolver en \* *OutStatementText*. Si el número de caracteres disponibles para devolver es mayor o igual a *BufferLength*, la traduce la cadena de SQL en \* *OutStatementText* se trunca a  *BufferLength* menos la longitud de un carácter de terminación null.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLNativeSql** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_DBC y un *controlar* de *ConnectionHandle*. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLNativeSql** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena derecha truncados|El búfer \* *OutStatementText* no era lo suficientemente grande como para devolver toda la cadena SQL, por lo que se truncó la cadena SQL. Se devuelve la longitud de la cadena SQL sin truncar en **TextLength2Ptr*. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|08003|Conexión no abierta|El *ConnectionHandle* no estaba en estado conectado.|  
|08S01|Error de vínculo de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos a la que se ha conectado el controlador antes del procesamiento de la función se ha completado.|  
|22007|Formato de datetime no válido|**InStatementText* contiene una cláusula de escape con un valor de fecha, hora o marca de tiempo no válido.|  
|24000|Estado de cursor no válido|El cursor hace referencia en la instrucción se coloca antes del inicio del conjunto de resultados o después del final del conjunto de resultados. Este error no puede devolver un controlador de una implementación nativa de cursor DBMS.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY009|Uso no válido del puntero nulo|(DM) **InStatementText* era un puntero nulo.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para la *ConnectionHandle* y aún se estaba ejecutando cuando se llamó a esta función.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el argumento *TextLength1* era menor que 0, pero no es igual a SQL_NTS.|  
|||(DM) el argumento *BufferLength* era menor que 0 y el argumento *OutStatementText* no era un puntero nulo.|  
|HY109|Posición del cursor no válido|La fila actual del cursor se había eliminada o no se ha tenido capturada. Este error no puede devolver un controlador de una implementación nativa de cursor DBMS.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *ConnectionHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 Los siguientes son ejemplos de lo que **SQLNativeSql** podría devolver la siguiente cadena de entrada SQL que contiene la función escalar CONVERT. Suponga que el empid columna es de tipo entero en el origen de datos:  
  
```  
SELECT { fn CONVERT (empid, SQL_SMALLINT) } FROM employee  
```  
  
 Un controlador de Microsoft SQL Server podría devolver la siguiente cadena traducida de SQL:  
  
```  
SELECT convert (smallint, empid) FROM employee  
```  
  
 Un controlador para el servidor ORACLE podría devolver la siguiente cadena traducida de SQL:  
  
```  
SELECT to_number (empid) FROM employee  
```  
  
 Un controlador para Ingres podría devolver la siguiente cadena traducida de SQL:  
  
```  
SELECT int2 (empid) FROM employee  
```  
  
 Para obtener más información, consulte [ejecución directa](../../../odbc/reference/develop-app/direct-execution-odbc.md) y [ejecución preparada](../../../odbc/reference/develop-app/prepared-execution-odbc.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
 Ninguno.  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
