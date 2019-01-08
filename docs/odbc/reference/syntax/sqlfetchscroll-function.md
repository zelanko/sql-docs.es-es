---
title: Función SQLFetchScroll | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLFetchScroll
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLFetchScroll
helpviewer_keywords:
- SQLFetchScroll function [ODBC]
ms.assetid: c0243667-428c-4dda-ae91-3c307616a1ac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f7b7e5141a465249c818b50466b34a8155adc1d6
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 11/28/2018
ms.locfileid: "52540814"
---
# <a name="sqlfetchscroll-function"></a>Función SQLFetchScroll
**Conformidad**  
 Versión de introducción: Compatibilidad de ODBC 3.0 estándares: 92 ISO  
  
 **Resumen**  
 **SQLFetchScroll** recupera el conjunto especificado filas de datos del conjunto de resultados y devuelve datos para todas las columnas enlazadas. Los conjuntos de filas pueden especificarse en una posición absoluta o relativa, o por el marcador.  
  
 Cuando se trabaja con un controlador ODBC 2.x, el Administrador de controladores se asigna esta función para **SQLExtendedFetch**. Para obtener más información, consulte [asignación de funciones de reemplazo para compatibilidad con versiones anteriores de aplicaciones](../../../odbc/reference/develop-app/mapping-replacement-functions-for-backward-compatibility-of-applications.md).  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLFetchScroll(  
      SQLHSTMT      StatementHandle,  
      SQLSMALLINT   FetchOrientation,  
      SQLLEN        FetchOffset);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *FetchOrientation*  
 [Entrada]  
  
 Tipo de captura:  
  
 SQL_FETCH_NEXT  
  
 SQL_FETCH_PRIOR  
  
 SQL_FETCH_FIRST  
  
 SQL_FETCH_LAST  
  
 SQL_FETCH_ABSOLUTE  
  
 SQL_FETCH_RELATIVE  
  
 SQL_FETCH_BOOKMARK  
  
 Para obtener más información, vea "Colocar el Cursor" en la sección "Comentarios".  
  
 *FetchOffset*  
 [Entrada]  
  
 Número de la fila que se va a capturar. La interpretación de este argumento depende del valor de la *FetchOrientation* argumento. Para obtener más información, vea "Colocar el Cursor" en la sección "Comentarios".  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLFetchScroll** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un HandleType de SQL_HANDLE_STMT y un identificador de StatementHandle. En la tabla siguiente se enumera los valores SQLSTATE devueltos normalmente por **SQLFetchScroll** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario. Si se produce un error en una sola columna, **SQLGetDiagField** se puede llamar con un DiagIdentifier de SQL_DIAG_COLUMN_NUMBER para determinar la columna que se produjo el error; y **SQLGetDiagField** se puede llamar a con un DiagIdentifier de SQL_DIAG_ROW_NUMBER para determinar la fila que contiene esa columna.  
  
 Para todas esas SQLSTATE que puede devolver SQL_SUCCESS_WITH_INFO o SQL_ERROR (excepto 01xxx SQLSTATEs), se devuelve SQL_SUCCESS_WITH_INFO, si se produce un error en uno o más, pero no todas las filas de una operación de varias filas, y se devuelve SQL_ERROR si se produce un error en un fila única operación.  
  
|SQLSTATE|Error|Descripción|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Específico del controlador de mensaje informativo. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01004|Datos de cadena derecha truncados|Cadena o datos binarios devueltos para una columna produjeron el truncamiento de carácter no en blanco o datos binarios que no son NULL. Si fuese un valor de cadena, era truncado a la derecha.|  
|01S01|Error en la fila|Se produjo un error al capturar una o varias filas.<br /><br /> (Si este SQLSTATE se devuelve cuando una aplicación ODBC 3 *.x* aplicación funciona con un ODBC 2 *.x* controlador, se puede hacer caso omiso.)|  
|01S06|Se intentó buscar antes de que el conjunto de resultados devuelve el primer conjunto de filas|El conjunto de filas solicitado superpuesto el inicio del conjunto cuando FetchOrientation era SQL_FETCH_PRIOR, era la actual posición más allá de la primera fila y el número de la fila actual es menor o igual que el tamaño del conjunto de filas de resultados.<br /><br /> El conjunto de filas solicitado superpuesto el inicio del conjunto cuando FetchOrientation era SQL_FETCH_PRIOR, era la actual posición más allá del final del conjunto de resultados y el tamaño del conjunto de filas es mayor que el tamaño del conjunto de los resultados de resultados.<br /><br /> El conjunto de filas solicitado superpuesto el inicio del conjunto cuando FetchOrientation era SQL_FETCH_RELATIVE, FetchOffset era negativo y el valor absoluto de FetchOffset era menor o igual que el tamaño del conjunto de filas de resultados.<br /><br /> El conjunto de filas solicitado superpuesta el inicio del conjunto de resultados cuando FetchOrientation era SQL_FETCH_ABSOLUTE, FetchOffset era negativo y el valor absoluto de FetchOffset era mayor que el conjunto de resultados tamaño menor o igual que el tamaño del conjunto de filas.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|01S07|Truncamiento fraccionario|Se truncaron los datos devueltos para una columna. Para los tipos de datos numéricos, se ha truncado la parte fraccionaria del número. De hora, marca de tiempo y los tipos de datos de intervalo que contiene un componente de tiempo, se trunca la parte fraccionaria del tiempo.<br /><br /> (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07006|Infracción del atributo de tipo de datos restringido|No se pudo convertir el valor de datos de una columna del conjunto de resultados para el tipo de datos especificado por *TargetType* en **SQLBindCol**.<br /><br /> La columna 0 se enlazó con un tipo de datos de SQL_C_BOOKMARK y se ha establecido el atributo de instrucción SQL_ATTR_USE_BOOKMARKS a SQL_UB_VARIABLE.<br /><br /> La columna 0 se enlazó con un tipo de datos de SQL_C_VARBOOKMARK y el atributo de instrucción SQL_ATTR_USE_BOOKMARKS no se estableció en SQL_UB_VARIABLE.|  
|07009|Índice de descriptor no válido|El controlador fue un 2 de ODBC *.x* controlador que no es compatible con **SQLExtendedFetch**, y un número de columna especificado en el enlace para una columna era 0.<br /><br /> Se enlazó a la columna 0 y se ha establecido el atributo de instrucción SQL_ATTR_USE_BOOKMARKS a SQL_UB_OFF.|  
|08S01|Error de vínculo de comunicación|Error en el vínculo de comunicación entre el controlador y el origen de datos a la que se ha conectado el controlador antes del procesamiento de la función se ha completado.|  
|22001|Datos de cadena derecha truncados|Se ha truncado un marcador de longitud variable devuelto para una columna.|  
|22002|Variable de indicador necesaria pero no proporcionado|Datos nulos se capturan en una columna cuya propiedad *StrLen_or_IndPtr* establecido por **SQLBindCol** (o SQL_DESC_INDICATOR_PTR establecido por **SQLSetDescField** o  **SQLSetDescRec**) era un puntero nulo.|  
|22003|Valor numérico fuera del intervalo|Devolver el valor numérico (como numérico o cadena) para uno o más columnas enlazadas, habría causado la parte entera (en contraposición a fraccionarios) del número se trunque.<br /><br /> Para obtener más información, consulte [convertir datos de SQL a tipos de datos C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md) en [apéndice D: Tipos de datos](../../../odbc/reference/appendixes/appendix-d-data-types.md).|  
|22007|Formato de datetime no válido|Una columna de caracteres del conjunto de resultados se enlazó con una fecha, hora o estructura de marca de tiempo C y un valor en la columna era, respectivamente, una fecha no válida, la hora o marca de tiempo.|  
|22012|División por cero|Devolvió un valor de una expresión aritmética, lo que resultó en la división por cero.|  
|22015|Desbordamiento de campo de intervalo|Asignación de un valor numérico exacto o el intervalo de tipo SQL a un tipo de intervalo C causó una pérdida de dígitos significativos en el campo inicial.<br /><br /> Al capturar datos para un tipo de intervalo de C, no hubo ninguna representación del valor del tipo SQL en el tipo de intervalo C.|  
|22018|Valor de carácter no válido para especificación cast|Una columna de caracteres del conjunto de resultados estaba enlazada a un búfer de caracteres de C y la columna contiene un carácter para el que se ha producido ninguna representación en el juego de caracteres del búfer.<br /><br /> El tipo C era un numérico exacto o aproximado, una fecha y hora o un tipo de datos del intervalo; el tipo SQL de la columna era un tipo de datos de caracteres; y el valor de la columna no es un literal válido de tipo C enlazado.|  
|24000|Estado de cursor no válido|El *StatementHandle* estaba en un estado ejecutado pero se ha asociado ningún conjunto de resultados la *StatementHandle*.|  
|40001|Error de serialización.|Se terminó la transacción en el que se ejecutó la operación de captura para evitar el interbloqueo.|  
|40003|Finalización de instrucción desconocida|Error en la conexión asociada durante la ejecución de esta función y no se puede determinar el estado de la transacción.|  
|HY000|Error general|Se produjo un error para que se ha producido ningún SQLSTATE específico y para los que se ha definido ningún SQLSTATE específicos de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el  *\*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar la memoria necesaria para admitir la ejecución o la finalización de la función.|  
|HY008|Operación cancelada|Procesamiento asincrónico se habilitó para la *StatementHandle*. Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle*. A continuación, la función se llamó de nuevo en el *StatementHandle*.<br /><br /> Se llamó a la función, y antes que completó la ejecución, **SQLCancel** o **SQLCancelHandle** se ha llamado en el *StatementHandle* desde un subproceso diferente en un aplicaciones multiproceso.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función que se ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Aún estaba ejecutando esta función asincrónica cuando el **SQLFetchScroll** se llamó a la función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* y devuelven SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) especificado *StatementHandle* no estaba en un estado ejecutado. Se llamó a la función sin llamar primero a **SQLExecDirect**, **SQLExecute** o una función de catálogo.<br /><br /> (DM) se llamó a una función que se ejecuta asincrónicamente (no ésta) para el *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el  *StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron datos para todas las columnas o parámetros de datos en ejecución.<br /><br /> (DM) **SQLFetch** se llamó para el *StatementHandle* después **SQLExtendedFetch** llamó y antes de **SQLFreeStmt** con el SQL_ Se llamó a la opción Cerrar.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos de memoria subyacente no se podrían tener acceso, posiblemente debido a memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|El atributo de instrucción SQL_ATTR_USE_BOOKMARK se estableció en SQL_UB_VARIABLE y la columna 0 estaba enlazada a un búfer cuya longitud no es igual a la longitud máxima para el marcador para este conjunto de resultados. (Esta longitud está disponible en el campo SQL_DESC_OCTET_LENGTH de IRD y se puede obtener mediante una llamada a **SQLDescribeCol**, **SQLColAttribute**, o **SQLGetDescField**.)|  
|HY106|Tipo de captura fuera del intervalo|DM) el valor especificado para el argumento FetchOrientation no era válido.<br /><br /> (DM) el argumento FetchOrientation era SQL_FETCH_BOOKMARK y se ha establecido el atributo de instrucción SQL_ATTR_USE_BOOKMARKS a SQL_UB_OFF.<br /><br /> El valor del atributo de instrucción SQL_ATTR_CURSOR_TYPE era SQL_CURSOR_FORWARD_ONLY y el valor del argumento que fetchorientation no era SQL_FETCH_NEXT.<br /><br /> El valor del atributo de instrucción SQL_ATTR_CURSOR_SCROLLABLE era SQL_NONSCROLLABLE y el valor del argumento que fetchorientation no era SQL_FETCH_NEXT.|  
|HY107|Valor de fila fuera del intervalo|El valor especificado con el atributo de instrucción SQL_ATTR_CURSOR_TYPE era SQL_CURSOR_KEYSET_DRIVEN, pero el valor especificado con el atributo de instrucción SQL_ATTR_KEYSET_SIZE era mayor que 0 y menor que el valor especificado con el SQL_ATTR_ROW_ARRAY_ Atributo de instrucción de tamaño.|  
|HY111|Valor de marcador no válido|El argumento FetchOrientation era SQL_FETCH_BOOKMARK, y el marcador señalado por el valor del atributo de instrucción SQL_ATTR_FETCH_BOOKMARK_PTR no era válido o era un puntero nulo.|  
|HY117|Conexión está suspendida debido al estado de transacción desconocido. Solo se desconecte y se permiten funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|El controlador u origen de datos no admite la conversión especificada por la combinación de la *TargetType* en **SQLBindCol** y el tipo de datos SQL de la columna correspondiente.|  
|HYT00|Se agotó el tiempo de espera|Ha expirado el período de tiempo de espera de consulta antes del origen de datos devuelve el conjunto de resultados solicitada. El período de tiempo de espera se establece a través de SQLSetStmtAttr, SQL_ATTR_QUERY_TIMEOUT.|  
|HYT01|Tiempo de espera de conexión agotado|Ha expirado el período de tiempo de espera de conexión antes de que el origen de datos que respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado con el *StatementHandle* no admite la función.|  
|IM017|Sondeo se deshabilita en modo de notificación asincrónica|Cada vez que se usa el modelo de notificación, se deshabilita el sondeo.|  
|IM018|**SQLCompleteAsync** no se ha llamado para completar la operación asincrónica anterior en este identificador.|Si la llamada de función anterior en el controlador devuelve SQL_STILL_EXECUTING y si está habilitado el modo de notificación, **SQLCompleteAsync** debe llamarse en el identificador para realizar el procesamiento posterior y completar la operación.|  
  
## <a name="comments"></a>Comentarios  
 **SQLFetchScroll** devuelve un conjunto de filas especificado del conjunto de resultados. Por posición absoluta o relativa o por marcador, se pueden especificar los conjuntos de filas. **SQLFetchScroll** se puede llamar solo mientras existe un conjunto de resultados: es decir, después de una llamada que crea un conjunto de resultados y antes del cursor sobre que el conjunto de resultados está cerrado. Si todas las columnas están enlazadas, devuelve los datos en esas columnas. Si la aplicación ha especificado un puntero a una matriz de Estados de fila o un búfer en el que se va a devolver el número de filas recuperadas, **SQLFetchScroll** devuelve esta información también. Las llamadas a **SQLFetchScroll** se pueden combinar con llamadas a **SQLFetch** pero no se pueden mezclar con las llamadas a **SQLExtendedFetch**.  
  
 Para obtener más información, consulte [utilizar cursores de bloque](../../../odbc/reference/develop-app/using-block-cursors.md) y [utilizando los cursores desplazables](../../../odbc/reference/develop-app/using-scrollable-cursors.md).  
  
## <a name="positioning-the-cursor"></a>Sitúe el Cursor  
 Cuando se crea el conjunto de resultados, el cursor se coloca antes del inicio del conjunto de resultados. **SQLFetchScroll** coloca el cursor de bloque según los valores de la *FetchOrientation* y *FetchOffset* argumentos tal como se muestra en la tabla siguiente. Las reglas exactas para determinar el inicio del nuevo conjunto de filas se muestran en la sección siguiente.  
  
|FetchOrientation|Significado|  
|----------------------|-------------|  
|SQL_FETCH_NEXT|Devuelve el siguiente conjunto de filas. Esto equivale a llamar a **SQLFetch**.<br /><br /> **SQLFetchScroll** omite el valor de *FetchOffset*.|  
|SQL_FETCH_PRIOR|Devuelve el conjunto de filas anterior.<br /><br /> **SQLFetchScroll** omite el valor de *FetchOffset*.|  
|SQL_FETCH_RELATIVE|Devuelve el conjunto de filas *FetchOffset* desde el principio del conjunto de filas actual.|  
|SQL_FETCH_ABSOLUTE|Devuelve el conjunto de filas empezando por fila *FetchOffset*.|  
|SQL_FETCH_FIRST|Devolver el primer conjunto de filas del conjunto de resultados.<br /><br /> **SQLFetchScroll** omite el valor de *FetchOffset*.|  
|SQL_FETCH_LAST|Devolver el último conjunto de filas completo en el conjunto de resultados.<br /><br /> **SQLFetchScroll** omite el valor de *FetchOffset*.|  
|SQL_FETCH_BOOKMARK|Devolver el conjunto de filas FetchOffset filas desde el marcador especificado por el atributo de instrucción SQL_ATTR_FETCH_BOOKMARK_PTR.|  
  
 Los controladores no son necesarios para admitir todas las orientaciones de captura; una aplicación llama a **SQLGetInfo** con un tipo de información de SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 o SQL_STATIC_CURSOR_ATTRIBUTES1 (según el tipo del cursor) para determinar qué fetch orientaciones son compatibles con el controlador. La aplicación debe mirar las máscaras de bits SQL_CA1_NEXT, SQL_CA1_RELATIVE, SQL_CA1_ABSOLUTE y WQL_CA1_BOOKMARK en estos tipos de información. Además, si el cursor es de solo avance y FetchOrientation no es SQL_FETCH_NEXT, **SQLFetchScroll** devuelve SQLSTATE HY106 (tipo fuera del intervalo de captura).  
  
 El atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE especifica el número de filas del conjunto de filas. Si el conjunto de filas que se va a buscar por **SQLFetchScroll** se superpone al final del conjunto de resultados, **SQLFetchScroll** devuelve un conjunto de filas parcial. Es decir, si S + R - 1 es mayor que L, donde S es la fila inicial del conjunto de filas que se capturan, R es el tamaño del conjunto de filas y L es la última fila del conjunto de resultados, a continuación, solo el primer L - S + 1 filas del conjunto de filas son válidas. Las filas restantes están vacías y tienen un estado de SQL_ROW_NOROW.  
  
 Después de **SQLFetchScroll** que devuelve la fila actual es la primera fila del conjunto de filas.  
  
## <a name="cursor-positioning-rules"></a>Reglas para colocar un cursor  
 Las secciones siguientes describen las reglas exactas para cada valor de FetchOrientation. Estas reglas usan la notación siguiente.  
  
|Notación|Significado|  
|--------------|-------------|  
|*Antes de comenzar*|El cursor de bloque se coloca antes del inicio del conjunto de resultados. Si es la primera fila del nuevo conjunto de filas antes del inicio del conjunto de resultados, **SQLFetchScroll** devuelve SQL_NO_DATA.|  
|*Después de finales*|Después de establece el final del resultado, se coloca el cursor de bloque. Si es la primera fila del conjunto de filas nuevo después del final del conjunto de resultados, **SQLFetchScroll** devuelve SQL_NO_DATA.|  
|*CurrRowsetStart*|El número de la primera fila del conjunto de filas actual.|  
|*LastResultRow*|El número de la última fila del conjunto de resultados.|  
|*RowsetSize*|El tamaño del conjunto de filas.|  
|*FetchOffset*|El valor de la *FetchOffset* argumento.|  
|*BookmarkRow*|La fila correspondiente al marcador especificado por el atributo de instrucción SQL_ATTR_FETCH_BOOKMARK_PTR.|  
  
## <a name="sqlfetchnext"></a>SQL_FETCH_NEXT  
 Las reglas siguientes se aplican.  
  
|Condición|Primera fila del conjunto de filas nuevas|  
|---------------|-----------------------------|  
|*Antes de comenzar*|1|  
|*CurrRowsetStart + RowsetSize*[1]  *\<= LastResultRow*|*CurrRowsetStart + RowsetSize*[1]|  
|*CurrRowsetStart + RowsetSize*[1]*> LastResultRow*|*Después de finales*|  
|*Después de finales*|*Después de finales*|  
  
 [1] Si ha cambiado el tamaño del conjunto de filas desde la llamada anterior a capturar filas, esto es el tamaño del conjunto de filas que se usó con la llamada anterior.  
  
## <a name="sqlfetchprior"></a>SQL_FETCH_PRIOR  
 Las reglas siguientes se aplican.  
  
|Condición|Primera fila del conjunto de filas nuevas|  
|---------------|-----------------------------|  
|*Antes de comenzar*|*Antes de comenzar*|  
|*CurrRowsetStart = 1*|*Antes de comenzar*|  
|*1 < CurrRowsetStart < = RowsetSize* <sup>[2].</sup>|*1* <sup>[1]</sup>|  
|*CurrRowsetStart > RowsetSize* <sup>[2]</sup>|*CurrRowsetStart - RowsetSize* <sup>[2]</sup>|  
|*Después de la finalización y LastResultRow < RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*Después de finales LastResultRow y > = RowsetSize* <sup>[2]</sup>|*LastResultRow - RowsetSize + 1* <sup>[2].</sup>|  
  
 [1] **SQLFetchScroll** devuelve SQLSTATE 01S06 (intento de recuperación antes de que el conjunto de resultados devuelve el primer conjunto de filas) y SQL_SUCCESS_WITH_INFO.  
  
 [2] Si ha cambiado el tamaño del conjunto de filas desde la llamada anterior a capturar filas, se trata el nuevo tamaño del conjunto de filas.  
  
## <a name="sqlfetchrelative"></a>SQL_FETCH_RELATIVE  
 Las reglas siguientes se aplican.  
  
|Condición|Primera fila del conjunto de filas nuevas|  
|---------------|-----------------------------|  
|*(Antes de iniciar y FetchOffset > 0) O (después de la finalización y FetchOffset < 0)*|*--* <sup>[1]</sup>|  
|*BeforeStart y FetchOffset < = 0*|*Antes de comenzar*|  
|*CurrRowsetStart = 1 FetchOffset AND < 0*|*Antes de comenzar*|  
|*CurrRowsetStart > 1 AND CurrRowsetStart + FetchOffset < 1 AND &#124; FetchOffset &#124; > RowsetSize* <sup>[3]</sup>|*Antes de comenzar*|  
|*CurrRowsetStart > 1 AND CurrRowsetStart + FetchOffset < 1 AND &#124; FetchOffset &#124; < = RowsetSize* <sup>[3]</sup>|*1* <sup>[2]</sup>|  
|*1 < = CurrRowsetStart + FetchOffset \<= LastResultRow*|*CurrRowsetStart + FetchOffset*|  
|*CurrRowsetStart + FetchOffset > LastResultRow*|*Después de finales*|  
|*Después de finales FetchOffset y > = 0*|*Después de finales*|  
  
 [1] ***SQLFetchScroll*** devuelve el mismo conjunto de filas como si se llama con FetchOrientation establecido en SQL_FETCH_ABSOLUTE. Para obtener más información, consulte la sección "SQL_FETCH_ABSOLUTE".  
  
 [2] **SQLFetchScroll** devuelve SQLSTATE 01S06 (intento de recuperación antes de que el conjunto de resultados devuelve el primer conjunto de filas) y SQL_SUCCESS_WITH_INFO.  
  
 [3] Si ha cambiado el tamaño del conjunto de filas desde la llamada anterior a capturar filas, se trata el nuevo tamaño del conjunto de filas.  
  
## <a name="sqlfetchabsolute"></a>SQL_FETCH_ABSOLUTE  
 Las reglas siguientes se aplican.  
  
|Condición|Primera fila del conjunto de filas nuevas|  
|---------------|-----------------------------|  
|*FetchOffset < 0 AND &#124; FetchOffset &#124; < = LastResultRow*|*LastResultRow + FetchOffset + 1*|  
|*FetchOffset < 0 AND &#124; FetchOffset &#124; > LastResultRow AND &#124; FetchOffset &#124; > RowsetSize* <sup>[2]</sup>|*Antes de comenzar*|  
|*FetchOffset < 0 AND &#124; FetchOffset &#124; > LastResultRow AND &#124; FetchOffset &#124; < = RowsetSize* <sup>[2]</sup>|*1* <sup>[1]</sup>|  
|*FetchOffset = 0*|*Antes de comenzar*|  
|*1 < = FetchOffset \<= LastResultRow*|*FetchOffset*|  
|*FetchOffset > LastResultRow*|*Después de finales*|  
  
 [1] **SQLFetchScroll** devuelve SQLSTATE 01S06 (intento de recuperación antes de que el conjunto de resultados devuelve el primer conjunto de filas) y SQL_SUCCESS_WITH_INFO.  
  
 [2] Si ha cambiado el tamaño del conjunto de filas desde la llamada anterior a capturar filas, se trata el nuevo tamaño del conjunto de filas.  
  
 Una captura absoluta que se realizan en un cursor dinámico no puede proporcionar el resultado requerido porque las posiciones de fila en un cursor dinámico están indeterminadas. Esta operación equivale a una captura primero, seguida por una captura relativa; no es una operación atómica, como es una captura absoluta en un cursor estático.  
  
## <a name="sqlfetchfirst"></a>SQL_FETCH_FIRST  
 Las reglas siguientes se aplican.  
  
|Condición|Primera fila del conjunto de filas nuevas|  
|---------------|-----------------------------|  
|*Cualquier*|*1*|  
  
## <a name="sqlfetchlast"></a>SQL_FETCH_LAST  
 Las reglas siguientes se aplican.  
  
|Condición|Primera fila del conjunto de filas nuevas|  
|---------------|-----------------------------|  
|*RowsetSize* <sup>[1]</sup> < = LastResultRow|*LastResultRow - RowsetSize + 1* <sup>[1]</sup>|  
|*RowsetSize* <sup>[1]</sup> > LastResultRow|*1*|  
  
 [1] Si ha cambiado el tamaño del conjunto de filas desde la llamada anterior a capturar filas, se trata el nuevo tamaño del conjunto de filas.  
  
## <a name="sqlfetchbookmark"></a>SQL_FETCH_BOOKMARK  
 Las reglas siguientes se aplican.  
  
|Condición|Primera fila del conjunto de filas nuevas|  
|---------------|-----------------------------|  
|*BookmarkRow + FetchOffset < 1*|*Antes de comenzar*|  
|*1 < = BookmarkRow + FetchOffset \<= LastResultRow*|*BookmarkRow + FetchOffset*|  
|*BookmarkRow + FetchOffset > LastResultRow*|*Después de finales*|  
  
 Para obtener información acerca de los marcadores, vea [marcadores (ODBC)](../../../odbc/reference/develop-app/bookmarks-odbc.md).  
  
## <a name="effect-of-deleted-added-and-error-rows-on-cursor-movement"></a>Efecto de agregado, eliminado y las filas de Error en el desplazamiento del Cursor  
 Los cursores estáticos y controlados por detectan a veces filas agregadas al resultado de establecer y quitar las filas eliminadas del conjunto de resultados. Mediante una llamada a **SQLGetInfo** con el SQL_STATIC_CURSOR_ATTRIBUTES2 y SQL_KEYSET_CURSOR_ATTRIBUTES2 opciones y examinando los SQL_CA2_SENSITIVITY_ADDITIONS, SQL_CA2_SENSITIVITY_DELETIONS y SQL_CA2_SENSITIVITY_ Las máscaras de bits de las actualizaciones, una aplicación determina si los cursores implementados un controlador determinado hacer esto. Para los controladores que pueden detectar las filas eliminadas y quitarlos, los siguientes párrafos describen los efectos de este comportamiento. Para los controladores que pueden detectar las filas eliminadas, pero no pueden eliminarlos, las eliminaciones no tienen ningún efecto en los movimientos de cursor y no se aplican los siguientes párrafos.  
  
 Si el cursor detecta filas agregadas al conjunto de resultados o quita las filas eliminadas del conjunto de resultados, parece como si detecta estos cambios solo cuando captura los datos. Esto incluye el caso cuando **SQLFetchScroll** se llama con FetchOrientation establecido en SQL_FETCH_RELATIVE y FetchOffset se establece en 0 para volver a obtener el mismo conjunto de filas, pero no incluye el caso cuando se llama a SQLSetPos con a fOption establecido SQL_ ACTUALIZACIÓN. En el último caso, se actualizan los datos en los búferes de conjunto de filas, pero no se quitan las filas no volver a capturar y eliminadas del conjunto de resultados. Por lo tanto, cuando se elimina de una fila o se inserta en el conjunto de filas actual, el cursor no modifica los búferes de conjunto de filas. En su lugar, detecta el cambio cuando captura cualquier conjunto de filas que anteriormente incluía la fila eliminada o ahora incluye la fila insertada.  
  
 Por ejemplo:  
  
```  
// Fetch the next rowset.  
SQLFetchScroll(hstmt, SQL_FETCH_NEXT, 0);  
// Delete third row of the rowset. Does not modify the rowset buffers.  
SQLSetPos(hstmt, 3, SQL_DELETE, SQL_LOCK_NO_CHANGE);  
// The third row has a status of SQL_ROW_DELETED after this call.  
SQLSetPos(hstmt, 3, SQL_REFRESH, SQL_LOCK_NO_CHANGE);  
// Refetch the same rowset. The third row is removed, replaced by what  
// was previously the fourth row.  
SQLFetchScroll(hstmt, SQL_FETCH_RELATIVE, 0);  
```  
  
 Cuando **SQLFetchScroll** devuelve un nuevo conjunto de filas que tiene una posición en relación con el conjunto de filas actual: es decir, FetchOrientation es SQL_FETCH_NEXT, SQL_FETCH_PRIOR o SQL_FETCH_RELATIVE: no incluye los cambios realizados en el conjunto de filas actual al calcular la posición inicial del nuevo conjunto de filas. Sin embargo, incluyen cambios fuera del conjunto de filas actual si es capaz de detectar en ellos. Además, cuando **SQLFetchScroll** devuelve un nuevo conjunto de filas que tiene una posición independiente del conjunto de filas actual: es decir, FetchOrientation SQL_FETCH_FIRST, SQL_FETCH_LAST, SQL_FETCH_ABSOLUTE o SQL_FETCH_BOOKMARK -, incluye todos los cambios que es capaz de detectar, aunque estén en el conjunto de filas actual.  
  
 Al determinar si las filas recién agregadas son dentro o fuera del conjunto de filas actual, se considera un conjunto de filas parcial al final de la última fila válida; es decir, la última fila para el que el estado de fila no es SQL_ROW_NOROW. Por ejemplo, suponga que el cursor es capaz de detectar filas recién agregadas, el conjunto de filas actual es un conjunto de filas parcial, la aplicación agrega nuevas filas y el cursor agrega estas filas al final del conjunto de resultados. Si la aplicación llama a **SQLFetchScroll** con FetchOrientation establecido en SQL_FETCH_NEXT, **SQLFetchScroll** devuelve el conjunto de filas a partir de la primera fila recién agregada.  
  
 Por ejemplo, suponga que el conjunto de filas actual consta de filas 21 y 30, el tamaño del conjunto de filas es 10, el cursor quita las filas eliminadas del conjunto de resultados y cursor detecta filas agregadas al conjunto de resultados. La siguiente tabla muestra las filas **SQLFetchScroll** devuelve en diversas situaciones.  
  
|Cambiar|Tipo de captura|FetchOffset|Nuevo conjunto de filas [1]|  
|------------|----------------|-----------------|---------------------|  
|Eliminar fila 21|NEXT|0|31 a 40|  
|Eliminar fila 31|NEXT|0|32 a 41|  
|Insertar una fila entre las filas 21 y 22|NEXT|0|31 a 40|  
|Insertar una fila entre filas 30 y 31|NEXT|0|Fila insertada, 31 a 39|  
|Eliminar fila 21|PRIOR|0|11 a 20|  
|Eliminar fila 20|PRIOR|0|10 a 19|  
|Insertar una fila entre las filas 21 y 22|PRIOR|0|11 a 20|  
|Insertar fila entre las filas de 20 y 21|PRIOR|0|fila insertada de 12 a 20|  
|Eliminar fila 21|RELATIVE|0|22 a 31<sup>[2]</sup>|  
|Eliminar fila 21|RELATIVE|1|22 a 31|  
|Insertar una fila entre las filas 21 y 22|RELATIVE|0|fila insertada 21, 22 a 29|  
|Insertar una fila entre las filas 21 y 22|RELATIVE|1|22 a 31|  
|Eliminar fila 21|ABSOLUTE|21|22 a 31<sup>[2]</sup>|  
|Eliminar fila 22|ABSOLUTE|21|21, 23 y 31|  
|Insertar una fila entre las filas 21 y 22|ABSOLUTE|22|Fila insertada, 22 a 29|  
  
 [1] esta columna utiliza los números de fila antes de que se insertaron o se eliminó ninguna fila.  
  
 [2] en este caso, el cursor intenta devolver las filas a partir de la fila 21. Porque se ha eliminado la fila 21, la primera fila devuelve es 22.  
  
 Las filas de error (es decir, las filas con un estado de SQL_ROW_ERROR) no afectan al movimiento de cursor. Por ejemplo, si el conjunto de filas actual comienza con la fila 11 y el estado de fila 11 es SQL_ROW_ERROR, una llamada a **SQLFetchScroll** con FetchOrientation establecido en SQL_FETCH_RELATIVE y FetchOffset establecido en 5 devuelve el conjunto de filas a partir de la fila 16, al igual que haría si el estado de fila 11 era SQL_SUCCESS.  
  
## <a name="returning-data-in-bound-columns"></a>Devolver datos en las columnas enlazadas  
 **SQLFetchScroll** devuelve datos en las columnas enlazadas de la misma manera que **SQLFetch**. Para obtener más información, vea "devolución de datos en columnas"enlazadas en [función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
 Si no hay columnas están enlazadas, **SQLFetchScroll** no devuelve datos, pero mueve el cursor de bloque a la posición especificada. Si se pueden recuperar datos de las columnas sin enlazar de un cursor de bloque con **SQLGetData** depende del controlador. Esta funcionalidad se admite si una llamada a **SQLGetInfo** devuelve el SQL_GD_BLOCK bit para el tipo de información SQL_GETDATA_EXTENSIONS.  
  
## <a name="buffer-addresses"></a>Direcciones de búfer  
 **SQLFetchScroll** usa la misma fórmula para determinar la dirección de búferes de datos y el indicador de longitud como **SQLFetch**. Para obtener más información, vea "Direcciones de búfer" en [función SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md).  
  
## <a name="row-status-array"></a>Matriz de Estados de fila  
 **SQLFetchScroll** establece los valores de la matriz de estado de fila en la misma manera que SQLFetch. Para obtener más información, vea "Matriz de Estados de fila" en [función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="rows-fetched-buffer"></a>Búfer de filas capturadas  
 **SQLFetchScroll** devuelve el número de filas capturadas en el búfer de filas recuperadas de la misma manera que **SQLFetch**. Para obtener más información, vea "Búfer de captura de filas" en [función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="error-handling"></a>Tratamiento de errores  
 Cuando una aplicación llama **SQLFetchScroll** en un controlador ODBC 3.x, el Administrador de controladores llama **SQLFetchScroll** en el controlador. Cuando una aplicación llama **SQLFetchScroll** en un controlador ODBC 2.x, el Administrador de controladores llama SQLExtendedFetch en el controlador. Dado que **SQLFetchScroll** y SQLExtendedFetch controlar los errores de forma ligeramente diferente, la aplicación ve el comportamiento de errores ligeramente diferentes al llamarla **SQLFetchScroll** en ODBC 2.x y ODBC controladores de 3.x.  
  
 **SQLFetchScroll** devuelve errores y advertencias de la misma manera que **SQLFetch**; para obtener más información, vea "Control de errores" en **SQLFetch**. **SQLExtendedFetch** devuelve errores en la misma manera que **SQLFetch**, con las siguientes excepciones:  
  
 Cuando se produce una advertencia que se aplica a una fila determinada en el conjunto de filas, SQLExtendedFetch establece la entrada correspondiente en la matriz de Estados de fila a SQL_ROW_SUCCESS, no SQL_ROW_SUCCESS_WITH_INFO.  
  
 Si se producen errores en cada fila del conjunto de filas, SQLExtendedFetch devuelve SQL_SUCCESS_WITH_INFO, no SQL_ERROR.  
  
 En cada grupo de registros de estado que se aplica a una fila individual, el primer registro de estado devuelto por SQLExtendedFetch debe contener SQLSTATE 01S01 (Error en la fila); **SQLFetchScroll** no devuelve este SQLSTATE. Si no puede devolver SQLSTATEs adicionales SQLExtendedFetch, todavía debe devolver este SQLSTATE.  
  
## <a name="sqlfetchscroll-and-optimistic-concurrency"></a>SQLFetchScroll y simultaneidad optimista  
 Si un cursor utiliza simultaneidad optimista, es decir, el atributo de instrucción SQL_ATTR_CONCURRENCY tiene un valor de SQL_CONCUR_VALUES o SQL_CONCUR_ROWVER - **SQLFetchScroll** actualiza los valores de la simultaneidad optimista utilizados por los datos origen para detectar si una fila ha cambiado. Esto ocurre cada vez que **SQLFetchScroll** captura un nuevo conjunto de filas, incluso cuando vuelve a obtener el conjunto de filas actual. (Se llama con FetchOrientation establecido en SQL_FETCH_RELATIVE y FetchOffset establecido en 0).  
  
## <a name="sqlfetchscroll-and-odbc-2x-drivers"></a>Controladores de 2.x ODBC y SQLFetchScroll  
 Cuando una aplicación llama **SQLFetchScroll** en un controlador ODBC 2.x, el Administrador de controladores se asigna esta llamada a **SQLExtendedFetch**. Pasa los siguientes valores para los argumentos de **SQLExtendedFetch**.  
  
|Argumento SQLExtendedFetch|Valor|  
|-------------------------------|-----------|  
|StatementHandle|StatementHandle en **SQLFetchScroll**.|  
|FetchOrientation|FetchOrientation en **SQLFetchScroll**.|  
|FetchOffset|Si FetchOrientation no es SQL_FETCH_BOOKMARK, el valor del argumento FetchOffset en **SQLFetchScroll** se utiliza.<br /><br /> Si FetchOrientation es SQL_FETCH_BOOKMARK, se usa el valor almacenado en la dirección especificada por el atributo de instrucción SQL_ATTR_FETCH_BOOKMARK_PTR.|  
|RowCountPtr|La dirección especificada por el atributo de instrucción SQL_ATTR_ROWS_FETCHED_PTR.|  
|RowStatusArray|La dirección especificada por el atributo de instrucción SQL_ATTR_ROW_STATUS_PTR.|  
  
 Para obtener más información, consulte [cursores de bloque, cursores desplazables y compatibilidad con versiones anteriores](../../../odbc/reference/appendixes/block-cursors-scrollable-cursors-and-backward-compatibility.md) en Apéndice G: Directrices de controlador para la compatibilidad con versiones anteriores.  
  
## <a name="descriptors-and-sqlfetchscroll"></a>Descriptores y SQLFetchScroll  
 **SQLFetchScroll** interactúa con los descriptores de la misma manera que **SQLFetch**. Para obtener más información, vea la sección "Descriptores y SQLFetchScroll" en [función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md).  
  
## <a name="code-example"></a>Ejemplo de código  
 Consulte [el enlace](../../../odbc/reference/develop-app/column-wise-binding.md), [el enlace](../../../odbc/reference/develop-app/row-wise-binding.md), [coloca las instrucciones Update y Delete](../../../odbc/reference/develop-app/positioned-update-and-delete-statements.md), y [actualizar las filas del conjunto de filas con SQLSetPos](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Enlazar un búfer con una columna en un conjunto de resultados|[Función SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|Realizar operaciones de eliminación, actualización o inserción masiva|[Función SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|Procesamiento de una instrucción de cancelación|[Función SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|Devolver información acerca de una columna en un conjunto de resultados|[Función SQLDescribeCol](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Ejecutar una instrucción SQL|[Función SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|Ejecutar una instrucción SQL preparada|[Función SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|Obtención de una sola fila o un bloque de datos en una dirección de solo avance|[Función SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Cierre el cursor en la instrucción|[Función SQLFreeStmt](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Columnas del conjunto de devolver el número de resultados|[Función SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|Sitúe el cursor, actualizar los datos en el conjunto de filas, o actualizar o eliminar datos en el conjunto de resultados|[Función SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
|Establecer un atributo de instrucción|[Función SQLSetStmtAttr](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
