---
title: Principales funciones de API de nivel (controlador ODBC para Oracle) | Documentos de Microsoft
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
ms.topic: conceptual
helpviewer_keywords:
- functions [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], functions
- core level API functions [ODBC]
- ODBC core level API functions [ODBC]
ms.assetid: 8596eed7-bda6-4cac-ae1f-efde1aab785f
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a13402af87e10475f988523f26a0012ff3f1936a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="core-level-api-functions-odbc-driver-for-oracle"></a>Funciones de API de nivel de núcleo (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, utilice el controlador ODBC proporcionado por Oracle.  
  
 Funciones en este nivel constituyen el nivel mínimo de conformidad de interfaz para los controladores ODBC.  
  
|Función de la API|Notas|  
|------------------|-----------|  
|**SQLAllocConnect**|Asigna memoria para un identificador de conexión, *hdbc*, dentro del entorno identificado por *henv*. El Administrador de controladores procesa esta llamada y llama al controlador **SQLAllocConnect** cada vez que la función **SQLConnect**, **SQLBrowseConnect**, o  **SQLDriverConnect** se llama.|  
|**SQLAllocEnv**|Muestra un cuadro de diálogo especificar los requisitos de software de cliente de Oracle y, a continuación, devuelve SQL_NULL_HANDLE. Si no está instalado el software cliente de Oracle, esta función asigna memoria para un identificador de entorno, *henv*e inicializa la interfaz de nivel de llamada ODBC para su uso por una aplicación.|  
|**SQLAllocStmt**|Asigna memoria para un identificador de instrucción y asocia el identificador de instrucción con la conexión especificada por hdbc. El Administrador de controladores pasa esta llamada al controlador, lo que le asigna memoria para la estructura de hstmt.|  
|**SQLBindCol**|Asigna espacio de almacenamiento para una columna de resultados y especifica el tipo del resultado.|  
|**SQLCancel**|Cancela el procesamiento en un identificador de instrucción, hstmt. En algunos casos, Oracle no admite la cancelación de una instrucción de ejecución. Esto significa que una instrucción de ejecución continuará hasta que Oracle completa el proceso, momento en el que se cancelan los resultados de las instrucciones por el controlador ODBC para Oracle.|  
|**SQLColAttributes**|Devuelve información del descriptor para una columna de un conjunto de resultados. Información del descriptor se devuelve como una cadena de caracteres, un valor de dependiente de descriptor de 32 bits o un valor entero.|  
|**SQLConnect**|Se conecta a un origen de datos. Para usar la autenticación de sistema operativo de Oracle, especifique "/" como el *szUID* parámetro y "" como el *szAuthStr* parámetro.|  
|**SQLDescribeCol**|Devuelve el nombre, el tipo, la precisión, la escala y la nulabilidad de la columna de resultados determinado. **Nota:****SQLDescribeCol** informa de las columnas calculadas como SQL_VARCHAR.|  
|**SQLDisconnect**|Cierra una conexión. Si la agrupación de conexiones está habilitada para un entorno compartido y llama a una aplicación **SQLDisconnect** en una conexión en el entorno, la conexión se devuelve al grupo de conexiones y sigue estando disponible para otros componentes por medio el mismo entorno compartido.|  
|**SQLError**|Devuelve información de estado o de error sobre el último error. El controlador mantiene una pila o una lista de errores que se pueden devolver para la *hstmt*, *hdbc*, y *henv* argumentos, dependiendo de cómo la llamada a **SQLError**  se realiza. La cola de errores se vacía después de cada instrucción. Normalmente recupera un mensaje de error de Oracle y en caso contrario, está vacío.|  
|**SQLExecDirect**|Ejecuta una instrucción SQL nueva, no preparada. El controlador utiliza los valores actuales de las variables de marcador de parámetro, si existe algún parámetro en la instrucción. Si la tabla, vista o nombres de campo contienen espacios, encierre los nombres en la parte posterior oferta marcas. Por ejemplo, si la base de datos contiene una tabla denominada *mi tabla* y el campo *mi campo*, incluya cada elemento del identificador de este modo:<br /><br /> Seleccione \`mi tabla\`. \`Mi Field1\`, \`Mi tabla\`.\` Mi Field2\` FROM \`la tabla '|  
|**SQLExecute**|Ejecuta una instrucción SQL preparada (una instrucción ya preparada por **SQLPrepare**). El controlador utiliza los valores actuales de las variables de marcador de parámetro, si existe algún parámetro en la instrucción.|  
|**SQLFetch**|Recupera una fila de un conjunto de resultados en las ubicaciones especificadas por las llamadas anteriores a **SQLBindCol**. El controlador se prepara para una llamada a **SQLGetData** para las columnas sin enlazar.|  
|**SQLFreeConnect**|Libera un identificador de conexión y libera toda la memoria asignada para el identificador.|  
|**SQLFreeEnv**|Cierra el controlador ODBC para Oracle y libera toda la memoria asociada con el controlador.|  
|**SQLFreeStmt**|Detiene el procesamiento asociado a un hstmt específico, se cierra cualquier cursor abierto asociado con el identificador hstmt, descarta los resultados pendientes y, opcionalmente, libera todos los recursos asociados con el identificador de instrucción.|  
|**SQLGetCursorName**|Devuelve el nombre del cursor asociado con el identificador hstmt determinado.|  
|**SQLNumResultCols**|Devuelve el número de columnas en un cursor de conjunto de resultados.|  
|**SQLPrepare**|Prepara una instrucción SQL mediante la planeación de optimizar y ejecute la instrucción. Se compila la instrucción SQL para la ejecución mediante **SQLExecDirect**.<br /><br /> Si la tabla, vista o nombres de campo contienen espacios, encierre los nombres en la parte posterior oferta marcas. Por ejemplo, si la base de datos contiene una tabla denominada *mi tabla* y el campo *mi campo*, incluya cada elemento del identificador como sigue:<br /><br /> Seleccione \`mi tabla\`.\` Mi campo\` FROM \`la tabla '<br /><br /> Para obtener información sobre el uso de conjuntos de resultados que contengan matrices como parámetros formales, consulte [devolver los parámetros de matriz de procedimientos almacenados](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md).|  
|**SQLRowCount**|Oracle no proporciona una manera de determinar el número de filas de un conjunto de resultados hasta después de capturar la última fila, por lo que devuelve – 1.|  
|**SQLSetCursorName**|Asocia un nombre de cursor con un identificador de instrucción activa, *hstmt*.|  
|**SQLSetParam**|Reemplazado por SQLBindParameter en ODBC 2. *x*.|  
|**SQLTransact**|Solicita una operación de confirmación o reversión para todas las operaciones activas en todos los identificadores de instrucciones (hstmts) asociados a una conexión o para todas las conexiones asociadas con el identificador de entorno, *henv*. Si se produce un error en una confirmación en el modo manual, la transacción permanece activa; puede revertir la transacción o vuelva a intentar la operación de confirmación. Si se produce un error en una operación de confirmación cuando está en modo de transacción automática, la transacción se revierte automáticamente; la transacción no puede estar inactiva.|
