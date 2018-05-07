---
title: Principales interfaz conformidad | Documentos de Microsoft
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- core-level interface conformance levels [ODBC]
ms.assetid: aaaa864a-6477-45ff-a50a-96d8db66a252
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7c45fdfe2b01ddfd34e7db391b799b95ce696da8
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 05/03/2018
---
# <a name="core-interface-conformance"></a>Conformidad de interfaz de núcleo
Todos los controladores ODBC deben exhibir el mínimo nivel de núcleo conformidad de interfaz. Dado que las características en el nivel de principales son las que necesitan aplicaciones interoperables más genéricas, el controlador puede trabajar con dichas aplicaciones. Las características en el nivel de núcleo también corresponden a las características que se define en la especificación ISO CLI y a las características no opcionales definidas en la especificación de CLI de grupo abierto. Un controlador ODBC de nivel de núcleo compatible con interfaz permite que la aplicación realizar todo lo siguiente:  
  
-   Asignar y liberar todos los tipos de identificadores, mediante una llamada a **SQLAllocHandle** y **SQLFreeHandle**.  
  
-   Usar todas las formas de la **SQLFreeStmt** función.  
  
-   Enlazar columnas del conjunto de resultados, mediante una llamada a **SQLBindCol**.  
  
-   Controlar los parámetros dinámicos, incluidas las matrices de parámetros, en la dirección de entrada solo, mediante una llamada a **SQLBindParameter** y **SQLNumParams**. (Los parámetros en la dirección de salida son características 203 en [conformidad de interfaz de nivel 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   Especifique un desplazamiento de enlace.  
  
-   Utilice el cuadro de diálogo de datos en ejecución, que implican las llamadas a **SQLParamData** y **SQLPutData**.  
  
-   Administrar nombres de cursores y los cursores mediante una llamada a **SQLCloseCursor**, **SQLGetCursorName**, y **SQLSetCursorName**.  
  
-   Obtener acceso a la descripción (metadatos) de conjuntos de resultados, mediante una llamada a **SQLColAttribute**, **SQLDescribeCol**, **SQLNumResultCols**, y **SQLRowCount** . (Uso de estas funciones en la columna número 0 para recuperar los metadatos de marcador es característica 204 en [conformidad de interfaz de nivel 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   Consultar el diccionario de datos, mediante una llamada a las funciones de catálogo **SQLColumns**, **SQLGetTypeInfo**, **SQLStatistics**, y **SQLTables**.  
  
     El controlador no es necesario para admitir nombres de varias partes de tablas de base de datos y vistas. (Para obtener más información, vea la función 101 en [cumplimiento a nivel 1 interfaz](../../../odbc/reference/develop-app/level-1-interface-conformance.md) y características 201 en [conformidad de interfaz de nivel 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).) Sin embargo, ciertas características de la especificación de SQL-92, como nombres de índices y calificación de columna son sintácticamente comparables a nombres de varias partes. La lista de características ODBC no pretende introducir nuevas opciones en estos aspectos de SQL-92.  
  
-   Administrar orígenes de datos y las conexiones, mediante una llamada a **SQLConnect**, **SQLDataSources**, **SQLDisconnect**, y **SQLDriverConnect**. Obtener información acerca de los controladores, con independencia de qué ODBC nivel admiten, mediante una llamada a **SQLDrivers**.  
  
-   Preparar y ejecutar instrucciones SQL, mediante una llamada a **SQLExecDirect**, **SQLExecute**, y **SQLPrepare**.  
  
-   Capturar una fila del conjunto de resultados o varias filas, en la dirección hacia delante, mediante una llamada a **SQLFetch** o mediante una llamada a **SQLFetchScroll** con el *FetchOrientation* argumento se establece en SQL_FETCH_NEXT.  
  
-   Obtener una columna sin enlazar en partes, mediante una llamada a **SQLGetData**.  
  
-   Obtener los valores actuales de todos los atributos, mediante una llamada a **SQLGetConnectAttr**, **SQLGetEnvAttr**, y **SQLGetStmtAttr**y establezca todos los atributos en sus valores predeterminados y establecer determinados atributos a valores no predeterminados mediante una llamada a **SQLSetConnectAttr**, **SQLSetEnvAttr**, y **SQLSetStmtAttr**.  
  
-   Manipular algunos de los campos de descriptores, mediante una llamada a **SQLCopyDesc**, **SQLGetDescField**, **SQLGetDescRec**, **SQLSetDescField**, y **SQLSetDescRec**.  
  
-   Obtener información de diagnóstico, mediante una llamada a **SQLGetDiagField** y **SQLGetDiagRec**.  
  
-   Detectar las capacidades del controlador, mediante una llamada a **SQLGetFunctions** y **SQLGetInfo**. Además, detectar el resultado de cualquier sustitución de texto que se realizan en una instrucción SQL antes de que se envíe al origen de datos, mediante una llamada a **SQLNativeSql**.  
  
-   Use la sintaxis de **SQLEndTran** para confirmar una transacción. Un controlador de nivel de núcleo no necesita admitir transacciones true; por lo tanto, la aplicación no puede especificar SQL_ROLLBACK ni SQL_AUTOCOMMIT_OFF para el atributo de conexión SQL_ATTR_AUTOCOMMIT. (Para obtener más información, vea la función 109 en [conformidad de interfaz de nivel 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
-   Llame a **SQLCancel** para cancelar el cuadro de diálogo de datos en ejecución y, en entornos multiproceso, cancelar una función ODBC ejecutando en otro subproceso. Conformidad de interfaz de nivel de núcleo no impone la compatibilidad con la ejecución asincrónica de las funciones, ni el uso de **SQLCancel** para cancelar una función ODBC que se ejecutan de forma asincrónica. La plataforma ni el controlador ODBC tienen que ser segura para el controlador llevar a cabo actividades independientes al mismo tiempo. Sin embargo, en entornos multiproceso, el controlador ODBC debe ser seguro para subprocesos. Serialización de las solicitudes de la aplicación es una manera de conforme para implementar esta especificación, aunque podrían crear problemas graves de rendimiento.  
  
-   Obtener la columna SQL_BEST_ROWID de identificación de filas de tablas, mediante una llamada a **SQLSpecialColumns**. (Compatibilidad con SQL_ROWVER es característica 208 en [conformidad de interfaz de nivel 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)  
  
    > [!IMPORTANT]  
    >  Controladores ODBC debe implementar las funciones en el nivel de conformidad de interfaz de núcleo.
