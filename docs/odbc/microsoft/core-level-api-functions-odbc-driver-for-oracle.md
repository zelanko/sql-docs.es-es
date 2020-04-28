---
title: Funciones de la API de nivel básico (controlador ODBC para Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- core level API functions [ODBC]
- ODBC core level API functions [ODBC]
ms.assetid: 8596eed7-bda6-4cac-ae1f-efde1aab785f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 19751bb6d0556b117d0a73967d4db00c408733ac
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/27/2020
ms.locfileid: "81281025"
---
# <a name="core-level-api-functions-odbc-driver-for-oracle"></a>Funciones de API de nivel de núcleo (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Las funciones de este nivel comprenden el nivel mínimo de cumplimiento de la interfaz para los controladores ODBC.  
  
|Función de API|Notas|  
|------------------|-----------|  
|**SQLAllocConnect**|Asigna memoria para un identificador de conexión, *hdbc*, dentro del entorno identificado por *HENV*. El administrador de controladores procesa esta llamada y llama a la función **SQLAllocConnect** del controlador cada vez que se llama a **SQLConnect**, **SQLBrowseConnect**o **SQLDriverConnect** .|  
|**SQLAllocEnv**|Muestra un cuadro de diálogo que especifica el requisito del software cliente de Oracle y, a continuación, devuelve SQL_NULL_HANDLE. Si el software cliente de Oracle no está instalado, esta función asigna memoria para un identificador de entorno, *HENV*, e inicializa la interfaz de nivel de llamada ODBC para que la use una aplicación.|  
|**SQLAllocStmt**|Asigna memoria para un identificador de instrucción y asocia el identificador de instrucción a la conexión especificada por hdbc. El administrador de controladores pasa esta llamada al controlador, que asigna la memoria para la estructura hstmt.|  
|**SQLBindCol**|Asigna espacio de almacenamiento para una columna de resultados y especifica el tipo del resultado.|  
|**SQLCancel**|Cancela el procesamiento de un identificador de instrucción, hstmt. En algunos casos, Oracle no permite la cancelación de una instrucción en ejecución. Esto significa que una instrucción en ejecución continuará hasta que Oracle complete el proceso, momento en el que el controlador ODBC para Oracle cancela los resultados de las instrucciones.|  
|**SQLColAttributes**|Devuelve información del descriptor de una columna de un conjunto de resultados. La información del descriptor se devuelve como una cadena de caracteres, un valor dependiente del descriptor de 32 bits o un valor entero.|  
|**SQLConnect**|Se conecta a un origen de datos. Para usar la autenticación del sistema operativo de Oracle, especifique "/" como el parámetro *szUID* y "" como el parámetro *szAuthStr* .|  
|**SQLDescribeCol**|Devuelve el nombre, el tipo, la precisión, la escala y la nulabilidad de la columna de resultados especificada. **Nota: SQLDescribeCol** informa de las columnas calculadas como SQL_VARCHAR.|  
|**SQLDisconnect**|Cierra una conexión. Si la agrupación de conexiones está habilitada para un entorno compartido y una aplicación llama a **SQLDisconnect** en una conexión de ese entorno, la conexión se devuelve al grupo de conexiones y sigue estando disponible para otros componentes que usen el mismo entorno compartido.|  
|**SQLError**|Devuelve información de error o de estado sobre el último error. El controlador mantiene una pila o lista de errores que se pueden devolver para los argumentos *hstmt*, *hdbc*y *HENV* , en función de cómo se realice la llamada a **SQLError** . La cola de errores se vacía después de cada instrucción. Normalmente recupera un mensaje de error de Oracle y, de lo contrario, está vacío.|  
|**SQLExecDirect**|Ejecuta una nueva instrucción SQL no preparada. El controlador utiliza los valores actuales de las variables de marcador de parámetro si existe algún parámetro en la instrucción. Si los nombres de tabla, vista o campo contienen espacios, incluya los nombres entre comillas tipográficas. Por ejemplo, si la base de datos contiene una tabla denominada *mi tabla* y el campo *mi campo*, incluya cada elemento del identificador de la manera siguiente:<br /><br /> Seleccione \`mi tabla\`. \`Mi Campo1\`,; \`Mi tabla\`. \`Mi Campo2\` de \`mi tabla\`|  
|**SQLExecute**|Ejecuta una instrucción SQL preparada (una instrucción ya preparada por **SQLPrepare**). El controlador utiliza los valores actuales de las variables de marcador de parámetro si existe algún parámetro en la instrucción.|  
|**SQLFetch**|Recupera una fila de un conjunto de resultados en las ubicaciones especificadas por las llamadas anteriores a **SQLBindCol**. Prepara el controlador para una llamada a **SQLGetData** para las columnas sin enlazar.|  
|**SQLFreeConnect**|Libera un identificador de conexión y libera toda la memoria asignada para el identificador.|  
|**SQLFreeEnv**|Cierra el controlador ODBC para Oracle y libera toda la memoria asociada al controlador.|  
|**SQLFreeStmt**|Detiene el procesamiento asociado a un hstmt específico, cierra cualquier cursor abierto asociado a hstmt, descarta los resultados pendientes y, de forma opcional, libera todos los recursos asociados al identificador de instrucción.|  
|**SQLGetCursorName**|Devuelve el nombre del cursor asociado al hstmt especificado.|  
|**SQLNumResultCols**|Devuelve el número de columnas de un cursor de conjunto de resultados.|  
|**SQLPrepare**|Prepara una instrucción SQL planeando cómo optimizar y ejecutar la instrucción. La instrucción SQL se compila para su ejecución mediante **SQLExecDirect**.<br /><br /> Si los nombres de tabla, vista o campo contienen espacios, incluya los nombres entre comillas tipográficas. Por ejemplo, si la base de datos contiene una tabla denominada *My Table* y *el campo Field, incluya*cada elemento del identificador de la manera siguiente:<br /><br /> Seleccione \`mi tabla\`. \`Mi campo\` de \`la tabla\`<br /><br /> Para obtener información sobre el uso de conjuntos de resultados que contienen matrices como parámetros formales, vea [devolver parámetros de matriz a partir de procedimientos almacenados](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md).|  
|**SQLRowCount**|Oracle no proporciona una manera de determinar el número de filas de un conjunto de resultados hasta que se obtiene la última fila, de modo que devuelve-1.|  
|**SQLSetCursorName**|Asocia un nombre de cursor a un identificador de instrucción activo, *hstmt*.|  
|**SQLSetParam**|Se reemplaza por SQLBindParameter en ODBC 2. *x*.|  
|**SQLTransact**|Solicita una operación de confirmación o reversión para todas las operaciones activas en todos los identificadores de instrucciones (hstmts) asociados a una conexión, o para todas las conexiones asociadas al identificador de entorno, *HENV*. Si se produce un error en una confirmación en el modo manual, la transacción permanece activa; puede optar por revertir la transacción o volver a intentar la operación de confirmación. Si se produce un error en una operación de confirmación en el modo de transacción automática, la transacción se revierte automáticamente. la transacción no puede estar inactiva.|
