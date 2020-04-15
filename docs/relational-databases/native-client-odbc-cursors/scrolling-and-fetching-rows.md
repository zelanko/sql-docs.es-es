---
title: Desplazamiento y obtención de filas de desplazamiento de filas de desplazamiento y obtención de filas de desplazamiento de filas de desplazamiento Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 0ae9f1079f329951045d4b3f61b39c12efc153fb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302501"
---
# <a name="scrolling-and-fetching-rows"></a>Desplazamiento y captura de filas
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Para utilizar un cursor desplazable, una aplicación ODBC debe:  
  
-   Establezca las capacidades del cursor mediante [SQLSetStmtAttr](../../relational-databases/native-client-odbc-api/sqlsetstmtattr.md).  
  
-   Abra el cursor mediante **SQLExecute** o **SQLExecDirect**.  
  
-   Desplácese y captura filas mediante **SQLFetch** o [SQLFetchScroll](../../relational-databases/native-client-odbc-api/sqlfetchscroll.md).  
  
 **SQLFetch** y **SQLFetchSroll** pueden capturar bloques de filas a la vez. El número de filas devueltas se especifica mediante **SQLSetStmtAttr** para establecer el SQL_ATTR_ROW_ARRAY_SIZE parámetro.  
  
 Las aplicaciones ODBC pueden usar **SQLFetch** para capturar a través de un cursor de solo avance.  
  
 **SQLFetchScroll** se utiliza para desplazarse alrededor de un cursor. **SQLFetchScroll** admite la obtención de los conjuntos de filas siguiente, anterior, primero y último además de la obtención relativa (capturar el conjunto de filas *n* filas desde el inicio del conjunto de filas actual) y la obtención absoluta (capturar el conjunto de filas que comienza en la fila *n*). Si *n* es negativo en una captura absoluta, las filas se cuentan desde el final del conjunto de resultados. Una captura absoluta de la fila -1 significa que se capturará el conjunto de filas que empieza con la última fila del conjunto de resultados.  
  
 Las aplicaciones que usan **SQLFetchScroll** solo para sus capacidades de cursor de bloque, como informes, es probable que pasen a través del conjunto de resultados una sola vez, utilizando solo la opción para capturar el siguiente conjunto de filas. Las aplicaciones basadas en pantalla, por otro lado, pueden aprovechar todas las capacidades de **SQLFetchScroll**. Si la aplicación establece el tamaño del conjunto de filas en el número de filas que se muestran en la pantalla y enlaza los búferes de pantalla al conjunto de resultados, puede traducir las operaciones de la barra de desplazamiento directamente a las llamadas a **SQLFetchScroll**.  
  
|Funcionamiento de la barra de desplazamiento|Opción de desplazamiento de SQLFetchScroll|  
|--------------------------|-------------------------------------|  
|Re Pág|SQL_FETCH_PRIOR|  
|Página abajo|SQL_FETCH_NEXT|  
|Línea arriba|SQL_FETCH_RELATIVE con FetchOffset igual a -1|  
|Línea abajo|SQL_FETCH_RELATIVE con FetchOffset igual a 1|  
|Cuadro de desplazamiento hacia arriba|SQL_FETCH_FIRST|  
|Cuadro de desplazamiento hacia abajo|SQL_FETCH_LAST|  
|Posición del cuadro de desplazamiento aleatoria|SQL_FETCH_ABSOLUTE|  
  
## <a name="in-this-section"></a>En esta sección  
  
-   [Marcar filas en ODBC](../../relational-databases/native-client-odbc-cursors/scrolling-and-fetching-rows-bookmarking-rows-in-odbc.md)  
  
## <a name="see-also"></a>Consulte también  
 [Uso de cursores &#40;&#41;ODBC](../../relational-databases/native-client-odbc-cursors/using-cursors-odbc.md)  
  
  
