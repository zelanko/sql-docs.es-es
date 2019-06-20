---
title: Cumplimiento de la interfaz de núcleo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- core-level interface conformance levels [ODBC]
ms.assetid: aaaa864a-6477-45ff-a50a-96d8db66a252
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e41d71cd3651e1db5d1a533159012b645b8c7764
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/15/2019
ms.locfileid: "63043769"
---
# <a name="core-interface-conformance"></a>Conformidad de interfaz de núcleo
Todos los controladores ODBC deben presentar como nivel básico al menos cumplimiento de la interfaz. Dado que las características en el nivel de núcleo son las necesarias en aplicaciones interoperables más genéricas, el controlador puede trabajar con dichas aplicaciones. Las características en el nivel de núcleo también corresponden a las características definidas en la especificación ISO CLI y a las características no opcionales definidas en la especificación de CLI de grupo abierto. Un controlador ODBC de función de la interfaz de nivel básico permite a la aplicación hacerlo siguiente:  
  
-   Asignar y liberar todos los tipos de identificadores, mediante una llamada a **SQLAllocHandle** y **SQLFreeHandle**.  
  
-   Usar todas las formas de la **SQLFreeStmt** función.  
  
-   Enlazar columnas del conjunto de resultados, mediante una llamada a **SQLBindCol**.  
  
-   Controlar los parámetros dinámicos, incluidas las matrices de parámetros, en la dirección de entrada solo, mediante una llamada a **SQLBindParameter** y **SQLNumParams**. (Los parámetros en la dirección de salida son características 203 en [cumplimiento de la interfaz de nivel 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   Especifique un desplazamiento de enlace.  
  
-   Utilice el cuadro de diálogo de datos en ejecución, que implican las llamadas a **SQLParamData** y **SQLPutData**.  
  
-   Administra los cursores y los nombres de cursor, al llamar a **SQLCloseCursor**, **SQLGetCursorName**, y **SQLSetCursorName**.  
  
-   Obtener acceso a la descripción (metadatos) de conjuntos de resultados, mediante una llamada a **SQLColAttribute**, **SQLDescribeCol**, **SQLNumResultCols**, y **SQLRowCount** . (Uso de estas funciones en la columna número 0 para recuperar los metadatos de marcador es característica 204 en [cumplimiento de la interfaz de nivel 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   Consultar el diccionario de datos, mediante una llamada a las funciones de catálogo **SQLColumns**, **SQLGetTypeInfo**, **SQLStatistics**, y **SQLTables**.  
  
     El controlador no es necesario para admitir nombres de tablas de base de datos y vistas de varias partes. (Para obtener más información, vea la característica 101 en [cumplimiento de la interfaz de nivel 1](../../../odbc/reference/develop-app/level-1-interface-conformance.md) y características 201 en [cumplimiento de la interfaz de nivel 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).) Sin embargo, ciertas características de la especificación de SQL-92, como nombres de índices y calificación de columna son sintácticamente comparables a la nomenclatura de varias partes. La lista de funciones ODBC no está pensada para introducir nuevas opciones en estos aspectos de SQL-92.  
  
-   Administrar orígenes de datos y las conexiones, mediante una llamada a **SQLConnect**, **SQLDataSources**, **SQLDisconnect**, y **SQLDriverConnect**. Obtener información acerca de los controladores, independientemente de qué ODBC nivel que admiten, mediante una llamada a **SQLDrivers**.  
  
-   Preparar y ejecutar instrucciones SQL, mediante una llamada a **SQLExecDirect**, **SQLExecute**, y **SQLPrepare**.  
  
-   Capturar una fila del conjunto de resultados o varias filas, en la dirección de avance solo, mediante una llamada a **SQLFetch** o mediante una llamada a **SQLFetchScroll** con el *FetchOrientation* argumento se establece en SQL_FETCH_NEXT.  
  
-   Obtener una columna independiente en partes, mediante una llamada a **SQLGetData**.  
  
-   Obtener los valores actuales de todos los atributos, mediante una llamada a **SQLGetConnectAttr**, **SQLGetEnvAttr**, y **SQLGetStmtAttr**y establezca todos los atributos en sus valores predeterminados y establecer determinados atributos para los valores no predeterminados mediante una llamada a **SQLSetConnectAttr**, **SQLSetEnvAttr**, y **SQLSetStmtAttr**.  
  
-   Manipular algunos de los campos de los descriptores, mediante una llamada a **SQLCopyDesc**, **SQLGetDescField**, **SQLGetDescRec**, **SQLSetDescField**, y **SQLSetDescRec**.  
  
-   Obtener información de diagnóstico, mediante una llamada a **SQLGetDiagField** y **SQLGetDiagRec**.  
  
-   Detectar las capacidades del controlador, mediante una llamada a **SQLGetFunctions** y **SQLGetInfo**. Además, detectar el resultado de cualquier texto sustituciones a una instrucción SQL antes de enviarse al origen de datos, mediante una llamada a **SQLNativeSql**.  
  
-   Use la sintaxis de **SQLEndTran** para confirmar una transacción. Un controlador de nivel básico no necesita admitir transacciones true; por lo tanto, la aplicación no puede especificar SQL_ROLLBACK ni SQL_AUTOCOMMIT_OFF para el atributo de conexión SQL_ATTR_AUTOCOMMIT. (Para obtener más información, vea la característica 109 en [cumplimiento de la interfaz de nivel 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   Llame a **SQLCancel** para cancelar el cuadro de diálogo de datos en ejecución y, en entornos multiproceso, para cancelar una función ODBC ejecutando en otro subproceso. Cumplimiento de la interfaz de nivel básico no impone la compatibilidad con la ejecución asincrónica de funciones, ni el uso de **SQLCancel** para cancelar una función ODBC que se ejecuta de forma asincrónica. La plataforma ni del controlador ODBC necesita ser multiproceso para el controlador para llevar a cabo actividades independientes al mismo tiempo. Sin embargo, en entornos multiproceso, el controlador ODBC debe ser seguro para subprocesos. Serialización de solicitudes de la aplicación es una manera de función para implementar esta especificación, aunque podrían crear problemas graves de rendimiento.  
  
-   Obtener la columna que identifica la fila SQL_BEST_ROWID de tablas, mediante una llamada a **SQLSpecialColumns**. (Compatibilidad con SQL_ROWVER es característica 208 en [cumplimiento de la interfaz de nivel 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
    > [!IMPORTANT]  
    >  Controladores ODBC debe implementar las funciones en el nivel de conformidad de interfaz de núcleo.
