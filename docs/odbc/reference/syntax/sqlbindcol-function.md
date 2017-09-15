---
title: "SQLBindCol (función) | Documentos de Microsoft"
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
- SQLBindCol
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLBindCol
helpviewer_keywords:
- SQLBindCol function [ODBC]
ms.assetid: 41a37655-84cd-423f-9daa-e0b47b88dc54
caps.latest.revision: 37
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 641b08ab3d3aec59f66dd0405770cf19d4690769
ms.contentlocale: es-es
ms.lasthandoff: 09/09/2017

---
# <a name="sqlbindcol-function"></a>SQLBindCol (función)
**Conformidad**  
 Versión introdujo: Cumplimiento de estándares 1.0 de ODBC: ISO 92  
  
 **Resumen**  
 **SQLBindCol** enlaza los búferes de datos de aplicación a las columnas del conjunto de resultados.  
  
## <a name="syntax"></a>Sintaxis  
  
```  
  
SQLRETURN SQLBindCol(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   ColumnNumber,  
      SQLSMALLINT    TargetType,  
      SQLPOINTER     TargetValuePtr,  
      SQLLEN         BufferLength,  
      SQLLEN *       StrLen_or_Ind);  
```  
  
## <a name="arguments"></a>Argumentos  
 *StatementHandle*  
 [Entrada] Identificador de instrucción.  
  
 *ColumnNumber*  
 [Entrada] Número del resultado conjunto de columna que se va a enlazar. Las columnas se numeran en orden creciente de las columnas a partir de 0, donde la columna 0 es la columna de marcador. Si no se usan marcadores: es decir, se establece el atributo de instrucción de SQL_ATTR_USE_BOOKMARKS a SQL_UB_OFF, a continuación, los números de columna empiezan en 1.  
  
 *TargetType*  
 [Entrada] El identificador del tipo de datos C de la \* *TargetValuePtr* búfer. Cuando está recuperando datos desde el origen de datos con **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**, o **SQLSetPos**, el controlador convierte los datos para este tipo; Cuando envía datos al origen de datos con **SQLBulkOperations** o **SQLSetPos**, el controlador convierte los datos de este tipo. Para obtener una lista de tipos de datos válidos de C y los identificadores de tipo, consulte el [tipos de datos C](../../../odbc/reference/appendixes/c-data-types.md) sección en tipos de datos de apéndice D:.  
  
 Si el *TargetType* argumento es un tipo de datos de intervalo, la precisión iniciales de intervalo (2) y la precisión de segundos de intervalo predeterminado (6), como se establece en los campos SQL_DESC_DATETIME_INTERVAL_PRECISION y SQL_DESC_PRECISION de Descartar, respectivamente, se usan para los datos. Si el *TargetType* argumento es SQL_C_NUMERIC, la precisión predeterminada (definida por el controlador) y predeterminado escala (0), como se establece en los campos SQL_DESC_PRECISION y SQL_DESC_SCALE de la descartar, se usan para los datos. Si cualquier valor predeterminado de precisión o escala no es adecuada, la aplicación debe establecer explícitamente el campo descriptor adecuado mediante una llamada a **SQLSetDescField** o **SQLSetDescRec**.  
  
 También puede especificar un tipo de datos C extendido. Para obtener más información, consulte [tipos de datos C en ODBC](../../../odbc/reference/develop-app/c-data-types-in-odbc.md).  
  
 *TargetValuePtr*  
 [Entrada/salida diferida] Puntero al búfer de datos para enlazar a la columna. **SQLFetch** y **SQLFetchScroll** devolver datos en este búfer. **SQLBulkOperations** devuelve datos en este búfer cuando *operación* es SQL_FETCH_BY_BOOKMARK; recupera los datos de este búfer cuando *operación* es SQL_ADD o SQL_UPDATE_BY_BOOKMARK . **SQLSetPos** devuelve datos en este búfer cuando *operación* es SQL_REFRESH; recupera los datos de este búfer cuando *operación* es SQL_UPDATE.  
  
 Si *TargetValuePtr* es un puntero nulo, el controlador desenlaza el búfer de datos para la columna. Una aplicación puede deshacer el enlace de todas las columnas mediante una llamada a **SQLFreeStmt** con la opción SQL_UNBIND. Una aplicación puede desenlazar el búfer de datos para una columna pero que siga habiendo un búfer de longitud/indicador enlazado para la columna, si la *TargetValuePtr* argumento en la llamada a **SQLBindCol** es un puntero nulo, pero el *StrLen_or_IndPtr* argumento es un valor válido.  
  
 *BufferLength*  
 [Entrada] Longitud de la **TargetValuePtr* búfer en bytes.  
  
 El controlador utiliza *BufferLength* para evitar escribir más allá del final de la \* *TargetValuePtr* almacena en búfer cuando devuelve datos de longitud variable, como datos de caracteres o binarios. Tenga en cuenta que el controlador de cuenta, el carácter de terminación null cuando devuelve datos de caracteres a \* *TargetValuePtr*. **TargetValuePtr* , por tanto, debe contener un espacio para el carácter de terminación null o el controlador, se truncará los datos.  
  
 Cuando el controlador devuelve datos de longitud fija, como un entero o una estructura de fecha, el controlador omite *BufferLength* y se supone que el búfer es lo suficientemente grande como para contener los datos. Por lo tanto, es importante para la aplicación asignar un búfer lo suficientemente grande como para datos de longitud fija o el controlador escribirá más allá del final del búfer.  
  
 **SQLBindCol** devuelve SQLSTATE HY090 (longitud de búfer o cadena no válida) al *BufferLength* es menor que 0 pero no cuando *BufferLength* es 0. Sin embargo, si *TargetType* especifica un tipo de carácter, una aplicación no debe establecer *BufferLength* en 0, porque los controladores compatibles con ISO CLI devuelven SQLSTATE HY090 (longitud de búfer o cadena no válida) en que caso.  
  
 *StrLen_or_IndPtr*  
 [Entrada/salida diferida] Puntero al búfer de longitud/indicador para enlazar a la columna. **SQLFetch** y **SQLFetchScroll** devuelven un valor de este búfer. **SQLBulkOperations** recupera un valor de este búfer cuando *operación* es SQL_ADD, SQL_UPDATE_BY_BOOKMARK o SQL_DELETE_BY_BOOKMARK. **SQLBulkOperations** devuelve un valor en este búfer cuando *operación* es SQL_FETCH_BY_BOOKMARK. **SQLSetPos** devuelve un valor en este búfer cuando *operación* es SQL_REFRESH; recupera un valor de este búfer cuando *operación* es SQL_UPDATE.  
  
 **SQLFetch**, **SQLFetchScroll**, **SQLBulkOperations**, y **SQLSetPos** puede devolver los valores siguientes en el búfer de longitud/indicador:  
  
-   La longitud de los datos disponibles para devolver  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 La aplicación puede colocar los valores siguientes en el búfer de longitud/indicador para su uso con **SQLBulkOperations** o **SQLSetPos**:  
  
-   La longitud de los datos que se envían  
  
-   SQL_NTS  
  
-   SQL_NULL_DATA  
  
-   SQL_DATA_AT_EXEC  
  
-   El resultado de la macro SQL_LEN_DATA_AT_EXEC  
  
-   SQL_COLUMN_IGNORE  
  
 Si el búfer de indicador y el búfer de longitud son independientes, el búfer de indicador puede devolver sólo SQL_NULL_DATA, mientras que el búfer de longitud puede devolver todos los demás valores.  
  
 Para obtener más información, consulte [función SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [SQLFetch, función](../../../odbc/reference/syntax/sqlfetch-function.md), [SQLSetPos, función](../../../odbc/reference/syntax/sqlsetpos-function.md), y [con valores de longitud/indicador](../../../odbc/reference/develop-app/using-length-and-indicator-values.md).  
  
 Si *StrLen_or_IndPtr* se usa un valor null de puntero, no hay longitud o indicador. Se trata de un error al capturar datos y los datos es NULL.  
  
 Vea [información ODBC de 64 bits](../../../odbc/reference/odbc-64-bit-information.md), si la aplicación se ejecutará en un sistema operativo de 64 bits.  
  
## <a name="returns"></a>Devuelve  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR o SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>Diagnósticos  
 Cuando **SQLBindCol** devuelve SQL_ERROR o SQL_SUCCESS_WITH_INFO, un valor SQLSTATE asociado se puede obtener mediante una llamada a **SQLGetDiagRec** con un *HandleType* de SQL_ HANDLE_STMT y un *controlar* de *StatementHandle*. En la tabla siguiente se enumera los valores SQLSTATE suelen ser devueltos por **SQLBindCol** y se explica cada uno de ellos en el contexto de esta función; la notación "(DM)" precede a las descripciones de SQLSTATE devuelto por el Administrador de controladores. El código de retorno asociado a cada valor SQLSTATE es SQL_ERROR, a menos que se indique lo contrario.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|Advertencia general|Mensaje informativo de específicas del controlador. (La función devuelve SQL_SUCCESS_WITH_INFO).|  
|07006|Infracción del atributo de tipo de datos restringido|(DM) la *ColumnNumber* argumento era 0 y el *TargetType* argumento no era SQL_C_BOOKMARK o SQL_C_VARBOOKMARK.|  
|07009|Índice de descriptor no válido|El valor especificado para el argumento *ColumnNumber* superó el número máximo de columnas del conjunto de resultados.|  
|HY000|Error general|Se produjo un error para que no hubo ninguna SQLSTATE específico y para el que se ha definido ningún SQLSTATE específico de la implementación. El mensaje de error devuelto por **SQLGetDiagRec** en el * \*MessageText* búfer describe el error y su causa.|  
|HY001|Error de asignación de memoria|El controlador no pudo asignar memoria que es necesario para admitir la ejecución o la finalización de la función.|  
|HY003|Tipo de búfer de aplicación no válido|El argumento *TargetType* no era un tipo de datos válido ni SQL_C_DEFAULT.|  
|HY010|Error de secuencia de función|(DM) se llamó a una función ejecuta de forma asincrónica para el identificador de conexión que está asociado el *StatementHandle*. Esta función asincrónica aún estaba ejecutando cuando **SQLBindCol** se llamó.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, o **SQLMoreResults** se llamó para el *StatementHandle* devolvió SQL_PARAM_DATA_ ESTÁ DISPONIBLE. Esta función se invoca antes de que se recuperan los datos para todos los parámetros transmitidos.<br /><br /> (DM) se llamó a una función ejecuta de forma asincrónica para la *StatementHandle* y aún se estaba ejecutando cuando se llamó a esta función.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, o **SQLSetPos** se llamó para el * StatementHandle* y devuelve SQL_NEED_DATA. Esta función se invoca antes de que se enviaron los datos para todas las columnas o parámetros de datos en ejecución.|  
|HY013|Error de administración de memoria|No se pudo procesar la llamada de función porque los objetos subyacentes de la memoria no se pudieron tener acceso, posiblemente debido a condiciones de memoria insuficiente.|  
|HY090|Longitud de búfer o cadena no válida|(DM) el valor especificado para el argumento *BufferLength* era menor que 0.<br /><br /> (DM) el controlador fue un 2 de ODBC. *x* controlador, el *ColumnNumber* argumento se establece en 0 y el valor especificado para el argumento *BufferLength* no era igual a 4.|  
|HY117|Se suspende la conexión debido al estado de transacción desconocido. Solo se desconecte y se permiten las funciones de solo lectura.|(DM) para obtener más información sobre el estado suspendido, consulte [función SQLEndTran](../../../odbc/reference/syntax/sqlendtran-function.md).|  
|HYC00|Característica opcional no implementada|El controlador u origen de datos no admite la conversión especificada por la combinación de la *TargetType* argumento y el tipo de datos SQL específicas del controlador de la columna correspondiente.<br /><br /> El argumento *ColumnNumber* es 0 y el controlador no admite marcadores.<br /><br /> El controlador es compatible con solo 2 de ODBC. *x* y el argumento *TargetType* era una de las siguientes acciones:<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> y cualquiera de los tipos de datos C de intervalo que aparecen en [tipos de datos C](../../../odbc/reference/appendixes/c-data-types.md) en tipos de datos de apéndice D:.<br /><br /> El controlador solo es compatible con las versiones ODBC anteriores 3.50 y el argumento *TargetType* era SQL_C_GUID.|  
|HYT01|Tiempo de espera de conexión expirado|El período de tiempo de espera de conexión finalizó antes de que el origen de datos se respondió a la solicitud. El período de tiempo de espera de conexión se establece a través de **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT.|  
|IM001|Controlador no admite esta función|(DM) el controlador asociado a la *StatementHandle* no admite la función.|  
  
## <a name="comments"></a>Comentarios  
 **SQLBindCol** se usa para asociar, o *enlazar,* columnas del resultado se establezcan en los búferes de datos y los búferes de longitud/indicador de la aplicación. Cuando la aplicación llama **SQLFetch**, **SQLFetchScroll**, o **SQLSetPos** para capturar los datos, el controlador devuelve los datos de las columnas enlazadas en los búferes especificados; para obtener más información, consulte [SQLFetch, función](../../../odbc/reference/syntax/sqlfetch-function.md). Cuando la aplicación llama **SQLBulkOperations** para actualizar o insertar una fila o **SQLSetPos** para actualizar una fila, el controlador JDBC recupera los datos de las columnas enlazadas desde los búferes especificados; para obtener más información , consulte [función SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md) o [SQLSetPos, función](../../../odbc/reference/syntax/sqlsetpos-function.md). Para obtener más información sobre el enlace, consulte [recuperar resultados (Basic)](../../../odbc/reference/develop-app/retrieving-results-basic.md).  
  
 Tenga en cuenta que las columnas no tiene que estar enlazado para recuperar datos de ellos. También puede llamar una aplicación **SQLGetData** para recuperar datos de las columnas. Aunque es posible enlazar algunas columnas de una fila y una llamada **SQLGetData** en otros casos, esto está sujeto a algunas restricciones. Para obtener más información, consulte [SQLGetData](../../../odbc/reference/syntax/sqlgetdata-function.md).  
  
## <a name="binding-unbinding-and-rebinding-columns"></a>Columnas de enlace, Desenlazando y reenlace  
 Una columna puede ser dependiente, sin enlazar o Reenlazar en cualquier momento, incluso después de que se hayan extraído los datos del conjunto de resultados. El nuevo enlace surte efecto la próxima vez que se invoque una función que usa enlaces. Por ejemplo, suponga que una aplicación enlaza las columnas de un conjunto de resultados y llamadas **SQLFetch**. El controlador devuelve los datos en los búferes de enlazado. Ahora suponga que la aplicación enlaza las columnas a un conjunto diferente de búferes. El controlador no colocar los datos de la fila just-capturados en los búferes recién enlazados. En su lugar, espera hasta que **SQLFetch** se llama de nuevo y, a continuación, coloca los datos de la fila siguiente en los búferes recién enlazados.  
  
> [!NOTE]  
>  El atributo de instrucción SQL_ATTR_USE_BOOKMARKS siempre debe establecerse antes de enlazar una columna a 0. Esto no es necesario, pero se recomienda encarecidamente.  
  
## <a name="binding-columns"></a>Enlazar columnas  
 Para enlazar una columna, una aplicación llama **SQLBindCol** y pasa el número de columna, tipo, dirección y longitud de un búfer de datos y la dirección de un búfer de longitud/indicador. Para obtener información sobre cómo se utilizan estas direcciones, vea "Direcciones de búfer", más adelante en esta sección. Para obtener más información acerca de las columnas de enlace, vea [utilizando SQLBindCol](../../../odbc/reference/develop-app/using-sqlbindcol.md).  
  
 El uso de estos búferes se aplaza; es decir, la aplicación enlaza en **SQLBindCol** , pero el controlador tiene acceso a ellos desde otras funciones, es decir, **SQLBulkOperations**, **SQLFetch**, ** SQLFetchScroll**, o **SQLSetPos**. Es responsabilidad de la aplicación para asegurarse de que los punteros especifican en **SQLBindCol** siguen siendo válidas siempre y cuando el enlace permanece en vigor. Si la aplicación permite a estos punteros deje de ser válida, por ejemplo, libera un búfer, y, a continuación, llama a una función que espera que sean válidas, las consecuencias son indefinidas. Para obtener más información, consulte [diferidas búferes](../../../odbc/reference/develop-app/deferred-buffers.md).  
  
 El enlace permanece en vigor hasta que se sustituye por un nuevo enlace, la columna no está enlazada o se libera la instrucción.  
  
## <a name="unbinding-columns"></a>Desenlazando columnas  
 Para desenlazar una sola columna, una aplicación llama **SQLBindCol** con *ColumnNumber* establecido en el número de esa columna y *TargetValuePtr* establecido en un puntero nulo. Si *ColumnNumber* hace referencia a una columna sin enlazar, **SQLBindCol** todavía devuelve SQL_SUCCESS.  
  
 Para desenlazar todas las columnas, una aplicación llama **SQLFreeStmt** con *fOption* establecido en SQL_UNBIND. Esto puede realizarse estableciendo el campo SQL_DESC_COUNT de la descartar en cero.  
  
## <a name="rebinding-columns"></a>Volver a enlazar las columnas  
 Una aplicación puede realizar cualquiera de las dos operaciones para cambiar un enlace:  
  
-   Llame a **SQLBindCol** para especificar un nuevo enlace para una columna que ya está enlazado. El controlador sobrescribe el enlace antiguo con uno nuevo.  
  
-   Especifique un desplazamiento que se va a agregar a la dirección de búfer que se especificó en la llamada de enlace a **SQLBindCol**. Para obtener más información, vea la sección siguiente, "Enlace desplazamientos".  
  
## <a name="binding-offsets"></a>Desplazamientos de enlace  
 Un desplazamiento de enlace es un valor que se agrega a las direcciones de los búferes de datos y longitud/indicador (según lo especificado en el *TargetValuePtr* y *StrLen_or_IndPtr* argumento) antes de que se desreferencian. Cuando se utilizan los desplazamientos, los enlaces son "plantilla" de cómo se distribuyen los búferes de la aplicación y la aplicación puede mover esta "plantilla" a diferentes áreas de memoria cambiando el desplazamiento. Como el mismo desplazamiento se agrega a todas las direcciones en cada enlace, las posiciones relativas entre búferes para diferentes columnas deben ser el mismo dentro de cada conjunto de búferes. Esto es siempre true cuando se usa el enlace de modo de fila; la aplicación debe diseñar cuidadosamente sus búferes para este valor es true cuando se utiliza el enlace.  
  
 Con un desplazamiento de enlace tiene básicamente el mismo efecto que volver a enlazar una columna mediante una llamada a **SQLBindCol**. La diferencia es que una nueva llamada a **SQLBindCol** especifica nuevas direcciones para el búfer de datos y búfer indicador de longitud, mientras que el uso de un desplazamiento de enlace no cambia las direcciones, pero solo agrega un desplazamiento a ellas. La aplicación puede especificar un desplazamiento nuevo cada vez que desea, y este desplazamiento siempre se agrega a las direcciones de enlace originalmente. En concreto, si el desplazamiento se establece en 0, o si se establece el atributo de instrucción en un puntero nulo, el controlador utiliza las direcciones de enlace originalmente.  
  
 Para especificar un desplazamiento de enlace, la aplicación establece el atributo de instrucción de SQL_ATTR_ROW_BIND_OFFSET_PTR a la dirección de un búfer SQLINTEGER. Antes de que la aplicación llama a una función que usa enlaces, coloca un desplazamiento en bytes en este búfer. Para determinar la dirección del búfer que se va a utilizar, el controlador agrega el desplazamiento a la dirección en el enlace. La suma de la dirección y el desplazamiento debe ser una dirección válida, pero la dirección a la que se agrega el desplazamiento no tiene que ser válido. Para obtener más información sobre cómo se utilizan los desplazamientos de enlace, vea "Direcciones de búfer", más adelante en esta sección.  
  
## <a name="binding-arrays"></a>Matrices de enlace  
 Si el tamaño del conjunto de filas (el valor del atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE) es mayor que 1, la aplicación enlaza las matrices de búferes en lugar de búferes únicos. Para obtener más información, consulte [cursores de bloque](../../../odbc/reference/develop-app/block-cursors.md).  
  
 La aplicación puede enlazar las matrices de dos maneras:  
  
-   Enlazar una matriz para cada columna. Esto se conoce como *el enlace* porque cada estructura de datos (matriz) contiene datos de una sola columna.  
  
-   Define una estructura para contener los datos para una fila completa y una matriz de estas estructuras de enlace. Esto se conoce como *el enlace* porque cada estructura de datos contiene los datos de una sola fila.  
  
 Cada matriz de búferes que debe tener al menos tantos elementos como el tamaño del conjunto de filas.  
  
> [!NOTE]  
>  Una aplicación debe comprobar que la alineación es válida. Para obtener más información acerca de las consideraciones de alineación, vea [alineación](../../../odbc/reference/develop-app/alignment.md).  
  
## <a name="column-wise-binding"></a>El enlace  
 En el enlace, la aplicación enlaza datos independiente y matrices de longitud/indicador para cada columna.  
  
 Para utilizar el enlace, la aplicación primero establece el atributo de instrucción SQL_ATTR_ROW_BIND_TYPE en SQL_BIND_BY_COLUMN. (Es el valor predeterminado.) Para que cada columna esté enlazada, la aplicación realiza los pasos siguientes:  
  
1.  Asigna una matriz de búferes de datos.  
  
2.  Asigna una matriz de búferes de longitud/indicador.  
  
    > [!NOTE]  
    >  Si la aplicación escribe directamente a descriptores cuando se usa el enlace, matrices independientes pueden usarse para los datos de longitud y el indicador.  
  
3.  Llamadas **SQLBindCol** con los argumentos siguientes:  
  
    -   *TargetType* es el tipo de un único elemento de la matriz de búferes de datos.  
  
    -   *TargetValuePtr* es la dirección de la matriz de búferes de datos.  
  
    -   *BufferLength* es el tamaño de un único elemento de la matriz de búferes de datos. El *BufferLength* argumento se omite cuando los datos son datos de longitud fija.  
  
    -   *StrLen_or_IndPtr* es la dirección de la matriz de longitud/indicador.  
  
 Para obtener más información sobre cómo se usa esta información, consulte "Direcciones de búfer", más adelante en esta sección. Para obtener más información sobre el enlace de modo de columna, vea [el enlace](../../../odbc/reference/develop-app/column-wise-binding.md).  
  
## <a name="row-wise-binding"></a>El enlace  
 En el enlace de modo de fila, la aplicación define una estructura que contiene datos y longitud/indicador búferes para cada columna que se va a enlazar.  
  
 Para utilizar el enlace, la aplicación realiza los pasos siguientes:  
  
1.  Define una estructura que contenga una sola fila de datos (incluidos los búferes de datos y el indicador de longitud) y asigna una matriz de estas estructuras.  
  
    > [!NOTE]  
    >  Si la aplicación escribe directamente a descriptores cuando se usa el enlace de modo de fila, campos independientes se pueden usar para los datos de longitud y el indicador.  
  
2.  Establece el atributo de instrucción de SQL_ATTR_ROW_BIND_TYPE con el tamaño de la estructura que contiene una sola fila de datos o hasta el tamaño de una instancia de un búfer en el que se enlazarán las columnas de resultados. La longitud debe incluir el espacio para todas las columnas enlazadas y cualquier relleno de la estructura o el búfer, para asegurarse de que cuando la dirección de una columna enlazada se incrementa con la longitud especificada, el resultado señalará al principio de la misma columna en la fila siguiente. Cuando se usa el *sizeof* operador en ANSI C, se garantiza que este comportamiento.  
  
3.  Llamadas **SQLBindCol** con los argumentos siguientes para cada columna que se va a enlazar:  
  
    -   *TargetType* es el tipo del miembro de búfer de datos se puede enlazar a la columna.  
  
    -   *TargetValuePtr* es la dirección del miembro de búfer de datos en el primer elemento de matriz.  
  
    -   *BufferLength* es el tamaño del búfer de miembro de datos.  
  
    -   *StrLen_or_IndPtr* es la dirección del miembro de longitud/indicador esté enlazado.  
  
 Para obtener más información sobre cómo se usa esta información, consulte "Direcciones de búfer", más adelante en esta sección. Para obtener más información sobre el enlace de modo de columna, vea [el enlace](../../../odbc/reference/develop-app/row-wise-binding.md).  
  
## <a name="buffer-addresses"></a>Direcciones de búfer  
 El *dirección del búfer* será la dirección real del búfer de datos o de longitud/indicador. El controlador calcula la dirección de búferes justo antes de que escribe en los búferes (por ejemplo, durante el momento de la captura). Se calcula a partir de la fórmula siguiente, que usa las direcciones especificadas en el *TargetValuePtr* y *StrLen_or_IndPtr* argumentos, el desplazamiento de enlace y el número de fila:  
  
 *Enlazado dirección* + *enlace desplazamiento* + ((*número de fila* – 1) x *tamaño del elemento*)  
  
 donde se definen las variables de la fórmula como se describe en la tabla siguiente.  
  
|Variable|Description|  
|--------------|-----------------|  
|*Enlazado de dirección*|Para los búferes de datos, la dirección especificada con la *TargetValuePtr* argumento en **SQLBindCol**.<br /><br /> Para los búferes de longitud/indicador, la dirección especificada con la *StrLen_or_IndPtr* argumento en **SQLBindCol**. Para obtener más información, vea "Comentarios adicionales" en la sección "Descriptores y SQLBindCol".<br /><br /> Si la dirección de enlace es 0, se devuelve ningún valor de datos, incluso si la dirección calculada mediante la fórmula anterior es distinto de cero.|  
|*Desplazamiento de enlace*|Si se usa el enlace, el valor almacenado en la dirección especificada con el atributo de instrucción SQL_ATTR_ROW_BIND_OFFSET_PTR.<br /><br /> Si se usa el enlace o si el valor del atributo de instrucción SQL_ATTR_ROW_BIND_OFFSET_PTR es un puntero nulo, *enlace desplazamiento* es 0.|  
|*Número de fila*|El número basado en 1 de la fila del conjunto de filas. Para capturar varias filas, que es el valor predeterminado, es 1.|  
|*Tamaño del elemento*|El tamaño de un elemento de la matriz enlazado.<br /><br /> Si se usa el enlace, se trata de **sizeof(SQLINTEGER)** para los búferes de longitud/indicador. Para los búferes de datos, es el valor de la *BufferLength* argumento en **SQLBindCol** si el tipo de datos es de longitud variable y el tamaño del tipo de datos si el tipo de datos tiene una longitud fija.<br /><br /> Si se usa el enlace, esto es el valor del atributo de instrucción SQL_ATTR_ROW_BIND_TYPE para los búferes de datos y de longitud/indicador.|  
  
## <a name="descriptors-and-sqlbindcol"></a>Descriptores y SQLBindCol  
 Las secciones siguientes describen cómo **SQLBindCol** interactúa con descriptores.  
  
> [!CAUTION]  
>  Al llamar a **SQLBindCol** para una instrucción puede afectar a otras instrucciones. Esto se produce cuando el descartar asociado con la instrucción se asigna explícitamente y también está asociado con otras instrucciones. Dado que **SQLBindCol** modifica el descriptor, las modificaciones se aplican a todas las instrucciones con el que está asociado este descriptor. Si no es el comportamiento requerido, la aplicación debe anular la asociación de este descriptor de las demás instrucciones antes de llamar a **SQLBindCol**.  
  
## <a name="argument-mappings"></a>Asignaciones de argumento  
 Conceptualmente, **SQLBindCol** realiza los siguientes pasos de secuencia:  
  
1.  Llamadas **SQLGetStmtAttr** para obtener el identificador de descartar.  
  
2.  Llamadas **SQLGetDescField** para obtener SQL_DESC_COUNT campo del descriptor y si el valor de la *ColumnNumber* argumento supera el valor de SQL_DESC_COUNT, llamadas **SQLSetDescField ** para aumentar el valor de SQL_DESC_COUNT a *ColumnNumber*.  
  
3.  Llamadas **SQLSetDescField** varias veces para asignar valores a los campos siguientes de la descartar:  
  
    -   Establece SQL_DESC_TYPE y SQL_DESC_CONCISE_TYPE en el valor de *TargetType*, excepto en que si *TargetType* es uno de los identificadores concisos de un subtipo de intervalo o datetime, Establece SQL_DESC_TYPE en SQL_ Fecha y hora o SQL_INTERVAL, respectivamente; establece SQL_DESC_CONCISE_TYPE en el identificador conciso; y conjuntos de SQL_DESC_DATETIME_INTERVAL_CODE para el valor de datetime correspondiente o el subcódigo de intervalo.  
  
    -   Establece una o varias de SQL_DESC_LENGTH, SQL_DESC_PRECISION, SQL_DESC_SCALE y SQL_DESC_DATETIME_INTERVAL_PRECISION, según corresponda para *TargetType*.  
  
    -   Establece el campo SQL_DESC_OCTET_LENGTH en el valor de *BufferLength*.  
  
    -   Establece el campo SQL_DESC_DATA_PTR en el valor de *TargetValue*.  
  
    -   Establece el campo SQL_DESC_INDICATOR_PTR en el valor de *StrLen_or_Ind*. (Vea el párrafo siguiente).  
  
    -   Establece el campo SQL_DESC_OCTET_LENGTH_PTR en el valor de *StrLen_or_Ind*. (Vea el párrafo siguiente).  
  
 La variable que el *StrLen_or_Ind* argumento hace referencia a se utiliza para obtener información de indicador y longitud. Si es un valor null para la columna encuentra con una captura, almacena SQL_NULL_DATA en esta variable; en caso contrario, almacena la longitud de datos en esta variable. Se pasa un puntero null como *StrLen_or_Ind* mantiene la operación de recopilación de devolver la longitud de datos pero hace que la operación de captura se producirá un error si se encuentra un valor null y no tiene ninguna manera de devuelven SQL_NULL_DATA.  
  
 Si la llamada a **SQLBindCol** se produce un error, el contenido de los campos de descriptor que habría establecido en el descartar están definidos y no se ha modificado el valor del campo SQL_DESC_COUNT de la descartar.  
  
## <a name="implicit-resetting-of-count-field"></a>Restablecimiento implícita del campo de número  
 **SQLBindCol** SQL_DESC_COUNT se establece en el valor de la *ColumnNumber* argumento solo cuando esto podría aumentar el valor de SQL_DESC_COUNT. Si el valor de la *TargetValuePtr* argumento es un puntero nulo y el valor de la *ColumnNumber* argumento es igual a SQL_DESC_COUNT (es decir, cuando desenlazar el nivel más alto columna dependiente), SQL_DESC_, a continuación, RECUENTO se establece en el número de la columna dependiente restante más alto.  
  
## <a name="cautions-regarding-sqldefault"></a>Precauciones con respecto a SQL_DEFAULT  
 Para recuperar correctamente datos de la columna, la aplicación debe determinar correctamente la longitud y el punto inicial de los datos en el búfer de aplicación. Cuando la aplicación especifica explícito *TargetType*, conceptos erróneos de aplicación se detectan fácilmente. Sin embargo, cuando la aplicación especifica un *TargetType* de SQL_DEFAULT, **SQLBindCol** puede aplicarse a una columna de un tipo de datos diferente de la que se pretende por la aplicación, cualquiera de los cambios a la metadatos o aplicando el código a una columna distinta. En este caso, la aplicación no puede siempre determinar el inicio o la longitud de los datos de la columna capturada. Esto puede conducir a errores sin informar de datos o a infracciones de la memoria.  
  
## <a name="code-example"></a>Ejemplo de código  
 En el ejemplo siguiente, se ejecuta una aplicación un **seleccione** instrucción en la tabla Customers para devolver un conjunto de resultados del cliente, identificadores, nombres y números de teléfono, ordenados por nombre. A continuación, se llama **SQLBindCol** para enlazar las columnas de datos a los búferes locales. Por último, la aplicación obtiene cada fila de datos con **SQLFetch** e imprime el número de teléfono, Id. y nombre de cada cliente.  
  
 Ver más ejemplos de código, consulte [función SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md), [función SQLColumns](../../../odbc/reference/syntax/sqlcolumns-function.md), [función SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md), y [SQLSetPos, función](../../../odbc/reference/syntax/sqlsetpos-function.md).  
  
```  
// SQLBindCol_ref.cpp  
// compile with: odbc32.lib  
#include <windows.h>  
#include <stdio.h>  
  
#define UNICODE  
#include <sqlext.h>  
  
#define NAME_LEN 50  
#define PHONE_LEN 20  
  
void show_error() {  
   printf("error\n");  
}  
  
int main() {  
   SQLHENV henv;  
   SQLHDBC hdbc;  
   SQLHSTMT hstmt = 0;  
   SQLRETURN retcode;  
   SQLWCHAR szName[NAME_LEN], szPhone[PHONE_LEN], sCustID[NAME_LEN];  
   SQLLEN cbName = 0, cbCustID = 0, cbPhone = 0;  
  
   // Allocate environment handle  
   retcode = SQLAllocHandle(SQL_HANDLE_ENV, SQL_NULL_HANDLE, &henv);  
  
   // Set the ODBC version environment attribute  
   if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
      retcode = SQLSetEnvAttr(henv, SQL_ATTR_ODBC_VERSION, (SQLPOINTER*)SQL_OV_ODBC3, 0);   
  
      // Allocate connection handle  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
         retcode = SQLAllocHandle(SQL_HANDLE_DBC, henv, &hdbc);  
  
         // Set login timeout to 5 seconds  
         if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
            SQLSetConnectAttr(hdbc, SQL_LOGIN_TIMEOUT, (SQLPOINTER)5, 0);  
  
            // Connect to data source  
            retcode = SQLConnect(hdbc, (SQLWCHAR*) L"NorthWind", SQL_NTS, (SQLWCHAR*) NULL, 0, NULL, 0);  
  
            // Allocate statement handle  
            if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {   
               retcode = SQLAllocHandle(SQL_HANDLE_STMT, hdbc, &hstmt);   
  
               retcode = SQLExecDirect(hstmt, (SQLWCHAR *) L"SELECT CustomerID, ContactName, Phone FROM CUSTOMERS ORDER BY 2, 1, 3", SQL_NTS);  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
  
                  // Bind columns 1, 2, and 3  
                  retcode = SQLBindCol(hstmt, 1, SQL_C_CHAR, &sCustID, 100, &cbCustID);  
                  retcode = SQLBindCol(hstmt, 2, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
                  retcode = SQLBindCol(hstmt, 3, SQL_C_CHAR, szPhone, PHONE_LEN, &cbPhone);   
  
                  // Fetch and print each row of data. On an error, display a message and exit.  
                  for (i ; ; i++) {  
                     retcode = SQLFetch(hstmt);  
                     if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO)  
                        show_error();  
                     if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO)  
                        wprintf(L"%d: %S %S %S\n", i + 1, sCustID, szName, szPhone);  
                     else  
                        break;  
                  }  
               }  
  
               // Process data  
               if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO) {  
                  SQLCancel(hstmt);  
                  SQLFreeHandle(SQL_HANDLE_STMT, hstmt);  
               }  
  
               SQLDisconnect(hdbc);  
            }  
  
            SQLFreeHandle(SQL_HANDLE_DBC, hdbc);  
         }  
      }  
      SQLFreeHandle(SQL_HANDLE_ENV, henv);  
   }  
}  
```  
  
 Vea también [programa de ejemplo ODBC](../../../odbc/reference/sample-odbc-program.md).  
  
## <a name="related-functions"></a>Funciones relacionadas  
  
|Para obtener información acerca de|Vea|  
|---------------------------|---------|  
|Devolver información acerca de una columna en un conjunto de resultados|[SQLDescribeCol (función)](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|Captura un bloque de datos o desplazarse a través de un resultado de conjunto|[SQLFetchScroll, función](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|Recopilación de varias filas de datos|[SQLFetch, función](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|Liberar los búferes de columna en la instrucción|[SQLFreeStmt, función](../../../odbc/reference/syntax/sqlfreestmt-function.md)|  
|Capturar parte o la totalidad de una columna de datos|[SQLGetData, función](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|Columnas del conjunto de devolver el número de resultados|[SQLNumResultCols (función)](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
  
## <a name="see-also"></a>Vea también  
 [Referencia de la API de ODBC](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [Archivos de encabezado de ODBC](../../../odbc/reference/install/odbc-header-files.md)
