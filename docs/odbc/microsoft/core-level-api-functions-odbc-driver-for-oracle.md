---
title: Principales funciones de nivel de API (controlador ODBC para Oracle) | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: ead4e816049f6dcce6bfc560a60d8f8bafa9d61c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47724693"
---
# <a name="core-level-api-functions-odbc-driver-for-oracle"></a>Funciones de API de nivel de núcleo (controlador ODBC para Oracle)
> [!IMPORTANT]  
>  Esta característica se quitará en una versión futura de Windows. Evite utilizar esta característica en nuevos trabajos de desarrollo y tenga previsto modificar las aplicaciones que actualmente la utilizan. En su lugar, use el controlador ODBC proporcionado por Oracle.  
  
 Las funciones en este nivel constituyen el nivel mínimo de cumplimiento de la interfaz para los controladores ODBC.  
  
|Función de la API|Notas|  
|------------------|-----------|  
|**SQLAllocConnect**|Asigna memoria para un identificador de conexión, *hdbc*, dentro del entorno identificado por *henv*. El Administrador de controladores se procesa esta llamada y se llama al controlador **SQLAllocConnect** cada vez que la función **SQLConnect**, **SQLBrowseConnect**, o  **SQLDriverConnect** se llama.|  
|**SQLAllocEnv**|Muestra un cuadro de diálogo especificar el requisito de software de cliente de Oracle y, a continuación, devuelve SQL_NULL_HANDLE. Si no está instalado el software cliente de Oracle, esta función asigna memoria para un identificador de entorno, *henv*e inicializa la interfaz de nivel de llamada ODBC para su uso por una aplicación.|  
|**SQLAllocStmt**|Asigna memoria para un identificador de instrucción y asocia el identificador de instrucción con la conexión especificada por hdbc. El Administrador de controladores pasa esta llamada al controlador, que asigna la memoria para la estructura hstmt.|  
|**SQLBindCol**|Se asigna espacio de almacenamiento para una columna de resultados y especifica el tipo del resultado.|  
|**SQLCancel**|Cancela el procesamiento en un identificador de instrucción hstmt. En algunos casos, Oracle no admite la cancelación de una instrucción de ejecución. Esto significa que una instrucción que se ejecuta, continuarán hasta que Oracle completa el proceso, momento en el que se cancelan los resultados de las instrucciones por el controlador ODBC para Oracle.|  
|**SQLColAttributes**|Devuelve información del descriptor para una columna de un conjunto de resultados. Información del descriptor se devuelve como una cadena de caracteres, un valor dependiente del descriptor de 32 bits o un valor entero.|  
|**SQLConnect**|Se conecta a un origen de datos. Para utilizar autenticación de sistema operativo de Oracle, especifique "/" como el *szUID* parámetro y "" como el *szAuthStr* parámetro.|  
|**SQLDescribeCol**|Devuelve el nombre de tipo, precisión, escala y la nulabilidad de la columna de resultados determinado. **Nota:****SQLDescribeCol** informa de las columnas calculadas como SQL_VARCHAR.  |  
|**SQLDisconnect**|Cierra una conexión. Si está habilitada la agrupación de conexiones para un entorno compartido y una aplicación llama a **SQLDisconnect** en una conexión en ese entorno, la conexión se devuelve al grupo de conexiones y sigue estando disponible para otros componentes mediante el mismo entorno compartido.|  
|**SQLError**|Devuelve información de estado o de error sobre el último error. El controlador mantiene una pila o una lista de errores que se pueden devolver para el *hstmt*, *hdbc*, y *henv* argumentos, dependiendo de cómo la llamada a **SQLError**  se realiza. La cola de errores se vacíe después de cada instrucción. Normalmente recupera un mensaje de error de Oracle y en caso contrario, está vacío.|  
|**SQLExecDirect**|Ejecuta una instrucción SQL nueva y no preparada. El controlador utiliza los valores actuales de las variables de marcador de parámetro, si existe algún parámetro en la instrucción. Si la tabla, vista o los nombres de campo contienen espacios, encierre los nombres de retroceso oferta marcas. Por ejemplo, si la base de datos contiene una tabla denominada *mi tabla* y el campo *mi campo*, incluya cada elemento del identificador de este modo:<br /><br /> Seleccione \`mi tabla\`. \`Mi Field1\`, \`Mi tabla\`.\` Mi Field2\` FROM \`mi tabla "|  
|**SQLExecute**|Ejecuta una instrucción SQL preparada (una instrucción ya preparada por **SQLPrepare**). El controlador utiliza los valores actuales de las variables de marcador de parámetro, si existe algún parámetro en la instrucción.|  
|**SQLFetch**|Recupera una fila de un conjunto de resultados en las ubicaciones especificadas por las llamadas anteriores a **SQLBindCol**. El controlador se prepara para una llamada a **SQLGetData** para las columnas sin enlazar.|  
|**SQLFreeConnect**|Libera un identificador de conexión y libera toda la memoria asignada para el identificador.|  
|**SQLFreeEnv**|El controlador ODBC para Oracle se cierra y libera toda la memoria asociada con el controlador.|  
|**SQLFreeStmt**|Detiene el procesamiento asociado con un hstmt específico, cierra cualquier cursor abierto asociado con el identificador hstmt, descarta los resultados pendientes y, opcionalmente, libera todos los recursos asociados con el identificador de instrucción.|  
|**SQLGetCursorName**|Devuelve el nombre del cursor asociado con el hstmt determinado.|  
|**SQLNumResultCols**|Devuelve el número de columnas en un cursor de conjunto de resultados.|  
|**SQLPrepare**|Prepara una instrucción SQL mediante la planeación de optimizar y ejecute la instrucción. La instrucción SQL se compila para ejecutarse en **SQLExecDirect**.<br /><br /> Si la tabla, vista o los nombres de campo contienen espacios, encierre los nombres de retroceso oferta marcas. Por ejemplo, si la base de datos contiene una tabla denominada *mi tabla* y el campo *mi campo*, incluya cada elemento del identificador como sigue:<br /><br /> Seleccione \`mi tabla\`.\` Mi campo\` FROM \`mi tabla "<br /><br /> Para obtener información sobre el uso de conjuntos de resultados que contienen matrices de parámetros formales, consulte [devolver los parámetros de matriz de los procedimientos almacenados](../../odbc/microsoft/returning-array-parameters-from-stored-procedures.md).|  
|**SQLRowCount**|Oracle no proporciona una manera de determinar el número de filas en un conjunto de resultados hasta después de capturar la última fila, por lo que devuelve – 1.|  
|**SQLSetCursorName**|Asocia un nombre de cursor con un identificador de instrucción activa *hstmt*.|  
|**SQLSetParam**|Reemplazado por SQLBindParameter de ODBC 2. *x*.|  
|**SQLTransact**|Solicita una operación de confirmación o reversión para todas las operaciones activas en todos los identificadores de instrucciones (hstmts) asociados a una conexión o para todas las conexiones asociadas con el identificador del entorno, *henv*. Si se produce un error en una confirmación en el modo manual, la transacción permanece activa; puede revertir la transacción o volver a intentar la operación de confirmación. Si se produce un error en una operación de confirmación cuando está en modo de transacción automática, la transacción se revierte automáticamente; la transacción no puede estar inactiva.|
