---
title: Desplazamiento y captura filas | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- scrollable cursors [SQL Server]
- SQL Server Native Client ODBC driver, cursors
- SQLFetchScroll function
- ODBC applications, cursors
- cursors [ODBC], fetching rows
- ODBC cursors, fetching rows
- cursors [ODBC], scrolling rows
- fetching [ODBC]
- ODBC cursors, scrolling rows
ms.assetid: 9109f10d-326b-4a6d-8c97-831f60da8c4c
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b5cddcfc7faef48198d8b810f44a08221b066c39
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/03/2018
ms.locfileid: "37421474"
---
# <a name="scrolling-and-fetching-rows"></a>Desplazamiento y captura de filas
  Para utilizar un cursor desplazable, una aplicación ODBC debe:  
  
-   Establecer las capacidades del cursor mediante [SQLSetStmtAttr](../native-client-odbc-api/sqlsetstmtattr.md).  
  
-   Abrir el cursor mediante **SQLExecute** o **SQLExecDirect**.  
  
-   Desplazarse y capturar filas mediante **SQLFetch** o [SQLFetchScroll](../native-client-odbc-api/sqlfetchscroll.md).  
  
 Ambos **SQLFetch** y **SQLFetchSroll** pueden capturar bloques de filas a la vez. El número de filas devueltas se especifica mediante el uso de **SQLSetStmtAttr** para establecer el parámetro SQL_ATTR_ROW_ARRAY_SIZE.  
  
 Las aplicaciones ODBC pueden utilizar **SQLFetch** para capturar a través de un cursor de solo avance.  
  
 **SQLFetchScroll** se utiliza para desplazarse alrededor de un cursor. **SQLFetchScroll** admite la recuperación de la siguiente, anterior, primero y último los conjuntos de filas además de una captura relativa (capturar el conjunto de filas *n* filas desde el principio del conjunto de filas actual) y una captura absoluta (captura del conjunto de filas empezando por fila *n*). Si *n* es negativo en una captura absoluta, las filas se cuentan desde el final del conjunto de resultados. Una captura absoluta de la fila -1 significa que se capturará el conjunto de filas que empieza con la última fila del conjunto de resultados.  
  
 Las aplicaciones que usan **SQLFetchScroll** sólo para su bloque de las capacidades del cursor, como informes, es probable que atraviese el conjunto de resultados de una sola vez, con solo la opción para capturar el siguiente conjunto de filas. Las aplicaciones basadas en la pantalla, por otro lado, pueden aprovechar todas las capacidades de **SQLFetchScroll**. Si la aplicación establece el tamaño del conjunto de filas en el número de filas que se muestran en la pantalla y enlaza los búferes de pantalla al conjunto de resultados, pueden traducir las operaciones de la barra de desplazamiento directamente a las llamadas a **SQLFetchScroll**.  
  
|Funcionamiento de la barra de desplazamiento|Opción de desplazamiento de SQLFetchScroll|  
|--------------------------|-------------------------------------|  
|Re Pág|SQL_FETCH_PRIOR|  
|AV PÁG|SQL_FETCH_NEXT|  
|Línea arriba|SQL_FETCH_RELATIVE con FetchOffset igual a -1|  
|Línea abajo|SQL_FETCH_RELATIVE con FetchOffset igual a 1|  
|Cuadro de desplazamiento hacia arriba|SQL_FETCH_FIRST|  
|Cuadro de desplazamiento hacia abajo|SQL_FETCH_LAST|  
|Posición del cuadro de desplazamiento aleatoria|SQL_FETCH_ABSOLUTE|  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Marcar filas en ODBC](scrolling-and-fetching-rows-bookmarking-rows-in-odbc.md)  
  
## <a name="see-also"></a>Vea también  
 [Uso de cursores &#40;ODBC&#41;](using-cursors-odbc.md)  
  
  
