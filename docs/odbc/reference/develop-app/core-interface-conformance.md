---
description: Conformidad de interfaz de núcleo
title: Conformidad con la interfaz principal | Microsoft Docs
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
ms.openlocfilehash: 1ca38e2b616c39839cfe813dad984f7eba3796a6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465847"
---
# <a name="core-interface-conformance"></a>Conformidad de interfaz de núcleo
Todos los controladores ODBC deben presentar al menos el cumplimiento de la interfaz de nivel básico. Dado que las características del nivel básico son las que requieren la mayoría de las aplicaciones interoperables genéricas, el controlador puede trabajar con estas aplicaciones. Las características del nivel básico también se corresponden con las características definidas en la especificación de la CLI ISO y con las características no opciones definidas en la especificación de la CLI Open Group. Un controlador ODBC compatible con la interfaz de nivel básico permite que la aplicación realice todas las acciones siguientes:  
  
-   Asigne y libere todos los tipos de identificadores llamando a **SQLAllocHandle** y **SQLFreeHandle**.  
  
-   Usar todas las formas de la función **SQLFreeStmt** .  
  
-   Enlazar columnas del conjunto de resultados mediante una llamada a **SQLBindCol**.  
  
-   Controlar los parámetros dinámicos, incluidas las matrices de parámetros, solo en la dirección de entrada, llamando a **SQLBindParameter** y **SQLNumParams**. (Los parámetros de la dirección de salida son la característica 203 en el cumplimiento de la [interfaz de nivel 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md)).  
  
-   Especifique un desplazamiento de enlace.  
  
-   Utilice el cuadro de diálogo de datos en ejecución, que implica llamadas a **SQLParamData** y **SQLPutData**.  
  
-   Administre los cursores y los nombres de cursor llamando a **SQLCloseCursor**, **SQLGetCursorName**y **SQLSetCursorName**.  
  
-   Obtenga acceso a la descripción (metadatos) de los conjuntos de resultados mediante una llamada a **SQLColAttribute**, **SQLDescribeCol**, **SQLNumResultCols**y **SQLRowCount**. (El uso de estas funciones en el número de columna 0 para recuperar los metadatos del marcador es la característica 204 en el cumplimiento de la [interfaz de nivel 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md)).  
  
-   Consulte el Diccionario de datos llamando a las funciones de catálogo **SQLColumns**, **SQLGetTypeInfo**, **SQLStatistics**y **SQLTables**.  
  
     No es necesario que el controlador admita nombres de varias partes de tablas y vistas de base de datos. (Para obtener más información, consulte la característica 101 del cumplimiento de la [interfaz de nivel 1](../../../odbc/reference/develop-app/level-1-interface-conformance.md) y la característica 201 en el cumplimiento de la [interfaz de nivel 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md)). Sin embargo, algunas características de la especificación SQL-92, como la calificación de columnas y los nombres de los índices, son sintácticamente comparables con la denominación de varias partes. La lista actual de características ODBC no está diseñada para introducir nuevas opciones en estos aspectos de SQL-92.  
  
-   Administrar orígenes de datos y conexiones, llamando a **SQLConnect**, **SQLDataSources**, **SQLDisconnect**y **SQLDriverConnect**. Obtenga información sobre los controladores, con independencia del nivel de ODBC que admitan, llamando a **SQLDrivers**.  
  
-   Preparar y ejecutar instrucciones SQL, llamando a **SQLExecDirect**, **SQLExecute**y **SQLPrepare**.  
  
-   Recupera una fila de un conjunto de resultados o varias filas, solo en la dirección hacia delante, llamando a **SQLFetch** o llamando a **SQLFetchScroll** con el argumento *FetchOrientation* establecido en SQL_FETCH_NEXT.  
  
-   Obtenga una columna sin enlazar en elementos, llamando a **SQLGetData**.  
  
-   Obtenga los valores actuales de todos los atributos llamando a **SQLGetConnectAttr**, **SQLGetEnvAttr**y **SQLGetStmtAttr**, y establezca todos los atributos en sus valores predeterminados y establezca ciertos atributos en valores no predeterminados mediante una llamada a **SQLSetConnectAttr**, **SQLSetEnvAttr**y **SQLSetStmtAttr**.  
  
-   Manipular determinados campos de descriptores llamando a **SQLCopyDesc**, **SQLGetDescField**, **SQLGetDescRec**, **SQLSetDescField**y **SQLSetDescRec**.  
  
-   Obtenga información de diagnóstico mediante una llamada a **SQLGetDiagField** y **SQLGetDiagRec**.  
  
-   Detecte las funcionalidades del controlador mediante una llamada a **SQLGetFunctions** y **SQLGetInfo**. Además, detecte el resultado de cualquier sustitución de texto realizada en una instrucción SQL antes de enviarla al origen de datos, llamando a **SQLNativeSql**.  
  
-   Use la sintaxis de **SQLEndTran** para confirmar una transacción. No es necesario que un controlador de nivel básico admita transacciones verdaderas; por lo tanto, la aplicación no puede especificar SQL_ROLLBACK ni SQL_AUTOCOMMIT_OFF para el atributo de conexión de SQL_ATTR_AUTOCOMMIT. (Para obtener más información, vea la característica 109 en el cumplimiento de la [interfaz de nivel 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md)).  
  
-   Llame a **SQLCancel** para cancelar el cuadro de diálogo de datos en ejecución y, en entornos multiproceso, para cancelar la ejecución de una función ODBC en otro subproceso. La conformidad con la interfaz de nivel básico no exige la compatibilidad con la ejecución asincrónica de funciones ni el uso de **SQLCancel** para cancelar una función ODBC que se ejecuta de forma asincrónica. Ni la plataforma ni el controlador ODBC deben ser multiproceso para que el controlador realice actividades independientes al mismo tiempo. Sin embargo, en entornos multiproceso, el controlador ODBC debe ser seguro para subprocesos. La serialización de solicitudes de la aplicación es una manera compatible de implementar esta especificación, aunque podría crear problemas de rendimiento graves.  
  
-   Obtenga la SQL_BEST_ROWID columna de identificación de filas de las tablas mediante una llamada a **SQLSpecialColumns**. (La compatibilidad con SQL_ROWVER es la característica 208 en el cumplimiento de la [interfaz de nivel 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md)).  
  
    > [!IMPORTANT]  
    >  Los controladores ODBC deben implementar las funciones en el nivel de conformidad de la interfaz principal.
