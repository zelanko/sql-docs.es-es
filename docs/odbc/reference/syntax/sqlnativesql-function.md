---
title: Función SQLNativeSql ? Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9666bc767affb3b6bb624c416614079193d4b921
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304726"
---
# <a name="sqlnativesql-function"></a>Función SQLNativeSql
**Conformidad**  
 Versión introducida: Cumplimiento de estándares ODBC 1.0: ODBC  
  
 **Resumen**  
 **SQLNativeSql** devuelve la cadena SQL modificada por el controlador. **SQLNativeSql** no ejecuta la instrucción SQL.  
  
## <a name="syntax"></a>Sintaxis  
  
```cpp  
  
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
 [Entrada] Cadena de texto SQL que se va a traducir.  
  
 *TextLength1*  
 [Entrada] Longitud en caracteres de **InStatementText* cadena de texto.  
  
 *OutStatementText*  
 [Salida] Puntero a un búfer en el que se va a devolver la cadena SQL traducida.  
  
 Si *OutStatementText* es NULL, *TextLength2Ptr* seguirá devolviendo el número total de caracteres (excluyendo el carácter de terminación nula para los datos de caracteres) disponibles para devolver en el búfer señalado por *OutStatementText*.  
  
 *BufferLength*  
 [Entrada] Número de caracteres en el \*búfer *OutStatementText.* Si el valor devuelto en * \*InStatementText* es una cadena Unicode (al llamar a **SQLNativeSqlW**), el argumento *BufferLength* debe ser un número par.  
  
 *TextLength2Ptr*  
 [Salida] Puntero a un búfer en el que se va a devolver el \*número total de caracteres (excluyendo la terminación nula) disponibles para devolver en *OutStatementText*. Si el número de caracteres disponibles para devolver es mayor o \*igual que *BufferLength*, la cadena SQL traducida en *OutStatementText* se trunca a *BufferLength* menos la longitud de un carácter de terminación null.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnóstico  
 Cuando **SQLNativeSql** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, se puede obtener un valor SQLSTATE asociado llamando a **SQLGetDiagRec** con un *HandleType* de SQL_HANDLE_DBC y un *control* de *ConnectionHandle*. En la tabla siguiente se enumeran los valores SQLSTATE devueltos normalmente por **SQLNativeSql** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATEs devueltas por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE se SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo específico del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|01004|Datos de cadena truncados a la derecha|El \*búfer *OutStatementText* no era lo suficientemente grande como para devolver toda la cadena SQL, por lo que la cadena SQL se truncó. La longitud de la cadena SQL no truncada se devuelve en **TextLength2Ptr*. (La función devuelve SQL_SUCCESS_WITH_INFO.)|  
|08003|Conexión no abierta|*ConnectionHandle* no estaba en un estado conectado.|  
|08S01|Fallo del enlace de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos al que estaba conectado el controlador antes de que la función completara el procesamiento.|  
|22007|Formato de fecha y hora no válido|**InStatementText* contenía una cláusula de escape con un valor de fecha, hora o marca de tiempo no válido.|  
|24000|Estado de cursor no válido|El cursor al que se hace referencia en la instrucción se colocó antes del inicio del conjunto de resultados o después del final del conjunto de resultados. Este error no puede ser devuelto por un controlador que tenga una implementación de cursor DBMS nativo.|  
|HY000|Error general|Se ha producido un error para el que no se ha definido sqlSTATE específico y para el que no se ha definido sqlSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*messageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o finalización de la función.|  
|HY009|Uso no válido de puntero nulo|(DM) **InStatementText* era un puntero nulo.|  
|HY010|Error de secuencia de funciones|(DM) se llamó a una función de ejecución asincrónica para *ConnectionHandle* y todavía se estaba ejecutando cuando se llamó a esta función.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque no se pudo tener acceso a los objetos de memoria subyacentes, posiblemente debido a condiciones de poca memoria.|  
|HY090|Cadena no válida o longitud de búfer|(DM) El argumento *TextLength1* era menor que 0, pero no igual a SQL_NTS.|  
|||(DM) el argumento *BufferLength* era menor que 0 y el argumento *OutStatementText* no era un puntero nulo.|  
|HY109|Posición del cursor no válida|La fila actual del cursor se ha eliminado o no se ha capturado. Este error no puede ser devuelto por un controlador que tenga una implementación de cursor DBMS nativo.|  
|HY117|La conexión se suspende debido al estado de transacción desconocido. Solo se permiten funciones de desconexión y de solo lectura.|(DM) Para obtener más información sobre el estado suspendido, vea [SqlEndTran (función).](../../../odbc/reference/syntax/sqlendtran-function.md)|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión expiró antes de que el origen de datos respondiera a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|El controlador no admite esta función|(DM) El controlador asociado a *ConnectionHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 A continuación se muestran ejemplos de lo que **SQLNativeSql** podría devolver para la siguiente cadena SQL de entrada que contiene la función escalar CONVERT. Supongamos que la columna empid es de tipo INTEGER en el origen de datos:  
  
```sql  
SELECT { fn CONVERT (empid, SQL_SMALLINT) } FROM employee  
```  
  
 Un controlador para Microsoft SQL Server podría devolver la siguiente cadena SQL traducida:  
  
```sql  
SELECT convert (smallint, empid) FROM employee  
```  
  
 Un controlador para ORACLE Server podría devolver la siguiente cadena SQL traducida:  
  
```sql  
SELECT to_number (empid) FROM employee  
```  
  
 Un controlador para Ingres podría devolver la siguiente cadena SQL traducida:  
  
```sql  
SELECT int2 (empid) FROM employee  
```  
  
 Para obtener más información, consulte [Ejecución directa](../../../odbc/reference/develop-app/direct-execution-odbc.md) y [ejecución preparada](../../../odbc/reference/develop-app/prepared-execution-odbc.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
 Ninguno.  
  
## <a name="see-also"></a>Consulte también  
 [Referencia de la API ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
