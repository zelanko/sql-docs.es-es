---
title: Conformidad de la interfaz de núcleo ( Core Interface Conformidad) Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 886ded1cd79b35488c0d47df3dbd8055dc6a8016
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302137"
---
# <a name="core-interface-conformance"></a>Conformidad de interfaz de núcleo
Todos los controladores ODBC deben mostrar al menos conformidad de interfaz de nivel principal. Dado que las características del nivel Core son las requeridas por la mayoría de las aplicaciones interoperables genéricas, el controlador puede trabajar con dichas aplicaciones. Las características en el nivel de núcleo también corresponden a las características definidas en la especificación ISO CLI y a las características no opcionales definidas en la especificación de la CLI de grupo abierto. Un controlador ODBC compatible con la interfaz de nivel principal permite a la aplicación realizar todo lo siguiente:  
  
-   Asigne y libere todos los tipos de identificadores, llamando a **SQLAllocHandle** y **SQLFreeHandle**.  
  
-   Utilice todas las formas de la función **SQLFreeStmt.**  
  
-   Enlazar columnas de conjunto de resultados, mediante una llamada a **SQLBindCol**.  
  
-   Controle los parámetros dinámicos, incluidas las matrices de parámetros, solo en la dirección de entrada, llamando a **SQLBindParameter** y **SQLNumParams**. (Los parámetros en la dirección de salida son la característica 203 en la conformidad de [interfaz](../../../odbc/reference/develop-app/level-2-interface-conformance.md)de nivel 2 .)  
  
-   Especifique un desplazamiento de enlace.  
  
-   Utilice el cuadro de diálogo de datos en ejecución, que implica llamadas a **SQLParamData** y **SQLPutData**.  
  
-   Administrar cursores y nombres de cursor, llamando a **SQLCloseCursor**, **SQLGetCursorName**y **SQLSetCursorName**.  
  
-   Obtenga acceso a la descripción (metadatos) de los conjuntos de resultados, llamando a **SQLColAttribute**, **SQLDescribeCol**, **SQLNumResultCols**y **SQLRowCount**. (El uso de estas funciones en el número de columna 0 para recuperar metadatos de marcadores es la característica 204 en Conformidad de [interfaz](../../../odbc/reference/develop-app/level-2-interface-conformance.md)de nivel 2 .)  
  
-   Consulte el diccionario de datos llamando a las funciones de catálogo **SQLColumns**, **SQLGetTypeInfo**, **SQLStatistics**y **SQLTables**.  
  
     El controlador no es necesario para admitir nombres multiparte de tablas y vistas de base de datos. (Para más información, vea la característica 101 en la conformidad de la [interfaz](../../../odbc/reference/develop-app/level-1-interface-conformance.md) del nivel 1 y la característica 201 en la conformidad de la interfaz del [nivel 2.)](../../../odbc/reference/develop-app/level-2-interface-conformance.md) Sin embargo, ciertas características de la especificación SQL-92, como la calificación de columna y los nombres de índices, son sintácticamente comparables a la nomenclatura multiparte. La lista actual de características ODBC no pretende introducir nuevas opciones en estos aspectos de SQL-92.  
  
-   Administrar orígenes de datos y conexiones mediante una llamada a **SQLConnect**, **SQLDataSources**, **SQLDisconnect**y **SQLDriverConnect**. Obtenga información sobre los controladores, independientemente del nivel ODBC que admitan, llamando a **SQLDrivers**.  
  
-   Prepare y ejecute instrucciones SQL mediante una llamada a **SQLExecDirect**, **SQLExecute**y **SQLPrepare**.  
  
-   Obtener una fila de un conjunto de resultados o varias filas, en la dirección de avance solamente, mediante una llamada a **SQLFetch** o mediante una llamada a **SQLFetchScroll** con el *FetchOrientation* argumento establecido en SQL_FETCH_NEXT.  
  
-   Obtenga una columna sin enlazar en partes, llamando a **SQLGetData**.  
  
-   Obtenga los valores actuales de todos los atributos, llamando a **SQLGetConnectAttr**, **SQLGetEnvAttr**y **SQLGetStmtAttr**, y establezca todos los atributos en sus valores predeterminados y establezca determinados atributos en valores no predeterminados llamando a **SQLSetConnectAttr**, **SQLSetEnvAttr**y **SQLSetStmtAttr**.  
  
-   Manipular determinados campos de descriptores mediante una llamada a **SQLCopyDesc**, **SQLGetDescField**, **SQLGetDescRec**, **SQLSetDescField**y **SQLSetDescRec**.  
  
-   Obtener información de diagnóstico mediante una llamada a **SQLGetDiagField** y **SQLGetDiagRec**.  
  
-   Detectar capacidades de controlador, mediante una llamada a **SQLGetFunctions** y **SQLGetInfo**. Además, detecte el resultado de las sustituciones de texto realizadas en una instrucción SQL antes de enviarla al origen de datos, llamando a **SQLNativeSql**.  
  
-   Utilice la sintaxis de **SQLEndTran** para confirmar una transacción. Un controlador de nivel principal no necesita admitir transacciones verdaderas; por lo tanto, la aplicación no puede especificar SQL_ROLLBACK ni SQL_AUTOCOMMIT_OFF para el atributo de conexión SQL_ATTR_AUTOCOMMIT. (Para obtener más información, consulte la característica 109 en conformidad de [interfaz](../../../odbc/reference/develop-app/level-2-interface-conformance.md)de nivel 2 .)  
  
-   Llame a **SQLCancel** para cancelar el cuadro de diálogo de datos en ejecución y, en entornos multiproceso, para cancelar una función ODBC que se ejecuta en otro subproceso. La conformidad de la interfaz de nivel principal no exige compatibilidad para la ejecución asincrónica de funciones, ni el uso de **SQLCancel** para cancelar una función ODBC que se ejecuta de forma asincrónica. Ni la plataforma ni el controlador ODBC deben ser multiproceso para que el controlador realice actividades independientes al mismo tiempo. Sin embargo, en entornos multiproceso, el controlador ODBC debe ser seguro para subprocesos. La serialización de solicitudes de la aplicación es una forma conforme de implementar esta especificación, aunque podría crear problemas de rendimiento graves.  
  
-   Obtenga la SQL_BEST_ROWID columna de tablas de identificación de filas, llamando a **SQLSpecialColumns**. (La compatibilidad con SQL_ROWVER es la característica 208 en conformidad de [interfaz](../../../odbc/reference/develop-app/level-2-interface-conformance.md)de nivel 2 .)  
  
    > [!IMPORTANT]  
    >  Los controladores ODBC deben implementar las funciones en el nivel de conformidad de la interfaz principal.
