---
title: Asignación de funciones de reemplazo para la compatibilidad de aplicaciones - ODBC | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- mapping replacement functions [ODBC]
- upgrading applications [ODBC], mapping replacement functions
- compatibility [ODBC], mapping replacement functions
- ODBC drivers [ODBC], backward compatibility
- functions [ODBC], mapping replacement functions
- application upgrades [ODBC], mapping replacement functions
- backward compatibility [ODBC], mapping replacement functions
ms.assetid: f5e6d9da-76ef-42cb-b3f5-f640857df732
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 400f1fd18788f361b3eada813a414077e62de1e1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/16/2018
---
# <a name="mapping-replacement-functions-for-backward-compatibility-of-applications"></a>Asignación de funciones de reemplazo para mantener la compatibilidad de aplicaciones
Una aplicación ODBC 3*.x* aplicación funcione a través de ODBC 3*.x* el Administrador de controladores funcionará con una API ODBC 2. *x* controlador siempre y cuando no se utilizan características nuevas. Ambos duplican la funcionalidad y cambios de comportamiento, sin embargo, ser afectan al modo en que ODBC 3. *x* aplicación funciona en una API ODBC 2. *x* controlador. Cuando se trabaja con una API ODBC 2. *x* controlador, el Administrador de controladores asigna el siguiente ODBC 3. *x* funciones, que se reemplazaron uno o más ODBC 2. *x* funciones, en la correspondiente API ODBC 2. *x* funciones.  
  
|ODBC 3. *x* (función)|ODBC 2. *x* (función)|  
|-------------------------|-------------------------|  
|**SQLAllocHandle**|**SQLAllocEnv**, **SQLAllocConnect**, o **SQLAllocStmt**|  
|**SQLBulkOperations**|**SQLSetPos**|  
|**SQLColAttribute**|**SQLColAttributes**|  
|**SQLEndTran**|**SQLTransact**|  
|**SQLFetch**|**SQLExtendedFetch**|  
|**SQLFetchScroll**|**SQLExtendedFetch**|  
|**SQLFreeHandle**|**SQLFreeEnv**, **SQLFreeConnect**, o **SQLFreeStmt**|  
|**SQLGetConnectAttr**|**SQLGetConnectOption**|  
|**SQLGetDiagRec**|**SQLError**|  
|**SQLGetStmtAttr**|**SQLGetStmtOption**[1]|  
|**SQLSetConnectAttr**|**SQLSetConnectOption**|  
|**SQLSetStmtAttr**|**SQLSetStmtOption**[1]|  
  
 [1] otras acciones podrían también se lleva a cabo, según el atributo que se solicita.  
  
## <a name="sqlallochandle"></a>SQLAllocHandle  
 El Administrador de controladores se asigna a **SQLAllocEnv**, **SQLAllocConnect**, o **SQLAllocStmt**, según corresponda. La siguiente llamada a **SQLAllocHandle**:  
  
```  
SQLAllocHandle(HandleType, InputHandle, OutputHandlePtr);  
```  
  
 se producirá en el Administrador de controladores realiza las siguientes acciones (conceptual, ninguna comprobación de errores) asignación:  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLAllocEnv(OutputHandlePtr));  
   case SQL_HANDLE_DBC: return (SQLAllocConnect (InputHandle, OutputHandlePtr));  
   case SQL_HANDLE_STMT: return (SQLAllocStmt (InputHandle, OutputHandlePtr));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlbulkoperations"></a>SQLBulkOperations  
 El Administrador de controladores se asigna a **SQLSetPos**. La siguiente llamada a **SQLBulkOperations**:  
  
```  
SQLBulkOperations(hstmt, Operation);  
```  
  
 se producirá la siguiente secuencia de pasos:  
  
1.  Si el argumento de la operación es SQL_ADD, el Administrador de controladores llama **SQLSetPos** como se indica a continuación:  
  
    ```  
    SQLSetPos (hstmt, 0, SQL_ADD, SQL_LOCK_NO_CHANGE);  
    ```  
  
2.  Si el argumento de operación no es SQL_ADD, el controlador devuelve SQLSTATE HY092 (identificador de atributo u opción no válido).  
  
3.  Si la aplicación intenta cambiar el SQL_ATTR_ROW_STATUS_PTR entre las llamadas a **SQLFetch** o **SQLFetchScroll** y **SQLBulkOperations**, el Administrador de controladores devolver SQLSTATE HY011 (atributo no se puede establecer ahora).  
  
4.  Si el argumento de la operación es SQL_ADD, la aplicación debe llamar a **SQLBindCol** para enlazar los datos que se va a insertar. No se puede llamar a **SQLSetDescField** o **SQLSetDescRec** para enlazar los datos que se va a insertar.  
  
5.  Si el argumento de la operación es SQL_ADD y el número de filas que se va a insertar no es el mismo que el tamaño actual del conjunto de filas, **SQLSetStmtAttr** debe llamarse para establecer el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE en el número de filas que se va a ser Insertar antes de llamar a **SQLBulkOperations**. Para volver al tamaño de conjunto de filas anterior, la aplicación debe establecer el atributo de instrucción SQL_ATTR_ROW_ARRAY_SIZE antes **SQLFetch**, **SQLFetchScroll**, o **SQLSetPos**se llama.  
  
## <a name="sqlcolattribute"></a>SQLColAttribute  
 El Administrador de controladores se asigna a **SQLColAttributes**. La siguiente llamada a **SQLColAttribute**:  
  
```  
SQLColAttribute(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
```  
  
 se producirá la siguiente secuencia de pasos:  
  
1.  Si *FieldIdentifier* es uno de los siguientes:  
  
     SQL_DESC_PRECISION, SQL_DESC_SCALE, SQL_DESC_LENGTH, SQL_DESC_OCTET_LENGTH, SQL_DESC_UNNAMED, SQL_DESC_BASE_COLUMN_NAME, SQL_DESC_LITERAL_PREFIX, SQL_DESC_LITERAL_SUFFIX o SQL_DESC_LOCAL_TYPE_NAME  
  
     el Administrador de controladores devuelve SQL_ERROR con SQLSTATE HY091 (identificador de campo descriptor no válido). Ninguna otra regla de esta sección se aplica.  
  
2.  El Administrador de controladores asigna SQL_COLUMN_COUNT, SQL_COLUMN_NAME o SQL_COLUMN_NULLABLE SQL_DESC_COUNT, SQL_DESC_NAME o SQL_DESC_NULLABLE, respectivamente. (Un ODBC 2*.x* controlador sólo necesita admitir SQL_COLUMN_COUNT, SQL_COLUMN_NAME, SQL_COLUMN_NULLABLE, SQL_DESC_COUNT, SQL_DESC_NAME y no SQL_DESC_NULLABLE.) La llamada a SQLColAttribute se asigna a:  
  
    ```  
    SQLColAttributes(StatementHandle, ColumnNumber, FieldIdentifier, CharacterAttributePtr, BufferLength, StringLengthPtr, NumericAttributePtr);  
    ```  
  
3.  Todos los demás *FieldIdentifier* valores se pasan al controlador, con **SQLColAttribute** asignado a **SQLColAttributes** tal y como se ha mostrado anteriormente.  
  
4.  Si *BufferLength* es menor que 0, el Administrador de controladores, devolverá SQL_ERROR con SQLSTATE HY090 (longitud de búfer o cadena no válida). Ninguna otra regla de esta sección se aplica.  
  
5.  Si *FieldIdentifier* es SQL_DESC_CONCISE_TYPE y el tipo de valor devuelto es un tipo de datos datetime concisa, las asignaciones de administrador de controladores, la devolución de valores para los códigos de fecha, hora y marca de tiempo.  
  
6.  El Administrador de controladores realiza comprobaciones necesarias para ver si SQLSTATE HY010 (error de secuencia de función) debe generarse. Si es así, el Administrador de controladores devuelve SQL_ERROR y SQLSTATE HY010 (error de secuencia de función). Ninguna otra regla de esta sección se aplica.  
  
## <a name="sqlendtran"></a>SQLEndTran  
 El Administrador de controladores se asigna a **SQLTransact**. La siguiente llamada a **SQLEndTran**:  
  
```  
SQLEndTran(HandleType, Handle, CompletionType);  
```  
  
 se producirá en el Administrador de controladores realiza las siguientes acciones (conceptual, ninguna comprobación de errores) asignación:  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV:return(SQLTransact(Handle, SQL_NULL_HDBC, CompletionType));  
   case SQL_HANDLE_DBC:return(SQLTransact(SQL_NULL_HENV, Handle, CompletionType);  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlfetch"></a>SQLFetch  
 El Administrador de controladores se asigna a **SQLExtendedFetch** con un *FetchOrientation* argumento de SQL_FETCH_NEXT. La siguiente llamada a **SQLFetch**:  
  
```  
SQLFetch (StatementHandle);  
```  
  
 se producirá en el Administrador de controladores, que llama a **SQLExtendedFetch**, como se indica a continuación:  
  
```  
rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, &RowCount, RowStatusArray);  
```  
  
 En esta llamada, el *pcRow* argumento tiene asignado el valor que la aplicación establece el atributo de instrucción de SQL_ATTR_ROWS_FETCHED_PTR como a través de una llamada a **SQLSetStmtAttr**.  
  
> [!NOTE]  
>  Cuando la aplicación llama **SQLSetStmtAttr** para establecer SQL_ATTR_ROW_STATUS_PTR para que apunte a una matriz de estado, el Administrador de controladores, almacena en caché el puntero. *RowStatusArray* puede ser igual a un puntero nulo.  
  
 Si el controlador no admite **SQLExtendedFetch** y se carga la biblioteca de cursores, el Administrador de controladores usa la biblioteca de cursores **SQLExtendedFetch** para asignar **SQLFetch** a **SQLExtendedFetch**. Si el controlador no admite **SQLExtendedFetch** y no se carga la biblioteca de cursores, el Administrador de controladores pasa la llamada a **SQLFetch** a través del controlador. Si la aplicación llama **SQLSetStmtAttr** para establecer SQL_ATTR_ROW_STATUS_PTR, el Administrador de controladores se asegura de que se rellena la matriz. Si la aplicación llama **SQLSetStmtAttr** para establecer SQL_ATTR_ROWS_FETCHED_PTR, el Administrador de controladores establece este campo en 1.  
  
## <a name="sqlfetchscroll"></a>SQLFetchScroll  
 El Administrador de controladores se asigna a **SQLExtendedFetch**. La siguiente llamada a **SQLFetchScroll**:  
  
```  
SQLFetchScroll(StatementHandle, FetchOrientation, FetchOffset);  
```  
  
 se producirá la siguiente secuencia de pasos:  
  
1.  Cuando la aplicación llama **SQLSetStmtAttr** para establecer SQL_ATTR_ROW_STATUS_PTR (que establece el campo SQL_DESC_ARRAY_STATUS_PTR IRD) para que señale a una matriz de estado, el Administrador de controladores, almacena en caché this (puntero). Supongamos que este puntero es *RowStatusArray*; en caso contrario, deje que *RowStatusArray* ser igual a un puntero nulo. Si el *RowStatusArray* argumento es un puntero nulo, el Administrador de controladores genera una matriz de estado de fila.  
  
2.  Si *FetchOrientation* no es uno de SQL_FETCH_NEXT, SQL_FETCH_PRIOR, SQL_FETCH_ABSOLUTE, SQL_FETCH_RELATIVE, SQL_FETCH_FIRST, SQL_FETCH_LAST o SQL_FETCH_BOOKMARK, el Administrador de controladores devuelve SQL_ERROR y SQLSTATE HY106 (tipo fuera del intervalo de captura). Ninguna otra regla de esta sección se aplica.  
  
3.  Caso:  
  
-   Si *FetchOrientation* es igual a SQL_FETCH_BOOKMARK, a continuación:  
  
    -   Si **SQLSetStmtAttr** se llamó anteriormente para establecer el valor de SQL_ATTR_FETCH_BOOKMARK_PTR, a continuación, dejar que *Bmk* sea el valor obtenido mediante desreferencia el puntero SQL_DESC_FETCH_BOOKMARK_PTR.  
  
    -   En caso contrario, devolverá SQL_ERROR con SQLSTATE HY111 (valor de marcador no válido). Ninguna otra regla de esta sección se aplica.  
  
     El Administrador de controladores se llama ahora **SQLExtendedFetch**, como se indica a continuación:  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, Bmk, pcRow, RowStatusArray);  
    ```  
  
-   En caso contrario, el Administrador de controladores llama **SQLExtendedFetch**, como se indica a continuación:  
  
    ```  
    rc = SQLExtendedFetch(StatementHandle, FetchOrientation, FetchOffset, pcRow, RowStatusArray);  
    ```  
  
     En estas llamadas, la *pcRow* argumento tiene asignado el valor que la aplicación establece el atributo de instrucción de SQL_ATTR_ROWS_FETCHED_PTR como a través de una llamada a **SQLSetStmtAttr**.  
  
-   SQL_ATTR_ROW_ARRAY_SIZE se asigna a SQL_ROWSET_SIZE.  
  
-   Si *rc* es igual a SQL_SUCCESS o SQL_SUCCESS_WITH_INFO y si *FetchOrientation* es igual a SQL_FETCH_BOOKMARK y *FetchOffset* es no es igual a 0, a continuación, el controlador El administrador envía una advertencia, SQLSTATE 01S10 (intenta capturar por un desplazamiento de marcador, se omite el valor de desplazamiento) y devuelve SQL_SUCCESS_WITH_INFO.  
  
## <a name="sqlfreehandle"></a>SQLFreeHandle  
 El Administrador de controladores se asigna a **SQLFreeEnv**, **SQLFreeConnect**, o **SQLFreeStmt** según corresponda. La siguiente llamada a **SQLFreeHandle**:  
  
```  
SQLFreeHandle(HandleType, Handle);  
```  
  
 se producirá en el Administrador de controladores realiza las siguientes acciones (conceptual, ninguna comprobación de errores) asignación:  
  
```  
switch (HandleType) {  
   case SQL_HANDLE_ENV: return (SQLFreeEnv(Handle));  
   case SQL_HANDLE_DBC: return (SQLFreeConnect(Handle));  
   case SQL_HANDLE_STMT: return (SQLFreeStmt(Handle, SQL_DROP));  
   default: // return SQL_ERROR, SQLSTATE HY092 ("Invalid attribute/option identifier")  
}  
```  
  
## <a name="sqlgetconnectattr"></a>SQLGetConnectAttr  
 El Administrador de controladores se asigna a **SQLGetConnectOption**. La siguiente llamada a **SQLGetConnectAttr**:  
  
```  
SQLGetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 se producirá la siguiente secuencia de pasos:  
  
1.  Si *atributo* no es un atributo de conexión o instrucción definidos por el controlador y no es un atributo definido en ODBC 2. *x*, el Administrador de controladores devuelve SQL_ERROR con SQLSTATE HY092 (identificador de atributo u opción no válido). Ninguna otra regla en esta sección se aplica.  
  
2.  Si *atributo* es igual a SQL_ATTR_AUTO_IPD o SQL_ATTR_METADATA_ID, el Administrador de controladores, devolverá SQL_ERROR con SQLSTATE HY092 (identificador de atributo u opción no válido).  
  
3.  El Administrador de controladores realiza comprobaciones necesarias para ver si SQLSTATE 08003 (conexión no abierta) o SQLSTATE HY010 (error de secuencia de función) se debe a que se genere. Si es así, el Administrador de controladores devuelve SQL_ERROR y envía el mensaje de error adecuado. Ninguna otra regla de esta sección se aplica.  
  
4.  Las llamadas del Administrador de controladores **SQLGetConnectOption** como se indica a continuación:  
  
    ```  
    SQLGetConnectOption (ConnectionHandle, Attribute, ValuePtr);  
    ```  
  
     Tenga en cuenta que la *BufferLength* y *StringLengthPtr* se omiten.  
  
## <a name="sqlgetdata"></a>SQLGetData  
 Cuando un ODBC 3. *x* aplicación trabajar con una API ODBC 2*.x* controlador llama **SQLGetData** con el *ColumnNumber* argumento igual a 0, el 3 de ODBC*.x* el Administrador de controladores se asigna a una llamada a **SQLGetStmtOption** con el *opción* atributo establecido en SQL_GET_BOOKMARK.  
  
## <a name="sqlgetstmtattr"></a>SQLGetStmtAttr  
 El Administrador de controladores se asigna a **SQLGetStmtOption**. La siguiente llamada a **SQLGetStmtAttr**:  
  
```  
SQLGetStmtAttr(StatementHandle, Attribute, ValuePtr, BufferLength, StringLengthPtr);  
```  
  
 se producirá la siguiente secuencia de pasos:  
  
1.  Si *atributo* no es un atributo de conexión o instrucción definidos por el controlador y no es un atributo definido en ODBC 2. *x*, el Administrador de controladores devuelve SQL_ERROR con SQLSTATE HY092 (identificador de atributo u opción no válido). Ninguna otra regla en esta sección se aplica.  
  
2.  Si *atributo* es uno de los siguientes:  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_AUTO_IPD  
  
     SQL_ATTR_ROW_BIND_TYPE  
  
     SQL_ATTR_IMP_ROW_DESC  
  
     SQL_ATTR_IMP_PARAM_DESC  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PREDICATE_PTR  
  
     SQL_ATTR_PREDICATE_OCTET_LENGTH_PTR  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     el Administrador de controladores devuelve SQL_ERROR con SQLSTATE HY092 (identificador de atributo u opción no válido). Ninguna otra regla de esta sección se aplica.  
  
3.  El Administrador de controladores realiza comprobaciones necesarias para ver si SQLSTATE HY010 (error de secuencia de función) debe generarse. Si es así, el Administrador de controladores devuelve SQL_ERROR y SQLSTATE HY010 (error de secuencia de función). Ninguna otra regla de esta sección se aplica.  
  
4.  Si *atributo* es igual a SQL_ATTR_ROWS_FETCHED_PTR, la devuelve el Administrador de controladores, un puntero a la variable interna del Administrador de controladores *gallo*, que ha utilizado o va a utilizar en una llamada a  **SQLExtendedFetch**. Ninguna otra regla de esta sección se aplica.  
  
5.  Si *atributo* es igual a SQL_DESC_FETCH_BOOKMARK_PTR, el Administrador de controladores devuelve el puntero adecuado que había almacenado en memoria caché durante una llamada a **SQLSetStmtAttr**.  
  
6.  Si *atributo* es igual a SQL_ATTR_ROW_STATUS_PTR, el Administrador de controladores devuelve el puntero adecuado que había almacenado en memoria caché durante una llamada a **SQLSetStmtAttr**.  
  
7.  Las llamadas del Administrador de controladores **SQLGetStmtOption** como se indica a continuación:  
  
    ```  
    SQLGetStmtOption (hstmt, fOption, pvParam);  
    ```  
  
     donde *hstmt*, *fOption*, y *pvParam* se establecerá en los valores de *StatementHandle*, *atributo*, y *ValuePtr*, respectivamente. El *BufferLength* y *StringLengthPtr* se omiten.  
  
## <a name="sqlsetconnectattr"></a>SQLSetConnectAttr  
 El Administrador de controladores se asigna a **SQLSetConnectOption**. La siguiente llamada a **SQLSetConnectAttr**:  
  
```  
SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, StringLength);  
```  
  
 se producirá la siguiente secuencia de pasos:  
  
1.  Si *atributo* no es un atributo de conexión o instrucción definidos por el controlador y no es un atributo definido en ODBC 2. *x*, el Administrador de controladores devuelve SQL_ERROR con SQLSTATE HY092 (identificador de atributo u opción no válido). Ninguna otra regla en esta sección se aplica.  
  
2.  Si *atributo* es igual a SQL_ATTR_AUTO_IPD, el Administrador de controladores, devolverá SQL_ERROR con SQLSTATE HY092 (identificador de atributo u opción no válido).  
  
3.  El Administrador de controladores realiza comprobaciones necesarias para ver si SQLSTATE 08003 (conexión no abierta) o SQLSTATE HY010 necesidad (error de secuencia de función) que se genere. Si uno de estos errores debe generarse, el Administrador de controladores devuelve SQL_ERROR y envía el mensaje de error adecuado. Ninguna otra regla de esta sección se aplica.  
  
4.  Las llamadas del Administrador de controladores **SQLSetConnectOption** como se indica a continuación:  
  
    ```  
    SQLSetConnectOption (hdbc, fOption, vParam);  
    ```  
  
     donde *hdbc*, *fOption*, y *vParam* se establecerá en los valores de *IdentificadorConexión*, *atributo*, y *ValuePtr*, respectivamente. *StringLengthPtr* se omite.  
  
> [!NOTE]  
>  La capacidad de establecer los atributos de instrucción en el nivel de conexión está en desuso. Atributos de instrucción nunca se deben establecer en el nivel de conexión por una aplicación ODBC 3. *x* aplicación.  
  
## <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 El Administrador de controladores se asigna a **SQLSetStmtOption**. La siguiente llamada a **SQLSetStmtAttr**:  
  
```  
SQLSetStmtAttr(StatementHandle, Attribute, ValuePtr, StringLength);  
```  
  
 se producirá la siguiente secuencia de pasos:  
  
1.  Si *atributo* no es un atributo de conexión o instrucción definidos por el controlador y no es un atributo definido en ODBC 2. *x*, el Administrador de controladores devuelve SQL_ERROR con SQLSTATE HY092 (identificador de atributo u opción no válido). Ninguna otra regla en esta sección se aplica.  
  
2.  Si *atributo* es uno de los siguientes:  
  
     SQL_ATTR_APP_ROW_DESC  
  
     SQL_ATTR_APP_PARAM_DESC  
  
     SQL_ATTR_AUTO_IPD  
  
     SQL_ATTR_ROW_BIND_TYPE  
  
     SQL_ATTR_IMP_ROW_DESC  
  
     SQL_ATTR_IMP_PARAM_DESC  
  
     SQL_ATTR_METADATA_ID  
  
     SQL_ATTR_PARAM_BIND_TYPE  
  
     SQL_ATTR_PREDICATE_PTR  
  
     SQL_ATTR_PREDICATE_OCTET_LENGTH_PTR  
  
     SQL_ATTR_PARAM_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_BIND_OFFSET_PTR  
  
     SQL_ATTR_ROW_OPERATION_PTR  
  
     SQL_ATTR_PARAM_OPERATION_PTR  
  
     el Administrador de controladores devuelve SQL_ERROR con SQLSTATE HY092 (identificador de atributo u opción no válido). Ninguna otra regla de esta sección se aplica.  
  
3.  El Administrador de controladores lleva a cabo los controles necesarios para ver si SQLSTATE HY010 (error de secuencia de función) necesita que se genere. Si es así, el Administrador de controladores devuelve SQL_ERROR y SQLSTATE HY010 (error de secuencia de función). Ninguna otra regla de esta sección se aplica.  
  
4.  Si *atributo* es igual a SQL_ATTR_PARAMSET_SIZE o SQL_ATTR_PARAMS_PROCESSED_PTR, vea la sección "Asignaciones de control de matrices de parámetros," más adelante en este tema. Ninguna otra regla de esta sección se aplica.  
  
5.  Si *atributo* es igual a SQL_ATTR_ROWS_FETCHED_PTR, las cachés de administrador de controladores, el puntero de valor para su uso posterior con **SQLFetchScroll**.  
  
6.  Si *atributo* es igual a SQL_ATTR_ROW_STATUS_PTR, las cachés de administrador de controladores, el puntero de valor para su uso posterior con **SQLFetchScroll** o **SQLSetPos**. Ninguna otra regla de esta sección se aplica.  
  
7.  Si *atributo* es igual a SQL_ATTR_FETCH_BOOKMARK_PTR, el Administrador de controladores, las memorias caché *ValuePtr* y utilizará el valor almacenado en caché más adelante en una llamada a **SQLFetchScroll**. Ninguna otra regla de esta sección se aplica.  
  
8.  Las llamadas del Administrador de controladores **SQLSetStmtOption** como se indica a continuación:  
  
    ```  
    SQLSetStmtOption (hstmt, fOption, vParam);  
    ```  
  
     donde *hstmt*, *fOption*, y *vParam* se establecerá en los valores de *StatementHandle*, *atributo*, y *ValuePtr*, respectivamente. El *StringLength* argumento se omite.  
  
     Si está un ODBC 2. *x* controlador admite opciones de la instrucción de cadena de caracteres, específica del controlador, una aplicación ODBC 3. *x* aplicación debe llamar a **SQLSetStmtOption** para establecer las opciones.  
  
## <a name="mappings-for-handling-parameter-arrays"></a>Asignaciones para el tratamiento de matrices de parámetros  
 Cuando llama a la aplicación:  
  
```  
SQLSetStmtAttr (StatementHandle, SQL_ATTR_PARAMSET_SIZE, Size, StringLength);  
```  
  
 las llamadas del Administrador de controladores:  
  
```  
SQLParamOptions (StatementHandle, Size, &RowCount);  
```  
  
 El Administrador de controladores posteriormente devuelve un puntero a esta variable cuando la aplicación llama **SQLGetStmtAttr** para recuperar SQL_ATTR_PARAMS_PROCESSED_PTR. El Administrador de controladores no se puede cambiar esta variable interna hasta que se devuelva el identificador de instrucción en el estado preparado o asignado.  
  
 Un ODBC 3. *x* aplicación puede llamar a **SQLGetStmtAttr** para obtener el valor de SQL_ATTR_PARAMS_PROCESSED_PTR aunque no establecido explícitamente el campo SQL_DESC_ARRAY_SIZE en el APD. Esta situación puede ocurrir, por ejemplo, si la aplicación tiene una rutina genérica que busca "row" de parámetros actual procesando cuando **SQLExecute** devuelve SQL_NEED_DATA. Esta rutina se invoca si o no la SQL_DESC_ARRAY_SIZE es 1 o es mayor que 1. Para tener en cuenta para esto, el Administrador de controladores tendrá que definir esta variable interna si o no la aplicación ha llamado **SQLSetStmtAttr** para establecer el campo SQL_DESC_ARRAY_SIZE en APD. Si no se ha establecido SQL_DESC_ARRAY_SIZE, el Administrador de controladores tiene que asegurarse de que esta variable contiene el valor 1 antes de devolver desde **SQLExecDirect** o **SQLExecute**.  
  
## <a name="error-handling"></a>Tratamiento de errores  
 En ODBC 3. *x*, si se llama **SQLFetch** o **SQLFetchScroll** rellena el SQL_DESC_ARRAY_STATUS_PTR en IRD y el campo SQL_DIAG_ROW_NUMBER de un determinado registro de diagnóstico contiene el número de la fila del conjunto de filas que pertenece este registro a. Con esto, la aplicación puede correlacionar un mensaje de error con una posición de fila determinada.  
  
 Un ODBC 2. *x* controlador no podrá proporcionar esta funcionalidad. Sin embargo, proporcionará demarcación de error con SQLSTATE 01S01 (Error en la fila). Un ODBC 3. *x* aplicación que esté utilizando **SQLFetch** o **SQLFetchScroll** al ir en una API ODBC 2. *x* controlador debe tener en cuenta este hecho. Tenga en cuenta también que este tipo de aplicación se podrá llamar a **SQLGetDiagField** realmente obtener el campo SQL_DIAG_ROW_NUMBER de todos modos. Un ODBC 3. *x* aplicación trabajar con una API ODBC 2. *x* controlador podrá llamar a **SQLGetDiagField** sólo con una *DiagIdentifier* argumento de SQL_DIAG_MESSAGE_TEXT, SQL_DIAG_NATIVE, SQL_DIAG_RETURNCODE o SQL_DIAG_ SQLSTATE. ODBC 3*.x* el Administrador de controladores mantiene la estructura de datos de diagnóstico cuando se trabaja con una API ODBC 2. *x* controlador, pero la API ODBC 2. *x* controlador devuelve solo estos cuatro campos.  
  
 Cuando un ODBC 2. *x* aplicación está trabajando con una API ODBC 2. *x* controlador, si una operación puede producir varios errores devolverá por el Administrador de controladores, errores diferentes pueden devolver ODBC 3*.x* Administrador de controladores que mediante la API ODBC 2. *x* el Administrador de controladores.  
  
## <a name="mappings-for-bookmark-operations"></a>Asignaciones para las operaciones de marcador  
 ODBC 3*.x* el Administrador de controladores realiza las siguientes asignaciones cuando una aplicación ODBC 3. *x* aplicación trabajar con una API ODBC 2. *x* controlador realiza operaciones de marcador.  
  
### <a name="sqlbindcol"></a>SQLBindCol  
 Cuando un ODBC 3. *x* aplicación trabajar con una API ODBC 2. *x* controlador llama **SQLBindCol** para enlazar a la columna 0 con *fCType* igual a SQL_C_VARBOOKMARK, ODBC 3*.x* comprueba el Administrador de controladores Si el *BufferLength* argumento es menor que 4 o mayor que 4 y si es así, devuelve SQLSTATE HY090 (longitud de búfer o cadena no válida). Si el *BufferLength* argumento es igual a 4, el Administrador de controladores llama **SQLBindCol** en el controlador, después de reemplazar *fCType* con SQL_C_BOOKMARK.  
  
### <a name="sqlcolattribute"></a>SQLColAttribute  
 Cuando un ODBC 3. *x* aplicación trabajar con una API ODBC 2. *x* controlador llama **SQLColAttribute** con el *ColumnNumber* argumento se establece en 0, el Administrador de controladores devuelve el *FieldIdentifier* valores se muestran en la tabla siguiente.  
  
|*FieldIdentifier*|Value|  
|-----------------------|-----------|  
|SQL_DESC_AUTO_UNIQUE_VALUE|SQL_FALSE|  
|SQL_DESC_CASE_SENSITIVE|SQL_FALSE|  
|SQL_DESC_CATALOG_NAME|"" (cadena vacía)|  
|SQL_DESC_CONCISE_TYPE|SQL_BINARY|  
|SQL_DESC_COUNT|El mismo valor devuelto por **SQLNumResultCols**|  
|SQL_DESC_DATETIME_INTERVAL_CODE|0|  
|SQL_DESC_DISPLAY_SIZE|8|  
|SQL_DESC_FIXED_PREC_SCALE|SQL_FALSE|  
|SQL_DESC_LABEL|"" (cadena vacía)|  
|SQL_DESC_LENGTH|0|  
|SQL_DESC_LITERAL_PREFIX|"" (cadena vacía)|  
|SQL_DESC_LITERAL_SUFFIX|"" (cadena vacía)|  
|SQL_DESC_LOCAL_TYPE_NAME|"" (cadena vacía)|  
|SQL_DESC_NAME|"" (cadena vacía)|  
|SQL_DESC_NULLABLE|SQL_NO_NULLS|  
|SQL_DESC_OCTET_LENGTH|4|  
|SQL_DESC_PRECISION|4|  
|SQL_DESC_SCALE|0|  
|SQL_DESC_SCHEMA_NAME|"" (cadena vacía)|  
|SQL_DESC_SEARCHABLE|SQL_PRED_NONE|  
|SQL_DESC_TABLE_NAME|"" (cadena vacía)|  
|SQL_DESC_TYPE|SQL_BINARY|  
|SQL_DESC_TYPE_NAME|"" (cadena vacía)|  
|SQL_DESC_UNNAMED|SQL_UNNAMED|  
|SQL_DESC_UNSIGNED|SQL_FALSE|  
|SQL_DESC_UPDATEABLE|SQL_ATTR_READ_ONLY|  
  
### <a name="sqldescribecol"></a>SQLDescribeCol  
 Cuando un ODBC 3. *x* aplicación trabajar con una API ODBC 2. *x* controlador llama **SQLDescribeCol** con el *ColumnNumber* argumento establecido en 0, el Administrador de controladores devuelve los valores enumerados en la tabla siguiente.  
  
|Búfer|Value|  
|------------|-----------|  
|ColumnName|"" (cadena vacía)|  
|* NameLengthPtr|0|  
|* DataTypePtr|SQL_BINARY|  
|* ColumnSizePtr|4|  
|* DecimalDigitsPtr|0|  
|* NullablePtr|SQL_NO_NULLS|  
  
### <a name="sqlgetdata"></a>SQLGetData  
 Cuando un ODBC 3. *x* aplicación trabajar con una API ODBC 2. *x* controlador realiza la llamada siguiente a **SQLGetData** para recuperar un marcador:  
  
```  
SQLGetData(StatementHandle, 0, SQL_C_VARBOOKMARK, TargetValuePtr, BufferLength, StrLen_or_IndPtr)  
```  
  
 la llamada se asigna a **SQLGetStmtOption** con una *fOption* de SQL_GET_BOOKMARK, como se indica a continuación:  
  
```  
SQLGetStmtOption(hstmt, SQL_GET_BOOKMARK, TargetValuePtr)  
```  
  
 donde *hstmt* y *pvParam* se establecen en los valores de *StatementHandle* y *TargetValuePtr*, respectivamente. El marcador se devuelve en el búfer señalado por el *pvParam* (*TargetValuePtr*) argumento. El valor en el búfer que señala el *StrLen_or_IndPtr* argumento en la llamada a **SQLGetData** se establece en 4.  
  
 Esta asignación es necesaria para tener en cuenta el caso en el que **SQLFetch** se llamó antes de la llamada a **SQLGetData** y la API ODBC 2. *x* controlador no admitía **SQLExtendedFetch**. En este caso, **SQLFetch** luego se pasarían a través de la API ODBC 2. *x* controlador, en el que no se admite la recuperación de marcador mayúsculas.  
  
 **SQLGetData** no se puede llamar varias veces en una API ODBC 2. *x* controlador que recupere un marcador en partes, por lo que una llamada a **SQLGetData** con el *BufferLength* establecido en un valor inferior a 4 y la *ColumnNumber*argumento establecido en 0 devolverá SQLSTATE HY090 (longitud de búfer o cadena no válida). **SQLGetData** , sin embargo, puede llamar varias veces para recuperar el mismo marcador.  
  
### <a name="sqlsetstmtattr"></a>SQLSetStmtAttr  
 Cuando un ODBC 3. *x* aplicación trabajar con una API ODBC 2. *x* controlador llama **SQLSetStmtAttr** para establecer el atributo SQL_ATTR_USE_BOOKMARKS en SQL_UB_VARIABLE, el Administrador de controladores define el atributo SQL_UB_ON en subyacente ODBC 2. *x* controlador.
